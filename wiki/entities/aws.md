---
title: "AWS (Amazon Web Services)"
type: entity
tags: [aws, cloud, infraestrutura]
created: 2026-05-18
updated: 2026-05-19
sources: 15
---

# AWS — Amazon Web Services

A plataforma de nuvem da Amazon. O wiki cobre AWS por **duas trilhas** distintas:

1. **Trilha hands-on** — curso prático cobrindo módulo IAM completo + módulo serverless (DynamoDB + Lambda + API Gateway + Cognito).
2. **Trilha CLF-C02** — preparatório conceitual para a certificação AWS Cloud Practitioner.

---

## Estado de cobertura (serviços)

| Serviço | Categoria | Status |
|---|---|---|
| [[entities/aws-iam]] | Identidade & acesso | 🟢 Módulo completo |
| [[entities/amazon-s3]] | Storage | 🟡 Permissões IAM + Block Public Access |
| [[entities/aws-lambda]] | Compute (serverless) | 🟢 Handler, role, CRUD, integração |
| [[entities/amazon-dynamodb]] | Database (NoSQL) | 🟢 Modelo de dados + operações CRUD |
| [[entities/amazon-api-gateway]] | API / Networking | 🟢 HTTP API, rotas, integration Lambda |
| [[entities/aws-cognito]] | Identidade de usuário final | 🟡 Conceitual; não implementado |
| [[entities/amazon-ec2]] | Compute (VM, [[concepts/iaas\|IaaS]]) | 🟡 Conceitual + ex. acesso negado |
| [[entities/aws-elastic-beanstalk]] | Compute ([[concepts/paas\|PaaS]]) | 🔴 Stub conceitual |

## Conceitos transversais cobertos

### Fundamentos cloud ([[topics/cloud-fundamentals|trilha CLF-C02]])
- [[concepts/cloud-computing]] — definição AWS, pay-as-you-go
- [[concepts/cloud-benefits]] — os 5 benefícios oficiais
- [[concepts/elasticity]]
- [[concepts/iaas]] / [[concepts/paas]] / [[concepts/saas]]
- [[concepts/on-premises]] / [[concepts/hybrid-cloud]] / [[concepts/private-cloud]]
- [[concepts/virtualization]]

### Identidade & autorização ([[topics/aws-security|trilha hands-on]])
- Modelo: **identidade + ação + recurso ([[concepts/arn|ARN]]) via [[concepts/iam-policy|policy]]**
- [[concepts/principle-of-least-privilege]]
- Hierarquia recomendada: **policy → grupo → usuário**; para serviços: **policy → role → serviço**
- [[concepts/jwt]] para autenticação de usuário final via Cognito

### Arquitetura
- [[concepts/serverless]] — Lambda + DynamoDB + API Gateway + Cognito
- [[concepts/nosql]] — DynamoDB

## Regra de ouro operacional

⚠️ **Todos os serviços de uma solução devem estar na mesma região AWS**. Misturar regiões exige configuração multi-região explícita.

## Arquitetura serverless do curso hands-on

```
Cliente (browser/Postman)
       ↓
[Cognito]  → emite JWT (futuro)
       ↓
[API Gateway] HTTP routes (+authorizer)
       ↓
[Lambda] (handler com switch por routeKey)
       ↓
[DynamoDB] / [S3] / etc.
```

## Fontes que referenciam AWS

### Trilha hands-on (11)
- [[sources/aws-course-01-mfa-iam-setup]]
- [[sources/aws-course-02-iam-policies-tags-credentials]]
- [[sources/aws-course-03-iam-user-login-inline-policy]]
- [[sources/aws-course-04-iam-groups]]
- [[sources/aws-course-05-iam-roles-custom-policies-lambda]]
- [[sources/aws-course-06-iam-permissions-validation-s3]]
- [[sources/aws-course-cognito-intro]]
- [[sources/aws-course-dynamo-01-table-lambda-intro]]
- [[sources/aws-course-dynamo-02-lambda-crud]]
- [[sources/aws-course-apigateway-01-api-routes]]
- [[sources/aws-course-apigateway-02-integration-postman]]

### Trilha CLF-C02 (4)
- [[sources/clf-c02-aula01-cloud-computing]]
- [[sources/clf-c02-aula02-cloud-benefits]]
- [[sources/clf-c02-aula03-service-models]]
- [[sources/clf-c02-aula04-deployment-models]]

## Tópicos relacionados

- [[topics/aws-security]] — trilha hands-on, foco em segurança e IAM
- [[topics/cloud-fundamentals]] — trilha CLF-C02, foco conceitual e certificação
