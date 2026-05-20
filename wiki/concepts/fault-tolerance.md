---
title: "Tolerância a Falhas (Fault Tolerance)"
type: concept
tags: [aws, arquitetura, fault-tolerance, availability-zone, clf-c02]
created: 2026-05-20
updated: 2026-05-20
sources: 2
---

# Tolerância a Falhas (Fault Tolerance)

**Tolerância a falhas** é a capacidade de uma arquitetura de **resistir a falhas de componentes sem interrupção do serviço**. A diferença para [[concepts/high-availability|alta disponibilidade]] é o foco: tolerância a falhas descreve o design da arquitetura, não apenas o resultado.

---

## Distinção

| Conceito | Foco |
|---|---|
| **Tolerância a falhas** | Como a *arquitetura* é projetada para resistir a falhas |
| **[[concepts/high-availability\|Alta disponibilidade]]** | O *resultado* — o serviço continua rodando mesmo com falha |

Na prática, os dois conceitos andam juntos e muitas vezes são usados de forma intercambiável.

---

## Como a AWS implementa

A AWS implementa tolerância a falhas através de:

1. **[[concepts/availability-zone|Múltiplas AZs]]** — falha em uma AZ não afeta as outras
2. **Serviços de escopo regional** (S3, DynamoDB, IAM) — distribuídos automaticamente entre AZs
3. **Replicação de dados** — dados em AZs distintas, protegidos contra perda

---

## Cenário prático

```
Arquitetura tolerante a falhas:
- EC2 em AZ-a + EC2 em AZ-b + Load Balancer
- RDS Multi-AZ (replicação automática)

Resultado:
- AZ-a falha → tráfego vai para AZ-b automaticamente
- Sem perda de dados, sem interrupção de serviço
```

---

## Relações

- [[concepts/availability-zone]] — mecanismo principal de tolerância a falhas
- [[concepts/high-availability]] — resultado garantido por uma arquitetura tolerante a falhas
- [[concepts/aws-region]] — contexto geográfico

## Fontes

- [[sources/clf-c02-aula05-global-infrastructure]]
- [[sources/clf-c02-aula06-regions-az]]
