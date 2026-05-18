---
title: "Multi-Factor Authentication (MFA)"
type: concept
tags: [segurança, autenticação, mfa, totp]
created: 2026-05-18
updated: 2026-05-18
sources: 1
---

# Multi-Factor Authentication (MFA)

Autenticação que exige **dois ou mais** fatores independentes — algo que você sabe (senha), algo que você tem (dispositivo/token), ou algo que você é (biometria).

---

## No contexto AWS

- Fortemente recomendado no usuário root da [[aws|AWS]] imediatamente após criar a conta.
- Uma vez ativado, todo login passa a exigir um código TOTP além da senha.
- O setup usa um **dispositivo virtual de MFA** (app autenticador, como o [[google-authenticator]]).
- Fluxo de pareamento: escanear QR Code → inserir dois códigos sequenciais → dispositivo fica vinculado.

## TOTP em resumo

- Códigos têm vida curta (normalmente 30s).
- O QR Code codifica um segredo compartilhado; cliente e servidor derivam o mesmo código baseado no tempo a partir desse segredo.
- Qualquer app TOTP compatível funciona — o [[google-authenticator]] é só o mais comum.

## Fontes

- [[aws-course-01-mfa-iam-setup]]

## Relacionados

- [[aws-iam]]
- [[aws-security]]
- [[principle-of-least-privilege]]
