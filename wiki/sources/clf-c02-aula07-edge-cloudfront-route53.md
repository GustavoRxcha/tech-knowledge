---
title: "CLF-C02 Aula 07 — Edge Locations, CloudFront e Route 53"
type: source
tags: [aws, clf-c02, edge-locations, cloudfront, route53, cdn, dns]
created: 2026-05-20
updated: 2026-05-20
sources: 1
---

# CLF-C02 Aula 07 — Edge Locations, CloudFront e Route 53

Detalhamento dos Pontos de Presença (Edge Locations), do Amazon CloudFront como CDN e do Amazon Route 53 como serviço DNS gerenciado na borda da rede.

---

## Origem

- **Arquivo:** `raw/clf-c02-aula07-edge-locations-cloudfront-route53.md`
- **Trilha:** CLF-C02 — Preparatório AWS Cloud Practitioner
- **Módulo:** Infraestrutura Global AWS (aula 03 do módulo / aula 07 do curso)

---

## Pontos de Presença (Edge Locations)

Termos equivalentes — todos se referem à mesma estrutura:
- **Edge Locations** (inglês — mais comum em docs)
- **Pontos de Presença** (português oficial)
- **Locais de Borda** / **Rede de Borda**

> Na prova CLF-C02, os três termos podem aparecer.

### Por que existem

Regiões e AZs garantem disponibilidade, mas estão em locais fixos. Um usuário acessando uma região muito distante sofre alta latência.

**Solução:** Servidores de borda instalados em pontos estratégicos ao redor do mundo, próximos aos usuários, armazenando conteúdo em **cache**.

```
1º acesso: usuário → região distante (cache miss)
Edge Location armazena o conteúdo
2º acesso: usuário → Edge Location local (cache hit) → muito mais rápido
```

---

## Amazon CloudFront

**CDN (Content Delivery Network)** da AWS. Utiliza a rede de Edge Locations para entregar conteúdo com máxima velocidade e mínima latência.

### Como funciona

1. Conteúdo hospedado na **origem** (S3, EC2, servidor externo) em uma região
2. CloudFront distribui para as **Edge Locations** globalmente
3. Usuário acessa a **Edge Location mais próxima**
4. Cache configurável por TTL; acessos subsequentes servidos localmente

### Benefícios

| Benefício | Descrição |
|---|---|
| Baixa latência | Conteúdo servido do ponto mais próximo |
| Alta taxa de transferência | Otimizado para grandes volumes |
| Cache inteligente | Conteúdo popular fica nas bordas |
| Segurança | Integração com Shield (DDoS) e WAF |
| Alcance global | 400+ pontos de presença |

### Casos de uso

- Streaming de vídeo
- Sites e apps estáticos
- Download de arquivos grandes
- APIs com usuários globais

---

## Amazon Route 53

**DNS (Domain Name System)** gerenciado da AWS. Opera nos Edge Locations para resolução de nomes rápida e confiável.

```
Usuário digita: www.meusite.com.br
    ↓ Route 53
Traduz para: 192.0.2.44
    ↓
Redireciona para o servidor mais próximo disponível
```

### Funcionalidades principais

| Funcionalidade | Descrição |
|---|---|
| Registro de domínios | Comprar e gerenciar domínios diretamente na AWS |
| Roteamento geográfico | Direcionar usuários por localização |
| Roteamento por latência | Direcionar para o servidor com menor latência |
| Health checks | Monitorar saúde e fazer failover automático |

---

## Comparativo: Regiões vs AZs vs Edge Locations

| | Regiões | AZs | Edge Locations |
|---|---|---|---|
| Quantidade | ~30+ | ~87+ | ~400+ |
| Propósito | Hospedar serviços | Alta disponibilidade | Entregar conteúdo |
| Serviços | EC2, S3, RDS, Lambda... | Redundância interna | CloudFront, Route 53 |
| Cache | ❌ | ❌ | ✅ |

---

## Conceitos/entidades relacionados

- [[concepts/edge-location]]
- [[entities/amazon-cloudfront]]
- [[entities/amazon-route53]]
- [[concepts/aws-region]]
- [[concepts/availability-zone]]
