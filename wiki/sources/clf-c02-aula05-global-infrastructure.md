---
title: "CLF-C02 Aula 05 — Infraestrutura Global AWS"
type: source
tags: [aws, clf-c02, infraestrutura-global, regioes, az, edge-locations]
created: 2026-05-20
updated: 2026-05-20
sources: 1
---

# CLF-C02 Aula 05 — Infraestrutura Global AWS

Aula introdutória do módulo de Infraestrutura Global do curso preparatório para a certificação AWS Cloud Practitioner (CLF-C02). Apresenta a hierarquia completa da infraestrutura física da AWS e as formas de provisionar recursos.

---

## Origem

- **Arquivo:** `raw/clf-c02-aula05-infraestrutura-global-aws.md`
- **Trilha:** CLF-C02 — Preparatório AWS Cloud Practitioner
- **Módulo:** Infraestrutura Global AWS (aula 01 do módulo)

---

## Conceito central

A **Infraestrutura Global AWS** é o conjunto de data centers, redes e recursos físicos distribuídos pelo mundo que sustenta todos os serviços da AWS (EC2, S3, RDS, Lambda, etc.). É o "chão" da plataforma.

Diferencia-se do modelo on-premises: a AWS construiu infra física compartilhada que qualquer cliente pode consumir via internet, sem gerenciar hardware.

---

## Hierarquia completa

```
Infraestrutura Global AWS
│
├── Regiões (27+ na gravação)
│   └── ex: sa-east-1 (São Paulo), us-east-1 (Virgínia)
│       └── Zonas de Disponibilidade (87+ no total)
│           └── ex: sa-east-1a, sa-east-1b, sa-east-1c
│               └── Data Centers físicos
│
└── Pontos de Presença / Edge Locations (400+)
    └── ex: São Paulo, Buenos Aires, Frankfurt, Tóquio...
```

---

## Regiões

- Área geográfica com múltiplos data centers, independente das demais.
- Código de identificação: `sa-east-1`, `us-east-1`, etc.
- Dados **não replicam automaticamente** entre regiões.
- Fatores de escolha: Latência · Compliance · Disponibilidade de serviços · Custo.

## Zonas de Disponibilidade (AZs)

- Um ou mais data centers fisicamente separados dentro de uma região.
- Energia, refrigeração e rede independentes.
- Separadas por dezenas de km: isolamento de falhas sem penalidade de performance.
- Boa prática: rodar em **pelo menos 2 AZs**.

## Pontos de Presença (Edge Locations)

- Locais físicos distribuídos globalmente, em número muito superior às regiões.
- Usados por: **CloudFront** (CDN), **Route 53** (DNS), **AWS Global Accelerator**.
- Armazenam conteúdo em cache próximo ao usuário final → latência mínima.

## Formas de provisionar recursos

| Método | Descrição |
|---|---|
| Console AWS | Interface web, visual e intuitiva |
| AWS CLI | Linha de comando — automação e scripts |
| SDKs | Bibliotecas para Python (boto3), JS, Java, etc. |
| CloudFormation / Terraform | Infraestrutura como código (IaC) |

---

## Conceitos/entidades relacionados

- [[concepts/aws-region]]
- [[concepts/availability-zone]]
- [[concepts/edge-location]]
- [[concepts/high-availability]]
- [[concepts/fault-tolerance]]
- [[entities/amazon-cloudfront]]
- [[entities/amazon-route53]]
- [[entities/aws-cloudformation]]
- [[concepts/infrastructure-as-code]]
