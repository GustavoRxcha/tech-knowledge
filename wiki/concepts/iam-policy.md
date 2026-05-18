---
title: "IAM Policy"
type: concept
tags: [aws, iam, policy, controle-de-acesso, json]
created: 2026-05-18
updated: 2026-05-18
sources: 4
---

# IAM Policy

Documento JSON que define o que uma identidade do [[aws-iam]] pode (ou não pode) fazer em quais recursos.

---

## Anatomia

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::meu-bucket/*"
    }
  ]
}
```

| Campo | Significado |
|---|---|
| `Version` | Versão da linguagem de policy. `2012-10-17` é o padrão atual. |
| `Effect` | `Allow` ou `Deny`. |
| `Action` | Uma ou mais ações de serviço, ex.: `s3:GetObject`. Wildcards permitidos. |
| `Resource` | Um ou mais [[arn|ARNs]] aos quais o statement se aplica. |

## Tipos de policy

| Tipo | Criada por | Reutilizável | Notas |
|---|---|---|---|
| **Gerenciada pela AWS** | AWS | Sim | Mantida pela AWS. Existem centenas. Preferida para casos de uso padrão. Exemplos: `AdministratorAccess`, `AWSLambdaFullAccess`. |
| **Gerenciada pelo cliente** | Conta | Sim | Reutilizável entre usuários/grupos/roles da conta. |
| **[[inline-policy|Inline]]** | Conta | Não | Embutida em uma única identidade; some quando ela é deletada. Para exceções. |

## Pontos de anexação

Uma policy pode ser anexada a:

- Um **usuário** [[aws-iam|IAM]] (direto).
- Um **[[iam-group|grupo]]** — todos os membros herdam (preferido).
- Uma **role** (não coberto ainda pelas fontes).

## `AdministratorAccess` — a policy canônica de "acesso total"

```json
{
  "Version": "2012-10-17",
  "Statement": [
    { "Effect": "Allow", "Action": "*", "Resource": "*" }
  ]
}
```

Cobre ~300 serviços AWS. Só deve ser anexada a administradores reais — ver [[principle-of-least-privilege]].

## Managed policies citadas no wiki

| Policy | Cobre |
|---|---|
| `AdministratorAccess` | Tudo (`*`, `*`) |
| `AWSLambdaFullAccess` | [[aws-lambda]] integral |

## Fontes

- [[aws-course-01-mfa-iam-setup]]
- [[aws-course-02-iam-policies-tags-credentials]]
- [[aws-course-03-iam-user-login-inline-policy]]
- [[aws-course-04-iam-groups]]

## Relacionados

- [[inline-policy]]
- [[iam-group]]
- [[arn]]
- [[access-keys]]
- [[principle-of-least-privilege]]
