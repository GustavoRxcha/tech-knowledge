---
title: "CLF-C02 Aula 15 — Amazon VPC: Virtual Private Cloud"
type: source
tags: [aws, vpc, redes, sub-redes, alta-disponibilidade, clf-c02]
created: 2026-05-20
updated: 2026-05-20
sources: 1
---

# CLF-C02 Aula 15 — Amazon VPC: Virtual Private Cloud

Primeira aula do módulo **Redes em AWS** do preparatório CLF-C02. Introduz a Amazon VPC como alicerce de toda infraestrutura na AWS.

**Arquivo raw:** `raw/clf-c02-aula15-amazon-vpc.md`

---

## Problema motivador

Na cloud surgem os mesmos desafios de um escritório físico: como conectar instâncias entre si? Como isolar um banco de dados da internet? Como estruturar tudo de forma organizada e segura? A resposta é a VPC.

## O que é Amazon VPC

[[entities/amazon-vpc|Amazon VPC]] (Virtual Private Cloud) — rede virtual privada na AWS que permite:

- Construir redes virtuais equivalentes a redes físicas
- Conectar recursos AWS (EC2, RDS, Lambda...) entre si
- Segmentar a infraestrutura em sub-redes públicas e privadas
- Implementar regras de segurança de tráfego

**Princípio central:** "Tudo começa com uma VPC" — é o primeiro recurso a configurar antes de qualquer outro.

## Sub-redes: pública vs privada

| Tipo | Acesso externo | Ideal para |
|---|---|---|
| **Pública** | Acessível da internet (bidirecional) | Servidores web, APIs públicas, Load Balancers |
| **Privada** | Isolada da internet | Bancos de dados, aplicações internas, recursos sensíveis |

> **Regra de ouro:** bancos de dados e recursos sensíveis **nunca** em sub-redes públicas.

## Arquitetura multi-AZ (padrão de alta disponibilidade)

```
Região AWS
├── AZ-1
│   ├── Sub-rede Pública  → EC2 Web Server
│   └── Sub-rede Privada  → RDS Database
└── AZ-2
    ├── Sub-rede Pública  → EC2 Web Server
    └── Sub-rede Privada  → RDS Database (Réplica)
```

Fluxo de uma requisição: `[Cliente] → [Load Balancer] → [AZ-1 ou AZ-2] → [EC2] → [Database]`

Se AZ-1 cair → AZ-2 continua atendendo. Se um servidor cair → o outro absorve o tráfego.

## Passo a passo de provisionamento

1. Criar a VPC (definir intervalo de IPs — CIDR block)
2. Criar sub-redes (pública + privada por AZ)
3. Provisionar recursos (EC2 nas públicas, RDS nas privadas)
4. Configurar conectividade (Internet Gateway, NAT Gateway, roteamento)

## Conceitos cobrados na prova

- *"O que é Amazon VPC?"* → Rede virtual isolada que permite organizar e conectar recursos AWS
- *"Diferença sub-rede pública vs privada?"* → Pública: acessível da internet. Privada: isolada da internet
- *"Onde deve estar um banco de dados?"* → Sub-rede privada
- *"Primeiro passo ao construir infraestrutura na AWS?"* → Criar a VPC
- *"O que garante resiliência em uma aplicação?"* → Implantação multi-AZ com Load Balancer

## Relações

- [[entities/amazon-vpc]]
- [[concepts/subnet]]
- [[concepts/high-availability]]
- [[concepts/fault-tolerance]]
- [[concepts/availability-zone]]
- [[entities/amazon-ec2]]
- [[entities/elastic-load-balancing]]
- [[topics/cloud-fundamentals]]
