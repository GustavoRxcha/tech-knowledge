---
title: "Amazon DynamoDB"
type: entity
tags: [aws, dynamodb, banco-de-dados, nosql, serverless]
created: 2026-05-18
updated: 2026-05-19
sources: 3
---

# Amazon DynamoDB

Banco de dados **[[concepts/nosql|NoSQL]] gerenciado e [[concepts/serverless|serverless]]** da [[entities/aws|AWS]]. Mistura key-value e document. Escala automática, alta disponibilidade, latência consistente.

---

## Modelo de dados

| Bloco | O que é |
|---|---|
| **Tabela** | Conjunto de itens |
| **Item** | Equivalente a uma "linha"; coleção de atributos |
| **Atributo** | Par chave/valor — colunas variáveis por item |

> Schemaless: cada item pode ter atributos diferentes. Só as **chaves** são obrigatórias.

## Chaves

| Chave | Função |
|---|---|
| **Partition Key** | Obrigatória. Identifica unicamente cada item (ou particiona o grupo de itens). |
| **Sort Key** | Opcional. Junto com a Partition Key forma uma chave composta — a combinação deve ser única. |

Tipos suportados em chaves: `String (S)`, `Number (N)`, `Binary (B)`.

### Exemplo

| Partition Key | Sort Key | Resto |
|---|---|---|
| `product_id = "prod-0001"` | `title = "Batata"` | `price`, `name`, etc. |

## Métodos de consulta

| Método | Custo | Recomendação |
|---|---|---|
| **Query** | Baixo — usa Partition Key (+ opcional Sort Key) | ✅ Padrão em produção |
| **Scan** | Alto — varre toda a tabela | ⚠️ Evitar em produção |

Regra prática: **se você precisa de Scan, provavelmente o modelo de dados está errado** (faltou um índice ou key apropriada).

## Operações SDK (Node.js — DocumentClient)

| Operação | Método | Comportamento |
|---|---|---|
| Inserir / substituir item | `put` | Sobrescreve item inteiro pela chave |
| Buscar por chave | `get` | Retorna item único |
| Atualizar parcial | `update` + `UpdateExpression` | Modifica só os campos especificados |
| Deletar por chave | `delete` | Remove item |
| Listar tudo | `scan` | Caro — só admin/debug/tabelas pequenas |

Exemplo de update parcial:

```javascript
await dynamo.update({
  TableName: "Product",
  Key: { id: pathId },
  UpdateExpression: "set price = :r",
  ExpressionAttributeValues: { ":r": newPrice }
}).promise();
```

## DocumentClient (JS) vs cliente base

- **`DocumentClient`** ✅ — trabalha com objetos JS nativos; converte tipos automaticamente.
- **Cliente base** — exige especificar tipos (`{"S": "..."}`, `{"N": "..."}`).

Em Python o equivalente é `boto3.resource("dynamodb")` (resource interface) — mesma conveniência.

## ARN

```
arn:aws:dynamodb:<região>:<conta>:table/<nome-da-tabela>
```

Necessário em policies que escopam acesso à tabela.

## Permissões IAM relevantes

| Action | Uso |
|---|---|
| `dynamodb:GetItem` | get |
| `dynamodb:PutItem` | put |
| `dynamodb:UpdateItem` | update |
| `dynamodb:DeleteItem` | delete |
| `dynamodb:Scan` | scan |
| `dynamodb:Query` | query |

Em produção, prefira uma [[concepts/customer-managed-policy|customer-managed policy]] restrita ao recurso/ações necessárias em vez de `AmazonDynamoDBFullAccess`.

## Integração típica

```
Lambda (com execution role) ─ put/get/update/delete ─→ DynamoDB
```

A Lambda usa as credenciais temporárias da [[concepts/iam-role|execution role]] — nunca hardcodar.

## Boas práticas

- ✅ Query > Scan
- ✅ Nome de tabela em **constante** ou env var
- ✅ Policies restritas (action + ARN da tabela)
- ✅ Todos os serviços na mesma região
- ✅ Modelar chaves pensando nos padrões de acesso primeiro

## Lacunas

- GSIs / LSIs (índices secundários)
- Streams
- Transactions
- Capacidade on-demand vs provisioned
- Consistência forte vs eventual
- TTL, encryption at rest, backups

> [!question] Aprofundar quando o curso voltar ao DynamoDB ou em uma ingestão dedicada.

## Fontes

- [[sources/aws-course-04-iam-groups]] — menção inicial
- [[sources/aws-course-dynamo-01-table-lambda-intro]] — modelo de dados, chaves, Query/Scan
- [[sources/aws-course-dynamo-02-lambda-crud]] — operações via SDK

## Relações

- [[entities/aws]]
- [[entities/aws-lambda]] — consumidor típico
- [[concepts/nosql]]
- [[concepts/serverless]]
- [[concepts/arn]]
- [[concepts/iam-role]]
