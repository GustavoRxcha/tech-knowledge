---
title: "CLF-C02 Aula 13 — Computação Sem Servidor: AWS Lambda"
type: source
tags: [aws, clf-c02, lambda, serverless, triggers, computacao]
created: 2026-05-20
updated: 2026-05-20
sources: 1
---

# CLF-C02 Aula 13 — Computação Sem Servidor: AWS Lambda

Conceito de serverless e o principal serviço serverless da AWS: Lambda. Triggers, modelo de cobrança, casos de uso e ecossistema serverless completo.

---

## Origem

- **Arquivo:** `raw/clf-c02-aula13-serverless-lambda.md`
- **Trilha:** CLF-C02 — Preparatório AWS Cloud Practitioner
- **Módulo:** Computação na AWS (aula 05 do módulo / aula 13 do curso)

---

## O que é serverless

Execução de código onde toda a infraestrutura (CPU, memória, SO, rede) é gerenciada automaticamente pelo provedor cloud. Você não provisiona, configura ou gerencia servidores.

> "Sem servidor" não significa que não há servidores — significa que você **não precisa se preocupar** com eles.

**EC2 vs Lambda:**

| Aspecto | EC2 (IaaS) | Lambda (Serverless) |
|---|---|---|
| Provisionar servidor | ✅ Você configura | ❌ Não necessário |
| Gerenciar SO | ✅ Você atualiza | ❌ Não necessário |
| Escalabilidade | Manual ou Auto Scaling | Automática e instantânea |
| Cobrança | Por hora da instância ligada | Por tempo de execução do código |

---

## AWS Lambda

Principal serviço serverless da AWS. Execução baseada em **eventos (triggers)**.

**Fluxo:**
```
[Escreve o código] → [Faz upload] → [Configura trigger] → [Evento ocorre] → Lambda executa
```

**Linguagens:** Python, Node.js, Java, Go, Ruby, C#/.NET e outras.

---

## Triggers — o que pode acionar uma função Lambda

| Trigger | Descrição |
|---|---|
| Upload no S3 | Arquivo cai em bucket → Lambda processa |
| Chamada HTTP | Requisição via API Gateway → Lambda responde |
| Mensagem no SQS | Mensagem entra na fila → Lambda consome |
| Evento do SNS | Tópico SNS publica → Lambda é notificada |
| Agendamento (EventBridge) | Horários definidos (ex: todo dia às 8h) |
| Mudança no DynamoDB | Item inserido/atualizado → Lambda reage |

> O Lambda é o "cola" entre serviços AWS — conecta eventos de um serviço a ações em outro.

---

## Modelo de cobrança

| Fator | Descrição |
|---|---|
| Número de invocações | Cada vez que a função é chamada |
| Tempo de execução (duração) | Medido em milissegundos × memória configurada |

**Nível gratuito permanente:** 1 milhão de invocações + 400.000 GB-segundos/mês.

---

## Ecossistema serverless na AWS

| Serviço | Função |
|---|---|
| **AWS Lambda** | Execução de código por evento |
| **Amazon API Gateway** | API HTTP serverless |
| **Amazon DynamoDB** | Banco NoSQL serverless |
| **Amazon S3** | Armazenamento serverless |
| **AWS Fargate** | Containers serverless |
| **Amazon EventBridge** | Barramento de eventos serverless |

---

## Conexão com o módulo prático

O Lambda foi usado extensivamente no curso prático (módulo Serverless): API Gateway → Lambda (switch routeKey) → DynamoDB. A aula CLF-C02 consolida os conceitos por trás dessa prática.

---

## Conceitos/entidades relacionados

- [[entities/aws-lambda]]
- [[concepts/serverless]]
- [[entities/amazon-api-gateway]]
- [[entities/amazon-sqs]]
- [[entities/amazon-sns]]
- [[entities/amazon-dynamodb]]
- [[entities/amazon-s3]]
