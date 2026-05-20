---
title: "Auto Scaling (Escalabilidade Automática)"
type: concept
tags: [aws, auto-scaling, escalabilidade, elasticidade, alta-disponibilidade]
created: 2026-05-20
updated: 2026-05-20
sources: 1
---

# Auto Scaling (Escalabilidade Automática)

**Auto Scaling** é a capacidade de ajustar automaticamente a quantidade de recursos computacionais (instâncias, containers, etc.) com base na demanda atual, sem intervenção manual.

---

## Escalabilidade horizontal vs vertical

| Tipo | Descrição | Vantagem |
|---|---|---|
| **Horizontal (scale out/in)** | Adiciona ou remove **instâncias** com a mesma configuração | Sem downtime; é o que o Auto Scaling faz |
| **Vertical (scale up/down)** | Aumenta ou diminui o **tamanho** de uma instância | Mais simples, mas requer downtime para trocar o tipo |

O EC2 Auto Scaling trabalha com **escalabilidade horizontal**.

---

## Parâmetros de um grupo de Auto Scaling

| Parâmetro | Descrição |
|---|---|
| **Capacidade mínima** | Garante que sempre haja pelo menos X instâncias rodando |
| **Capacidade desejada** | Número default que o grupo tenta manter |
| **Capacidade máxima** | Teto que controla custo — evita explosão de instâncias |

---

## Abordagens

### Preditiva
Usa histórico + machine learning para prever picos e provisionar **antecipadamente**. Ideal para padrões regulares e previsíveis.

### Dinâmica
Reage a métricas em tempo real (CPU, tráfego). Ideal para variações imprevisíveis.

---

## Relação com [[concepts/elasticity|Elasticidade]]

Elasticidade é o conceito (escalar conforme demanda); Auto Scaling é a implementação técnica desse conceito na AWS.

---

## Relações

- [[entities/amazon-ec2-auto-scaling]] — implementação AWS do conceito
- [[concepts/elasticity]] — o benefício que o auto scaling entrega
- [[concepts/high-availability]] — multi-AZ + auto scaling = alta disponibilidade
- [[entities/elastic-load-balancing]] — distribui o tráfego entre as instâncias escaladas

## Fontes

- [[sources/clf-c02-aula10-ec2-auto-scaling]]
