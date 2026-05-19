---
title: "AWS IAM (Identity and Access Management)"
type: entity
tags: [aws, iam, segurança, identidade, controle-de-acesso]
created: 2026-05-18
updated: 2026-05-18
sources: 6
---

# AWS IAM — Identity and Access Management

Serviço da [[aws|AWS]] para gerenciar identidades e permissões de acesso com granularidade fina.

---

## Blocos principais

| Bloco | Função |
|---|---|
| **User** | Identidade de longa duração para uma pessoa ou aplicação |
| **Group** | Coleção de usuários compartilhando permissões — ver [[iam-group]] |
| **Role** | Identidade assumível temporariamente por serviços, contas externas ou identidades federadas — ver [[concepts/iam-role]] |
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

## Tipos de policy

| Tipo | Criada por | Reutilizável | Quando usar |
|---|---|---|---|
| Managed (AWS) | AWS | Sim | Casos de uso padrão |
| [[concepts/customer-managed-policy\|Customer-managed]] | Você | Sim | Permissões específicas do negócio |
| [[concepts/inline-policy\|Inline]] | Você | Não (1:1) | Exceções pontuais |

## Encerramento do módulo IAM (aula 06)

Boas práticas consolidadas:
- MFA no root desde o início
- Nunca usar root para operações diárias
- Usuários em grupos com políticas bem definidas
- [[concepts/iam-role|Roles]] para comunicação entre serviços (nunca hardcodar credenciais)
- [[concepts/resource-tags|Tags]] para organizar recursos
- Download do CSV de credenciais imediatamente após criar usuários

## Fontes

- [[sources/aws-course-01-mfa-iam-setup]]
- [[sources/aws-course-02-iam-policies-tags-credentials]]
- [[sources/aws-course-03-iam-user-login-inline-policy]]
- [[sources/aws-course-04-iam-groups]]
- [[sources/aws-course-05-iam-roles-custom-policies-lambda]]
- [[sources/aws-course-06-iam-permissions-validation-s3]]

## Relações

- [[concepts/iam-group]]
- [[concepts/iam-role]]
- [[concepts/iam-policy]]
- [[concepts/customer-managed-policy]]
- [[concepts/inline-policy]]
- [[concepts/principle-of-least-privilege]]
- [[concepts/mfa]]
- [[concepts/resource-tags]]
- [[concepts/arn]]
- [[topics/aws-security]]
