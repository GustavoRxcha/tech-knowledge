---
title: "AWS IAM (Identity and Access Management)"
type: entity
tags: [aws, iam, segurança, identidade, controle-de-acesso]
created: 2026-05-18
updated: 2026-05-18
sources: 4
---

# AWS IAM — Identity and Access Management

Serviço da [[aws|AWS]] para gerenciar identidades e permissões de acesso com granularidade fina.

---

## Blocos principais

| Bloco | Função |
|---|---|
| **User** | Identidade de longa duração para uma pessoa ou aplicação |
| **Group** | Coleção de usuários compartilhando permissões — ver [[iam-group]] |
| **Role** | Identidade assumível (ainda não coberta nas fontes atuais) |
| **Policy** | Documento JSON que concede ou nega ações sobre recursos — ver [[iam-policy]] |

## Caminhos para anexar permissões

Há três formas de conceder permissões a um usuário IAM:

1. **Filiação a grupo** (preferido) — ver [[iam-group]]. Anexa-se a policy ao grupo, e os membros herdam.
2. **Clonagem de permissões** — copiar de um usuário existente.
3. **Anexação direta** — anexar uma policy (managed ou [[inline-policy|inline]]) diretamente ao usuário. Aceitável como exceção, evitar como padrão.

> Boa prática (consolidada em [[aws-course-04-iam-groups]]): permissões devem vir do **grupo**, não do usuário. Depois de mover um usuário para um grupo, remova a inline policy anterior.

## Tipos de credencial

- **Console**: username + senha (login web).
- **Programática**: [[access-keys|Access Key ID + Secret Access Key]] para CLI/SDK/API.

Um usuário pode ter uma, ambas ou nenhuma.

## Notas operacionais

- O CSV de criação do usuário contém o link de login do console (já preenche o ID da conta), o username e a senha inicial. A AWS força a troca de senha no primeiro acesso.
- A **Secret Access Key é exibida apenas uma vez**; se perdida, regenerar o par.
- Para gerenciar outros usuários é necessário ter permissões de admin no IAM no principal operador.
- Tentar uma ação sem permissão retorna: `You are not authorized to perform this operation.`

## Tipos de policy anexáveis via IAM

- **Gerenciadas pela AWS** (ex.: `AdministratorAccess`, `AWSLambdaFullAccess`) — preferidas para casos de uso padrão.
- **Gerenciadas pelo cliente** (reutilizáveis, da conta).
- **[[inline-policy|Inline]]** (vinculadas a uma única identidade) — para exceções.

Ver [[iam-policy]] para estrutura e exemplos.

## Fontes

- [[aws-course-01-mfa-iam-setup]]
- [[aws-course-02-iam-policies-tags-credentials]]
- [[aws-course-03-iam-user-login-inline-policy]]
- [[aws-course-04-iam-groups]]

## Relacionados

- [[iam-group]]
- [[principle-of-least-privilege]]
- [[mfa]]
- [[resource-tags]]
- [[arn]]
- [[aws-security]]
