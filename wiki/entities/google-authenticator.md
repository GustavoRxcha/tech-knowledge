---
title: "Google Authenticator"
type: entity
tags: [segurança, mfa, totp, autenticador]
created: 2026-05-18
updated: 2026-05-18
sources: 1
---

# Google Authenticator

App móvel autenticador que implementa TOTP (one-time password baseado em tempo).

---

## O que sabemos até agora

- App mais comum para configurar [[mfa]] na AWS (segundo [[aws-course-01-mfa-iam-setup]]).
- Pareia com um serviço via QR Code; o serviço fica vinculado ao dispositivo.
- TOTP padrão — qualquer app autenticador compatível serve no lugar (Authy, 1Password etc.).
- O enrollment de MFA da AWS pede **dois códigos sequenciais** para confirmar o pareamento.

## Fontes

- [[aws-course-01-mfa-iam-setup]]

## Relacionados

- [[mfa]]
