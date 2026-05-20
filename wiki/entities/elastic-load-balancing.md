---
title: "Elastic Load Balancing (ELB)"
type: entity
tags: [aws, elb, load-balancer, alta-disponibilidade, alb, nlb, gwlb]
created: 2026-05-20
updated: 2026-05-20
sources: 1
---

# Elastic Load Balancing (ELB)

Serviço da [[entities/aws|AWS]] que **distribui automaticamente o tráfego de entrada** entre múltiplas instâncias EC2 (ou outros alvos), garantindo uso equilibrado e evitando que qualquer instância fique sobrecarregada.

---

## Por que existe

O [[entities/amazon-ec2-auto-scaling|EC2 Auto Scaling]] resolve a escala — mas sem um distribuidor, as requisições chegam de forma desequilibrada. O ELB decide para qual instância cada requisição vai.

```
SEM ELB: [Usuários] → instâncias EC2 (desequilibrado — uma sobrecarregada, outras ociosas)
COM ELB: [Usuários] → [ELB] → instâncias EC2 (equilibrado)
```

---

## Tipos de Load Balancer

| Tipo | Sigla | Camada OSI | Melhor para |
|---|---|---|---|
| **Application Load Balancer** | ALB | Camada 7 (HTTP/HTTPS) | Apps web, APIs REST, roteamento por URL/header |
| **Network Load Balancer** | NLB | Camada 4 (TCP/UDP) | Alto desempenho, baixa latência, jogos, IoT |
| **Gateway Load Balancer** | GWLB | Camada 3 (IP) | Appliances de segurança (firewalls, IDS/IPS) |

> Para a prova CLF-C02: **ALB** é o mais cobrado — padrão para apps web e APIs.

---

## Tipos de uso

- **Externo (Internet-facing):** entre usuários da internet e instâncias EC2
- **Interno:** entre componentes internos da aplicação (frontend → backend, microsserviços)

---

## Características

| Característica | Descrição |
|---|---|
| **Escopo regional** | Automaticamente distribuído entre AZs — sem config manual de redundância |
| **Health checks** | Monitora instâncias; para de enviar tráfego para as indisponíveis |
| **Escalabilidade automática** | Escala sua própria capacidade conforme o volume de requisições |
| **Integração com Auto Scaling** | Coordena automaticamente com ASGs |

---

## Arquitetura ELB + Auto Scaling

```
Tráfego alto   → Auto Scaling adiciona instâncias → ELB distribui para elas
Tráfego baixo  → Auto Scaling remove instâncias   → ELB ajusta automaticamente
Instância falha → ELB detecta → redireciona tráfego → Auto Scaling repõe
```

---

## Para a prova CLF-C02

- *"Qual serviço distribui o tráfego entre múltiplas instâncias EC2?"* → **ELB**
- *"O que acontece quando uma instância fica indisponível com ELB?"* → **Health check** detecta e redireciona
- *"Qual tipo de LB para aplicações web HTTP/HTTPS?"* → **ALB**
- *"Qual combinação cria aplicações altamente disponíveis e escaláveis?"* → **ELB + EC2 Auto Scaling**

---

## Relações

- [[entities/amazon-ec2]] — alvos do balanceamento
- [[entities/amazon-ec2-auto-scaling]] — parceiro para escalabilidade
- [[concepts/load-balancing]] — conceito base
- [[concepts/high-availability]] — garantida pela combinação ELB + multi-AZ
- [[concepts/availability-zone]] — o ELB distribui entre AZs automaticamente

## Fontes

- [[sources/clf-c02-aula11-elastic-load-balancing]]
