---
title: "Private Cloud (Nuvem Privada)"
type: concept
tags: [cloud, private, deployment, clf-c02]
created: 2026-05-19
updated: 2026-05-19
sources: 1
---

# Private Cloud — Nuvem Privada

Ambiente que usa **tecnologia cloud** (virtualização, automação, elasticidade) mas roda **localmente**, na infraestrutura da própria organização. Não é nem [[concepts/on-premises|on-premises tradicional]] nem nuvem pública.

---

## Características

- Hardware fica **nas dependências da organização** (ou em colocation dedicado).
- Mas o software de orquestração entrega experiência de **cloud**: provisionar VM em minutos, APIs de auto-scaling, etc.
- Dedicada a **uma única organização** (sem multi-tenancy externa).

## Tecnologias típicas

- **VMware** (vSphere, vCloud Suite)
- **OpenStack** (open-source)
- **AWS Outposts** — hardware AWS rodando no seu data center, com APIs idênticas à cloud pública
- **Azure Stack**, **Google Anthos** (equivalentes dos outros provedores)

## Por que existe

- **Compliance** que exige dados estritamente locais, sem perder a agilidade da cloud.
- **Latência ultra-baixa** para cargas específicas (manufatura, telecom).
- **Soberania de dados** (governo, defesa).
- **Investimento sunk** em data center que ainda compensa explorar.

## Mapa conceitual: não confunda

| Conceito | Localização | Usa tecnologia cloud? |
|---|---|---|
| [[concepts/on-premises\|On-premises tradicional]] | Local | ❌ |
| **Nuvem privada** | Local | ✅ |
| Nuvem pública | Provedor (AWS, Azure, GCP) | ✅ |
| [[concepts/hybrid-cloud\|Nuvem híbrida]] | Local + provedor | ✅ |

> A "armadilha" típica da prova: assumir que tudo local é on-premises tradicional. **Não é** — pode ser nuvem privada.

## Para a prova CLF-C02

Aparece como **distinção** entre modelos, não tanto como modelo principal. Palavras-gatilho: "VMware no data center próprio", "AWS Outposts", "nuvem dedicada", "infra cloud local".

## Fontes

- [[sources/clf-c02-aula04-deployment-models]]

## Relações

- [[concepts/on-premises]]
- [[concepts/hybrid-cloud]]
- [[concepts/cloud-computing]]
- [[concepts/virtualization]]
- [[topics/cloud-fundamentals]]
