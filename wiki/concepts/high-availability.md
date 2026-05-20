---
title: "Alta Disponibilidade (High Availability)"
type: concept
tags: [aws, arquitetura, alta-disponibilidade, availability-zone, clf-c02]
created: 2026-05-20
updated: 2026-05-20
sources: 2
---

# Alta Disponibilidade (High Availability)

**Alta disponibilidade** é a capacidade de um sistema continuar operando mesmo quando componentes individuais falham. O serviço permanece acessível sem interrupção perceptível para o usuário.

---

## Distinção importante

| Conceito | Definição |
|---|---|
| **Alta disponibilidade** | O serviço *continua rodando* mesmo com falha parcial |
| **[[concepts/fault-tolerance\|Tolerância a falhas]]** | A *arquitetura* resiste a falhas sem nenhuma interrupção |

> Alta disponibilidade foca no resultado (uptime). Tolerância a falhas foca no design (como a arquitetura resiste).

---

## Como a AWS implementa

A AWS implementa alta disponibilidade principalmente através das [[concepts/availability-zone|Zonas de Disponibilidade (AZs)]]:

```
App rodando em AZ-a e AZ-b (mesma Região)
        ↓
AZ-a sofre falha catastrófica
        ↓
AZ-b absorve o tráfego → usuários não percebem interrupção
```

---

## Boa prática

> Sempre provisionar recursos críticos (como [[entities/amazon-ec2|EC2]]) em **pelo menos 2 AZs** para garantir alta disponibilidade.

---

## Relações

- [[concepts/availability-zone]] — mecanismo principal de alta disponibilidade na AWS
- [[concepts/fault-tolerance]] — conceito relacionado (design de arquitetura)
- [[concepts/aws-region]] — contexto geográfico das AZs

## Fontes

- [[sources/clf-c02-aula05-global-infrastructure]]
- [[sources/clf-c02-aula06-regions-az]]
