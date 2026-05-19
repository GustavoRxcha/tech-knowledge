---
title: "Hybrid Cloud (Nuvem Híbrida)"
type: concept
tags: [cloud, hybrid, deployment, clf-c02]
created: 2026-05-19
updated: 2026-05-19
sources: 1
---

# Hybrid Cloud — Nuvem Híbrida

Modelo de implantação em que a solução roda **parte na nuvem e parte no [[concepts/on-premises|on-premises]]** ao mesmo tempo, com os dois ambientes coexistindo e se comunicando.

---

## Quando é usado

### Migração gradual (caso mais comum)

```
Mês 1:  100% on-premises
Mês 3:  primeiros workloads na cloud → híbrido
Mês 6:  equilíbrio híbrido
Mês 12: 100% cloud
```

Durante a transição, a empresa **necessariamente** opera em modo híbrido.

### Outros casos

- **Compliance parcial**: dados sensíveis locais, resto na cloud.
- **Sistemas legados**: ficam locais e se integram a serviços novos na cloud.
- **Cloud bursting**: infra local atende baseline, cloud absorve picos.
- **Continuidade de negócio**: cloud como redundância do data center local.

## Características

| Aspecto | Descrição |
|---|---|
| **Flexibilidade** | Combina controle do on-prem com elasticidade da cloud |
| **Complexidade** | Maior — gerenciamento e integração de dois ambientes |
| **Custo** | Mantém parte do CapEx + paga OpEx da cloud |
| **Conectividade** | Exige link seguro entre on-prem e cloud (VPN, Direct Connect) |

## Para a prova CLF-C02

Palavras-gatilho: "migração gradual", "parte local, parte na nuvem", "transição", "compliance + nuvem", "alguns sistemas ainda locais".

Cenário típico: "Empresa migrando do data center próprio para a AWS ao longo de 12 meses, com sistemas em ambos durante o processo" → **Híbrido**.

## Comparativo rápido

| | On-Prem | Híbrido | Cloud |
|---|---|---|---|
| Localização | Só local | Local + provedor | Só provedor |
| Controle | Total | Parcial | Compartilhado |
| Custo inicial | Alto | Médio | Baixo/zero |

## Fontes

- [[sources/clf-c02-aula04-deployment-models]]

## Relações

- [[concepts/on-premises]]
- [[concepts/private-cloud]]
- [[concepts/cloud-computing]]
- [[topics/cloud-fundamentals]]
