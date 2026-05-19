---
title: "PaaS — Platform as a Service"
type: concept
tags: [cloud, paas, modelo-de-serviço, clf-c02]
created: 2026-05-19
updated: 2026-05-19
sources: 1
---

# PaaS — Platform as a Service

Modelo de serviço em que o provedor entrega uma **plataforma completa** para implantação de aplicações. O cliente entrega o **código**; a plataforma cuida de SO, runtime, balanceadores, escala.

---

## Posição no espectro

| On-Prem | [[concepts/iaas\|IaaS]] | **PaaS** | [[concepts/saas\|SaaS]] |
|---|---|---|---|
| Você faz tudo | Você gerencia SO+ | Você gerencia app+ | Você só usa |

## Responsabilidade

| Camada | Quem |
|---|---|
| Aplicação | Você |
| Dados | Você |
| Runtime | Provedor |
| Sistema Operacional | Provedor |
| Virtualização | Provedor |
| Servidores físicos | Provedor |
| Storage físico | Provedor |
| Rede física | Provedor |

## Quando usar

- Você é **desenvolvedor** e quer focar no código, não em infra.
- Não quer gerenciar SO, runtime ou configuração de rede.
- Prioridade é **velocidade de entrega**.

## Exemplo canônico na AWS

**[[entities/aws-elastic-beanstalk|AWS Elastic Beanstalk]]**: você faz upload do código; a plataforma provisiona servidores, balanceadores, monitoramento. Você não vê (nem precisa ver) o SO.

> [[entities/aws-lambda|AWS Lambda]] é frequentemente classificada como **FaaS** (subcategoria de PaaS) — você entrega função, a plataforma cuida do resto. Ver [[concepts/serverless]].

Outros exemplos fora da AWS: Heroku, Google App Engine, Azure App Service.

## Para a prova CLF-C02

A distinção **PaaS vs [[concepts/iaas|IaaS]]** é a mais cobrada. Foque em "quem gerencia o quê":
- SO + runtime sob o provedor → PaaS
- SO + runtime sob você → IaaS

Palavra-gatilho: "deploy de código", "foco no desenvolvimento", "plataforma cuida da infra".

## Fontes

- [[sources/clf-c02-aula03-service-models]]

## Relações

- [[concepts/iaas]]
- [[concepts/saas]]
- [[concepts/serverless]]
- [[entities/aws-elastic-beanstalk]]
- [[entities/aws-lambda]]
- [[topics/cloud-fundamentals]]
