---
title: "Microsserviços (Microservices)"
type: concept
tags: [arquitetura, microsservicos, desacoplamento, mensageria, sqs, sns]
created: 2026-05-20
updated: 2026-05-20
sources: 1
---

# Microsserviços (Microservices)

**Microsserviços** são pequenas aplicações com **escopo bem definido** que fazem parte de uma arquitetura maior. Cada microsserviço é responsável por um único domínio de negócio e pode ser desenvolvido, implantado e escalado de forma independente.

---

## Exemplo

E-commerce decomposto em microsserviços:

```
[MS Compras] → processa pedidos
[MS Fraude]  → analisa transações suspeitas
[MS E-mail]  → envia notificações ao usuário
[MS Estoque] → atualiza o inventário
```

---

## O problema do acoplamento direto

Se os microsserviços se comunicam diretamente (acoplamento forte), uma falha em qualquer um pode derrubar toda a cadeia:

```
[MS Compras] → chama diretamente → [MS Fraude] (fora do ar)
                                          ↓
                               ❌ Compra falha completamente
```

---

## Solução: desacoplamento via mensageria

Com serviços de mensageria, cada microsserviço opera no seu ritmo sem depender diretamente do outro:

```
[MS Compras] → publica na fila SQS → [MS Fraude consome quando disponível]
               (não precisa esperar a resposta)
```

---

## Ferramentas de desacoplamento na AWS

| Serviço | Padrão | Uso |
|---|---|---|
| [[entities/amazon-sqs|SQS]] | Fila (one-to-one) | Processamento sequencial e assíncrono |
| [[entities/amazon-sns|SNS]] | Pub/Sub (one-to-many) | Notificações simultâneas para múltiplos serviços |
| SNS + SQS | Fanout | Máximo desacoplamento com resiliência |

---

## Relações

- [[entities/amazon-sqs]] — mecanismo de desacoplamento via fila
- [[entities/amazon-sns]] — mecanismo de notificação Pub/Sub
- [[concepts/pub-sub]] — padrão de comunicação entre microsserviços
- [[concepts/containers]] — forma padrão de empacotar e implantar microsserviços
- [[concepts/serverless]] — microsserviços podem ser implementados como funções Lambda

## Fontes

- [[sources/clf-c02-aula12-messaging-sqs-sns]]
