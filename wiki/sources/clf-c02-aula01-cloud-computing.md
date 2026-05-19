---
title: "CLF-C02 Aula 01 — O que é Cloud Computing"
type: source
tags: [aws, clf-c02, cloud, certificação, conceitual]
created: 2026-05-19
updated: 2026-05-19
sources: 1
---

# CLF-C02 Aula 01 — O que é Cloud Computing

Arquivo fonte: `raw/clf-c02-aula01-o-que-e-cloud-computing.md` (PT-BR)

Primeira aula do preparatório **AWS Cloud Practitioner (CLF-C02)**. Conceitual, sem pré-requisitos técnicos. Apresenta o mundo pré-cloud (cliente-servidor, on-premises, virtualização) e a definição formal de [[concepts/cloud-computing|Cloud Computing]] pela AWS, ancorando o conceito de **pay-as-you-go**.

---

## Pontos-chave

- **Pré-cloud**: arquitetura cliente-servidor → data centers próprios ([[concepts/on-premises|on-premises]]) → [[concepts/virtualization|virtualização]] (hypervisor).
- A massificação da internet, mobile e IoT tornou data centers locais inviáveis para escala global.
- **Definição AWS de [[concepts/cloud-computing|Cloud Computing]]**: "Entrega de recursos de TI sob demanda, por meio da internet, com precificação baseada em pagamento conforme o uso."
- **Pay-as-you-go**: paga só pelo que consome, sem custo fixo de infra — chave para entender o resto do curso.
- A virtualização (hypervisor permite múltiplas VMs em um único hardware) é a base técnica sobre a qual a cloud foi construída.

## Linha do tempo conceitual

```
Cliente-Servidor  →  On-Premises (data centers)  →  Virtualização  →  Cloud Computing
```

## On-Premises vs Cloud (do material)

| Aspecto | On-Premises | Cloud |
|---|---|---|
| Custo inicial | Alto | Zero |
| Custo operacional | Alto (equipe, energia, refrigeração) | Proporcional ao uso |
| Escalabilidade | Lenta e cara | Imediata e elástica |
| Gerenciamento | Responsabilidade da empresa | Compartilhado ou gerenciado pelo provedor |
| Tempo de provisionar | Semanas/meses | Segundos/minutos |

## Dica de prova destacada

A **definição formal da AWS** e o conceito **pay-as-you-go** caem direto no exame. Saber distinguir on-premises, cloud e híbrido é base para várias questões.

---

## Entidades e conceitos tocados

- Entidades: [[entities/aws]]
- Conceitos: [[concepts/cloud-computing]] (novo), [[concepts/on-premises]] (novo), [[concepts/virtualization]] (novo)
- Tópicos: [[topics/cloud-fundamentals]] (novo)
