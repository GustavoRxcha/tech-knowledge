---
title: "IAM Group"
type: concept
tags: [aws, iam, grupos, controle-de-acesso]
created: 2026-05-18
updated: 2026-05-18
sources: 1
---

# IAM Group

Coleção de usuários do [[aws-iam|IAM]] que **compartilham o mesmo conjunto de permissões**. As [[iam-policy|policies]] são anexadas ao grupo; cada usuário membro herda todas elas.

---

## Modelo mental

> Você não anexa policies a usuários individuais. Você anexa policies a grupos, e move usuários para dentro/fora dos grupos.

Isso transforma o gerenciamento de permissões em uma operação **de cardinalidade baixa** (poucos grupos) em vez de **alta** (muitos usuários).

## Por que usar grupos

- **Escala**: alterar uma policy do grupo afeta todos os membros instantaneamente.
- **Consistência**: usuários no mesmo papel têm exatamente as mesmas permissões.
- **Auditoria**: revisar 5 grupos é mais simples que revisar 50 usuários.
- **Alinhamento com [[principle-of-least-privilege]]**: cada grupo carrega só o que aquele papel precisa.

## Padrão de empresa típico

| Grupo | Papel |
|---|---|
| `admins` | Acesso total — `AdministratorAccess` |
| `developers` | Lambda, S3, DynamoDB e similares |
| `data` | Acesso a recursos de dados |
| `finance` / `hr` | Serviços internos relevantes ao setor |

## Boa prática: migração de inline → grupo

Quando um usuário recebe uma permissão temporariamente via [[inline-policy]] e depois entra em um grupo que já cobre essa permissão:

1. Confirme que o grupo entrega a permissão equivalente.
2. **Remova a inline policy do usuário.**
3. Agora a única fonte de permissão dele é o grupo — sem inconsistências futuras.

Foi exatamente isso que [[aws-course-04-iam-groups]] fez com o usuário admin.

## Limites (segundo experiência com AWS, não diretamente declarado na fonte)

- Grupos **não podem conter outros grupos** (sem aninhamento).
- Grupos **não podem ser usados como principal** em resource policies (use roles para isso).

> [!question] Limites exatos (número máximo de grupos por conta, usuários por grupo) ainda não cobertos pelas fontes ingeridas.

## Fontes

- [[aws-course-04-iam-groups]]

## Relacionados

- [[aws-iam]]
- [[iam-policy]]
- [[inline-policy]]
- [[principle-of-least-privilege]]
- [[aws-security]]
