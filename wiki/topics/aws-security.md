---
title: "Segurança AWS"
type: topic
tags: [aws, segurança, iam, mfa]
created: 2026-05-18
updated: 2026-05-18
sources: 4
---

# Segurança AWS

Página de tópico agrupando tudo o que o wiki sabe sobre proteger uma conta [[aws|AWS]]. Atualmente focada em bootstrap de conta e gerenciamento de acesso via IAM.

---

## Checklist baseline (das fontes atuais)

- [x] Ativar [[mfa]] no usuário root imediatamente após criar a conta.
- [x] **Desativar a access key do root.**
- [x] Parar de usar root para o dia a dia — operar via usuários [[aws-iam|IAM]].
- [x] Aplicar o [[principle-of-least-privilege]] a toda identidade.
- [x] Organizar permissões em [[iam-group|grupos]] por papel; anexar policies ao grupo, não ao usuário.
- [x] Ao mover um usuário para um grupo, **remover [[inline-policy|inline policies]] redundantes** do usuário.
- [x] Preferir [[iam-policy|managed policies]] da AWS para casos padrão; criar inline ou customer-managed apenas em exceções.
- [x] Reservar `AdministratorAccess` para administradores reais.
- [x] Baixar o CSV de credenciais na criação do usuário — a Secret Access Key é mostrada uma única vez.
- [x] Taguear recursos desde o dia 1 para governança — ver [[resource-tags]].
- [x] Validar permissões após cada configuração (login de teste para confirmar acessos permitidos e negados).

## Sub-áreas

### Identidade & acesso
- [[aws-iam]]
- [[iam-group]]
- [[iam-policy]] / [[inline-policy]]
- [[access-keys]]
- [[principle-of-least-privilege]]

### Autenticação
- [[mfa]]
- [[google-authenticator]]

### Identificação & governança de recursos
- [[arn]]
- [[resource-tags]]

## Lacunas

- **IAM Roles** — próxima aula do curso; nada coberto ainda.
- **Policies personalizadas** (customer-managed) — próxima aula.
- Sem cobertura de SCPs (Service Control Policies), AWS Organizations, KMS, Secrets Manager, GuardDuty, CloudTrail, Security Hub, IAM Access Analyzer.
- Resource-based policies (bucket policies do [[amazon-s3]], etc.) — não cobertas.
- Tag-based conditions em policies (`aws:ResourceTag`) — não cobertas.

## Fontes

- [[aws-course-01-mfa-iam-setup]]
- [[aws-course-02-iam-policies-tags-credentials]]
- [[aws-course-03-iam-user-login-inline-policy]]
- [[aws-course-04-iam-groups]]
