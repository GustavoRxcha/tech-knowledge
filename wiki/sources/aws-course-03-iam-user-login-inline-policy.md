---
title: "Curso AWS 03 — Login com Usuário IAM e Inline Policies para S3"
type: source
tags: [aws, iam, s3, inline-policy, arn, curso]
created: 2026-05-18
updated: 2026-05-18
sources: 1
---

# Curso AWS 03 — Login com Usuário IAM e Inline Policies para S3

Arquivo fonte: `raw/aula-03-login-usuario-iam-inline-policy-s3.md` (PT-BR)

Terceira aula do curso. Demonstra o login com o novo usuário IAM e cria uma [[inline-policy]] anexada diretamente a ele, usando o [[amazon-s3]] como recurso de exemplo. Apresenta [[arn]] (Amazon Resource Name) como identificador universal de recursos AWS.

---

## Pontos-chave

- O CSV gerado na criação do usuário contém um **link de login do console** que já preenche o número da conta.
- No primeiro login, a AWS força a **redefinição de senha**.
- Uma [[inline-policy]] é uma policy **criada manualmente e anexada a um único usuário** — não reutilizável, ao contrário das managed policies.
- Todo recurso AWS tem um [[arn]]; ARNs são usados no campo `Resource` das policies.
- A aula concede `s3:PutObject` e `s3:GetObject` em um bucket específico como exemplo prático.
- Para gerenciar permissões de outros usuários, o operador precisa ter permissões de admin no IAM.

## Managed vs inline policy

| Aspecto | Managed Policy | Inline Policy |
|---|---|---|
| Criada por | AWS ou cliente | Admin da conta |
| Reutilizável entre usuários | Sim | Não (vinculada a um único) |
| Ciclo de vida | Independente | Atrelado ao usuário |

Ver [[iam-policy]] e [[inline-policy]].

## Formato do ARN

```
arn:aws:<serviço>:<região>:<conta>:<tipo-recurso>/<nome-recurso>
```

Exemplos para S3:

```
arn:aws:s3:::meu-bucket          # o bucket em si
arn:aws:s3:::meu-bucket/*        # todos os objetos dentro do bucket
```

> Região e conta ficam vazias para buckets S3 porque o namespace de buckets é global.

## Exemplo prático — inline policy para S3

1. IAM → Users → escolher o usuário → Permissions → **Add permissions → Create inline policy**.
2. Serviço: **S3**.
3. Ações: `PutObject`, `GetObject`.
4. Resource ARN: `arn:aws:s3:::<bucket>/*`.
5. Review, nomear a policy (ex.: `policy-s3-curso`), criar.

## Progresso do curso (até a aula 3)

| Etapa | Status |
|---|---|
| MFA no root | ✅ (aula 01) |
| Usuário IAM criado | ✅ (aula 01) |
| Login com novo usuário IAM | ✅ (aula 03) |
| Inline policy para S3 | ✅ (aula 03) |
| Grupos IAM | 🔜 próxima aula |

---

## Entidades e conceitos tocados

- Entidades: [[aws]], [[aws-iam]], [[amazon-s3]]
- Conceitos: [[iam-policy]], [[inline-policy]], [[arn]], [[access-keys]]
- Tópicos: [[aws-security]]
