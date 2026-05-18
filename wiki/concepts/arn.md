---
title: "ARN — Amazon Resource Name"
type: concept
tags: [aws, arn, identificadores]
created: 2026-05-18
updated: 2026-05-18
sources: 1
---

# ARN — Amazon Resource Name

Identificador único de qualquer recurso na [[aws|AWS]]. Usado no campo `Resource` das [[iam-policy|IAM policies]] para escopar permissões.

---

## Formato

```
arn:aws:<serviço>:<região>:<conta>:<tipo-recurso>/<nome-recurso>
```

Alguns serviços omitem `região` e/ou `conta` quando o namespace é global.

## Exemplos

| Recurso | ARN |
|---|---|
| Bucket S3 | `arn:aws:s3:::meu-bucket` |
| Todos os objetos do bucket | `arn:aws:s3:::meu-bucket/*` |
| Instância EC2 | `arn:aws:ec2:us-east-1:123456789012:instance/i-abc123` |
| Usuário IAM | `arn:aws:iam::123456789012:user/alice` |

> [!note] Nomes de bucket S3 são globalmente únicos, então os segmentos de região e conta ficam vazios nos ARNs de S3.

## Padrões comuns

- **Wildcard de sufixo** `/*` — aplica-se a todos os objetos/sub-recursos dentro de um pai.
- **Wildcard de serviço** `arn:aws:s3:::*` — todo bucket S3 (perigoso fora de policies admin).

## Como obter um ARN

No console AWS, toda página de detalhe de recurso expõe seu ARN. A CLI normalmente retorna nas chamadas `describe-*`.

## Fontes

- [[aws-course-03-iam-user-login-inline-policy]]

## Relacionados

- [[iam-policy]]
- [[inline-policy]]
- [[amazon-s3]]
- [[aws-iam]]
