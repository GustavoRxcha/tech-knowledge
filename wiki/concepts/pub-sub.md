---
title: "Pub/Sub (Publisher/Subscriber)"
type: concept
tags: [arquitetura, pub-sub, mensageria, sns, desacoplamento]
created: 2026-05-20
updated: 2026-05-20
sources: 1
---

# Pub/Sub (Publisher/Subscriber)

**Pub/Sub** é um padrão de comunicação assíncrona onde um **publicador** envia mensagens para um **tópico** e todos os **assinantes** daquele tópico recebem a mensagem simultaneamente, sem o publicador precisar conhecê-los individualmente.

---

## Componentes

- **Publicador (Publisher):** envia a mensagem para um tópico — não sabe quem vai receber
- **Tópico (Topic):** canal de comunicação identificado por assunto
- **Assinante (Subscriber):** registrado no tópico; recebe todas as mensagens publicadas nele

---

## Fluxo

```
[Publicador] → publica mensagem → [Tópico]
                                      ↓ distribui
                              [Assinante 1]
                              [Assinante 2]
                              [Assinante 3]
```

---

## Por que usar

- **Desacoplamento:** publicador e assinantes não se conhecem diretamente
- **Flexibilidade:** novos assinantes podem ser adicionados sem mudar o publicador
- **Simultaneidade:** todos os assinantes recebem a mensagem ao mesmo tempo
- **Fanout:** um evento gera múltiplas reações paralelas

---

## Pub/Sub vs Fila (Queue)

| | Pub/Sub (SNS) | Fila (SQS) |
|---|---|---|
| Destinatários | Múltiplos (todos os assinantes) | Um por vez (um consumidor) |
| Entrega | Push (empurra para os assinantes) | Pull (consumidor busca) |
| Após entrega | Mensagem descartada | Consumidor apaga a mensagem |
| Modelo | One-to-many | One-to-one |

---

## Implementação na AWS

O [[entities/amazon-sns|Amazon SNS]] implementa o padrão Pub/Sub. O padrão **fanout** combina SNS + [[entities/amazon-sqs|SQS]]:

```
[Evento] → [Tópico SNS] → [Fila SQS A] → [MS A]
                        → [Fila SQS B] → [MS B]
```

---

## Relações

- [[entities/amazon-sns]] — implementação AWS do padrão Pub/Sub
- [[entities/amazon-sqs]] — complementar; padrão de fila (alternativo/combinável)
- [[concepts/microservices]] — Pub/Sub é o mecanismo de desacoplamento em arquiteturas de microsserviços

## Fontes

- [[sources/clf-c02-aula12-messaging-sqs-sns]]
