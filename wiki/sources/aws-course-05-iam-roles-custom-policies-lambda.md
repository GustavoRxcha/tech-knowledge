---
title: "Curso AWS 05 — IAM Roles, Policies Personalizadas e Lambda"
type: source
tags: [aws, iam, roles, lambda, s3, customer-managed-policy]
created: 2026-05-18
updated: 2026-05-18
sources: 1
---

# Curso AWS 05 — IAM Roles, Policies Personalizadas e Lambda

Aula final do módulo IAM. Introduz [[concepts/iam-role|IAM Roles]] e [[concepts/customer-managed-policy|policies personalizadas]], com demonstração prática de [[entities/aws-lambda|Lambda]] acessando [[entities/amazon-s3|S3]] via role de execução.

---

## Conceitos novos

### IAM Role

- Identidade IAM **sem dono fixo** — não pertence a um usuário
- Pode ser **assumida temporariamente** por usuários, serviços ou contas externas
- Principal caso de uso nesta aula: **AWS Service Role** (serviço assume a role)

| Tipo | Exemplo |
|---|---|
| Serviço → Serviço | Lambda acessando S3 ou DynamoDB |
| Cross-account | Usuário de outra conta AWS |
| Identidade federada | Login via Google, Active Directory |
| IaC | SAM, CloudFormation assumindo roles |

### Customer-managed policy

- Policy criada pelo próprio usuário (vs managed policy da AWS)
- Estrutura JSON: `Effect` / `Action` / `Resource`
- Exemplo criado: `policy-s3-developers` com `ListBucket`, `GetObject`, `PutObject`, `DeleteObject`

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": ["s3:ListBucket", "s3:GetObject", "s3:PutObject", "s3:DeleteObject"],
      "Resource": ["arn:aws:s3:::*", "arn:aws:s3:::*/*"]
    }
  ]
}
```

---

## Fluxo prático

1. Criar `policy-s3-developers` em **IAM → Policies → Create policy**
2. Atribuir a policy ao grupo `developers`
3. Criar role `role-lambda-s3` em **IAM → Roles → Create role → AWS Service → Lambda**
4. Atribuir a role à função Lambda na seção **Execution role**
5. Testar: sem role → erro; com role → lista buckets

### Código Lambda de teste

```javascript
const { S3Client, ListBucketsCommand } = require("@aws-sdk/client-s3");

exports.handler = async () => {
  const client = new S3Client({});
  const response = await client.send(new ListBucketsCommand({}));
  return response.Buckets;
};
```

---

## Distinção-chave

| | Policy direta (usuário/grupo) | Role (serviço) |
|---|---|---|
| Quem usa | Usuários e grupos IAM | Serviços AWS, contas externas |
| Vínculo | Permanente | Temporário (assume) |
| Caso de uso | Pessoas no console/API | Serviços comunicando entre si |

---

## Boas práticas destacadas

- Sempre usar roles para comunicação entre serviços — **nunca hardcodar credenciais**
- Aplicar [[concepts/principle-of-least-privilege|menor privilégio]] nas policies da role
- Nomear roles de forma descritiva: `role-lambda-s3-readonly`

---

## Relações

- [[concepts/iam-role]] — conceito completo de roles
- [[concepts/customer-managed-policy]] — policies criadas pelo usuário
- [[entities/aws-lambda]] — serviço que assume a role neste exemplo
- [[entities/amazon-s3]] — recurso acessado via role
- [[concepts/iam-policy]] — estrutura JSON das policies
- [[concepts/arn]] — usado para especificar resources nas policies
