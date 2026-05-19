---
title: "Curso AWS — DynamoDB 02: Lambda com CRUD no DynamoDB"
type: source
tags: [aws, lambda, dynamodb, crud, nodejs, python, curso]
created: 2026-05-19
updated: 2026-05-19
sources: 1
---

# Curso AWS — DynamoDB 02: Lambda com CRUD no DynamoDB

Arquivo fonte: `raw/aula-dynamo-02-lambda-crud-dynamodb.md` (PT-BR)

Implementação prática: uma única função [[entities/aws-lambda|Lambda]] em **Node.js** (com equivalente Python via boto3) que roteia eventos do [[entities/amazon-api-gateway|API Gateway]] via `event.routeKey` e executa **CRUD completo** na tabela `Product` do [[entities/amazon-dynamodb|DynamoDB]].

---

## Arquitetura da função

```
HTTP → API Gateway → Lambda (switch event.routeKey) → DynamoDB ("Product")
```

A Lambda recebe `event.routeKey`, `event.body` e `event.pathParameters`, executa a operação correta e retorna `{ statusCode, body, headers }`.

## Dependências (Node.js)

```javascript
const AWS = require("aws-sdk");
const dynamo = new AWS.DynamoDB.DocumentClient();
```

- `aws-sdk` já vem no runtime Lambda — não precisa instalar.
- **`DocumentClient`** é o cliente de alto nível: trabalha com objetos JS nativos, sem precisar especificar os tipos internos do DynamoDB. **Preferível** ao cliente base.

## Estrutura do handler

```javascript
exports.handler = async (event) => {
  let body;
  let statusCode = 200;
  const headers = { "Content-Type": "application/json" };

  try {
    switch (event.routeKey) {
      // casos das rotas
    }
  } catch (err) {
    statusCode = 400;
    body = err.message;
  } finally {
    body = JSON.stringify(body);
  }
  return { statusCode, body, headers };
};
```

| Elemento | Uso |
|---|---|
| `event.routeKey` | Rota chamada (ex.: `"GET /items"`) |
| `event.body` | Corpo HTTP — string, precisa de `JSON.parse` |
| `event.pathParameters.id` | Parâmetro de rota (`{id}`) |
| `try/catch/finally` | Erro → 400; `finally` sempre serializa body |

## Operações CRUD

| Rota | Método DynamoDB | Comportamento |
|---|---|---|
| `POST /items` | `put` | Insere ou **substitui** item inteiro |
| `GET /items` | `scan` | Lista todos (custoso — só por didática) |
| `GET /items/{id}` | `get` | Busca por chave primária |
| `PUT /items/{id}` | `update` | **Atualização parcial** via `UpdateExpression` |
| `DELETE /items/{id}` | `delete` | Remove pela chave |

### Diferença chave: `put` vs `update`

- **`put`** → substitui o item inteiro (`Item` recebe o objeto completo).
- **`update`** → modifica só os campos do `UpdateExpression`, preserva os demais.

### Exemplo do `update` parcial

```javascript
await dynamo.update({
  TableName: "Product",
  Key: { id: event.pathParameters.id },
  UpdateExpression: "set price = :r",
  ExpressionAttributeValues: { ":r": requestJSON.price }
}).promise();
```

- `UpdateExpression`: o que alterar
- `ExpressionAttributeValues`: bind dos valores referenciados (`:r`)

### Default case

```javascript
default:
  throw new Error(`Unsupported route: "${event.routeKey}"`);
```

Cai no `catch` → 400 com mensagem.

## Equivalente Python (boto3)

```python
import boto3
dynamodb = boto3.resource("dynamodb")
table = dynamodb.Table("Product")
```

Diferenças importantes JS → Python:

| Aspecto | JS (aws-sdk) | Python (boto3) |
|---|---|---|
| Import | `require("aws-sdk")` | `import boto3` |
| Tabela | passada em cada call | `dynamodb.Table("Product")` |
| Assíncrono | `.promise()` | síncrono nativo |
| Parse body | `JSON.parse(event.body)` | `json.loads(event["body"])` |
| Switch | `switch (event.routeKey)` | `if/elif` (sem `match` ≤3.10) |

## Deploy

1. Editor do console Lambda → ajustar `TableName` para casar com a tabela criada (`"Product"`)
2. **Deploy** publica a versão atual
3. ⚠️ Verificar que a execution role tem permissão de leitura/escrita no DynamoDB **antes** de testar

---

## Entidades e conceitos tocados

- Entidades: [[entities/aws-lambda]], [[entities/amazon-dynamodb]], [[entities/amazon-api-gateway]]
- Conceitos: [[concepts/iam-role]], [[concepts/serverless]]
- Tópicos: [[topics/aws-security]]
