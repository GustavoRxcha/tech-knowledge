---
title: "Index"
type: overview
updated: 2026-05-18
---

# Index

Catálogo principal de todas as páginas do wiki. O LLM lê isto primeiro para navegar.

---

## Sources
- [[sources/aws-course-01-mfa-iam-setup]] — Setup inicial: MFA no root e criação do primeiro usuário IAM (2026-05-18)
- [[sources/aws-course-02-iam-policies-tags-credentials]] — Estrutura de policies, tags e manuseio de credenciais IAM (2026-05-18)
- [[sources/aws-course-03-iam-user-login-inline-policy]] — Login com usuário IAM e criação de inline policy para S3 (2026-05-18)
- [[sources/aws-course-04-iam-groups]] — Grupos IAM, atribuição de permissões por grupo e validação prática de menor privilégio (2026-05-18)
- [[sources/aws-course-05-iam-roles-custom-policies-lambda]] — IAM Roles, policies personalizadas e Lambda acessando S3 (2026-05-18)
- [[sources/aws-course-06-iam-permissions-validation-s3]] — Validação prática de permissões no S3 e encerramento do módulo IAM (2026-05-18)

## Entities
- [[entities/aws]] — A plataforma de nuvem da Amazon
- [[entities/aws-iam]] — Serviço de identidade e acesso da AWS
- [[entities/amazon-s3]] — Serviço de armazenamento de objetos da AWS
- [[entities/aws-lambda]] — Serviço serverless de computação; usa execution roles para acessar outros serviços
- [[entities/amazon-ec2]] — Serviço de máquinas virtuais (stub)
- [[entities/amazon-dynamodb]] — Banco NoSQL gerenciado (stub)
- [[entities/google-authenticator]] — App TOTP usado para MFA

## Concepts
- [[concepts/mfa]] — Multi-Factor Authentication (TOTP, dispositivo virtual)
- [[concepts/iam-policy]] — Estrutura JSON das policies IAM
- [[concepts/inline-policy]] — Policy embutida em uma única identidade IAM
- [[concepts/customer-managed-policy]] — Policy criada pelo usuário; reutilizável, mais específica que as managed da AWS
- [[concepts/iam-group]] — Coleção de usuários IAM compartilhando permissões
- [[concepts/iam-role]] — Identidade sem dono fixo, assumida temporariamente por serviços ou usuários
- [[concepts/access-keys]] — Credenciais de longa duração para acesso programático
- [[concepts/principle-of-least-privilege]] — Princípio do menor privilégio
- [[concepts/arn]] — Amazon Resource Name, identificador universal de recursos
- [[concepts/resource-tags]] — Tags chave/valor para classificação e custo
- [[concepts/s3-block-public-access]] — Configuração que impede exposição pública acidental de buckets S3

## Topics
- [[topics/aws-security]] — Módulo IAM completo: baseline de segurança, roles, S3

## Synthesis
*(ainda vazio)*
