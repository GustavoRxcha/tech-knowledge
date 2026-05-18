---
title: "Princípio do Menor Privilégio"
type: concept
tags: [segurança, controle-de-acesso, boas-práticas]
created: 2026-05-18
updated: 2026-05-18
sources: 3
---

# Princípio do Menor Privilégio (Principle of Least Privilege)

Conceder a cada identidade (usuário, serviço, processo) **apenas as permissões necessárias para fazer o trabalho — e nada além disso**. Princípio fundamental no design de controle de acesso.

---

## Por quê

- Limita o raio de impacto de uma credencial comprometida.
- Reduz danos acidentais por erro do operador.
- Torna a auditoria tratável — menos permissões = revisão mais clara.

## Como aparece nas fontes [[aws|AWS]]

- Evitar usar o usuário root para trabalho diário — ver [[aws-security]].
- Desativar a access key do root.
- Preferir [[iam-policy|policies]] estreitas (ações específicas, [[arn|ARNs]] específicos) em vez de algo como `AdministratorAccess`.
- Organizar permissões em [[iam-group|grupos]] por papel — um grupo carrega só o que aquele papel precisa.
- Usar [[inline-policy|inline policies]] para exceções pontuais e específicas de uma identidade.
- Reservar `AdministratorAccess` apenas para administradores reais.

## Validação prática (de [[aws-course-04-iam-groups]])

O curso testa o princípio ao logar com um usuário do grupo `developers` (apenas `AWSLambdaFullAccess`):

| Ação | Resultado |
|---|---|
| Acessar [[aws-lambda|Lambda]] | ✅ |
| Acessar [[amazon-ec2|EC2]] | ❌ `You are not authorized to perform this operation.` |
| Acessar [[aws-iam|IAM]] para criar usuários | ❌ mesma mensagem |

A interface do serviço sequer carrega completamente quando a identidade não tem nenhuma permissão associada — o feedback de negação é imediato e visível.

## Fontes

- [[aws-course-01-mfa-iam-setup]]
- [[aws-course-02-iam-policies-tags-credentials]]
- [[aws-course-04-iam-groups]]

## Relacionados

- [[aws-iam]]
- [[iam-group]]
- [[iam-policy]]
- [[mfa]]
- [[aws-security]]
