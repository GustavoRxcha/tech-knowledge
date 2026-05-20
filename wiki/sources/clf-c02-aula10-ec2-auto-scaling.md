---
title: "CLF-C02 Aula 10 — EC2 Auto Scaling"
type: source
tags: [aws, clf-c02, auto-scaling, escalabilidade, alta-disponibilidade]
created: 2026-05-20
updated: 2026-05-20
sources: 1
---

# CLF-C02 Aula 10 — EC2 Auto Scaling

Escalabilidade horizontal automática para instâncias EC2: Auto Scaling Group (ASG), parâmetros min/desejado/máximo, escalabilidade preditiva vs dinâmica e implantação multi-AZ.

---

## Origem

- **Arquivo:** `raw/clf-c02-aula10-ec2-auto-scaling.md`
- **Trilha:** CLF-C02 — Preparatório AWS Cloud Practitioner
- **Módulo:** Computação na AWS (aula 02 do módulo / aula 10 do curso)

---

## O problema

E-commerce com variação de tráfego semanal:
- Escalar para capacidade máxima → ociosa nos dias tranquilos (paga à toa)
- Escalar para capacidade média → sobrecarga no pico (experiência ruim)
- Escalar conforme necessidade → ✅ EC2 Auto Scaling

---

## O que é

O **Amazon EC2 Auto Scaling** adiciona ou remove instâncias EC2 automaticamente com base na demanda. Trabalha com **escalabilidade horizontal** — mais instâncias, não instâncias maiores.

```
Escalabilidade vertical: [instância pequena] → [instância maior] (requer downtime)
Escalabilidade horizontal: [1 instância] → [2] → [4] (sem downtime)
```

---

## Auto Scaling Group (ASG) — parâmetros

| Parâmetro | Descrição | Exemplo |
|---|---|---|
| **Capacidade mínima** | Mínimo de instâncias sempre em execução | `1` |
| **Capacidade desejada** | Instâncias que o grupo tenta manter por padrão | `2` |
| **Capacidade máxima** | Máximo que pode ser lançado (controla custo) | `4` |

---

## Abordagens de escalabilidade

### Escalabilidade Preditiva

- Analisa histórico + machine learning para prever picos
- Provisiona instâncias **antecipadamente**, antes do pico
- Requisito: histórico de uso consistente e representativo
- Melhor para: padrões **previsíveis e regulares**

### Escalabilidade Dinâmica

- Reage a **métricas em tempo real** (CPU, requisições)
- Quando métrica ultrapassa threshold → escala para cima
- Quando métrica cai → escala para baixo
- Melhor para: variações **imprevisíveis ou irregulares**

> As duas abordagens podem ser combinadas simultaneamente.

---

## Multi-AZ com Auto Scaling

```
Auto Scaling Group
├── AZ-a: [instância 1] [instância 2]
└── AZ-b: [instância 3] [instância 4]
         ↓ AZ-a falha
├── AZ-a: ❌ indisponível
└── AZ-b: continua + Auto Scaling lança novas instâncias na AZ-b
```

---

## Benefícios

| Benefício | Descrição |
|---|---|
| Elasticidade | Ajusta capacidade automaticamente |
| Tolerância a falhas | Substitui instâncias indisponíveis automaticamente |
| Alta disponibilidade | Suporte a implantação multi-AZ |
| Gestão de custos | Escala para baixo nos períodos de baixa demanda |

---

## Conceitos/entidades relacionados

- [[entities/amazon-ec2-auto-scaling]]
- [[entities/amazon-ec2]]
- [[concepts/auto-scaling]]
- [[concepts/elasticity]]
- [[concepts/high-availability]]
- [[concepts/fault-tolerance]]
- [[concepts/availability-zone]]
