---
title: "CLF-C02 Aula 12 — Mensageria: Amazon SQS e Amazon SNS"
type: source
tags: [aws, clf-c02, sqs, sns, mensageria, microsservicos, pub-sub, desacoplamento]
created: 2026-05-20
updated: 2026-05-20
sources: 1
---

# CLF-C02 Aula 12 — Mensageria: Amazon SQS e Amazon SNS

Serviços de mensageria para desacoplamento de microsserviços: SQS (fila FIFO produtor/consumidor) e SNS (Pub/Sub com múltiplos assinantes). Padrão fanout combinando os dois.

---

## Origem

- **Arquivo:** `raw/clf-c02-aula12-mensageria-sqs-sns.md`
- **Trilha:** CLF-C02 — Preparatório AWS Cloud Practitioner
- **Módulo:** Computação na AWS (aula 04 do módulo / aula 12 do curso)

---

## Contexto: microsserviços e acoplamento

Microsserviços são pequenas aplicações com escopo bem definido. O problema: se comunicam diretamente, uma falha em qualquer um derruba toda a cadeia.

**Solução:** mensageria — comunicação **assíncrona e desacoplada**. Cada serviço opera no seu ritmo, sem depender diretamente do outro.

---

## Amazon SQS — Simple Queue Service

**Fila de mensagens** gerenciada. Modelo: Produtor → Fila → Consumidor.

```
[MS Compras] → [msg1][msg2][msg3] → [MS Fraude]
(enfileira)       (FIFO queue)      (lê, processa, apaga)
```

**Regras da fila:**
- **FIFO:** primeiro a entrar, primeiro a sair
- Consumidor faz **poll** (escuta) contínuo da fila
- Ao processar, o consumidor **apaga** a mensagem
- Se o consumidor estiver fora do ar, mensagens **ficam na fila** — nada é perdido

**Benefícios:** desacoplamento · resiliência · escalabilidade · ordem garantida (FIFO) · gerenciado

---

## Amazon SNS — Simple Notification Service

**Publicação e assinatura (Pub/Sub)** gerenciado. Uma mensagem vai para **múltiplos destinatários simultaneamente**.

Conceito central: **tópico** — canal de comunicação por assunto. Sistemas interessados tornam-se **assinantes (subscribers)**.

```
[MS Fraude] → "compra-autorizada" (topic) → MS E-mail
                                           → MS Estoque
                                           → App Mobile (push)
```

**Analogia:** como uma revista — quando publicada, **todos os assinantes** recebem simultaneamente.

**Casos de uso:** notificações para múltiplos sistemas · e-mail, SMS, push · fanout · alertas CloudWatch

---

## SQS vs SNS

| Característica | SQS (Fila) | SNS (Tópico) |
|---|---|---|
| Modelo | Produtor → Fila → Consumidor | Publicador → Tópico → N Assinantes |
| Destinatários | Um consumidor por vez | Múltiplos simultaneamente |
| Comunicação | Assíncrona (pull) | Assíncrona (push) |
| Estrutura | Fila (FIFO) | Tópico (Pub/Sub) |
| Mensagem após leitura | Apagada | Entregue a todos e descartada |
| Caso de uso | Processamento sequencial, filas de trabalho | Notificações, fanout |

---

## Padrão Fanout: SNS + SQS

```
[Evento]
    ↓
[Tópico SNS]
    ↓           ↓           ↓
[Fila SQS 1] [Fila SQS 2] [Fila SQS 3]
    ↓               ↓           ↓
[MS Estoque] [MS E-mail] [MS Relatório]
```

SNS distribui para múltiplas filas SQS; cada serviço processa no seu ritmo — máximo desacoplamento + máxima resiliência.

---

## Conceitos/entidades relacionados

- [[entities/amazon-sqs]]
- [[entities/amazon-sns]]
- [[concepts/microservices]]
- [[concepts/pub-sub]]
