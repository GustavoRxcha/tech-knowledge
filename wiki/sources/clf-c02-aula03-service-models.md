---
title: "CLF-C02 Aula 03 — Modelos de Serviço: IaaS, PaaS e SaaS"
type: source
tags: [aws, clf-c02, cloud, iaas, paas, saas, certificação]
created: 2026-05-19
updated: 2026-05-19
sources: 1
---

# CLF-C02 Aula 03 — Modelos de Serviço: IaaS, PaaS e SaaS

Arquivo fonte: `raw/clf-c02-aula03-modelos-de-servico-iaas-paas-saas.md` (PT-BR)

Apresenta os três modelos de computação em nuvem, organizados pelo **nível de responsabilidade** que o usuário assume.

---

## Os três modelos

| Modelo | Nome completo | Analogia | Exemplo AWS |
|---|---|---|---|
| [[concepts/iaas\|IaaS]] | Infrastructure as a Service | Aluga o terreno e constrói | [[entities/amazon-ec2\|EC2]] |
| [[concepts/paas\|PaaS]] | Platform as a Service | Aluga o espaço e decora | [[entities/aws-elastic-beanstalk\|Elastic Beanstalk]] |
| [[concepts/saas\|SaaS]] | Software as a Service | Aluga pronto e usa | Gmail, Slack, Salesforce |

## Matriz de responsabilidade (do material)

| Camada | On-Premises | IaaS | PaaS | SaaS |
|---|---|---|---|---|
| Aplicação | Você | Você | Você | Provedor |
| Dados | Você | Você | Você | Provedor |
| Runtime | Você | Você | Provedor | Provedor |
| Sistema Operacional | Você | Você | Provedor | Provedor |
| Virtualização | Você | Provedor | Provedor | Provedor |
| Servidores | Você | Provedor | Provedor | Provedor |
| Armazenamento | Você | Provedor | Provedor | Provedor |
| Rede | Você | Provedor | Provedor | Provedor |

> Regra: **quanto mais à direita, menos você gerencia**.

## Perfil de usuário típico

| Perfil | Modelo | Foco |
|---|---|---|
| Sysadmin / time de infra | [[concepts/iaas\|IaaS]] | Controle total, configuração granular |
| Dev / DevOps | [[concepts/paas\|PaaS]] | Deploy rápido, sem mexer em infra |
| Usuário final / negócio | [[concepts/saas\|SaaS]] | Apenas usar o produto |

## Analogia da pizza (mnemônico)

- Você faz tudo em casa → **On-Premises**
- Compra a massa pronta e monta → **IaaS**
- Pede para montar e só escolhe os ingredientes → **PaaS**
- Pede pizza pronta e só come → **SaaS**

## Dica de prova destacada

Questões geralmente apresentam um **cenário de usuário** e pedem para identificar o modelo. A distinção mais cobrada é **IaaS vs PaaS** — foque em "quem gerencia o quê" (especialmente Runtime e SO).

---

## Entidades e conceitos tocados

- Entidades: [[entities/amazon-ec2]] (contexto IaaS), [[entities/aws-elastic-beanstalk]] (novo, PaaS)
- Conceitos: [[concepts/iaas]] (novo), [[concepts/paas]] (novo), [[concepts/saas]] (novo)
- Tópicos: [[topics/cloud-fundamentals]]
