---
title: "CLF-C02 Aula 11 — Elastic Load Balancing (ELB)"
type: source
tags: [aws, clf-c02, elb, load-balancer, alta-disponibilidade, alb, nlb]
created: 2026-05-20
updated: 2026-05-20
sources: 1
---

# CLF-C02 Aula 11 — Elastic Load Balancing (ELB)

Distribuição automática de tráfego entre instâncias EC2: o que é o ELB, tipos de Load Balancer (ALB, NLB, GWLB), integração com Auto Scaling e arquitetura completa ELB + Auto Scaling.

---

## Origem

- **Arquivo:** `raw/clf-c02-aula11-elastic-load-balancing.md`
- **Trilha:** CLF-C02 — Preparatório AWS Cloud Practitioner
- **Módulo:** Computação na AWS (aula 03 do módulo / aula 11 do curso)

---

## O problema

O Auto Scaling cria múltiplas instâncias — mas quem decide para qual instância cada requisição vai? Sem um distribuidor, as requisições chegam de forma desequilibrada: uma instância sobrecarregada, outras ociosas.

---

## O que é o ELB

O **Elastic Load Balancing (ELB)** distribui automaticamente o tráfego de entrada entre múltiplas instâncias EC2 (ou outros alvos), garantindo uso equilibrado.

```
ANTES: [Usuários] → diretamente para instâncias (desequilibrado)
DEPOIS: [Usuários] → [ELB] → distribui para instâncias (equilibrado)
```

---

## Integração com EC2 Auto Scaling

| Situação | O que acontece |
|---|---|
| Auto Scaling lança nova instância | ELB começa a enviar tráfego para ela automaticamente |
| Auto Scaling encerra uma instância | ELB para de enviar requisições antes do encerramento |
| Instância fica indisponível | ELB detecta e redireciona para instâncias saudáveis |

---

## Tipos de Load Balancer

| Tipo | Sigla | Camada | Melhor para |
|---|---|---|---|
| **Application LB** | ALB | Camada 7 (HTTP/HTTPS) | Apps web, APIs REST, roteamento por URL |
| **Network LB** | NLB | Camada 4 (TCP/UDP) | Alto desempenho, baixa latência, jogos, IoT |
| **Gateway LB** | GWLB | Camada 3 (IP) | Appliances de segurança (firewalls, IDS/IPS) |

> Para a prova CLF-C02: **ALB** é o mais cobrado — é o padrão para apps web e APIs.

---

## Tipos de uso

- **Externo (Internet-facing):** ELB entre usuários da internet e instâncias EC2
- **Interno:** ELB entre componentes internos (frontend → backend, microsserviços)

---

## Características gerais

| Característica | Descrição |
|---|---|
| Escopo regional | Automaticamente distribuído entre AZs |
| Alta disponibilidade | Integrado com múltiplas AZs |
| Escalabilidade automática | Escala sua própria capacidade conforme o tráfego |
| Health checks | Para de enviar tráfego para instâncias indisponíveis |

---

## Arquitetura completa: ELB + Auto Scaling

```
Tráfego alto → Auto Scaling adiciona instâncias → ELB distribui para elas
Tráfego baixo → Auto Scaling remove instâncias → ELB ajusta automaticamente
Instância falha → ELB detecta → redireciona tráfego → Auto Scaling repõe
```

---

## Conceitos/entidades relacionados

- [[entities/elastic-load-balancing]]
- [[entities/amazon-ec2-auto-scaling]]
- [[entities/amazon-ec2]]
- [[concepts/load-balancing]]
- [[concepts/high-availability]]
- [[concepts/availability-zone]]
