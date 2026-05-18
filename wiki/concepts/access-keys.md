---
title: "AWS Access Keys"
type: concept
tags: [aws, iam, credenciais, access-keys, segurança]
created: 2026-05-18
updated: 2026-05-18
sources: 2
---

# AWS Access Keys

Credenciais de longa duração para **acesso programático** à [[aws|AWS]] (CLI, SDKs, APIs). Uma access key é um par:

- **Access Key ID** — identificador público.
- **Secret Access Key** — a metade secreta; assina as requisições à API.

---

## Ciclo de vida

- Gerada quando um usuário do [[aws-iam|IAM]] é criado com acesso programático (ou depois, via IAM → Security credentials).
- A Secret Access Key é mostrada **exatamente uma vez** na criação. Baixe o CSV de credenciais antes de fechar a tela.
- Se perder: a key não é recuperável. Delete a existente e crie um novo par.
- Cada usuário pode ter até 2 pares ativos (para permitir rotação).

## Keys do root vs do usuário IAM

- A access key do **usuário root** deve ficar **desativada** como baseline de segurança (ver [[aws-security]]).
- Keys de usuário IAM devem seguir o [[principle-of-least-privilege]] — escopadas só ao que o usuário precisa.

## Conteúdo do CSV (no momento da criação do usuário)

| Coluna | Uso |
|---|---|
| Console login link | URL de login web (já preenche o ID da conta) |
| Username | Login do console |
| Password | Senha inicial (troca obrigatória no primeiro login) |
| Access Key ID | Identificador programático |
| Secret Access Key | Segredo programático |

## Fontes

- [[aws-course-01-mfa-iam-setup]]
- [[aws-course-02-iam-policies-tags-credentials]]

## Relacionados

- [[aws-iam]]
- [[mfa]]
- [[principle-of-least-privilege]]
