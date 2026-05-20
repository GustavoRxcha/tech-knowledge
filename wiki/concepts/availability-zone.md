---
title: "Zona de Disponibilidade (Availability Zone — AZ)"
type: concept
tags: [aws, infraestrutura-global, availability-zone, alta-disponibilidade, clf-c02]
created: 2026-05-20
updated: 2026-05-20
sources: 2
---

# Zona de Disponibilidade (Availability Zone — AZ)

Uma **AZ** é um agrupamento de um ou mais data centers físicos dentro de uma [[concepts/aws-region|Região]], com infraestrutura **completamente independente** das demais AZs da mesma região.

---

## Infraestrutura independente

Cada AZ tem sua própria:
- Energia elétrica
- Refrigeração
- Rede e conectividade
- Localização física

---

## Exemplo

```
Região: sa-east-1 (São Paulo)
├── AZ: sa-east-1a  (data center A)
├── AZ: sa-east-1b  (data center B)
└── AZ: sa-east-1c  (data center C)
```

---

## Equilíbrio estratégico

As AZs são posicionadas de forma estratégica dentro da região:

```
Distância entre AZs:
├── Longe o suficiente → um desastre (tornado, enchente, falha elétrica)
│                        afeta apenas UMA AZ, não as outras
└── Perto o suficiente → latência de comunicação entre AZs permanece baixa
                         (dezenas de milissegundos)
```

> Esse equilíbrio é o que torna as AZs eficazes: **isolamento de falhas sem penalidade de performance**.

---

## Por que existem — Tolerância a Falhas

**Sem AZs:**
```
Região com 1 data center → tornado/falha elétrica → serviço indisponível + risco de perda de dados
```

**Com AZs (app rodando nas AZs A e B):**
```
AZ-a fica indisponível (desastre localizado)
AZ-b continua operando → serviço continua disponível sem interrupção
```

---

## Escopo de serviços

Serviços AWS operam em dois escopos:

| Escopo | Serviços | Implicação |
|---|---|---|
| **AZ-scope** | EC2, EBS | Vinculado a uma AZ. Se falhar, o serviço nela hospedado fica indisponível. |
| **Regional-scope** | S3, DynamoDB, IAM | Distribuído automaticamente entre as AZs da região. Sem config manual. |

---

## Boa prática

> Sempre arquitetar aplicações para rodar em **pelo menos 2 AZs** — garante que uma falha em uma zona não derrube o serviço.

```
EC2 na AZ-a  +  EC2 na AZ-b
     ↓ AZ-a falha
EC2 na AZ-b continua atendendo as requisições
```

---

## Para a prova CLF-C02

- *"O que garante que um desastre em um data center não derruba o serviço?"* → **Múltiplas AZs**
- *"Qual serviço AWS precisa ser configurado em múltiplas AZs?"* → Serviços de **escopo de AZ** como EC2

---

## Relações

- [[concepts/aws-region]] — cada AZ fica dentro de uma Região
- [[concepts/high-availability]] — múltiplas AZs são o mecanismo de alta disponibilidade
- [[concepts/fault-tolerance]] — AZs são o mecanismo de tolerância a falhas
- [[entities/amazon-ec2]] — escopo de AZ
- [[entities/amazon-s3]] — escopo regional (não depende de AZ individual)

## Fontes

- [[sources/clf-c02-aula05-global-infrastructure]]
- [[sources/clf-c02-aula06-regions-az]]
