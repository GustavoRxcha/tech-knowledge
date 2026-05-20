---
title: "CLF-C02 Aula 06 — Regiões e Zonas de Disponibilidade"
type: source
tags: [aws, clf-c02, regioes, availability-zones, compliance, lgpd, gdpr]
created: 2026-05-20
updated: 2026-05-20
sources: 1
---

# CLF-C02 Aula 06 — Regiões e Zonas de Disponibilidade

Aprofundamento sobre Regiões e Availability Zones: isolamento de dados, conformidade legal (LGPD/GDPR), critérios de escolha de região e escopo de serviços (AZ-scope vs regional-scope).

---

## Origem

- **Arquivo:** `raw/clf-c02-aula06-regioes-zonas-disponibilidade.md`
- **Trilha:** CLF-C02 — Preparatório AWS Cloud Practitioner
- **Módulo:** Infraestrutura Global AWS (aula 02 do módulo / aula 06 do curso)

---

## Regiões — detalhes

### Isolamento de dados

Dados armazenados em uma região **não saem dela automaticamente**. Para mover dados entre regiões é necessário configurar explicitamente (ex: replicação S3 cross-region).

> Garante controle total sobre a localização física dos dados.

### Conectividade entre regiões

Todas as regiões são interconectadas por rede de **fibra óptica de alta velocidade** da própria AWS, atravessando oceanos e continentes.

### Conformidade legal (soberania de dados)

Cada região está sujeita às leis e regulamentações locais:

| País / Região | Regulamentação |
|---|---|
| Brasil | LGPD |
| Europa | GDPR |
| China | Legislação local de soberania de dados |
| EUA | HIPAA, CCPA e outras |

### 4 critérios de escolha de região

| Critério | Pergunta-chave |
|---|---|
| **Compliance** | Há requisitos legais que exigem que os dados fiquem em um país específico? |
| **Latência** | Onde estão os usuários finais? |
| **Disponibilidade de serviços** | O serviço AWS que preciso está disponível nessa região? |
| **Custo** | O preço dos serviços varia entre regiões |

> **Compliance sempre tem prioridade.** Se a lei exige dados no Brasil, `sa-east-1` é obrigatória.

---

## Zonas de Disponibilidade — detalhes

### Equilíbrio estratégico das AZs

```
Distância entre AZs:
├── Longe o suficiente → desastre afeta apenas UMA AZ
└── Perto o suficiente → latência entre AZs permanece baixa (dezenas de ms)
```

### Cenário com e sem AZs

**Sem AZs:**
```
1 data center → tornado/falha → serviço indisponível + risco de perda de dados
```

**Com AZs (app nas AZs A e B):**
```
AZ-a fica indisponível → AZ-b continua operando → sem interrupção
```

---

## Escopo de serviços: AZ vs Regional

| Escopo | Serviços | Implicação |
|---|---|---|
| **AZ-scope** | EC2, EBS | Se a AZ falhar, o serviço nela hospedado falha. Provisionar em ≥2 AZs. |
| **Regional-scope** | S3, DynamoDB, IAM | Distribuídos automaticamente entre AZs. Sem config. manual de redundância. |

---

## Conceitos/entidades relacionados

- [[concepts/aws-region]]
- [[concepts/availability-zone]]
- [[concepts/high-availability]]
- [[concepts/fault-tolerance]]
- [[entities/amazon-ec2]]
- [[entities/amazon-s3]]
- [[entities/amazon-dynamodb]]
- [[entities/aws-iam]]
