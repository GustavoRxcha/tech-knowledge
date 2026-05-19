---
title: "AWS Cognito"
type: entity
tags: [aws, cognito, autenticação, identidade]
created: 2026-05-19
updated: 2026-05-19
sources: 1
---

# AWS Cognito

Serviço gerenciado da [[entities/aws|AWS]] para **identidade e autenticação de usuários finais** de uma aplicação. Cuida do fluxo completo de sign-up, sign-in, recuperação, MFA, login social e geração de tokens.

---

## Quando usar (vs IAM)

| Cenário | Solução |
|---|---|
| Cadastro/login de **usuários finais** da app | ✅ Cognito |
| API protegida por autenticação de usuário | ✅ Cognito |
| Acesso entre **serviços AWS** | ❌ Use [[concepts/iam-role\|IAM Roles]] |
| Acesso de **devs/admins** ao console AWS | ❌ Use [[entities/aws-iam\|IAM Users]] |

> Regra: Cognito é para usuários da aplicação. IAM é para identidades operacionais da AWS. Os dois coexistem.

## Conceito central: [[concepts/user-pool|User Pool]]

Um User Pool agrupa os usuários da aplicação e gerencia:

- Atributos de cadastro (e-mail, username, telefone, custom)
- Políticas de senha (tamanho mínimo, caracteres exigidos)
- [[concepts/mfa|MFA]] (compatível com [[entities/google-authenticator|Google Authenticator]] e outros TOTP)
- Claims que vão no token [[concepts/jwt|JWT]]
- Fluxos: signup, login, troca de senha, validação

## Tokens emitidos

Após login bem-sucedido, retorna três [[concepts/jwt|JWTs]]:

| Token | Uso |
|---|---|
| **ID Token** | Carrega claims do usuário (e-mail, nome, grupos) |
| **Access Token** | Autoriza requisições a recursos protegidos |
| **Refresh Token** | Renova os outros sem novo login |

Todos têm TTL configurável.

## Integração com IAM

```
Usuário → Cognito (auth) → JWT → assume Role IAM → acesso ao serviço AWS
```

Usuários autenticados podem assumir [[concepts/iam-role|IAM Roles]] específicas, definindo o que podem fazer dentro da AWS (ex.: ler de S3 com o próprio identificador).

## Funcionalidades

- Sign-up / sign-in / recuperação de senha
- Validação de e-mail e telefone
- MFA (TOTP, SMS)
- Federação: login social (Google, Facebook, Apple), SAML, OIDC
- **Hosted UI** — interface de login pronta, customizável (logo, cores), com domínio próprio opcional
- **Triggers Lambda** em eventos do Cognito (pré-signup, pós-confirmação, pré-token, etc.) — permite hook customizado
- Grupos dentro do User Pool — segmentar usuários por papel

## Uso típico no API Gateway

[[entities/amazon-api-gateway|API Gateway]] aceita **authorizers** que validam JWTs emitidos pelo Cognito **antes** da requisição chegar à Lambda — autenticação na borda.

## Fontes

- [[sources/aws-course-cognito-intro]]

## Lacunas

- Setup detalhado do User Pool (atributos, fluxos OAuth) — não implementado nesta fase do curso.
- Identity Pool (diferente de User Pool — fornece credenciais AWS temporárias) — não coberto.
- Custom auth flows, device tracking, advanced security — pendentes.

> [!question] Revisitar quando o módulo de autenticação com Cognito for implementado de fato.

## Relações

- [[entities/aws]]
- [[entities/aws-iam]] — coexiste e integra
- [[entities/aws-lambda]] — Cognito pode disparar Lambdas em triggers
- [[concepts/user-pool]]
- [[concepts/jwt]]
- [[concepts/mfa]]
