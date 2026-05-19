---
title: "Elasticidade (Cloud)"
type: concept
tags: [cloud, elasticidade, auto-scaling, clf-c02]
created: 2026-05-19
updated: 2026-05-19
sources: 1
---

# Elasticidade

Capacidade de **aumentar ou diminuir recursos automaticamente** conforme a demanda. Um dos 5 benefícios oficiais da cloud pela AWS e termo recorrente no exame **CLF-C02**.

---

## Como funciona

1. Serviços monitoram métricas (CPU, memória, requisições por segundo, latência).
2. Quando a métrica passa de um limite, novas instâncias são provisionadas automaticamente.
3. Quando a demanda cai, instâncias excedentes são encerradas.
4. Você paga só pelo tempo em que cada instância esteve ativa.

```
Demanda baixa  → poucos recursos  → custo baixo
Demanda alta   → muitos recursos  → custo proporcional
Demanda normal → escala reduzida automaticamente
```

## Problema que resolve

O dilema clássico do [[concepts/on-premises|on-premises]]:

- Comprar para o pico → paga por capacidade ociosa o resto do tempo.
- Comprar abaixo do pico → sistema cai na Black Friday.

A elasticidade da cloud quebra esse trade-off: você dimensiona dinamicamente, sem precisar adivinhar.

## Elasticidade ≠ Escalabilidade

Distinção fina mas relevante:
- **Escalabilidade**: capacidade de crescer (não necessariamente automática).
- **Elasticidade**: crescer **e encolher**, automaticamente, em curto prazo.

Toda elasticidade é escalabilidade, mas nem toda escalabilidade é elástica.

## Para a prova

Palavras-gatilho: "pico", "Black Friday", "escalar automaticamente", "sazonalidade", "tráfego variável", "auto scaling".

> Cenário típico: "Empresa de e-commerce quer suportar 3x mais tráfego em datas comemorativas sem deixar capacidade ociosa o resto do ano." → **Elasticidade**.

## Implementação na AWS (referencial)

- **Auto Scaling Groups** (para EC2)
- **Lambda** já é elástica por design — escala automática até a concorrência configurada
- **DynamoDB** com on-demand capacity
- **RDS** com read replicas dinâmicas

## Fontes

- [[sources/clf-c02-aula02-cloud-benefits]]

## Relações

- [[concepts/cloud-benefits]]
- [[concepts/serverless]]
- [[entities/aws-lambda]]
- [[entities/amazon-dynamodb]]
- [[topics/cloud-fundamentals]]
