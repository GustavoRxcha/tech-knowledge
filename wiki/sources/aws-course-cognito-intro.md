---
title: "Curso AWS — Introdução ao Cognito"
type: source
tags: [aws, cognito, autenticação, jwt, curso]
created: 2026-05-19
updated: 2026-05-19
sources: 1
---

# Curso AWS — Introdução ao Cognito

Arquivo fonte: `raw/aula-cognito-introducao.md` (PT-BR)

Aula conceitual sobre o **[[entities/aws-cognito|AWS Cognito]]**, serviço gerenciado de identidade e autenticação. Não é implementado nesta aula — é apresentado para contextualizar a arquitetura do curso (DynamoDB + Lambda + API Gateway + Cognito + IAM).

---

## Pontos-chave

- [[entities/aws-cognito|Cognito]] cuida do fluxo completo de autenticação de usuários finais: sign-up, sign-in, recuperação de senha, MFA, login social.
- Conceito central: **[[concepts/user-pool|User Pool]]** — grupo de usuários da aplicação com atributos, políticas de senha e MFA.
- Após login, retorna 3 tokens [[concepts/jwt|JWT]]: **ID Token** (claims), **Access Token** (autorização), **Refresh Token** (renovação).
- Integra com [[entities/aws-iam|IAM]]: usuários autenticados pelo Cognito podem assumir [[concepts/iam-role|roles IAM]] para acessar recursos.
- **Hosted UI**: interface de login pronta, hospedada pela AWS.
- ⚠️ **Todos os serviços devem estar na mesma região AWS** — misturar regiões exige config multi-região adicional.

## Cognito vs IAM (quando usar cada um)

| Cenário | Solução |
|---|---|
| Cadastro/login de usuários finais da app | ✅ [[entities/aws-cognito\|Cognito]] |
| API protegida por autenticação de usuário | ✅ [[entities/aws-cognito\|Cognito]] |
| Acesso entre serviços AWS | ✅ [[concepts/iam-role\|IAM Roles]] |
| Acesso de devs/admins ao console AWS | ✅ [[entities/aws-iam\|IAM Users]] |

> Cognito ≠ IAM. Cognito é para **end-users da aplicação**. IAM é para **identidades operacionais da AWS**.

## Arquitetura do curso (referenciada)

| Serviço | Função |
|---|---|
| [[entities/amazon-dynamodb\|DynamoDB]] | NoSQL para os dados |
| [[entities/aws-lambda\|Lambda]] | Lógica de negócio |
| [[entities/amazon-api-gateway\|API Gateway]] | Rotas HTTP → Lambda |
| [[entities/aws-cognito\|Cognito]] | Autenticação dos usuários |
| [[entities/aws-iam\|IAM]] | Permissões entre serviços |

## Funcionalidades cobertas (visão geral)

- Sign-up / sign-in / recuperação / validação de e-mail e telefone
- MFA (compatível com [[entities/google-authenticator]] e outros TOTP)
- Federação: login social (Google, Facebook, Apple), SAML, OIDC
- Hosted UI customizável (logo, cores)
- **Triggers Lambda** em eventos do Cognito (ex.: pós-confirmação) — permite hook customizado no fluxo
- Atributos customizados além dos padrão
- Grupos dentro do User Pool para segmentação interna

---

## Entidades e conceitos tocados

- Entidades: [[entities/aws-cognito]] (novo), [[entities/aws-iam]], [[entities/aws-lambda]]
- Conceitos: [[concepts/user-pool]] (novo), [[concepts/jwt]] (novo), [[concepts/iam-role]], [[concepts/mfa]]
- Tópicos: [[topics/aws-security]]
