---
title: "Amazon SNS (Simple Notification Service)"
type: entity
tags: [aws, sns, mensageria, pub-sub, notificacoes, desacoplamento]
created: 2026-05-20
updated: 2026-05-20
sources: 1
---

# Amazon SNS — Simple Notification Service

Serviço de **publicação e assinatura (Pub/Sub)** gerenciado da [[entities/aws|AWS]]. Ao contrário do [[entities/amazon-sqs|SQS]] (one-to-one), o SNS envia uma mensagem para **múltiplos destinatários simultaneamente**.

---

## Conceito central: Tópico (Topic)

Canal de comunicação baseado em **assunto**. Sistemas interessados tornam-se **assinantes (subscribers)**.

```
[Publicador]     [Tópico SNS]       [Assinantes]
MS Fraude  →  "compra-autorizada" → MS E-mail
                                  → MS Estoque
                                  → App Mobile (push)
```

**Analogia:** como uma revista — quando publicada, **todos os assinantes recebem** a mesma edição ao mesmo tempo.

---

## Como funciona (Pub/Sub)

1. Um **publicador** publica uma mensagem em um tópico
2. Todos os **assinantes** daquele tópico recebem a mensagem simultaneamente
3. Cada assinante processa de forma independente

---

## Casos de uso

- Notificações de eventos para múltiplos sistemas
- Envio de **e-mails, SMS e push notifications**
- **Fanout** — distribuir uma mensagem para múltiplas filas SQS simultaneamente
- Alertas de monitoramento (CloudWatch → SNS → e-mail)

---

## SQS vs SNS

| | SQS | SNS |
|---|---|---|
| Modelo | Fila (one-to-one) | Tópico Pub/Sub (one-to-many) |
| Destinatários | Um por vez | Múltiplos simultaneamente |
| Comunicação | Assíncrona (pull) | Assíncrona (push) |
| Após leitura | Apagada | Entregue a todos e descartada |

---

## Padrão fanout (SNS + SQS)

O SNS distribui para múltiplas filas SQS — máximo desacoplamento + máxima resiliência:

```
[Evento] → [Tópico SNS] → [Fila SQS A] → [MS A]
                        → [Fila SQS B] → [MS B]
                        → [Fila SQS C] → [MS C]
```

---

## Para a prova CLF-C02

- *"Qual serviço envia uma mensagem para múltiplos destinatários simultaneamente?"* → **SNS**
- *"Um sistema precisa notificar e-mail, estoque e app mobile ao mesmo tempo. Qual serviço?"* → **SNS**

---

## Relações

- [[entities/amazon-sqs]] — complementar; SNS pode enviar para filas SQS (fanout)
- [[concepts/pub-sub]] — o padrão que o SNS implementa
- [[concepts/microservices]] — SNS desacopla serviços em arquiteturas orientadas a eventos
- [[entities/aws-lambda]] — Lambda pode ser assinante de tópicos SNS

## Fontes

- [[sources/clf-c02-aula12-messaging-sqs-sns]]
