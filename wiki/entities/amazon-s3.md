---
title: "Amazon S3 (Simple Storage Service)"
type: entity
tags: [aws, s3, storage, object-storage]
created: 2026-05-18
updated: 2026-05-18
sources: 1
---

# Amazon S3 — Simple Storage Service

Serviço de armazenamento de objetos da [[aws|AWS]]. Atualmente apresentado apenas em nível superficial — um módulo dedicado é esperado mais adiante no curso.

---

## O que sabemos até agora

- Armazena arquivos (objetos) acessíveis pela rede — analogia: Dropbox a nível de API.
- Objetos são organizados em **buckets** (containers parecidos com pastas).
- Cada objeto tem uma URL de acesso única.
- Nomes de bucket vivem em um **namespace global** — o [[arn]] de um bucket S3 omite região e conta: `arn:aws:s3:::meu-bucket`.
- ARN com wildcard para todos os objetos do bucket: `arn:aws:s3:::meu-bucket/*`.

## Ações IAM comuns referenciadas

| Ação | Efeito |
|---|---|
| `s3:PutObject` | Subir um objeto para o bucket |
| `s3:GetObject` | Ler/baixar um objeto |

Estas duas ações foram concedidas via [[inline-policy]] em [[aws-course-03-iam-user-login-inline-policy]].

## Fontes

- [[aws-course-03-iam-user-login-inline-policy]]

## Lacunas

- Sem cobertura ainda de: versionamento, criptografia, lifecycle rules, storage classes, bucket policies, ACLs, presigned URLs, hospedagem estática.

> [!question] Revisitar quando o módulo dedicado de S3 for ingerido.
