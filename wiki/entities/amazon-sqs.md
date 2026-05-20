---
title: "Amazon SQS (Simple Queue Service)"
type: entity
tags: [aws, sqs, mensageria, fila, desacoplamento, microsservicos, fifo]
created: 2026-05-20
updated: 2026-05-20
sources: 1
---

# Amazon SQS — Simple Queue Service

Serviço de **fila de mensagens** gerenciado da [[entities/aws|AWS]]. Permite que microsserviços se comuniquem de forma **assíncrona e desacoplada** através de uma estrutura de dados do tipo fila.

---

## Modelo: Produtor → Fila → Consumidor

```
[Produtor]          [Fila SQS]         [Consumidor]
MS Compras    →  [msg1][msg2][msg3]  →  MS Fraude
(enfileira)        (FIFO)              (lê, processa, apaga)
```

---

## Regras da fila

- **FIFO (First In, First Out):** primeiro a entrar é o primeiro a sair
- O consumidor faz **poll** (escuta ativa) na fila
- Ao processar uma mensagem, o consumidor a **apaga** da fila
- Se o consumidor estiver fora do ar, as mensagens **ficam na fila** — nada é perdido

---

## Por que usar

| Benefício | Descrição |
|---|---|
| **Desacoplamento** | Produtor e consumidor operam independentemente |
| **Resiliência** | Mensagens persistem na fila mesmo com falha do consumidor |
| **Escalabilidade** | Múltiplos consumidores podem ler da mesma fila em paralelo |
| **Ordem garantida** | Modo FIFO garante processamento em ordem de chegada |
| **Gerenciado** | Sem gerenciamento de infraestrutura da fila |

---

## Diferença do SNS

O SQS é **one-to-one** — um consumidor por vez. O [[entities/amazon-sns|SNS]] é **one-to-many** (Pub/Sub).

No **padrão fanout**, o SNS distribui para múltiplas filas SQS:
```
[Evento] → [Tópico SNS] → [Fila SQS 1] [Fila SQS 2] [Fila SQS 3]
                              ↓               ↓             ↓
                         [MS Estoque] [MS E-mail] [MS Relatório]
```

---

## Para a prova CLF-C02

- *"Qual serviço permite comunicação assíncrona com fila de mensagens?"* → **SQS**
- *"Qual serviço garante que mensagens sejam processadas na ordem de chegada?"* → **SQS FIFO**
- *"O que acontece com as mensagens se o consumidor falhar?"* → Ficam na **fila SQS** até serem processadas

---

## Relações

- [[entities/amazon-sns]] — complementar ao SQS; juntos formam o padrão fanout
- [[concepts/microservices]] — SQS é o mecanismo de desacoplamento entre microsserviços
- [[concepts/pub-sub]] — contraste: SQS é pull, SNS é push/pub-sub
- [[entities/aws-lambda]] — Lambda pode consumir mensagens da fila SQS como trigger

## Fontes

- [[sources/clf-c02-aula12-messaging-sqs-sns]]
