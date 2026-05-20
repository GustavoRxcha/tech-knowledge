---
title: "CLF-C02 Aula 09 — Amazon EC2 e Tipos de Instância"
type: source
tags: [aws, clf-c02, ec2, instancias, ami, computacao]
created: 2026-05-20
updated: 2026-05-20
sources: 1
---

# CLF-C02 Aula 09 — Amazon EC2 e Tipos de Instância

Aula introdutória do módulo de Computação na AWS. Cobre o problema do data center próprio, o que é o EC2, AMIs, ciclo de vida de instâncias e os 5 tipos (famílias) de instância.

---

## Origem

- **Arquivo:** `raw/clf-c02-aula09-ec2-tipos-instancia.md`
- **Trilha:** CLF-C02 — Preparatório AWS Cloud Practitioner
- **Módulo:** Computação na AWS (aula 01 do módulo / aula 09 do curso)

---

## O problema que o EC2 resolve

Montar infraestrutura própria exige: segurança física, analistas de rede, energia redundante, refrigeração, data center de backup, racks. É caro, complexo e exige equipes dedicadas só para manter infra.

**Dilema da capacidade:**

| Cenário | Problema |
|---|---|
| Compra hardware além do necessário | Capacidade ociosa — prejuízo |
| Compra hardware abaixo do necessário | Sistema não suporta a demanda |
| Negócio cresce rápido | Mais racks levam semanas/meses |
| Negócio não cresce | Investimento desperdiçado |

O EC2 resolve com: pagar pelo uso · [[concepts/elasticity|elasticidade]] · escalabilidade · disponibilidade.

---

## O que é o EC2

**EC2 = Elastic Compute Cloud** — capacidade computacional segura e redimensionável na nuvem.

> O nome tem dois "C"s → "2" no nome.

O que você configura em uma instância: CPU, RAM, armazenamento, rede, sistema operacional. Tudo pode ser alterado a qualquer momento sem comprar hardware.

**Modelo:** paga por hora ou por segundo conforme o uso. Instância parada = sem cobrança por computação.

---

## AMI — Amazon Machine Image

"Molde" a partir do qual a instância é criada. Define:
- Sistema operacional (Amazon Linux, Ubuntu, Windows Server...)
- Configurações iniciais
- Softwares pré-instalados (em AMIs customizadas)

---

## Ciclo de vida de uma instância

| Estado | Descrição |
|---|---|
| **Pendente** | Inicializando após ser lançada |
| **Executando** | Rodando e disponível |
| **Reiniciando** | Reboot — mantém IP e dados |
| **Parada** | Desligada — não cobra por compute, mas cobra pelo armazenamento |
| **Hibernada** | Salva o estado da memória em disco e para |
| **Encerrada** | Destruída permanentemente — não pode ser recuperada |

---

## 5 famílias de instância EC2

| Família | Foco | Palavra-chave | Exemplos de uso |
|---|---|---|---|
| **Uso Geral** | Equilíbrio CPU/RAM/Rede | "padrão", "balanceado" | Web servers, apps gerais |
| **Computação** | Alto desempenho de CPU | "processamento", "lote" | Batch, jogos, modelagem científica |
| **Memória** | Grande quantidade de RAM | "em memória", "tempo real" | Redis, SAP HANA, grandes datasets |
| **Acelerada** | GPU / hardware especializado | "gráficos", "ML", "GPU" | Deep Learning, rendering |
| **Armazenamento** | I/O de disco intensivo | "leitura/gravação", "OLTP" | Data warehouses, OLTP, HDFS |

---

## Módulo previsto (mapa das aulas)

| Etapa | Serviço |
|---|---|
| 1 | Amazon EC2 — esta aula |
| 2 | EC2 Auto Scaling |
| 3 | Elastic Load Balancing (ELB) |
| 4 | Computação Serverless (Lambda) |
| 5 | Containers (ECS, EKS, Fargate) |

---

## Conceitos/entidades relacionados

- [[entities/amazon-ec2]]
- [[concepts/elasticity]]
- [[concepts/iaas]]
- [[concepts/auto-scaling]]
