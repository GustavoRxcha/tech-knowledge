---
title: "Edge Location (Ponto de Presença)"
type: concept
tags: [aws, infraestrutura-global, edge-location, cdn, cloudfront, route53, clf-c02]
created: 2026-05-20
updated: 2026-05-20
sources: 2
---

# Edge Location (Ponto de Presença)

**Edge Locations** (também chamados de **Pontos de Presença** ou **Locais de Borda**) são locais físicos distribuídos globalmente — em número muito superior às [[concepts/aws-region|Regiões]] — que servem para **distribuir conteúdo com baixa latência** e melhorar a conectividade para usuários ao redor do mundo.

---

## Termos equivalentes

Na prova CLF-C02, os três termos podem aparecer — todos se referem à mesma estrutura:

| Termo | Contexto |
|---|---|
| **Edge Locations** | Inglês — mais comum em documentações |
| **Pontos de Presença** | Português — tradução oficial |
| **Locais de Borda** / **Rede de Borda** | Usado em alguns materiais |

---

## Por que existem

Regiões e AZs garantem disponibilidade, mas estão em locais geográficos fixos. Quando um usuário acessa um serviço em uma região distante, a latência aumenta.

### Solução: cache na borda

```
1º acesso: usuário → região distante (lento — cache miss)
           ↓ Edge Location local armazena o conteúdo em cache
2º acesso: usuário → Edge Location local (rápido — cache hit)
```

---

## Números de referência

| | Quantidade |
|---|---|
| Regiões | ~30+ |
| Zonas de Disponibilidade | ~87+ |
| **Edge Locations** | **~400+** |

---

## Serviços que usam Edge Locations

| Serviço | Função |
|---|---|
| [[entities/amazon-cloudfront]] | CDN — distribui conteúdo em cache |
| [[entities/amazon-route53]] | DNS — resolve domínios com baixa latência |
| AWS Global Accelerator | Otimiza roteamento de tráfego para apps globais |

---

## Diferença em relação às Regiões

| | Regiões | Edge Locations |
|---|---|---|
| Propósito | Hospedar serviços | Entregar conteúdo ao usuário final |
| Quantidade | ~30+ | ~400+ |
| Cache | ❌ | ✅ |
| Exemplos de serviços | EC2, S3, RDS | CloudFront, Route 53 |

---

## Para a prova CLF-C02

- *"O que reduz a latência para usuários globais?"* → **Edge Locations / CloudFront**
- *"Qual a diferença entre Região e Edge Location?"* → Região hospeda serviços; Edge Location entrega conteúdo em cache próximo ao usuário

---

## Relações

- [[concepts/aws-region]] — Regiões hospedam os serviços; Edge Locations entregam o conteúdo
- [[entities/amazon-cloudfront]] — usa Edge Locations para CDN
- [[entities/amazon-route53]] — usa Edge Locations para DNS

## Fontes

- [[sources/clf-c02-aula05-global-infrastructure]]
- [[sources/clf-c02-aula07-edge-cloudfront-route53]]
