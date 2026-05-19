---
title: "Curso AWS — API Gateway 02: Integração Lambda, Permissões e Testes com Postman"
type: source
tags: [aws, api-gateway, lambda, postman, iam, curso]
created: 2026-05-19
updated: 2026-05-19
sources: 1
---

# Curso AWS — API Gateway 02: Integração Lambda, Permissões e Testes com Postman

Arquivo fonte: `raw/aula-apigateway-02-integracao-lambda-testes-postman.md` (PT-BR)

Encerramento do módulo prático. Integra as rotas do API Gateway à função Lambda, corrige um erro real de IAM (`User is not authorized to perform: dynamodb:PutItem`) anexando policy de DynamoDB à execution role, e valida o CRUD completo com [[entities/postman|Postman]].

---

## Pontos-chave

- **Uma única integração Lambda** serve todas as rotas — a Lambda distingue via `event.routeKey`.
- ⚠️ A função Lambda deve estar **na mesma região** da API.
- **Authorizers** do API Gateway: filtros de autenticação executados **antes** de chegar à Lambda. Tipicamente validam [[concepts/jwt|JWT]] (ex.: emitido pelo [[entities/aws-cognito|Cognito]]). Não implementado nesta aula.
- Erros de permissão são **detectados em runtime**: a chamada HTTP retorna o erro IAM literal, ex.:
  ```
  User is not authorized to perform: dynamodb:PutItem on resource: arn:aws:dynamodb:...
  ```
- Solução: anexar `AmazonDynamoDBFullAccess` (ou policy restrita) à execution role da Lambda.

## Integração rota → Lambda (passo a passo)

1. API Gateway → rota → **Attach integration → Create and attach an integration**
2. Tipo: **Lambda function**
3. Verificar região
4. Selecionar a função
5. Confirmar

Auto-deploy ativado: publicado automaticamente.

## Policy restrita recomendada para produção

A aula usou `AmazonDynamoDBFullAccess` por didática, mas em produção o ideal é uma [[concepts/customer-managed-policy|customer-managed policy]] restrita:

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "dynamodb:GetItem",
        "dynamodb:PutItem",
        "dynamodb:UpdateItem",
        "dynamodb:DeleteItem",
        "dynamodb:Scan"
      ],
      "Resource": "arn:aws:dynamodb:<região>:<conta>:table/Product"
    }
  ]
}
```

Aplicação direta do [[concepts/principle-of-least-privilege|menor privilégio]].

## Bug capturado: nome de tabela inconsistente

Durante os testes, identificou-se nome da tabela **diferente entre métodos** (resultado de copy/paste). Lição:

```javascript
const TABLE_NAME = "Product";  // usar em TODAS as operações
```

```python
TABLE_NAME = "Product"
table = dynamodb.Table(TABLE_NAME)
```

**Regra**: nome de tabela, ARN e qualquer valor repetido em múltiplos pontos deve ser **constante ou variável de ambiente**.

## Testes com Postman — CRUD completo

Base: `https://<api-id>.execute-api.<região>.amazonaws.com`

| # | Método | Rota | Body | Resultado |
|---|---|---|---|---|
| 1 | `POST` | `/items` | `{id, name, price}` | ✅ `"Put item prod-0001"` |
| 2 | `GET` | `/items` | — | ✅ Lista completa |
| 3 | `GET` | `/items/prod-0001` | — | ✅ Objeto do item |
| 4 | `PUT` | `/items/prod-0001` | `{"price": 320000}` | ✅ Atualização **parcial** (preserva `name`) |
| 5 | `DELETE` | `/items/prod-0001` | — | ✅ Item removido |

Cada teste foi validado também no console DynamoDB.

## Arquitetura final do módulo

```
[Postman / Cliente HTTP]
         ↓
[API Gateway - HTTP API]
  ├── POST   /items        ──┐
  ├── GET    /items        ──┤
  ├── GET    /items/{id}   ──┼──→ [Lambda Function]
  ├── PUT    /items/{id}   ──┤         ↓
  └── DELETE /items/{id}   ──┘   [DynamoDB - "Product"]
```

## Próximos passos do curso

| Etapa | Descrição |
|---|---|
| **Auth com Cognito** | Authorizer no API Gateway validando [[concepts/jwt\|JWT]] |
| **Frontend** | Interface web consumindo a API autenticada |
| **Hospedagem estática** | Publicar frontend em S3 + CloudFront |

## Boas práticas reforçadas

- ✅ Verificar **região** de todos os serviços
- ✅ **Constantes/env vars** para nomes de recursos
- ✅ **Policies restritas** em produção (não `FullAccess`)
- ✅ Testar cada rota individualmente
- ✅ Confirmar resultado direto no console DynamoDB

---

## Entidades e conceitos tocados

- Entidades: [[entities/amazon-api-gateway]], [[entities/aws-lambda]], [[entities/amazon-dynamodb]], [[entities/postman]] (novo), [[entities/aws-cognito]]
- Conceitos: [[concepts/jwt]], [[concepts/customer-managed-policy]], [[concepts/principle-of-least-privilege]], [[concepts/iam-role]]
- Tópicos: [[topics/aws-security]]
