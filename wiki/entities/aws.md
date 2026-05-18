---
title: "AWS (Amazon Web Services)"
type: entity
tags: [aws, cloud, infraestrutura]
created: 2026-05-18
updated: 2026-05-18
sources: 4
---

# AWS — Amazon Web Services

A plataforma de nuvem da Amazon. O wiki atualmente cobre AWS principalmente através de um curso sobre IAM e segurança básica de conta.

---

## O que sabemos até agora

- A AWS abrange cerca de **300 serviços** (referência à cobertura da policy `AdministratorAccess`).
- Identidade e acesso são tratados pelo [[aws-iam]].
- Armazenamento de objetos é feito pelo [[amazon-s3]].
- Computação serverless é feita pelo [[aws-lambda]].
- Computação em VM é feita pelo [[amazon-ec2]].
- NoSQL gerenciado é o [[amazon-dynamodb]].
- Todo recurso tem um [[arn]] globalmente único.
- Recursos podem ser classificados com [[resource-tags|tags]].

## Baseline de segurança da conta

- O **usuário root** tem acesso irrestrito — proteger fortemente.
- Ativar [[mfa]] no root imediatamente; desativar a access key do root.
- Operar o dia a dia com usuários [[aws-iam|IAM]] organizados em [[iam-group|grupos]], aplicando [[principle-of-least-privilege|menor privilégio]].

## Serviços cobertos no wiki

| Serviço | Status |
|---|---|
| [[aws-iam]] | 🟢 base cobrindo users, groups, policies, inline policies |
| [[amazon-s3]] | 🟡 só introdução conceitual + duas actions de IAM |
| [[aws-lambda]] | 🔴 stub (mencionado, módulo dedicado pendente) |
| [[amazon-ec2]] | 🔴 stub (mencionado como acesso-negado) |
| [[amazon-dynamodb]] | 🔴 stub (menção rápida) |

## Fontes que referenciam AWS

- [[aws-course-01-mfa-iam-setup]]
- [[aws-course-02-iam-policies-tags-credentials]]
- [[aws-course-03-iam-user-login-inline-policy]]
- [[aws-course-04-iam-groups]]

## Tópicos relacionados

- [[aws-security]]
