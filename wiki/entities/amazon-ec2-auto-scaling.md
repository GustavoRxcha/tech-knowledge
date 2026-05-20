---
title: "Amazon EC2 Auto Scaling"
type: entity
tags: [aws, auto-scaling, ec2, escalabilidade, alta-disponibilidade]
created: 2026-05-20
updated: 2026-05-20
sources: 1
---

# Amazon EC2 Auto Scaling

Serviço que **adiciona ou remove instâncias [[entities/amazon-ec2|EC2]] automaticamente** com base na demanda atual, garantindo sempre a quantidade certa de capacidade computacional — nem demais (custo), nem de menos (performance).

---

## Tipo de escalabilidade: horizontal

Em vez de aumentar o tamanho de uma instância (vertical), o Auto Scaling **adiciona mais instâncias** com a mesma configuração.

```
Vertical: [instância pequena] → [instância maior] (requer downtime)
Horizontal: [1 instância] → [2] → [4] (sem downtime)
```

---

## Auto Scaling Group (ASG)

Configuração central do serviço. Três parâmetros principais:

| Parâmetro | Descrição |
|---|---|
| **Capacidade mínima** | Mínimo de instâncias sempre em execução (garante disponibilidade) |
| **Capacidade desejada** | Instâncias que o grupo tenta manter por padrão |
| **Capacidade máxima** | Máximo que pode ser lançado (controla custo, evita explosão de instâncias) |

```
Mínima:  [■]          → 1 instância sempre rodando
Desejada: [■][■]      → 2 instâncias normalmente
Máxima:  [■][■][■][■] → até 4 no pico
```

---

## Abordagens de escalabilidade

### Escalabilidade Preditiva

- Analisa **histórico** + machine learning para prever picos
- Provisiona instâncias **antes** do pico acontecer (proativo)
- Requisito: padrão histórico consistente
- Melhor para: padrões **previsíveis e regulares**

### Escalabilidade Dinâmica

- Reage a **métricas em tempo real** (CPU, número de requisições)
- Quando métrica ultrapassa threshold → escala para cima; quando cai → escala para baixo
- Melhor para: variações **imprevisíveis ou irregulares**

> As duas abordagens podem ser usadas simultaneamente.

---

## Multi-AZ

Para máxima tolerância a falhas, o ASG distribui instâncias em **múltiplas AZs**:
- AZ falha → instâncias restantes continuam atendendo
- Auto Scaling lança novas instâncias na AZ saudável automaticamente

---

## Integração com ELB

Trabalha em conjunto com o [[entities/elastic-load-balancing|Elastic Load Balancing]]:
- Nova instância lançada → ELB começa a enviar tráfego automaticamente
- Instância encerrada → ELB para de enviar requisições antes do encerramento
- Instância falha → ELB detecta via health check e redireciona; Auto Scaling repõe

---

## Para a prova CLF-C02

- *"Qual serviço adiciona e remove instâncias EC2 automaticamente?"* → **EC2 Auto Scaling**
- *"Qual abordagem escala com base em padrões históricos?"* → **Escalabilidade Preditiva**
- *"Qual abordagem reage a métricas em tempo real?"* → **Escalabilidade Dinâmica**
- *"Qual parâmetro garante que sempre haja pelo menos X instâncias?"* → **Capacidade mínima**

---

## Relações

- [[entities/amazon-ec2]] — instâncias gerenciadas pelo Auto Scaling
- [[entities/elastic-load-balancing]] — distribui o tráfego entre as instâncias
- [[concepts/auto-scaling]] — conceito de escalabilidade horizontal
- [[concepts/elasticity]] — benefício central do Auto Scaling
- [[concepts/high-availability]] — garantida por multi-AZ
- [[concepts/availability-zone]] — múltiplas AZs para tolerância a falhas

## Fontes

- [[sources/clf-c02-aula10-ec2-auto-scaling]]
