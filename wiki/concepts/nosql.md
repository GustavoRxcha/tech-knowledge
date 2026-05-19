---
title: "NoSQL"
type: concept
tags: [bancos-de-dados, nosql, modelagem]
created: 2026-05-19
updated: 2026-05-19
sources: 1
---

# NoSQL

Categoria ampla de bancos **não-relacionais**. Inclui key-value, documento, coluna larga, grafo. Difere de SQL na ausência (ou flexibilidade) de schema fixo, no modelo de consulta e nas garantias de consistência.

---

## Principais diferenças vs SQL relacional

| Aspecto | SQL | NoSQL |
|---|---|---|
| Schema | Fixo, definido antecipadamente | Flexível (schemaless ou semi-estruturado) |
| Joins | Sim (núcleo da linguagem) | Geralmente não — desnormalização é a norma |
| Consultas | Linguagem declarativa (SQL) | APIs específicas por banco |
| Escalabilidade | Vertical primeiro, horizontal complexo | Horizontal nativo |
| Consistência | ACID forte | Geralmente eventual (varia por banco) |

## Famílias

| Família | Modelo | Exemplos |
|---|---|---|
| **Key-Value** | Chave → valor opaco | Redis, DynamoDB (modo simples) |
| **Document** | Documentos JSON-like | MongoDB, DynamoDB (com attrs) |
| **Wide-column** | Tabelas com famílias de colunas | Cassandra, HBase, Bigtable |
| **Graph** | Nós + arestas | Neo4j, Neptune |

## DynamoDB como exemplo

[[entities/amazon-dynamodb]] mistura key-value e document:

- **Tabelas** com itens.
- Cada item é uma coleção de **atributos** (chave/valor).
- Itens podem ter **atributos diferentes** — não precisa declarar colunas.
- Identidade do item: **Partition Key** (obrigatória) + **Sort Key** (opcional).
- Consultas eficientes só pela chave; varredura geral (`scan`) é cara.

## Quando usar NoSQL

- Volumes muito grandes e acesso por chave.
- Schema evolui rápido ou varia por entidade.
- Latência baixa previsível mais importante que joins complexos.
- Escala horizontal massiva.

## Quando preferir SQL

- Relacionamentos ricos entre entidades.
- Consultas ad-hoc e flexíveis.
- Transações multi-tabela com garantias ACID fortes.
- Time já conhece SQL e o modelo encaixa.

## Fontes

- [[sources/aws-course-dynamo-01-table-lambda-intro]]

## Relações

- [[entities/amazon-dynamodb]]
- [[concepts/serverless]] — DynamoDB também é serverless
