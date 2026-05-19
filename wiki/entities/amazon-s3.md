---
title: "Amazon S3 (Simple Storage Service)"
type: entity
tags: [aws, s3, storage, object-storage, segurança]
created: 2026-05-18
updated: 2026-05-18
sources: 3
---

# Amazon S3 — Simple Storage Service

Serviço de armazenamento de objetos da [[entities/aws|AWS]]. Arquivos (objetos) são armazenados em **buckets** e acessíveis via API, console ou SDK. Um módulo dedicado é esperado mais adiante no curso.

---

## Conceitos básicos

- Objetos são organizados em **buckets** (namespace global — nome único em toda a AWS)
- Cada objeto tem URL de acesso única
- ARN de bucket: `arn:aws:s3:::nome-do-bucket`
- ARN com wildcard para objetos: `arn:aws:s3:::nome-do-bucket/*`

---

## Ações IAM referenciadas

| Ação | Efeito |
|---|---|
| `s3:ListAllMyBuckets` | Lista todos os buckets da conta |
| `s3:ListBucket` | Lista objetos dentro de um bucket específico |
| `s3:GetObject` | Lê/baixa um objeto |
| `s3:PutObject` | Faz upload de um objeto |
| `s3:DeleteObject` | Exclui um objeto |
| `s3:PutObjectVersioning` | Gerencia versionamento (não configurado no curso) |

---

## Acesso via roles

Serviços como [[entities/aws-lambda|Lambda]] acessam o S3 via [[concepts/iam-role|execution role]] — nunca com credenciais hardcodadas no código.

---

## Segurança: Block Public Access

> ⚠️ Buckets sem **Block Public Access** ficam expostos publicamente na internet.

- Habilitar por padrão em qualquer bucket não destinado a acesso público
- Para servir conteúdo público, preferir **CloudFront + Origin Access Control** (bucket permanece privado)
- Ver [[concepts/s3-block-public-access]]

---

## Lacunas

- Sem cobertura ainda de: versionamento, criptografia, lifecycle rules, storage classes, bucket policies, ACLs, presigned URLs, hospedagem estática, CloudFront, Glacier.

> [!question] Revisitar quando o módulo dedicado de S3 for ingerido (próximo módulo do curso).

---

## Fontes

- [[sources/aws-course-03-iam-user-login-inline-policy]]
- [[sources/aws-course-05-iam-roles-custom-policies-lambda]]
- [[sources/aws-course-06-iam-permissions-validation-s3]]

---

## Relações

- [[concepts/iam-policy]] — policies que controlam acesso ao S3
- [[concepts/arn]] — identifica buckets e objetos
- [[concepts/s3-block-public-access]] — configuração de segurança essencial
- [[concepts/inline-policy]] — primeira forma de acesso ao S3 vista no curso
- [[concepts/customer-managed-policy]] — policy-s3-developers criada nas aulas 5–6
- [[entities/aws-lambda]] — serviço que acessa S3 via role
