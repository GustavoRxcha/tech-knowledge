---
title: "CLF-C02 Aula 04 — Modelos de Implantação"
type: source
tags: [aws, clf-c02, cloud, on-premises, hybrid, deployment, certificação]
created: 2026-05-19
updated: 2026-05-19
sources: 1
---

# CLF-C02 Aula 04 — Modelos de Implantação

Arquivo fonte: `raw/clf-c02-aula04-modelos-de-implantacao.md` (PT-BR)

Apresenta os três modelos de **implantação** — **onde** a solução roda. Não confundir com modelos de **serviço** (IaaS/PaaS/SaaS = nível de gerenciamento).

---

## Os três modelos principais

| Modelo | Onde roda | Quem gerencia |
|---|---|---|
| [[concepts/on-premises\|On-Premises]] | Data center próprio / local | A própria organização |
| [[concepts/hybrid-cloud\|Híbrido]] | Parte local + parte na nuvem | Compartilhado |
| **Cloud (Pública)** | Totalmente em provedor (AWS, Azure, GCP) | Provedor + organização |

## Comparativo (do material)

| Critério | On-Premises | Híbrido | Cloud |
|---|---|---|---|
| Localização | Data center próprio | Local + Nuvem | Provedor cloud |
| Controle | Total | Parcial | Compartilhado |
| Custo inicial | Alto | Médio | Baixo/Zero |
| Escalabilidade | Lenta e cara | Parcial | Imediata |
| Gerenciamento | 100% interno | Compartilhado | Provedor + time |
| Casos de uso | Compliance, legado | Migração, compliance parcial | Novos projetos, nativas cloud |

## Modelo híbrido em migrações

Padrão típico de transição:

```
Mês 1:  100% on-premises
Mês 3:  primeiros workloads na cloud → modo híbrido
Mês 6:  equilíbrio híbrido
Mês 12: 100% cloud
```

Outros casos: dados sensíveis locais por compliance, cloud bursting (picos), sistemas legados integrados a serviços novos.

## Distinção importante: [[concepts/private-cloud|Private Cloud]]

| Conceito | Localização | Tecnologia |
|---|---|---|
| On-premises tradicional | Local | Sem cloud |
| **Nuvem privada** | Local | **Com tecnologia cloud** (VMware, OpenStack, AWS Outposts) |
| Nuvem pública | Provedor (AWS, Azure, GCP) | Cloud |
| Nuvem híbrida | Local + Provedor | Misto |

> Nem todo on-premises é "sem cloud" — pode ser nuvem privada rodando localmente.

## Pergunta diagnóstica

> "Onde está sua aplicação?"
> - Só no servidor local → **On-Premises**
> - Parte local, parte na nuvem → **Híbrido**
> - Toda na AWS/Azure/GCP → **Cloud**

## Dica de prova destacada

Cenário comum: descrição de empresa → identificar modelo. Palavras-gatilho:
- "data center próprio" → on-premises
- "migração gradual", "parte local" → híbrido
- "tudo na nuvem" → cloud

---

## Entidades e conceitos tocados

- Entidades: [[entities/aws]]
- Conceitos: [[concepts/on-premises]], [[concepts/hybrid-cloud]] (novo), [[concepts/private-cloud]] (novo), [[concepts/cloud-computing]]
- Tópicos: [[topics/cloud-fundamentals]]
