---
title: "AWS Lambda"
type: entity
tags: [aws, lambda, serverless, computação, roles, triggers]
created: 2026-05-18
updated: 2026-05-20
sources: 6
---

# AWS Lambda

Serviço **[[concepts/serverless|serverless]]** de computação da [[entities/aws|AWS]]. Executa funções sob demanda, sem provisionar servidor — modelo FaaS (Function-as-a-Service).

---

## Características principais

- Execução **acionada por eventos** (HTTP via API Gateway, Cognito triggers, S3 events, schedule, fila, etc.)
- Cobra apenas pelo tempo de execução real
- Múltiplos runtimes: **Node.js**, Python, Java, Go, Ruby, .NET, custom
- Limite duro: **15 minutos** por invocação
- Ideal para microsserviços e arquiteturas event-driven

## Formas de criar uma função

| Método | Quando |
|---|---|
| **Author from scratch** | Código no editor do console |
| **Use a blueprint** | Template pré-pronto (ex.: Hello World, S3 trigger) |
| **Container image** | Imagem Docker no ECR |
| **Upload .zip** | Pacote local |
| **Repo (GitHub etc.)** | Fonte externa |

## Execution Role — obrigatória

Para acessar **qualquer** outro serviço AWS, a Lambda precisa de uma [[concepts/iam-role|IAM Role]] (a *execution role*) com as policies adequadas.

> **Nunca** hardcodar credenciais no código. A role provê credenciais temporárias automaticamente via AWS STS.

Opções na criação:

| Opção | Quando |
|---|---|
| Create new role with basic Lambda permissions | Função sem acessar outros serviços |
| Use an existing role | Já existe role adequada |
| Create from AWS policy templates | Casos pré-definidos |

## Handler — anatomia (Node.js)

```javascript
exports.handler = async (event) => {
  // event traz o payload do trigger (HTTP, S3, etc.)
  // context (segundo arg) traz metadados da invocação

  return {
    statusCode: 200,
    body: JSON.stringify({ ok: true }),
    headers: { "Content-Type": "application/json" }
  };
};
```

Quando o trigger é [[entities/amazon-api-gateway|API Gateway]] HTTP:

| Campo do event | Conteúdo |
|---|---|
| `event.routeKey` | `"METHOD /path"` (ex.: `"POST /items"`) |
| `event.body` | Corpo HTTP (string — usar `JSON.parse`) |
| `event.pathParameters` | Parâmetros da URL (ex.: `{id}` → `event.pathParameters.id`) |
| `event.queryStringParameters` | Query string |
| `event.headers` | Headers HTTP |

## Padrão: uma Lambda + várias rotas

Mesma função pode servir todas as rotas de uma API:

```javascript
switch (event.routeKey) {
  case "POST /items":     /* ... */ break;
  case "GET /items":      /* ... */ break;
  case "GET /items/{id}": /* ... */ break;
  // ...
}
```

Vantagem: menos integrações para gerenciar. Desvantagem: a função cresce — em escala, prefira uma Lambda por rota.

## Exemplos práticos do curso

**Listar buckets S3** (aula 05):

```javascript
const { S3Client, ListBucketsCommand } = require("@aws-sdk/client-s3");

exports.handler = async () => {
  const client = new S3Client({});
  const response = await client.send(new ListBucketsCommand({}));
  return response.Buckets;
};
```

| Cenário | Resultado |
|---|---|
| Sem permissão S3 na role | ❌ Acesso negado |
| Com policy S3 adequada | ✅ Buckets listados |

**CRUD em DynamoDB** (aula dynamo-02):

```javascript
const AWS = require("aws-sdk");
const dynamo = new AWS.DynamoDB.DocumentClient();

exports.handler = async (event) => {
  // switch (event.routeKey) com put/get/update/delete/scan
};
```

Erro real capturado quando a role não tinha policy de DynamoDB:

```
User is not authorized to perform: dynamodb:PutItem on resource: arn:aws:dynamodb:...
```

Solução: anexar `AmazonDynamoDBFullAccess` (didática) ou [[concepts/customer-managed-policy|customer-managed policy]] restrita (produção).

## Deploy

No console: editar código → **Deploy** publica a versão atual. Para automação real, use SAM, Serverless Framework, CDK ou Terraform — fora do escopo do curso até aqui.

## Managed policies referenciadas

| Policy | Para o quê |
|---|---|
| `AWSLambdaFullAccess` | Acesso total ao Lambda (para usuários IAM) |
| `AmazonDynamoDBFullAccess` | Acesso total ao DynamoDB (para execution role) |
| `policy-s3-developers` | Customer-managed do curso, acesso ao S3 |

## Boas práticas

- ✅ Runtime na versão mais recente disponível
- ✅ Constantes/env vars para nomes de tabela e recursos
- ✅ Policies restritas em produção
- ✅ `try/catch/finally` no handler com erro → status 4xx
- ✅ Logs estruturados (CloudWatch captura tudo do `console.log` / `print`)
- ✅ Lambda + API Gateway + Cognito na **mesma região**

## Triggers comuns (event sources)

| Trigger | Descrição |
|---|---|
| **API Gateway** | Requisição HTTP → Lambda processa e responde |
| **Upload no S3** | Arquivo cai em bucket → Lambda processa |
| **Mensagem no SQS** | Mensagem entra na fila → Lambda consome |
| **Evento do SNS** | Tópico SNS publica → Lambda é notificada |
| **Agendamento (EventBridge)** | Horários definidos (ex: todo dia às 8h) |
| **Mudança no DynamoDB** | Item inserido/atualizado via Streams → Lambda reage |
| **Cognito** | Triggers de auth (pre-signup, post-confirm, etc.) |

> O Lambda é o "cola" entre serviços AWS — conecta eventos de um serviço a ações em outro.

## Modelo de cobrança

| Fator | Descrição |
|---|---|
| Número de invocações | Cada vez que a função é chamada |
| Tempo de execução | Medido em milissegundos × memória configurada (GB-segundos) |

**Nível gratuito permanente:** 1 milhão de invocações + 400.000 GB-segundos/mês.

## Ecossistema serverless na AWS

| Serviço | Função |
|---|---|
| **AWS Lambda** | Execução de código por evento |
| **Amazon API Gateway** | API HTTP serverless |
| **Amazon DynamoDB** | Banco NoSQL serverless |
| **Amazon S3** | Armazenamento serverless |
| **AWS Fargate** | Containers serverless |
| **Amazon EventBridge** | Barramento de eventos serverless |

## Lacunas

- Layers e dependências externas
- Cold starts e provisioned concurrency
- VPC config
- Observabilidade (X-Ray, structured logging, métricas custom)

## Fontes

- [[sources/clf-c02-aula13-serverless-lambda]] — visão conceitual (triggers, pricing, ecossistema)
- [[sources/aws-course-04-iam-groups]] — mencionado
- [[sources/aws-course-05-iam-roles-custom-policies-lambda]] — execution role + S3
- [[sources/aws-course-dynamo-01-table-lambda-intro]] — criação da função
- [[sources/aws-course-dynamo-02-lambda-crud]] — handler CRUD completo (JS + Python)
- [[sources/aws-course-apigateway-02-integration-postman]] — integração + erro de IAM + testes

## Relações

- [[entities/aws]]
- [[entities/amazon-api-gateway]] — trigger HTTP típico
- [[entities/amazon-dynamodb]] — backend de dados típico
- [[entities/amazon-s3]] — outro target comum
- [[entities/aws-cognito]] — pode disparar Lambdas em triggers de auth
- [[concepts/iam-role]] — execution role
- [[concepts/serverless]]
- [[concepts/customer-managed-policy]]
