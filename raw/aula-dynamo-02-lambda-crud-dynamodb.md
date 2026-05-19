# AWS Lambda: Função de CRUD com DynamoDB

## Visão Geral

Esta aula implementa uma **função Lambda em Node.js** que realiza operações de **CRUD** (Create, Read, Update, Delete) em uma tabela do **DynamoDB**. A função recebe eventos do **API Gateway**, identifica a rota chamada e executa a operação correspondente no banco de dados.

---

## 1. Arquitetura da Função

```
Cliente HTTP
    ↓
API Gateway (rotas)
    ↓
Lambda (switch por rota)
    ↓
DynamoDB (tabela "Product")
```

A função Lambda atua como camada intermediária entre o API Gateway e o DynamoDB. Ela:
1. Recebe o evento do API Gateway com a rota (`event.routeKey`) e dados (`event.body`, `event.pathParameters`)
2. Executa a operação correta no DynamoDB
3. Retorna a resposta HTTP com `statusCode`, `body` e `headers`

---

## 2. Dependências e Inicialização

```javascript
const AWS = require("aws-sdk");
const dynamo = new AWS.DynamoDB.DocumentClient();
```

- **`aws-sdk`** — SDK oficial da AWS para Node.js, já disponível no ambiente Lambda (não precisa instalar)
- **`DynamoDB.DocumentClient`** — cliente de alto nível do DynamoDB que trabalha diretamente com objetos JavaScript, sem necessidade de especificar tipos de dados manualmente

> 📌 O `DocumentClient` é preferível ao cliente base do DynamoDB por ser mais simples — converte automaticamente os tipos JS para o formato interno do DynamoDB.

---

## 3. Estrutura Geral do Handler

```javascript
exports.handler = async (event) => {
    let body;
    let statusCode = 200;
    const headers = { "Content-Type": "application/json" };

    try {
        switch (event.routeKey) {
            // casos de cada rota
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

### Pontos importantes

| Elemento | Descrição |
|---|---|
| `event.routeKey` | Identifica qual rota foi chamada (ex: `"GET /items"`) |
| `event.body` | Corpo da requisição HTTP (string JSON — precisa de `JSON.parse`) |
| `event.pathParameters.id` | Parâmetro de rota (ex: o `{id}` em `GET /items/{id}`) |
| `try/catch/finally` | Erros retornam `statusCode 400`; o `finally` sempre serializa o body |

---

## 4. Operações CRUD Implementadas

### POST /items — Inserir item

```javascript
case "POST /items":
    requestJSON = JSON.parse(event.body);
    await dynamo.put({
        TableName: "Product",
        Item: {
            id: requestJSON.id,
            price: requestJSON.price,
            name: requestJSON.name
        }
    }).promise();
    body = `Put item ${requestJSON.id}`;
    break;
```

- Usa o método **`put`** — insere ou **substitui** o item se a chave já existir
- Lê `id`, `price` e `name` do corpo da requisição

---

### DELETE /items/{id} — Deletar item

```javascript
case "DELETE /items/{id}":
    await dynamo.delete({
        TableName: "Product",
        Key: { id: event.pathParameters.id }
    }).promise();
    body = `Deleted item ${event.pathParameters.id}`;
    break;
```

- Usa o método **`delete`** — remove o item pela chave primária (`id`)
- O `id` vem como parâmetro de rota (`pathParameters`)

---

### GET /items/{id} — Buscar item por ID

```javascript
case "GET /items/{id}":
    body = await dynamo.get({
        TableName: "Product",
        Key: { id: event.pathParameters.id }
    }).promise();
    break;
```

- Usa o método **`get`** — busca um único item pela chave primária
- Equivalente ao **Query** visto na aula anterior

---

### GET /items — Listar todos os itens

```javascript
case "GET /items":
    body = await dynamo.scan({ TableName: "Product" }).promise();
    break;
```

- Usa o método **`scan`** — retorna todos os itens da tabela
- ⚠️ Como discutido na aula anterior, **Scan é custoso em produção** — adequado apenas para tabelas pequenas ou uso administrativo

---

### PUT /items/{id} — Atualizar item

```javascript
case "PUT /items/{id}":
    requestJSON = JSON.parse(event.body);
    await dynamo.update({
        TableName: "Product",
        Key: { id: event.pathParameters.id },
        UpdateExpression: "set price = :r",
        ExpressionAttributeValues: { ":r": requestJSON.price }
    }).promise();
    body = `Put item ${event.pathParameters.id}`;
    break;
```

- Usa o método **`update`** — atualiza apenas os campos especificados (sem substituir o item inteiro)
- **`UpdateExpression`**: expressão que define quais campos atualizar (`set price = :r`)
- **`ExpressionAttributeValues`**: mapeamento dos valores usados na expressão (`:r` → `requestJSON.price`)

> 📌 Diferença entre `put` e `update`:
> - `put` → substitui o item inteiro
> - `update` → modifica apenas os campos especificados, preservando os demais

---

### Default — Rota não suportada

```javascript
default:
    throw new Error(`Unsupported route: "${event.routeKey}"`);
```

- Capturado pelo `catch`, retornando `statusCode 400` com a mensagem de erro

---

## 5. Equivalente em Python (boto3)

Para programadores Python, o mesmo comportamento é implementado com **boto3** (SDK AWS para Python):

```python
import json
import boto3

dynamodb = boto3.resource("dynamodb")
table = dynamodb.Table("Product")

def lambda_handler(event, context):
    status_code = 200
    headers = {"Content-Type": "application/json"}
    body = None

    try:
        route_key = event.get("routeKey")

        # POST /items — Inserir item
        if route_key == "POST /items":
            request_body = json.loads(event["body"])
            table.put_item(Item={
                "id": request_body["id"],
                "price": request_body["price"],
                "name": request_body["name"]
            })
            body = f"Put item {request_body['id']}"

        # DELETE /items/{id} — Deletar item
        elif route_key == "DELETE /items/{id}":
            item_id = event["pathParameters"]["id"]
            table.delete_item(Key={"id": item_id})
            body = f"Deleted item {item_id}"

        # GET /items/{id} — Buscar item por ID
        elif route_key == "GET /items/{id}":
            item_id = event["pathParameters"]["id"]
            response = table.get_item(Key={"id": item_id})
            body = response.get("Item", {})

        # GET /items — Listar todos os itens
        elif route_key == "GET /items":
            response = table.scan()
            body = response.get("Items", [])

        # PUT /items/{id} — Atualizar item
        elif route_key == "PUT /items/{id}":
            item_id = event["pathParameters"]["id"]
            request_body = json.loads(event["body"])
            table.update_item(
                Key={"id": item_id},
                UpdateExpression="set price = :r",
                ExpressionAttributeValues={":r": request_body["price"]}
            )
            body = f"Updated item {item_id}"

        else:
            raise ValueError(f'Unsupported route: "{route_key}"')

    except Exception as err:
        status_code = 400
        body = str(err)

    return {
        "statusCode": status_code,
        "body": json.dumps(body),
        "headers": headers
    }
```

### Diferenças JS → Python

| Aspecto | JavaScript (aws-sdk) | Python (boto3) |
|---|---|---|
| Import do SDK | `require("aws-sdk")` | `import boto3` |
| Cliente DynamoDB | `new AWS.DynamoDB.DocumentClient()` | `boto3.resource("dynamodb")` |
| Referência à tabela | passada em cada operação (`TableName`) | `dynamodb.Table("Product")` — referência direta |
| Async/await | `.promise()` em cada operação | nativo — boto3 é síncrono por padrão |
| Parse do body | `JSON.parse(event.body)` | `json.loads(event["body"])` |
| Switch/case | `switch (event.routeKey)` | `if/elif` (Python não tem switch nativo até 3.10+) |

---

## 6. Deploy da Função no Console Lambda

Após escrever o código:

1. No editor do console Lambda, ajustar o **nome da tabela** no código para corresponder à tabela criada no DynamoDB (ex: `"Product"`)
2. Clicar em **Deploy** — publica a versão atual da função
3. A função estará disponível para ser integrada ao **API Gateway** na próxima etapa

> ⚠️ Lembrar de verificar se a **role de execução** da função Lambda tem permissão de escrita e leitura no DynamoDB antes de testar.

---

## 7. Próximos Passos

- Configurar as **permissões DynamoDB** na role da função Lambda
- Criar as **rotas no API Gateway** integradas a esta função
- Testar o fluxo completo: `HTTP request → API Gateway → Lambda → DynamoDB`

---

*Aula 02 — Módulo DynamoDB + Lambda | Curso AWS*
