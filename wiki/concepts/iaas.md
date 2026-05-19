---
title: "IaaS — Infrastructure as a Service"
type: concept
tags: [cloud, iaas, modelo-de-serviço, clf-c02]
created: 2026-05-19
updated: 2026-05-19
sources: 1
---

# IaaS — Infrastructure as a Service

Modelo de serviço em que o provedor entrega **componentes básicos de TI** (servidores virtuais, storage, rede). O cliente gerencia **tudo acima da virtualização** — SO, runtime, aplicação, dados.

---

## Posição no espectro

| On-Prem | **IaaS** | [[concepts/paas\|PaaS]] | [[concepts/saas\|SaaS]] |
|---|---|---|---|
| Você faz tudo | Você gerencia SO+ | Você gerencia app+ | Você só usa |

## Responsabilidade

| Camada | Quem |
|---|---|
| Aplicação | Você |
| Dados | Você |
| Runtime | Você |
| Sistema Operacional | Você |
| Virtualização | Provedor |
| Servidores físicos | Provedor |
| Storage físico | Provedor |
| Rede física | Provedor |

## Quando usar

- Precisa de **controle total** sobre a infra.
- Time tem capacidade de configurar e manter SO + runtime.
- Requisitos muito específicos que não cabem em plataformas prontas.

## Exemplo canônico na AWS

**[[entities/amazon-ec2|EC2 — Elastic Compute Cloud]]**: você escolhe tamanho da instância (CPU/RAM/disco), SO, configura redes e segurança, instala software, aplica patches.

Outros exemplos:
- AWS EBS (storage de bloco)
- VPC (rede)
- Linode, DigitalOcean Droplets (concorrentes)

## Para a prova CLF-C02

A distinção **IaaS vs [[concepts/paas|PaaS]]** é a mais cobrada. Pergunta-chave: **quem gerencia o SO e o runtime?**
- SO + runtime sob sua responsabilidade → IaaS
- SO + runtime sob o provedor → PaaS

Palavra-gatilho: "controle sobre o sistema operacional", "configurar servidor", "instalar dependências".

## Fontes

- [[sources/clf-c02-aula03-service-models]]

## Relações

- [[concepts/paas]]
- [[concepts/saas]]
- [[entities/amazon-ec2]]
- [[topics/cloud-fundamentals]]
