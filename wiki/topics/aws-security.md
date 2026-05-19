---
title: "Segurança AWS"
type: topic
tags: [aws, segurança, iam, mfa, s3, roles]
created: 2026-05-18
updated: 2026-05-18
sources: 6
---

# Segurança AWS

Página de tópico agrupando tudo o que o wiki sabe sobre proteger uma conta [[entities/aws|AWS]]. Cobre o módulo completo de IAM (aulas 01–06): bootstrap de conta, gerenciamento de acesso, roles e segurança básica do S3.

---

## Checklist baseline (módulo IAM completo)

### Conta e root
- [x] Ativar [[concepts/mfa|MFA]] no usuário root imediatamente após criar a conta
- [x] Desativar a access key do root
- [x] Nunca usar root para operações do dia a dia

### Usuários e grupos
- [x] Criar usuários IAM individuais — nunca compartilhar credenciais
- [x] Organizar usuários em [[concepts/iam-group|grupos]] por papel; anexar policies ao grupo
- [x] Ao mover usuário para grupo, remover [[concepts/inline-policy|inline policies]] redundantes
- [x] Baixar CSV de credenciais imediatamente — Secret Access Key exibida uma única vez

### Policies e permissões
- [x] Aplicar sempre o [[concepts/principle-of-least-privilege|princípio do menor privilégio]]
- [x] Preferir managed policies da AWS; criar [[concepts/customer-managed-policy|customer-managed]] só quando necessário
- [x] [[concepts/inline-policy|Inline policies]] apenas para exceções únicas — nunca como padrão
- [x] Validar permissões após cada configuração (login de teste)
- [x] Reservar `AdministratorAccess` para administradores reais

### Roles e serviços
- [x] Usar [[concepts/iam-role|roles]] para comunicação entre serviços AWS — **nunca hardcodar credenciais**
- [x] Nomear roles de forma descritiva: `role-[serviço]-[função]`
- [x] Revisar policies das roles periodicamente

### Organização e governança
- [x] Taguear recursos desde o dia 1 — ver [[concepts/resource-tags]]

### S3
- [x] Habilitar [[concepts/s3-block-public-access|Block Public Access]] em todos os buckets por padrão
- [x] Acesso público deve ser decisão deliberada e documentada
- [x] Usar bucket policies + IAM policies para controle granular

---

## Sub-áreas

### Identidade & acesso
- [[entities/aws-iam]]
- [[concepts/iam-group]]
- [[concepts/iam-role]]
- [[concepts/iam-policy]] / [[concepts/inline-policy]] / [[concepts/customer-managed-policy]]
- [[concepts/access-keys]]
- [[concepts/principle-of-least-privilege]]

### Autenticação
- [[concepts/mfa]]
- [[entities/google-authenticator]]

### Identificação & governança de recursos
- [[concepts/arn]]
- [[concepts/resource-tags]]

### Segurança S3
- [[concepts/s3-block-public-access]]
- [[entities/amazon-s3]]

---

## Lacunas

- SCPs (Service Control Policies), AWS Organizations — sem cobertura
- KMS, Secrets Manager, GuardDuty, CloudTrail, Security Hub, IAM Access Analyzer — sem cobertura
- Resource-based policies (bucket policies do S3) — sem cobertura
- Tag-based conditions em policies (`aws:ResourceTag`) — sem cobertura
- Cross-account roles e identidade federada — citados, não detalhados

---

## Fontes

- [[sources/aws-course-01-mfa-iam-setup]]
- [[sources/aws-course-02-iam-policies-tags-credentials]]
- [[sources/aws-course-03-iam-user-login-inline-policy]]
- [[sources/aws-course-04-iam-groups]]
- [[sources/aws-course-05-iam-roles-custom-policies-lambda]]
- [[sources/aws-course-06-iam-permissions-validation-s3]]
