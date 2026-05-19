# API Gateway: Criação de API HTTP e Rotas integradas ao Lambda

## Visão Geral

Esta aula cria uma **API HTTP no API Gateway**, configura todas as **rotas** correspondentes às operações CRUD implementadas na função Lambda na aula anterior, e prepara a integração entre os dois serviços.

---

## 1. O que é o API Gateway?

O **Amazon API Gateway** é o serviço da AWS para criar, publicar e gerenciar **APIs**. Ele atua como a "porta de entrada" das requisições HTTP, direcionando-as para os serviços de backend (neste caso, o Lambda).

```
Cliente HTTP → API Gateway (rotas) → Lambda → DynamoDB
```

---

## 2. Tipos de API disponíveis

| Tipo | Descrição | Quando usar |
|---|---|---|
| **HTTP API** | Mais simples, menor latência e custo | Maioria dos casos — integração com Lambda e backends HTTP |
| **REST API** | Mais completa, com mais recursos de gerenciamento | APIs complexas com necessidade de throttling, caching, etc. |
| **WebSocket API** | Comunicação bidirecional em tempo real | Chats, notificações em tempo real |

> ✅ Neste curso é utilizada a **HTTP API** — mais simples, de menor custo e suficiente para o caso de uso do projeto.

---

## 3. Criando a API HTTP

### Passo a passo no console

1. Acessar o console AWS → **API Gateway**
2. Clicar em **Create API**
3. Selecionar o tipo **HTTP API**
4. Definir o **nome da API** (ex: `products-api`)
5. Configurar o **Auto-deploy**

### Auto-deploy

| Configuração | Comportamento |
|---|---|
| **Auto-deploy ativado** ✅ | Qualquer alteração feita na API é publicada automaticamente no stage |
| **Auto-deploy desativado** | É necessário fazer um **redeploy manual** para ativar as alterações |

> 📌 Com auto-deploy ativado, o trabalho de publicar alterações é eliminado — recomendado para ambientes de desenvolvimento.

### Stage e Invoke URL

Ao criar a API, um **stage** padrão (`$default`) é gerado automaticamente. Junto com ele, é gerada a **Invoke URL** — a URL pública base da API:

```
https://<api-id>.execute-api.<região>.amazonaws.com/
```

> 📌 Essa URL será usada para testar a API e integrá-la com o frontend ou ferramentas como Postman/Insomnia.

---

## 4. Criando as Rotas

As rotas do API Gateway devem corresponder **exatamente** às chaves definidas no `switch` da função Lambda (`event.routeKey`).

### Rotas criadas

| Método | Rota | Operação | Lambda case |
|---|---|---|---|
| `POST` | `/items` | Inserir item | `POST /items` |
| `DELETE` | `/items/{id}` | Deletar item por ID | `DELETE /items/{id}` |
| `GET` | `/items/{id}` | Buscar item por ID | `GET /items/{id}` |
| `GET` | `/items` | Listar todos os itens | `GET /items` |
| `PUT` | `/items/{id}` | Atualizar item por ID | `PUT /items/{id}` |

### Como criar uma rota

1. No painel da API criada, acessar **Routes** → **Create**
2. Selecionar o **método HTTP** (GET, POST, PUT, DELETE)
3. Informar o **path** da rota (ex: `/items` ou `/items/{id}`)
4. Repetir para cada rota

### Parâmetro de rota `{id}`

O `{id}` entre chaves indica um **parâmetro dinâmico** na URL. Ao chamar a rota, o valor passado na URL é automaticamente disponibilizado no Lambda via `event.pathParameters.id`.

```
Chamada:  DELETE /items/prod-0001
Lambda:   event.pathParameters.id → "prod-0001"
```

---

## 5. Estrutura de Rotas no Console

Após criar todas as rotas, a estrutura visual no console fica:

```
/items
├── GET        → listar todos (Scan)
└── POST       → inserir item

/items/{id}
├── GET        → buscar por ID
├── DELETE     → deletar por ID
└── PUT        → atualizar por ID
```

---

## 6. Próximos Passos

Com as rotas criadas, o próximo passo é configurar a **integração** de cada rota com a função Lambda — apontando para a função correta que processará as requisições.

Após a integração:
1. Cada rota receberá requisições HTTP
2. O API Gateway repassará o evento para a função Lambda
3. A função executará a operação correspondente no DynamoDB
4. O resultado será retornado ao cliente

---

## Resumo do Fluxo Completo até aqui

```
[Cliente HTTP]
      ↓  requisição HTTP (ex: POST /items)
[API Gateway]
      ↓  evento com routeKey, body, pathParameters
[Lambda - switch(event.routeKey)]
      ↓  operação DynamoDB (put/get/delete/update/scan)
[DynamoDB - tabela "Product"]
      ↓  resposta
[Lambda]
      ↓  { statusCode, body, headers }
[API Gateway]
      ↓  resposta HTTP
[Cliente HTTP]
```

---

*Aula 03 — Módulo API Gateway + Lambda | Curso AWS*
