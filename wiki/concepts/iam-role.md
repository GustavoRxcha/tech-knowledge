---
title: "IAM Role"
type: concept
tags: [aws, iam, roles, segurança, identidade]
created: 2026-05-18
updated: 2026-05-18
sources: 1
---

# IAM Role

Identidade IAM que **não pertence a um usuário específico**. Contém um conjunto de [[concepts/iam-policy|policies]] e pode ser **assumida temporariamente** por usuários, serviços AWS, contas externas ou identidades federadas.

---

## Características

- Não tem login/senha permanente
- Gera **credenciais temporárias** (via AWS STS) quando assumida
- Pode ter uma **trust policy** que define quem pode assumi-la
- Pode ter **permission policies** que definem o que o assumidor pode fazer

---

## Casos de uso

| Tipo | Descrição | Exemplo |
|---|---|---|
| **AWS Service Role** | Serviço AWS acessa outro serviço | Lambda acessando S3 |
| **Cross-account** | Usuário de outra conta AWS | Conta de produção acessando conta de logging |
| **Identidade federada** | Login via provedor externo | Google, Active Directory, SAML |
| **IaC** | Ferramentas de infraestrutura como código | SAM, CloudFormation |

---

## Role vs Policy direta

| | Policy direta (usuário/grupo) | Role |
|---|---|---|
| Quem usa | Usuários e grupos IAM | Serviços, contas externas, federados |
| Vínculo | Permanente | Temporário (assume e expira) |
| Credenciais | Access key de longa duração | Temporárias via STS |
| Caso de uso | Pessoas no console/API | Serviços comunicando entre si |

---

## Execution role (Lambda)

Quando uma função [[entities/aws-lambda|Lambda]] precisa acessar outro serviço, ela precisa de uma **execution role**:

1. Criar a role em **IAM → Roles → Create role → AWS Service → Lambda**
2. Anexar as policies necessárias (ex: `policy-s3-developers`)
3. Na função Lambda, definir a role em **Execution role → Use an existing role**

---

## Boas práticas

- Preferir roles a [[concepts/access-keys|access keys]] para comunicação entre serviços
- **Nunca hardcodar credenciais** no código — role é o jeito correto
- Aplicar [[concepts/principle-of-least-privilege|menor privilégio]] nas policies da role
- Nomear de forma descritiva: `role-lambda-s3-readonly`
- Revisar permissões periodicamente

---

## Relações

- [[concepts/iam-policy]] — policies anexadas à role
- [[concepts/access-keys]] — alternativa de longa duração (evitar para serviços)
- [[entities/aws-iam]] — serviço que gerencia roles
- [[entities/aws-lambda]] — consumidor típico de execution roles
- [[concepts/principle-of-least-privilege]] — princípio a aplicar ao criar roles
