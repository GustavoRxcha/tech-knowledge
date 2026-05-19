---
title: "SaaS — Software as a Service"
type: concept
tags: [cloud, saas, modelo-de-serviço, clf-c02]
created: 2026-05-19
updated: 2026-05-19
sources: 1
---

# SaaS — Software as a Service

Modelo em que o provedor entrega um **produto pronto** — aplicação completa executada e gerenciada por ele. O cliente apenas **usa** o serviço.

---

## Posição no espectro

| On-Prem | [[concepts/iaas\|IaaS]] | [[concepts/paas\|PaaS]] | **SaaS** |
|---|---|---|---|
| Você faz tudo | Você gerencia SO+ | Você gerencia app+ | Você só usa |

## Responsabilidade

| Camada | Quem |
|---|---|
| Uso da aplicação | Você |
| Aplicação | Provedor |
| Dados (infra) | Provedor |
| Runtime / SO / Virtualização / Servidores / Rede | Provedor |

## Quando usar

- Você só quer **usar** uma funcionalidade.
- Sem necessidade de implantação, configuração ou manutenção.
- Qualquer usuário (técnico ou não) precisa acessar.

## Exemplos

- **E-mail**: Gmail, Outlook 365
- **Mensagens**: Slack, Microsoft Teams, Discord
- **CRM**: Salesforce, HubSpot
- **Storage para usuário final**: Dropbox, Google Drive, OneDrive
- **Produtividade**: Notion, Google Workspace

## Para a prova CLF-C02

Sinal mais óbvio dos três modelos: **SaaS = você não instala nada, só faz login**.

Palavra-gatilho: "pronto para uso", "acesso pelo navegador", "sem configuração", "produto completo".

## Fontes

- [[sources/clf-c02-aula03-service-models]]

## Relações

- [[concepts/iaas]]
- [[concepts/paas]]
- [[topics/cloud-fundamentals]]
