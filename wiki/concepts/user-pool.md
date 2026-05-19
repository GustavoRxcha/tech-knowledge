---
title: "User Pool (Cognito)"
type: concept
tags: [aws, cognito, autenticação, identidade]
created: 2026-05-19
updated: 2026-05-19
sources: 1
---

# User Pool

Abstração central do [[entities/aws-cognito|AWS Cognito]]: um **diretório de usuários** da aplicação. Cada User Pool gerencia cadastro, login e atributos de um grupo de usuários finais.

---

## O que um User Pool gerencia

| Aspecto | Detalhe |
|---|---|
| **Atributos de cadastro** | E-mail, username, telefone, atributos customizados |
| **Políticas de senha** | Tamanho mínimo, caracteres especiais, maiúsculas/minúsculas |
| **MFA** | Suporte a TOTP ([[entities/google-authenticator]], outros) e SMS |
| **Claims** | Atributos que vão no [[concepts/jwt\|ID Token]] (e-mail, nome, grupos) |
| **Fluxos** | Sign-up, sign-in, troca/recuperação de senha, validação de e-mail/telefone |
| **Triggers Lambda** | Hooks customizados em eventos do pool (ex.: pós-confirmação) |
| **Grupos** | Segmentação interna de usuários por papel |
| **Federação** | Identidade externa (Google, Facebook, SAML, OIDC) |

## Fluxo de criação (alto nível)

1. Console → Cognito → **Create user pool**
2. Definir atributos de login (e-mail, username, telefone)
3. Políticas de senha
4. MFA (off / opcional / obrigatório)
5. Atributos requeridos no cadastro
6. Configurar app clients (cada aplicação que vai consumir o pool)
7. Domínio + Hosted UI (opcional)

## User Pool ≠ Identity Pool

> [!question] Distinção citada na fonte conceitualmente, ainda não detalhada na ingestão:
> - **User Pool** = diretório de usuários (autenticação + claims em JWT)
> - **Identity Pool** = serviço que troca um token federado por **credenciais AWS temporárias** (autorização para chamar serviços AWS direto)

## Fontes

- [[sources/aws-course-cognito-intro]]

## Relações

- [[entities/aws-cognito]]
- [[concepts/jwt]]
- [[concepts/mfa]]
- [[concepts/iam-role]]
