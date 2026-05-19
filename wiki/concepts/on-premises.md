---
title: "On-Premises"
type: concept
tags: [infraestrutura, on-premises, deployment, clf-c02]
created: 2026-05-19
updated: 2026-05-19
sources: 2
---

# On-Premises

Modelo de implantação em que **toda a infraestrutura está fisicamente nas instalações da organização** — seu data center, sala de servidores, hardware próprio.

---

## Características

- Hardware, rede, SO e aplicações **comprados e gerenciados internamente**.
- Controle total sobre a infraestrutura.
- Custos altos de aquisição, manutenção, energia, refrigeração, segurança física.
- Escalabilidade lenta e cara (comprar mais hardware leva semanas/meses).
- Necessidade de equipe dedicada à infra.

## Trade-off central

| Vantagem | Custo |
|---|---|
| Controle total | Capex pesado + equipe dedicada |
| Dados ficam no seu prédio | Sem [[concepts/elasticity\|elasticidade]] real |
| Compliance fácil (em casos sensíveis) | Provisionamento lento |
| Sem dependência de provedor | Sem economias de escala globais |

## Quando ainda faz sentido

- Requisitos regulatórios que **exigem** dados locais (alguns setores: defesa, saúde, financeiro).
- Sistemas legados ainda não modernizados.
- Organizações que ainda não iniciaram migração.
- Cargas de trabalho com perfil **previsível e constante** (sem picos), onde a economia da cloud não compensa.

## On-Premises vs [[concepts/cloud-computing|Cloud]]

| Aspecto | On-Premises | Cloud |
|---|---|---|
| Custo inicial | Alto | Zero |
| Custo operacional | Alto fixo | Proporcional ao uso |
| Escalabilidade | Lenta | Imediata |
| Tempo de provisionar | Semanas/meses | Segundos/minutos |
| Gerenciamento da infra física | Você | Provedor |

## Atenção: on-premises ≠ "sem cloud"

É possível rodar uma [[concepts/private-cloud|nuvem privada]] localmente (VMware, OpenStack, AWS Outposts) — a infra é local mas usa tecnologia cloud. Não confunda os termos:

| | Localização | Tecnologia cloud? |
|---|---|---|
| On-premises tradicional | Local | Não |
| **Nuvem privada** | Local | **Sim** |
| Nuvem pública | Provedor | Sim |
| [[concepts/hybrid-cloud\|Híbrida]] | Local + provedor | Misto |

## Para a prova CLF-C02

Palavras-gatilho: "data center próprio", "servidores na empresa", "infra local", "hardware comprado".

Cenário típico: "Empresa mantém todos os servidores em seu prédio principal" → **On-Premises**.

## Fontes

- [[sources/clf-c02-aula01-cloud-computing]]
- [[sources/clf-c02-aula04-deployment-models]]

## Relações

- [[concepts/cloud-computing]]
- [[concepts/hybrid-cloud]]
- [[concepts/private-cloud]]
- [[concepts/cloud-benefits]]
- [[concepts/virtualization]]
- [[topics/cloud-fundamentals]]
