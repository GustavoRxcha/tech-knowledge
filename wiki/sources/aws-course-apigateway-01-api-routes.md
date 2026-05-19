---
title: "Curso AWS — API Gateway 01: Criação de API HTTP e Rotas"
type: source
tags: [aws, api-gateway, http-api, rotas, curso]
created: 2026-05-19
updated: 2026-05-19
sources: 1
---

# Curso AWS — API Gateway 01: Criação de API HTTP e Rotas

Arquivo fonte: `raw/aula-apigateway-01-criacao-api-rotas.md` (PT-BR)

Cria uma **HTTP API** no [[entities/amazon-api-gateway|API Gateway]] e define todas as rotas CRUD que serão integradas à Lambda construída em [[sources/aws-course-dynamo-02-lambda-crud]].

---

## Pontos-chave

- [[entities/amazon-api-gateway|API Gateway]] é a "porta de entrada" HTTP → Lambda → DynamoDB.
- 3 tipos de API disponíveis:

| Tipo | Quando usar |
|---|---|
| **HTTP API** ✅ | Maioria dos casos — menos latência e custo |
| **REST API** | APIs complexas (throttling, caching, etc.) |
| **WebSocket API** | Comunicação bidirecional em tempo real |

- **Auto-deploy** ativado publica mudanças automaticamente no stage padrão (`$default`) — recomendado para dev.
- **Invoke URL** gerada automaticamente: `https://<api-id>.execute-api.<região>.amazonaws.com/`
- **Rotas devem casar exatamente** com as chaves do `switch (event.routeKey)` na Lambda.
- Parâmetros dinâmicos na URL usam chaves: `{id}` → chega na Lambda como `event.pathParameters.id`.

## Rotas criadas (todas integram à mesma Lambda)

| Método | Path | Operação |
|---|---|---|
| `POST` | `/items` | Inserir item |
| `GET` | `/items` | Listar todos (`scan`) |
| `GET` | `/items/{id}` | Buscar por ID |
| `PUT` | `/items/{id}` | Atualizar item |
| `DELETE` | `/items/{id}` | Deletar |

Estrutura visual no console:

```
/items
├── GET    → listar
└── POST   → inserir

/items/{id}
├── GET    → buscar
├── PUT    → atualizar
└── DELETE → deletar
```

## Como criar uma rota

1. Painel da API → **Routes → Create**
2. Selecionar método HTTP
3. Informar path (ex.: `/items`, `/items/{id}`)
4. Repetir para cada rota

## Parâmetro de rota

```
DELETE /items/prod-0001
                 ↓
event.pathParameters.id === "prod-0001"
```

## Próximo passo

Configurar a **integração** de cada rota com a função Lambda — apontando para a função correta que processa as requisições. Ver [[sources/aws-course-apigateway-02-integration-postman]].

---

## Entidades e conceitos tocados

- Entidades: [[entities/amazon-api-gateway]] (novo), [[entities/aws-lambda]]
- Tópicos: [[topics/aws-security]]
