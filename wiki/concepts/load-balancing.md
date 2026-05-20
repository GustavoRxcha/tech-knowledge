---
title: "Balanceamento de Carga (Load Balancing)"
type: concept
tags: [aws, load-balancing, alta-disponibilidade, distribuicao-de-trafego]
created: 2026-05-20
updated: 2026-05-20
sources: 1
---

# Balanceamento de Carga (Load Balancing)

**Load balancing** é o processo de distribuir o tráfego de entrada entre múltiplos servidores (ou instâncias), de forma que nenhum fique sobrecarregado enquanto outros ficam ociosos.

---

## O problema que resolve

```
SEM balanceamento:
[Usuários] → instâncias EC2 (uma sobrecarregada 🔥, outras ociosas)

COM balanceamento:
[Usuários] → [Load Balancer] → distribui de forma equilibrada entre todas
```

---

## Como funciona

O Load Balancer age como um **proxy reverso** — os clientes se conectam a ele, e ele decide para qual servidor backend encaminhar cada requisição. O algoritmo de decisão pode variar (round-robin, least connections, etc.).

---

## Componentes-chave

- **Health check:** verificação periódica da saúde de cada instância; tráfego não é enviado para instâncias indisponíveis
- **Target group:** conjunto de instâncias (ou outros alvos) para os quais o LB pode enviar tráfego

---

## Relação com Auto Scaling

Load balancing e auto scaling são complementares:
- **Auto scaling** decide *quantas* instâncias existem
- **Load balancing** decide *para qual* instância cada requisição vai

---

## Relações

- [[entities/elastic-load-balancing]] — implementação AWS do conceito
- [[concepts/auto-scaling]] — conceito complementar
- [[concepts/high-availability]] — LB é um dos mecanismos de alta disponibilidade

## Fontes

- [[sources/clf-c02-aula11-elastic-load-balancing]]
