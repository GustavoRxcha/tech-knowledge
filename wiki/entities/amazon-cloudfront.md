---
title: "Amazon CloudFront"
type: entity
tags: [aws, cloudfront, cdn, edge-location, cache, latencia]
created: 2026-05-20
updated: 2026-05-20
sources: 1
---

# Amazon CloudFront

O **Amazon CloudFront** é o serviço de **CDN (Content Delivery Network — Rede de Entrega de Conteúdo)** da [[entities/aws|AWS]]. Utiliza a rede de [[concepts/edge-location|Edge Locations]] para entregar conteúdo ao usuário final com máxima velocidade e mínima latência.

---

## Como funciona

1. O conteúdo está hospedado em uma **origem** (S3, EC2, ALB, ou servidor externo) em uma região AWS
2. O CloudFront distribui esse conteúdo para as **Edge Locations** ao redor do mundo
3. Quando um usuário acessa o conteúdo, o CloudFront serve a partir da **Edge Location mais próxima**
4. O conteúdo fica em **cache** na Edge Location por um período configurável (TTL)
5. Acessos subsequentes são servidos diretamente do cache local — sem precisar ir até a origem

```
[Origem: S3 em us-east-1]
         ↓ distribuição
[Edge Location SP] [Edge Location Frankfurt] [Edge Location Tóquio]
         ↓
[Usuário em SP acessa] → cache local → resposta muito rápida
```

---

## Benefícios

| Benefício | Descrição |
|---|---|
| Baixa latência | Conteúdo servido do ponto mais próximo do usuário |
| Alta taxa de transferência | Otimizado para entrega de grandes volumes |
| Cache inteligente | Conteúdo popular fica armazenado nas bordas |
| Segurança | Integração com Shield (DDoS) e WAF |
| Alcance global | Rede com 400+ pontos de presença |

---

## Casos de uso

- Distribuição de vídeos e streaming
- Entrega de sites e aplicações web estáticas
- Download de arquivos grandes (software, jogos)
- APIs com usuários globais

---

## Para a prova CLF-C02

- *"Qual serviço reduz a latência para usuários globais?"* → **CloudFront**
- *"Qual serviço da AWS implementa CDN?"* → **Amazon CloudFront**

---

## Relações

- [[concepts/edge-location]] — infraestrutura que o CloudFront utiliza
- [[entities/amazon-s3]] — origem comum para distribuição via CloudFront
- [[entities/amazon-route53]] — usado em conjunto para roteamento de domínios
- [[concepts/aws-region]] — onde ficam as origens dos conteúdos

## Fontes

- [[sources/clf-c02-aula05-global-infrastructure]]
- [[sources/clf-c02-aula07-edge-cloudfront-route53]]
