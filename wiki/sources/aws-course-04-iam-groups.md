---
title: "Curso AWS 04 — Grupos de Usuários IAM e Gerenciamento de Permissões"
type: source
tags: [aws, iam, grupos, managed-policy, curso]
created: 2026-05-18
updated: 2026-05-18
sources: 1
---

# Curso AWS 04 — Grupos de Usuários IAM e Gerenciamento de Permissões

Arquivo fonte: `raw/aula-04-grupos-usuarios-iam.md` (PT-BR)

Penúltima aula do módulo IAM. Foco em **grupos de usuários**, atribuição de permissões por grupo, e validação prática do [[principle-of-least-privilege|menor privilégio]] tentando acessar serviços para os quais o usuário não tem policy.

---

## Pontos-chave

- [[iam-group|Grupos IAM]] são coleções de usuários que **compartilham o mesmo conjunto de permissões**. Anexa-se a policy ao grupo; os membros herdam.
- Boa prática: **permissões devem vir do grupo**, não diretamente do usuário. Depois de mover um usuário para um grupo, remova a [[inline-policy]] anterior dele.
- A aula usou exclusivamente **managed policies da AWS** (`AWSLambdaFullAccess`, `AdministratorAccess`) — não cria-se policy do zero para casos padrão.
- Há centenas de managed policies; não é esperado conhecer todas — é esperado saber pesquisar.
- O teste de negação no console mostra `You are not authorized to perform this operation.` quando a ação não está coberta por nenhuma policy aplicada à identidade.

## Cenário prático montado

| Grupo | Membros | Policies |
|---|---|---|
| `developers` | usuário developer (novo, criado nesta aula) | `AWSLambdaFullAccess` (e outras de perfil dev) |
| `admins` | usuário admin (preexistente) | `AdministratorAccess` |

A inline policy de admin que existia direto no usuário admin foi removida — todas as permissões dele agora chegam **via grupo**.

## Validação de acesso (login como novo usuário developer)

| Serviço | Resultado | Motivo |
|---|---|---|
| [[aws-lambda|Lambda]] | ✅ permitido | `AWSLambdaFullAccess` está no grupo `developers` |
| [[amazon-ec2|EC2]] | ❌ negado | nenhuma policy do grupo cobre EC2 |
| [[aws-iam|IAM]] | ❌ negado | usuário developer não pode criar usuários nem mexer em policies |

> Demonstra na prática o [[principle-of-least-privilege]]: o usuário só acessa o que tem permissão explícita.

## Categorias mencionadas como típicas de empresa

| Grupo | Acesso típico |
|---|---|
| Developers | Lambda, S3, DynamoDB |
| Admins | Acesso total (`AdministratorAccess`) |
| RH / Financeiro | Apenas serviços internos relevantes |

## Próxima aula (anunciada)

- **IAM Roles** — permissões assumidas temporariamente por serviços ou usuários.
- **Policies personalizadas** (customer-managed) para recursos específicos.
- Integração: usuários, grupos, policies e roles em conjunto.

---

## Entidades e conceitos tocados

- Entidades: [[aws]], [[aws-iam]], [[aws-lambda]] (novo), [[amazon-ec2]] (novo, em modo negação), [[amazon-dynamodb]] (novo, menção breve)
- Conceitos: [[iam-group]] (novo), [[iam-policy]], [[inline-policy]], [[principle-of-least-privilege]]
- Tópicos: [[aws-security]]
