---
title: "Inline Policy"
type: concept
tags: [aws, iam, policy, controle-de-acesso]
created: 2026-05-18
updated: 2026-05-18
sources: 2
---

# Inline Policy

Uma [[iam-policy]] **embutida diretamente** em uma única identidade do [[aws-iam|IAM]] (user, group ou role). Não tem existência independente — quando a identidade é deletada, a policy vai junto.

---

## Quando usar vs managed policy

| Pergunta | Use inline | Use managed |
|---|---|---|
| A permissão é única deste usuário? | ✅ | |
| Vai ser reaproveitada entre identidades? | | ✅ |
| Quero ciclo de vida 1:1 com a identidade? | ✅ | |
| Quero versionamento centralizado de policy? | | ✅ |
| É um caso de uso padrão (já existe managed)? | | ✅ |

Inline policies servem para permissões **excepcionais e específicas de uma identidade**. Para tudo padrão, prefira managed policies anexadas a um [[iam-group|grupo]].

## Exemplo prático (de [[aws-course-03-iam-user-login-inline-policy]])

Conceder a um único usuário a capacidade de put e get em um bucket S3 específico:

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": ["s3:PutObject", "s3:GetObject"],
      "Resource": "arn:aws:s3:::meu-bucket/*"
    }
  ]
}
```

Criada via: IAM → Users → usuário → Permissions → Add permissions → **Create inline policy**.

## Anti-padrão: deixar inline policy depois de mover para grupo

Em [[aws-course-04-iam-groups]], quando o usuário admin foi colocado no grupo `admins` (com `AdministratorAccess`), a inline policy anterior dele **foi removida**. Manter as duas fontes ativas causa inconsistência futura — a permissão deve vir do grupo.

**Regra prática**: ao migrar um usuário de inline → grupo, remova a inline policy depois de confirmar que o grupo já entrega a permissão equivalente.

## Fontes

- [[aws-course-03-iam-user-login-inline-policy]]
- [[aws-course-04-iam-groups]]

## Relacionados

- [[iam-policy]]
- [[iam-group]]
- [[arn]]
- [[amazon-s3]]
