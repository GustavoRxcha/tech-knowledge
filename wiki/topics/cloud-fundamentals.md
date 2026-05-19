---
title: "Cloud Fundamentals (CLF-C02)"
type: topic
tags: [cloud, fundamentos, clf-c02, certificação, conceitual]
created: 2026-05-19
updated: 2026-05-19
sources: 4
---

# Cloud Fundamentals — Trilha CLF-C02

Página de tópico que agrupa todo o conteúdo conceitual do preparatório **AWS Cloud Practitioner (CLF-C02)** — fundamentos de cloud computing, modelos de serviço, modelos de implantação, benefícios.

> Esta trilha é **conceitual e voltada para certificação**. Complementa a trilha hands-on do outro curso, que está agrupada em [[topics/aws-security]] e nos serviços (EC2, S3, Lambda, etc.).

---

## Mapa do conteúdo

### Conceito raiz
- [[concepts/cloud-computing]] — definição AWS, pay-as-you-go, evolução pré-cloud

### Benefícios (5 oficiais)
- [[concepts/cloud-benefits]] — CapEx→OpEx, elasticidade, escala, agilidade, alcance global
- [[concepts/elasticity]] — em destaque, conceito muito cobrado

### Modelos de serviço (nível de gerenciamento)
- [[concepts/iaas]] — Infrastructure as a Service ([[entities/amazon-ec2|EC2]])
- [[concepts/paas]] — Platform as a Service ([[entities/aws-elastic-beanstalk|Elastic Beanstalk]])
- [[concepts/saas]] — Software as a Service (Gmail, Salesforce)

### Modelos de implantação (onde roda)
- [[concepts/on-premises]] — local, controle total, alto custo fixo
- [[concepts/hybrid-cloud]] — local + nuvem, migração ou compliance parcial
- [[concepts/private-cloud]] — local + tecnologia cloud (VMware, Outposts)
- Nuvem pública — coberto via [[concepts/cloud-computing]] e [[entities/aws]]

### Tecnologias de base
- [[concepts/virtualization]] — hypervisor, fundação técnica da cloud

---

## Atalho para a prova

### Mapeamento cenário → conceito

| Palavra-gatilho no enunciado | Resposta provável |
|---|---|
| "custo inicial", "investimento em hardware" | Benefício: CapEx → OpEx ([[concepts/cloud-benefits]]) |
| "Black Friday", "pico de tráfego", "auto scaling" | [[concepts/elasticity\|Elasticidade]] |
| "lançar MVP rápido" | Benefício: agilidade |
| "latência para usuários globais" | Benefício: alcance global |
| "controle sobre SO e runtime" | [[concepts/iaas\|IaaS]] |
| "deploy sem gerenciar infra" | [[concepts/paas\|PaaS]] |
| "pronto pra usar, só login" | [[concepts/saas\|SaaS]] |
| "data center próprio" | [[concepts/on-premises]] |
| "migração gradual", "parte local + nuvem" | [[concepts/hybrid-cloud]] |
| "VMware/OpenStack local" | [[concepts/private-cloud]] |

### Pares que mais caem

- **[[concepts/iaas|IaaS]] vs [[concepts/paas|PaaS]]** — quem gerencia SO + runtime?
- **[[concepts/on-premises|On-premises]] vs [[concepts/private-cloud|Private Cloud]]** — usa tecnologia cloud localmente?
- **[[concepts/hybrid-cloud|Híbrido]] vs Público** — tem componente local ou só na cloud?

---

## Estado da trilha

| Aula | Tema | Source |
|---|---|---|
| 01 | O que é Cloud Computing | ✅ [[sources/clf-c02-aula01-cloud-computing]] |
| 02 | Benefícios da Cloud | ✅ [[sources/clf-c02-aula02-cloud-benefits]] |
| 03 | Modelos de Serviço | ✅ [[sources/clf-c02-aula03-service-models]] |
| 04 | Modelos de Implantação | ✅ [[sources/clf-c02-aula04-deployment-models]] |
| 05+ | (próximos módulos) | 🔜 |

## Próximos temas esperados no curso

A última aula citou como próximos blocos: "Benefícios da Cloud, Modelos de Serviço, Modelos de Implantação" — esses três já estão cobertos. A continuação típica do CLF-C02 inclui:

- AWS Global Infrastructure (regiões, AZs, edge locations)
- AWS Well-Architected Framework
- Shared Responsibility Model
- AWS Pricing & Support Plans
- Principais serviços AWS por categoria (compute, storage, database, network)

## Lacunas

- Tudo após a aula 04 — nada ingerido ainda.
- Sem cobertura de Well-Architected, Shared Responsibility, regiões, billing.

## Fontes

- [[sources/clf-c02-aula01-cloud-computing]]
- [[sources/clf-c02-aula02-cloud-benefits]]
- [[sources/clf-c02-aula03-service-models]]
- [[sources/clf-c02-aula04-deployment-models]]
