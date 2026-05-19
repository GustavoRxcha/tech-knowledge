---
title: "JWT — JSON Web Token"
type: concept
tags: [autenticação, autorização, tokens, segurança]
created: 2026-05-19
updated: 2026-05-19
sources: 1
---

# JWT — JSON Web Token

Padrão aberto ([RFC 7519](https://datatracker.ietf.org/doc/html/rfc7519)) para representar **claims** (afirmações sobre uma entidade) em um token compacto, autocontido e assinado. Largamente usado em autenticação e autorização entre serviços.

---

## Anatomia

Três partes Base64URL separadas por `.`:

```
<header>.<payload>.<signature>
```

| Parte | Conteúdo |
|---|---|
| **Header** | Tipo (`JWT`) e algoritmo de assinatura (ex.: `RS256`, `HS256`) |
| **Payload** | Claims — atributos sobre o sujeito (e-mail, expiração, grupos, etc.) |
| **Signature** | Assinatura HMAC ou RSA sobre header+payload com a chave do emissor |

## Claims comuns

| Claim | Significado |
|---|---|
| `iss` | Issuer — quem emitiu |
| `sub` | Subject — quem é o usuário |
| `aud` | Audience — para quem o token é válido |
| `exp` | Expira em (Unix timestamp) |
| `iat` | Issued at |
| `nbf` | Not before |

Mais claims customizadas dependem do emissor.

## Propriedades importantes

- **Autocontido**: o validador não precisa consultar um banco — basta verificar a assinatura.
- **Stateless**: server não guarda sessão (escala bem).
- **Imutável**: alterar o payload invalida a assinatura.
- ⚠️ **Não é criptografado por padrão** — qualquer um pode ler o payload. Para sigilo use JWE.
- ⚠️ Revogação é difícil — o token vale até expirar. Tokens curtos + refresh token mitigam isso.

## Uso típico no contexto AWS

Fluxo padrão com [[entities/aws-cognito|Cognito]] + [[entities/amazon-api-gateway|API Gateway]]:

```
Usuário → Cognito (login) → JWT (ID/Access/Refresh)
                                    ↓
              cliente HTTP → API Gateway (authorizer valida JWT)
                                    ↓
                              Lambda (já autenticado)
```

Cognito emite três JWTs após login:

| Token | Papel |
|---|---|
| **ID Token** | Identifica o usuário (claims: nome, e-mail, grupos) |
| **Access Token** | Autoriza ações em recursos protegidos |
| **Refresh Token** | Renova os outros sem novo login |

## Validação (o que o authorizer faz)

1. Decodificar header → identificar algoritmo e `kid` (key id)
2. Buscar a chave pública correspondente no JWKS endpoint do emissor
3. Verificar a assinatura
4. Checar `iss`, `aud`, `exp`, `nbf`

## Fontes

- [[sources/aws-course-cognito-intro]]
- [[sources/aws-course-apigateway-02-integration-postman]]

## Relações

- [[entities/aws-cognito]]
- [[entities/amazon-api-gateway]] — authorizers validam JWT
- [[concepts/user-pool]]
