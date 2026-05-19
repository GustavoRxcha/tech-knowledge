---
title: "Amazon API Gateway"
type: entity
tags: [aws, api-gateway, http, rotas, integração]
created: 2026-05-19
updated: 2026-05-19
sources: 2
---

# Amazon API Gateway

Serviço gerenciado da [[entities/aws|AWS]] para criar, publicar e gerenciar **APIs HTTP/REST/WebSocket**. Atua como porta de entrada das requisições, roteando-as para backends — tipicamente [[entities/aws-lambda|Lambda]].

---

## Posição na arquitetura

```
Cliente HTTP → API Gateway (rotas + auth) → Lambda → DynamoDB / S3 / outro
```

## Tipos de API

| Tipo | Quando usar |
|---|---|
| **HTTP API** ✅ | Maioria dos casos — menor latência e custo |
| **REST API** | APIs complexas (throttling, caching, validação avançada) |
| **WebSocket API** | Comunicação bidirecional em tempo real (chats, pushes) |

> O curso usa **HTTP API** — suficiente para integração Lambda + CRUD.

## Conceitos centrais

| Conceito | O que é |
|---|---|
| **Route** | Combinação `método + path`, ex.: `POST /items` |
| **Integration** | Onde a route encaminha a requisição (Lambda, HTTP backend, mock) |
| **Stage** | Ambiente publicado da API (`$default` é o padrão) |
| **Invoke URL** | URL pública do stage: `https://<api-id>.execute-api.<região>.amazonaws.com/` |
| **Authorizer** | Filtro de auth executado antes da integration (tipicamente valida [[concepts/jwt\|JWT]]) |

## Parâmetros dinâmicos

`/items/{id}` → o valor passado chega na Lambda como `event.pathParameters.id`.

## Auto-deploy

Quando ativo, qualquer mudança na API é publicada automaticamente no stage. Recomendado para dev — elimina o redeploy manual.

## Padrão: uma Lambda + várias rotas

Mesma função Lambda pode servir múltiplas rotas. A Lambda decide o que fazer via `event.routeKey`:

```javascript
switch (event.routeKey) {
  case "POST /items":    /* ... */ break;
  case "GET /items/{id}": /* ... */ break;
}
```

Reduz a duplicação de integrações e mantém o roteamento dentro do código.

## Authorizers — segurança na borda

Bloqueiam requisições antes de gastar invocação Lambda. Casos típicos:

- Validar [[concepts/jwt|JWT]] emitido pelo [[entities/aws-cognito|Cognito]]
- Lambda authorizer customizado
- IAM-based authorizer

## Boas práticas (do curso)

- ✅ API e Lambda na **mesma região**
- ✅ Path parameters com `{nome}` consistentes com o `routeKey` da Lambda
- ✅ Auto-deploy em dev; controle de deploy em prod
- ✅ Adicionar authorizer antes de expor publicamente

## Fontes

- [[sources/aws-course-apigateway-01-api-routes]]
- [[sources/aws-course-apigateway-02-integration-postman]]

## Lacunas

- Custom domain, CORS detalhado, throttling, usage plans, API keys, mapping templates, request validation — pendentes.

## Relações

- [[entities/aws]]
- [[entities/aws-lambda]] — backend default
- [[entities/aws-cognito]] — fornece JWT para authorizers
- [[concepts/jwt]]
