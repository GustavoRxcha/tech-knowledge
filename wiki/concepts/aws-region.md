---
title: "Região AWS (Region)"
type: concept
tags: [aws, infraestrutura-global, regiao, compliance, latencia, clf-c02]
created: 2026-05-20
updated: 2026-05-20
sources: 2
---

# Região AWS (Region)

Uma **Região** é um agrupamento de data centers da AWS em uma **localização geográfica específica** no mundo. Cada região é independente das demais — tem sua própria infraestrutura, energia, rede e conectividade.

---

## Identificação

Cada região tem um nome descritivo e um código:

| Região | Código |
|---|---|
| São Paulo | `sa-east-1` |
| Virgínia do Norte (EUA) | `us-east-1` |
| Irlanda (Europa) | `eu-west-1` |
| Tóquio (Ásia) | `ap-northeast-1` |

---

## Características fundamentais

### Isolamento de dados

Dados armazenados em uma região **não saem dela automaticamente**. Para mover dados entre regiões é necessário configurar explicitamente (ex: replicação S3 cross-region).

> Garante controle total sobre a localização física dos dados.

### Conectividade

Todas as regiões são interconectadas por **rede de fibra óptica de alta velocidade** da própria AWS, atravessando oceanos e continentes.

### Soberania de dados

Cada região está sujeita às leis e regulamentações locais de proteção de dados:

| País | Regulamentação |
|---|---|
| Brasil | LGPD |
| Europa | GDPR |
| China | Legislação local |
| EUA | HIPAA, CCPA e outras |

---

## 4 critérios de escolha de região

| Critério | Pergunta-chave |
|---|---|
| **Compliance** | Há requisitos legais que exigem dados em um país específico? |
| **Latência** | Onde estão os usuários finais? |
| **Disponibilidade de serviços** | O serviço AWS que preciso está nessa região? |
| **Custo** | O preço dos serviços varia entre regiões — qual oferece melhor custo-benefício? |

> **Compliance sempre tem prioridade.** Se a lei exige dados no Brasil, `sa-east-1` é obrigatória independente dos demais fatores.

---

## Relação com AZs e Edge Locations

```
Infraestrutura Global AWS
├── Regiões (30+)
│   └── Zonas de Disponibilidade (87+)
│       └── Data Centers físicos
└── Edge Locations (400+) — fora das regiões, próximas aos usuários
```

---

## Para a prova CLF-C02

- *"Por que os dados de uma região não aparecem em outra?"* → **Isolamento de dados por região**
- *"Qual critério deve ser priorizado ao escolher uma região?"* → **Compliance/conformidade legal**

---

## Relações

- [[concepts/availability-zone]] — contidas dentro de cada Região
- [[concepts/edge-location]] — distribuídas globalmente, separadas das Regiões
- [[concepts/high-availability]] — garantida por múltiplas AZs dentro da Região
- [[entities/amazon-s3]] — escopo regional
- [[entities/amazon-dynamodb]] — escopo regional
- [[entities/aws-iam]] — escopo regional

## Fontes

- [[sources/clf-c02-aula05-global-infrastructure]]
- [[sources/clf-c02-aula06-regions-az]]
