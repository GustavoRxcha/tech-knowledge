# API Gateway: Integração com Lambda, Permissões e Testes com Postman

## Visão Geral

Esta aula conclui a configuração da arquitetura **API Gateway + Lambda + DynamoDB**, realizando a integração entre as rotas criadas e a função Lambda, corrigindo erros de permissão via IAM, e validando todas as operações CRUD através do **Postman**.

---

## 1. Integrando as Rotas ao Lambda

Com as rotas criadas no API Gateway, o próximo passo é configurar a **integração** de cada rota com a função Lambda.

### Passo a passo

1. No console do API Gateway, acessar a rota desejada (ex: `POST /items`)
2. Clicar em **Attach integration** → **Create and attach an integration**
3. Selecionar o tipo: **Lambda function**
4. ⚠️ **Verificar a região** — a função Lambda deve estar na **mesma região** da API
5. Selecionar a função Lambda correspondente
6. Confirmar

> ✅ A mesma integração Lambda é usada para **todas as rotas** — não é necessário criar uma integração separada por rota. O Lambda identifica qual operação executar através do `event.routeKey`.

### Auto-deploy

Como o **auto-deploy** foi habilitado na criação da API, não é necessário fazer redeploy manual após cada alteração. As mudanças são publicadas automaticamente.

---

## 2. Authorizers — Filtros de Autenticação

O API Gateway permite configurar **authorizers** (autorizadores) — filtros de autenticação que são executados **antes** de a requisição chegar ao Lambda.

### Casos de uso

- Validar um **token JWT** (ex: gerado pelo Cognito)
- Verificar permissões de usuário antes de executar a operação
- Bloquear requisições não autorizadas na camada da API

> 📌 Os authorizers serão implementados em uma próxima etapa do curso, integrando o **Cognito** como provedor de autenticação. Nesta aula, a API ainda está sem autenticação.

---

## 3. Erro de Permissão — Lambda sem acesso ao DynamoDB

### Sintoma

Ao testar a primeira requisição (`GET /items`), a API retornou:

```
User is not authorized to perform: dynamodb:PutItem on resource: arn:aws:dynamodb:...
```

### Causa

A **execution role** da função Lambda não tinha permissão para acessar o DynamoDB.

### Solução: Adicionar política ao role da Lambda

1. Acessar o console **Lambda** → selecionar a função
2. Ir em **Configuration** → **Permissions**
3. Clicar na **role de execução** (abre o console IAM)
4. Clicar em **Add permissions** → **Attach policies**
5. Pesquisar por `DynamoDB`
6. Selecionar **`AmazonDynamoDBFullAccess`**
7. Clicar em **Attach policies**

> ⚠️ **Atenção:** A política `AmazonDynamoDBFullAccess` concede acesso total ao DynamoDB. Em produção, o ideal é criar uma **policy customizada** com acesso apenas à tabela específica e às operações necessárias (princípio do menor privilégio). Nesta aula, a política ampla é usada apenas para fins didáticos.

### Exemplo de policy restrita (recomendada para produção)

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

---

## 4. Erro no Código — Nome de Tabela Incorreto

Durante os testes foi identificado um erro no código Lambda: o nome da tabela estava **diferente** entre os métodos (resultado de um copy/paste de código de referência).

### Lição aprendida

> 📌 Sempre usar uma **variável de ambiente** ou **constante** para o nome da tabela, evitando inconsistências:

```javascript
// JavaScript
const TABLE_NAME = "Product";

// Usar TABLE_NAME em todas as operações
await dynamo.put({ TableName: TABLE_NAME, ... }).promise();
```

```python
# Python
TABLE_NAME = "Product"
table = dynamodb.Table(TABLE_NAME)
```

---

## 5. Testes com Postman

Após corrigir as permissões, todas as operações foram testadas com o **Postman**.

### O que é o Postman?

Ferramenta para testar e interagir com APIs HTTP — permite enviar requisições com diferentes métodos (GET, POST, PUT, DELETE), configurar headers, body e autenticação.

### Base URL da API

```
https://<api-id>.execute-api.<região>.amazonaws.com
```

---

### Teste 1 — POST /items (Inserir produto)

**Requisição:**
```http
POST /items
Content-Type: application/json

{
  "id": "prod-0001",
  "name": "Produto Teste",
  "price": 99.90
}
```

**Resposta:** `200 OK` — `"Put item prod-0001"`

**Verificação:** Item visível na tabela do DynamoDB no console AWS.

---

### Teste 2 — GET /items (Listar todos os produtos)

**Requisição:**
```http
GET /items
```

**Resposta:** `200 OK` — lista com todos os itens da tabela

> 📌 Internamente, usa o método `scan` do DynamoDB — retorna todos os itens.

---

### Teste 3 — GET /items/{id} (Buscar produto por ID)

**Requisição:**
```http
GET /items/prod-0001
```

**Resposta:** `200 OK` — objeto JSON com os dados do produto

> 📌 O `prod-0001` na URL vira `event.pathParameters.id` no Lambda, usado como **partition key** na consulta ao DynamoDB.

---

### Teste 4 — PUT /items/{id} (Atualizar preço)

**Requisição:**
```http
PUT /items/prod-0001
Content-Type: application/json

{
  "price": 320000
}
```

**Resposta:** `200 OK` — `"Put item prod-0001"`

**Verificação:** Preço atualizado no DynamoDB — apenas o campo `price` foi modificado, os demais atributos (`name`, `id`) foram preservados.

> 📌 O método `update` com `UpdateExpression` garante a **atualização parcial** — apenas os campos especificados são alterados.

---

### Teste 5 — DELETE /items/{id} (Deletar produto)

**Requisição:**
```http
DELETE /items/prod-0001
```

**Resposta:** `200 OK` — `"Deleted item prod-0001"`

**Verificação:** Item removido da tabela no console DynamoDB.

---

### Resumo dos testes

| Operação | Método | Rota | Resultado |
|---|---|---|---|
| Inserir produto | `POST` | `/items` | ✅ Item criado no DynamoDB |
| Listar produtos | `GET` | `/items` | ✅ Lista retornada |
| Buscar por ID | `GET` | `/items/{id}` | ✅ Item encontrado |
| Atualizar preço | `PUT` | `/items/{id}` | ✅ Preço atualizado |
| Deletar produto | `DELETE` | `/items/{id}` | ✅ Item removido |

---

## 6. Arquitetura Final do Módulo

```
[Postman / Cliente HTTP]
         ↓
[API Gateway - HTTP API]
  ├── POST   /items          ──┐
  ├── GET    /items          ──┤
  ├── GET    /items/{id}     ──┼──→ [Lambda Function]
  ├── PUT    /items/{id}     ──┤         ↓
  └── DELETE /items/{id}    ──┘   [DynamoDB - tabela "Product"]
```

---

## 7. Próximos Passos do Curso

A arquitetura base está completa. As próximas evoluções planejadas incluem:

| Próxima etapa | Descrição |
|---|---|
| **Autenticação com Cognito** | Adicionar authorizer no API Gateway com tokens JWT |
| **Frontend** | Interface web consumindo a API autenticada |
| **Hospedagem estática** | Publicar o frontend no **S3 + CloudFront** |

---

## Boas Práticas Reforçadas

- ✅ Verificar sempre a **região** de todos os serviços envolvidos
- ✅ Usar **variáveis/constantes** para nomes de tabelas e recursos
- ✅ Usar **policies restritas** na role do Lambda em produção (não `FullAccess`)
- ✅ Testar cada rota individualmente antes de avançar
- ✅ Verificar o resultado diretamente no console do DynamoDB para confirmar as operações

---

*Aula 04 — Módulo API Gateway + Lambda | Encerramento do módulo prático*
