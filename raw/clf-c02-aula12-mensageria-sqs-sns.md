# Serviços de Mensageria: Amazon SQS e Amazon SNS

> 📋 **Curso:** Computação na AWS — Preparatório AWS Cloud Practitioner (CLF-C02)
> 📌 **Aula:** Conceitual — Mensageria e Desacoplamento de Microsserviços

---

## 1. Contexto: Microsserviços e Desacoplamento

### O que são microsserviços?

**Microsserviços** são pequenas aplicações com **escopo bem definido** que fazem parte de uma arquitetura maior. Cada microsserviço é responsável por um domínio específico de negócio.

**Exemplo — e-commerce com microsserviços:**

```
[MS Compras] → processa pedidos
[MS Fraude]  → analisa transações suspeitas
[MS E-mail]  → envia notificações ao usuário
[MS Estoque] → atualiza o inventário
```

### O problema da comunicação direta

Se os microsserviços se comunicam **diretamente** entre si (acoplamento forte), um problema em qualquer um pode **derrubar toda a cadeia**:

```
[MS Compras] → chama diretamente → [MS Fraude] (fora do ar)
                                          ↓
                               ❌ Compra falha completamente
```

### A solução: Mensageria (desacoplamento)

Os serviços de mensageria permitem que os microsserviços se **comuniquem de forma assíncrona e desacoplada** — cada um opera em seu próprio ritmo, sem depender diretamente do outro.

> 📌 **Assíncrono** = você envia uma mensagem e não precisa esperar a resposta imediatamente para continuar operando.

---

## 2. Amazon SQS — Simple Queue Service

### O que é

O **Amazon SQS** é um serviço de **fila de mensagens** gerenciado. Permite que microsserviços se comuniquem de forma **assíncrona** através de uma estrutura de dados chamada **fila (queue)**.

### Como funciona: modelo Produtor → Fila → Consumidor

```
[Produtor]          [Fila SQS]         [Consumidor]
MS Compras    →  [msg1][msg2][msg3]  →  MS Fraude
(enfileira)        (FIFO)              (lê, processa, apaga)
```

### Regras da fila

- **FIFO (First In, First Out):** o primeiro a entrar é o primeiro a sair — como uma fila de supermercado
- O consumidor **escuta** (poll) a fila continuamente
- Ao processar uma mensagem, o consumidor a **apaga** da fila
- Se o consumidor estiver fora do ar, as mensagens **ficam na fila** aguardando — nada é perdido

### Exemplo prático — fluxo de compra

```
1. Usuário clica em "Comprar"
2. MS Compras publica mensagem na fila SQS:
   → "Usuário X comprou Produto Y"

3. MS Fraude escuta a fila:
   → Lê mensagem 1, analisa, registra no DynamoDB, apaga da fila
   → Lê mensagem 2, analisa, registra, apaga
   → ...

4. Cada mensagem é processada na ordem de chegada
5. O MS Compras não precisa esperar o MS Fraude — seguiu em frente
```

### Benefícios do SQS

| Benefício | Descrição |
|---|---|
| **Desacoplamento** | Produtor e consumidor operam independentemente |
| **Resiliência** | Mensagens ficam na fila mesmo se o consumidor falhar |
| **Escalabilidade** | Múltiplos consumidores podem ler da mesma fila em paralelo |
| **Ordem garantida** | Modo FIFO garante processamento em ordem de chegada |
| **Gerenciado** | Sem necessidade de gerenciar a infraestrutura da fila |

---

## 3. Amazon SNS — Simple Notification Service

### O que é

O **Amazon SNS** é um serviço de **publicação e assinatura (Pub/Sub)** gerenciado. Ao contrário do SQS (um produtor para um consumidor), o SNS permite enviar uma mensagem para **múltiplos destinatários simultaneamente**.

### Estrutura: Tópico (Topic)

O conceito central do SNS é o **tópico** — um canal de comunicação baseado em **assunto**. Os sistemas que têm interesse em um assunto se tornam **assinantes (subscribers)** do tópico.

```
[Publicador]          [Tópico SNS]          [Assinantes]
MS Fraude    →   "compra-autorizada"   →   MS E-mail
(publica)         (topic)              →   MS Estoque
                                       →   App Mobile (push)
```

### Como funciona: modelo Pub/Sub

1. Um **publicador** publica uma mensagem em um tópico
2. Todos os **assinantes** daquele tópico recebem a mensagem simultaneamente
3. Cada assinante processa a mensagem de forma independente

### Exemplo prático — compra autorizada

```
1. MS Fraude aprova a compra
2. Publica no tópico SNS "compra-autorizada":
   → "Compra #1234 aprovada para usuário X"

3. Todos os assinantes recebem a mensagem ao mesmo tempo:
   → MS E-mail:  envia e-mail de confirmação ao usuário
   → MS Estoque: dá baixa no produto no inventário
   → App Mobile: envia push notification ao usuário
```

### Analogia: Revista com assinantes

> Pense no SNS como uma revista: quando uma nova edição é publicada (mensagem no tópico), **todos os assinantes** recebem a mesma edição ao mesmo tempo — sem precisar buscar individualmente.

### Casos de uso do SNS

- Notificações de eventos para múltiplos sistemas
- Envio de **e-mails, SMS e push notifications**
- Fanout — distribuir uma mensagem para múltiplas filas SQS simultaneamente
- Alertas de monitoramento (ex: CloudWatch → SNS → e-mail)

---

## 4. SQS vs SNS — Diferenças Fundamentais

| Característica | SQS (Fila) | SNS (Tópico) |
|---|---|---|
| **Modelo** | Produtor → Fila → Consumidor | Publicador → Tópico → N Assinantes |
| **Destinatários** | Um consumidor por vez | Múltiplos simultaneamente |
| **Comunicação** | Assíncrona (pull) | Assíncrona (push) |
| **Estrutura** | Fila (FIFO) | Tópico (Pub/Sub) |
| **Mensagem após leitura** | Apagada pelo consumidor | Entregue a todos e descartada |
| **Caso de uso** | Processamento sequencial, filas de trabalho | Notificações em tempo real, fanout |

---

## 5. Padrão Combinado: SNS + SQS (Fanout)

Um padrão muito comum é combinar os dois serviços:

```
[Evento]
    ↓
[Tópico SNS]
    ↓           ↓           ↓
[Fila SQS 1] [Fila SQS 2] [Fila SQS 3]
    ↓               ↓           ↓
[MS Estoque] [MS E-mail] [MS Relatório]
```

> ✅ O SNS distribui para múltiplas filas SQS, e cada serviço processa no seu próprio ritmo — máximo desacoplamento com máxima resiliência.

---

## 6. Resumo dos Conceitos

| Conceito | Definição |
|---|---|
| **Mensageria** | Comunicação assíncrona entre serviços via mensagens |
| **Desacoplamento** | Serviços operam independentemente, sem dependência direta |
| **SQS** | Fila gerenciada — um consumidor por vez, FIFO |
| **SNS** | Tópico Pub/Sub — múltiplos assinantes recebem simultaneamente |
| **Produtor** | Serviço que envia/publica mensagens |
| **Consumidor** | Serviço que lê e processa mensagens da fila (SQS) |
| **Assinante** | Serviço registrado para receber mensagens de um tópico (SNS) |
| **FIFO** | First In, First Out — ordem de processamento |
| **Pub/Sub** | Publisher/Subscriber — padrão do SNS |

---

> 💡 **Dica para a prova CLF-C02:** Questões típicas sobre mensageria:
> - *"Qual serviço permite comunicação assíncrona com fila de mensagens?"* → **SQS**
> - *"Qual serviço envia uma mensagem para múltiplos destinatários simultaneamente?"* → **SNS**
> - *"Qual padrão é usado para desacoplar microsserviços?"* → **Mensageria com SQS e/ou SNS**
> - *"Um sistema precisa notificar e-mail, estoque e app mobile quando uma compra é aprovada. Qual serviço usar?"* → **SNS** (Pub/Sub com múltiplos assinantes)
> - *"Qual serviço garante que mensagens sejam processadas na ordem de chegada?"* → **SQS FIFO**

---

## Links Úteis

- [Amazon SQS — Visão Geral](https://aws.amazon.com/pt/sqs/)
- [Amazon SNS — Visão Geral](https://aws.amazon.com/pt/sns/)
- [Outros serviços de mensageria AWS](https://aws.amazon.com/pt/messaging/)

---

*Aula 04 — Módulo: Computação na AWS | Curso Preparatório AWS Cloud Practitioner*
