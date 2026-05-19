---
title: "AWS Lambda"
type: entity
tags: [aws, lambda, serverless, computação, roles]
created: 2026-05-18
updated: 2026-05-18
sources: 2
---

# AWS Lambda

Serviço **serverless** de computação da [[entities/aws|AWS]]. Permite executar código (funções) sem provisionar ou gerenciar servidores — FaaS (Function-as-a-Service).

---

## Características principais

- Executa código em resposta a eventos (triggers)
- Cobra apenas pelo tempo de execução (sem servidor ocioso)
- Suporta múltiplos runtimes: Node.js, Python, Go, Java, etc.
- Limite de execução: até 15 minutos por invocação

---

## IAM e permissões

Para que uma função Lambda acesse outros serviços AWS, ela precisa de uma **execution role** — uma [[concepts/iam-role|IAM Role]] com as policies necessárias.

### Criando a execution role

1. **IAM → Roles → Create role → AWS Service → Lambda**
2. Anexar as policies adequadas (ex: `policy-s3-developers`)
3. Na função Lambda: **Execution role → Use an existing role**

### Sem credenciais hardcodadas

> Lambda **nunca** deve ter credenciais hardcodadas no código. A execution role provê credenciais temporárias automaticamente via AWS STS.

---

## Exemplo prático (aula 05)

Função que lista buckets S3:

```javascript
const { S3Client, ListBucketsCommand } = require("@aws-sdk/client-s3");

exports.handler = async () => {
  const client = new S3Client({});
  const response = await client.send(new ListBucketsCommand({}));
  return response.Buckets;
};
```

| Cenário | Resultado |
|---|---|
| Sem execution role / sem permissão S3 | ❌ Acesso negado |
| Com role e policy S3 correta | ✅ Buckets listados |

---

## Managed policies referenciadas

| Policy | Efeito |
|---|---|
| `AWSLambdaFullAccess` | Acesso total ao serviço Lambda (para usuários IAM) |
| `policy-s3-developers` | Customer-managed policy com acesso ao S3 (para execution role) |

---

## Lacunas

- Sem cobertura ainda de: triggers/event sources, layers, limites detalhados, cold starts, VPC config, provisioned concurrency, pricing model.

> [!question] Revisitar quando o módulo dedicado de Lambda for ingerido.

---

## Fontes

- [[sources/aws-course-04-iam-groups]]
- [[sources/aws-course-05-iam-roles-custom-policies-lambda]]

---

## Relações

- [[entities/aws]] — plataforma
- [[concepts/iam-role]] — execution role que Lambda assume
- [[entities/amazon-s3]] — serviço acessado via role neste exemplo
- [[concepts/iam-policy]] — policies anexadas à role
