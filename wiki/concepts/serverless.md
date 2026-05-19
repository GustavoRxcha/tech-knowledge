---
title: "Serverless"
type: concept
tags: [arquitetura, serverless, faas, computação]
created: 2026-05-19
updated: 2026-05-19
sources: 2
---

# Serverless

Modelo de execução em que o desenvolvedor **não provisiona nem gerencia servidores**. O provedor de nuvem aloca recursos sob demanda, escala automaticamente e cobra pela execução real (não pelo tempo ocioso).

---

## Princípios

- **Sem servidor visível** (na prática há, mas é invisível para você).
- **Escala automática** — concorrência sobe com a carga.
- **Pay-per-use** — não paga por idle.
- **Eventos como gatilho** — funções respondem a HTTP, mensagens, mudanças em storage, schedule, etc.
- **Stateless por padrão** — estado vai para serviços externos (banco, cache).

## Implementações no contexto AWS

| Categoria | Serviço |
|---|---|
| **FaaS** (Function-as-a-Service) | [[entities/aws-lambda]] |
| **NoSQL serverless** | [[entities/amazon-dynamodb]] |
| **API serverless** | [[entities/amazon-api-gateway]] |
| **Auth serverless** | [[entities/aws-cognito]] |

Combinados formam uma stack completamente serverless — o padrão construído no curso.

## Vantagens

- **Custo**: paga só pela execução; idle é grátis.
- **Operação**: zero patching, zero scaling manual, zero capacity planning.
- **Tempo de entrega**: subir um endpoint HTTP é minutos, não dias.
- **Microsserviços naturais**: funções pequenas e independentes.

## Trade-offs

- **Cold start** — primeira invocação após inatividade tem latência extra (varia por runtime/memória).
- **Vendor lock-in** — APIs específicas da nuvem.
- **Limites duros** — Lambda tem 15min de execução, payload máximo, etc.
- **Debugging distribuído** mais difícil — logs/tracing exigem ferramentas (CloudWatch, X-Ray).
- **Custo pode escalar mal** sob altíssima carga sustentada (containers/EC2 ficam mais baratos a certo ponto).

## Padrão da arquitetura do curso

```
HTTP → API Gateway → Lambda → DynamoDB
```

Tudo serverless. Sem nenhuma VM. Sem nenhum container. Sem `cron`. Escala de 0 a N automaticamente.

## Fontes

- [[sources/aws-course-dynamo-01-table-lambda-intro]]
- [[sources/aws-course-dynamo-02-lambda-crud]]

## Relações

- [[entities/aws-lambda]] — exemplo canônico de FaaS
- [[entities/amazon-dynamodb]] — NoSQL serverless
- [[entities/amazon-api-gateway]] — API serverless
- [[entities/aws-cognito]] — auth serverless
