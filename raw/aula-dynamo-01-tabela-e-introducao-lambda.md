# DynamoDB: Criação de Tabela e Introdução ao AWS Lambda

## Visão Geral

Esta aula inicia a parte prática do curso, criando uma **tabela no DynamoDB** (banco de dados NoSQL da AWS) e introduzindo a criação de uma **função Lambda** que irá interagir com ela. A arquitetura sendo construída envolve DynamoDB + Lambda + API Gateway.

---

## 1. Amazon DynamoDB — Visão Geral

O **DynamoDB** é o serviço de banco de dados **NoSQL** (não relacional) gerenciado da AWS. Suas principais características:

- Totalmente **serverless** — sem necessidade de gerenciar servidores
- Alta disponibilidade e escalabilidade automática
- Dados organizados em **tabelas**, **itens** (linhas) e **atributos** (colunas)
- Suporta tipos de dados: `String`, `Number`, `Binary`, entre outros
- Dois tipos principais de consulta: **Query** e **Scan**

---

## 2. Criando uma Tabela no DynamoDB

### Passo a passo no console

1. Acessar o console AWS → pesquisar **DynamoDB**
2. No painel, acessar **Tables** → **Create table**
3. Definir o **nome da tabela** (ex: `products`)
4. Configurar as **chaves da tabela**

### Chaves do DynamoDB

| Chave | Nome técnico | Descrição |
|---|---|---|
| **Chave de partição** | Partition Key | Chave primária obrigatória — identifica unicamente cada item |
| **Chave de ordenação** | Sort Key | Chave secundária opcional — em conjunto com a Partition Key, forma um identificador composto |

> 📌 **Exemplo prático:** Em um catálogo de produtos, a Partition Key pode ser o `product_id` (ex: `prod-0001`) e a Sort Key pode ser o `title`. A combinação dos dois deve ser **única** em toda a tabela — nenhum item pode ter os mesmos valores nas duas chaves simultaneamente.

### Tipos de dados suportados nas chaves

- `String (S)`
- `Number (N)`
- `Binary (B)`

### Após a criação

A tabela leva alguns segundos para ficar disponível. No painel são exibidas:
- Lista de **itens** da tabela
- **Métricas de uso**
- Configurações de **alarmes** e **índices**

---

## 3. Inserindo Itens na Tabela

### Criando um item manualmente no console

1. Acessar a tabela → **Explore items** → **Create item**
2. Preencher os valores da Partition Key e Sort Key
3. Adicionar **atributos extras** (campos adicionais):
   - Ex: campo `name` do tipo `String` com valor `"batata"`
4. Clicar em **Save**

> 📌 No DynamoDB, diferentemente de bancos relacionais, **cada item pode ter atributos diferentes** — não é necessário definir todas as colunas com antecedência. Itens sem um determinado atributo simplesmente não o possuem.

---

## 4. Consultando Dados no DynamoDB

O DynamoDB oferece dois métodos de consulta:

### 4.1 Query (Consulta com filtro)

- Busca itens usando a **Partition Key** como filtro principal
- Pode combinar com a Sort Key para refinar
- **Recomendado** para uso em produção — eficiente e de baixo custo
- Retorna apenas os itens que correspondem ao filtro

```
Exemplo: buscar todos os itens com product_id = "prod-0001"
→ Retorna apenas esse item
```

### 4.2 Scan (Varredura completa)

- Percorre **todos os itens** da tabela e aplica filtros depois
- **Não recomendado para produção** — consome muita capacidade de leitura e é custoso
- Útil apenas para administração, debugging ou tabelas muito pequenas

> ⚠️ Em aplicações reais, sempre prefira **Query** ao **Scan**. O Scan em tabelas grandes pode gerar custos elevados e lentidão.

---

## 5. ARN do DynamoDB

Ao criar a tabela, um **ARN (Amazon Resource Name)** é gerado automaticamente:

```
arn:aws:dynamodb:<região>:<conta>:table/<nome-da-tabela>
```

> 📌 O ARN será necessário ao configurar as **permissões da role Lambda** para acessar essa tabela específica.

---

## 6. Introdução ao AWS Lambda

O **AWS Lambda** permite executar código (funções) sem provisionar ou gerenciar servidores — modelo **serverless**.

### Características

- Suporta múltiplos runtimes: **Node.js**, Python, Java, Go, etc.
- Cada função é independente e pode ser acionada por eventos
- Ideal para arquiteturas de **microsserviços** — várias funções pequenas que interagem entre si
- Suporta requisições **assíncronas** entre funções

### Formas de criar uma função Lambda

| Método | Descrição |
|---|---|
| **Do zero** | Código escrito diretamente no editor do console |
| **A partir de template** | Usar um blueprint pré-configurado da AWS |
| **Upload de arquivo .zip** | Enviar o código compactado para a função |
| **Via GitHub/repositório** | Código hospedado em repositório externo |

---

## 7. Criando uma Função Lambda

### Passo a passo

1. Acessar o console AWS → **Lambda** → **Create function**
2. Escolher o método de criação (ex: **Author from scratch**)
3. Definir o **nome da função** (ex: `getProducts`)
4. Selecionar o **runtime** (ex: `Node.js 20.x` — sempre usar a versão mais atual disponível)
5. Configurar a **execution role** (role de execução)

### Configuração da Execution Role

Este é um ponto crítico para quem está começando. A função Lambda precisa de uma **role IAM** com permissões para acessar os serviços que irá utilizar (neste caso, o DynamoDB).

Opções disponíveis:

| Opção | Quando usar |
|---|---|
| **Create a new role with basic Lambda permissions** | Para funções simples, sem acesso a outros serviços |
| **Use an existing role** | Quando já existe uma role com as permissões necessárias |
| **Create a new role from AWS policy templates** | Para casos específicos com templates pré-definidos |

> ✅ Para esta aula: criar uma **nova role** com permissões básicas de Lambda, e em seguida adicionar a política de acesso ao DynamoDB.

6. Clicar em **Create function**

---

## 8. Próximos Passos

Com a tabela DynamoDB criada e a função Lambda iniciada, os próximos passos do curso serão:

- Escrever o **código da função Lambda** para interagir com o DynamoDB (linguagem: Node.js)
- Configurar as **permissões de escrita** da role Lambda no DynamoDB
- Criar as **rotas no API Gateway** integradas à função Lambda

---

## Boas Práticas Mencionadas

- ✅ Sempre copiar o **ARN** dos recursos ao criar integrações
- ✅ Manter o **runtime da Lambda** sempre na versão mais atualizada disponível
- ✅ Usar **Query** no lugar de **Scan** em consultas DynamoDB em produção
- ✅ Garantir que todos os serviços estejam na **mesma região AWS**
- ✅ Configurar a **role de execução** corretamente antes de testar a função

---

*Aula 01 — Módulo DynamoDB + Lambda | Curso AWS*
