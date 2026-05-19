---
title: "Curso AWS — DynamoDB 01: Criação de Tabela e Introdução ao Lambda"
type: source
tags: [aws, dynamodb, lambda, nosql, curso]
created: 2026-05-19
updated: 2026-05-19
sources: 1
---

# Curso AWS — DynamoDB 01: Criação de Tabela e Introdução ao Lambda

Arquivo fonte: `raw/aula-dynamo-01-tabela-e-introducao-lambda.md` (PT-BR)

Início do módulo prático. Cria uma tabela `products` no [[entities/amazon-dynamodb|DynamoDB]] e inicia uma função [[entities/aws-lambda|Lambda]] que vai consumi-la. Apresenta os conceitos de chave de partição/ordenação e a distinção crítica entre Query e Scan.

---

## Pontos-chave

- [[entities/amazon-dynamodb|DynamoDB]]: [[concepts/nosql|NoSQL]] gerenciado, [[concepts/serverless|serverless]], escala automática.
- Estrutura: **tabelas → itens (linhas) → atributos (colunas)**. Schemaless: cada item pode ter atributos diferentes.
- Chaves:
  - **Partition Key** — obrigatória, identifica unicamente
  - **Sort Key** — opcional, forma chave composta com a Partition Key
- A combinação Partition+Sort deve ser única na tabela.
- Tipos suportados nas chaves: `String (S)`, `Number (N)`, `Binary (B)`.
- Dois modos de consulta:
  - **Query** ✅ — usa Partition Key como filtro, eficiente, recomendado
  - **Scan** ⚠️ — varre tudo, custoso, evitar em produção
- Todo recurso tem [[concepts/arn|ARN]]: `arn:aws:dynamodb:<região>:<conta>:table/<nome>`.

## Criação da tabela (passo a passo)

1. Console → DynamoDB → Tables → Create table
2. Nome: ex. `products`
3. Partition Key: ex. `product_id` (String)
4. Sort Key opcional: ex. `title` (String)
5. Após criação: ver itens, métricas, alarmes, índices

## Inserção manual de item

Via console → Explore items → Create item. Preencher chaves + atributos extras (ex.: `name = "batata"`). Como é schemaless, **não precisa declarar colunas antecipadamente**.

## Introdução ao [[entities/aws-lambda|Lambda]]

- Modelo [[concepts/serverless|serverless]] — sem provisionar servidor.
- Runtimes: Node.js, Python, Java, Go etc.
- Funções independentes, acionadas por eventos.
- Ideal para microsserviços; suporta chamadas assíncronas entre funções.

### Formas de criar uma função

| Método | Uso |
|---|---|
| **Author from scratch** | Código direto no editor do console |
| **Blueprint** | Template pré-configurado |
| **Upload .zip** | Código compactado |
| **GitHub/repo** | Código hospedado externamente |

### Execution Role — ponto crítico

A função precisa de uma [[concepts/iam-role|IAM Role]] com permissões para acessar serviços (ex.: DynamoDB):

| Opção | Quando |
|---|---|
| Create new role with basic Lambda permissions | Função simples sem acesso a outros serviços |
| Use an existing role | Já existe role adequada |
| Create from AWS policy templates | Casos pré-definidos |

**Decisão da aula**: criar nova role básica e depois anexar a policy do DynamoDB.

## Boas práticas mencionadas

- ✅ Copiar o ARN dos recursos ao criar integrações
- ✅ Runtime do Lambda na versão mais atual disponível (ex.: Node.js 20.x)
- ✅ **Query > Scan** em produção
- ✅ Todos os serviços na mesma região AWS
- ✅ Configurar a execution role antes de testar

---

## Entidades e conceitos tocados

- Entidades: [[entities/amazon-dynamodb]] (upgrade de stub), [[entities/aws-lambda]]
- Conceitos: [[concepts/nosql]] (novo), [[concepts/serverless]] (novo), [[concepts/iam-role]], [[concepts/arn]]
- Tópicos: [[topics/aws-security]]
