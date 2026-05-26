---
title: "SCP — Service Control Policies"
type: concept
tags: [aws, iam, organizations, scp, permissões, clf-c02]
created: 2026-05-26
updated: 2026-05-26
sources: 1
---

# SCP — Service Control Policies

Políticas de controle de serviço aplicadas em nível de **Organizational Unit (OU)** no [[entities/aws-organizations|AWS Organizations]]. Funcionam como **teto de permissões** para todas as contas dentro de uma OU.

---

## Como funciona

```
[SCP aplicada ao OU: Operações]
├── Proibido: acessar S3
├── Proibido: criar EC2 fora de us-east-1
└── Permitido: apenas serviços necessários

→ Qualquer usuário novo que entrar nesse OU
  já herda essas restrições automaticamente
```

A SCP não concede permissões — apenas **limita** o que é possível fazer. Mesmo um administrador da conta-filha não consegue ultrapassar o que a SCP permite.

---

## Diferença: SCP vs IAM Policy

| Aspecto | SCP | IAM Policy |
|---|---|---|
| Escopo | Conta inteira / OU | Usuário, grupo ou role específico |
| Quem define | Management Account | Administrador da conta |
| Efeito | Teto de permissões | Permissões efetivas |
| Herança | Automática por OU | Explícita por usuário/grupo |

SCPs e IAM Policies se combinam: o usuário só pode fazer o que **ambas** permitem.

---

## Caso de uso típico

Empresa com múltiplas contas quer garantir que o ambiente de desenvolvimento **nunca** acesse dados de produção, independente do que os administradores da conta-dev configurem.

```
[OU: Desenvolvimento]
    SCP: "Deny: acessar buckets S3 com prefixo 'prod-'"
    
→ Nenhum usuário na conta-dev, nem o admin,
  consegue acessar dados de produção
```

---

## Relações

- [[entities/aws-organizations]] — SCPs são um recurso do Organizations
- [[concepts/iam-policy]] — IAM Policies operam dentro do limite definido pela SCP
- [[concepts/principle-of-least-privilege]] — SCPs reforçam o menor privilégio em escala organizacional
- [[topics/aws-security]]
- [[sources/clf-c02-aulas1-6-seguranca-nuvem]]
