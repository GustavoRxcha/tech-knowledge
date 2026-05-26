---
title: "Segurança AWS"
type: topic
tags: [aws, segurança, iam, mfa, s3, roles, cognito, kms, shield, waf, guardduty, inspector, clf-c02]
created: 2026-05-18
updated: 2026-05-26
sources: 12
---

# Segurança AWS

Página de tópico agrupando tudo o que o wiki sabe sobre proteger uma conta [[entities/aws|AWS]]. Cobre o módulo completo de IAM (aulas 01–06) e a camada de autenticação de usuário final via [[entities/aws-cognito|Cognito]] introduzida no módulo serverless.

---

## Checklist baseline (consolidado)

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
- [x] Validar permissões após cada configuração (login de teste, erros reais como `User is not authorized to perform: dynamodb:PutItem`)
- [x] Reservar `AdministratorAccess` para administradores reais

### Roles e serviços
- [x] Usar [[concepts/iam-role|roles]] para comunicação entre serviços AWS — **nunca hardcodar credenciais**
- [x] Cada Lambda tem uma execution role com as policies mínimas para o que faz
- [x] Nomear roles de forma descritiva: `role-[serviço]-[função]`
- [x] Revisar policies das roles periodicamente

### Organização e governança
- [x] Taguear recursos desde o dia 1 — ver [[concepts/resource-tags]]
- [x] Todos os serviços de uma solução na **mesma região**

### S3
- [x] Habilitar [[concepts/s3-block-public-access|Block Public Access]] em todos os buckets por padrão
- [x] Acesso público deve ser decisão deliberada e documentada
- [x] Usar bucket policies + IAM policies para controle granular

### Autenticação de usuários finais
- [x] Usar [[entities/aws-cognito|Cognito]] para auth de usuários da aplicação (não IAM)
- [x] Configurar MFA opcional ou obrigatório no User Pool conforme o perfil
- [x] No [[entities/amazon-api-gateway|API Gateway]], usar authorizer que valida [[concepts/jwt|JWT]] do Cognito **antes** de chegar à Lambda
- [x] Tokens de curta duração + refresh token

---

## Sub-áreas

### Identidade & acesso (operacional — IAM)
- [[entities/aws-iam]]
- [[concepts/iam-group]]
- [[concepts/iam-role]]
- [[concepts/iam-policy]] / [[concepts/inline-policy]] / [[concepts/customer-managed-policy]]
- [[concepts/access-keys]]
- [[concepts/principle-of-least-privilege]]

### Identidade de usuário final
- [[entities/aws-cognito]]
- [[concepts/user-pool]]
- [[concepts/jwt]]

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

### Modelo de Responsabilidade Compartilhada
- [[concepts/shared-responsibility-model]] — AWS cuida da infra (DA nuvem); cliente cuida dos dados e acesso (NA nuvem)

### Criptografia
- [[entities/aws-kms]] — gerencia chaves criptográficas; dados em repouso (EBS, S3, RDS) e em trânsito (SSL/TLS)
- [[concepts/encryption]] — conceito base: data at rest vs data in transit

### Organização de Contas
- [[entities/aws-organizations]] — gerencia múltiplas contas; faturamento consolidado; gratuito
- [[concepts/scp]] — Service Control Policies; teto de permissões por OU

### Conformidade
- [[entities/aws-artifact]] — relatórios de auditoria (Reports) e contratos digitais (Agreements); gratuito

### Proteção de Aplicações e Rede
- [[entities/aws-waf]] — firewall L7 para apps web; bloqueia SQL Injection, XSS
- [[entities/aws-shield]] — proteção DDoS; Standard (gratuito, incluso) vs Advanced (pago)

### Verificação e Detecção
- [[entities/amazon-inspector]] — scan automático de CVEs em EC2 e containers
- [[entities/amazon-guardduty]] — detecção de ameaças em tempo real via ML; monitora logs DNS, VPC, CloudTrail

---

## Lacunas

- Secrets Manager — sem cobertura
- CloudTrail — mencionado como fonte de dados do GuardDuty, mas sem página própria
- Security Hub, IAM Access Analyzer — sem cobertura
- Bucket policies (resource-based) — sem cobertura
- Tag-based conditions em policies (`aws:ResourceTag`) — sem cobertura
- Cross-account roles e identidade federada — citados, não detalhados
- Identity Pool (Cognito) — só User Pool coberto
- Authorizers do API Gateway na prática — ainda não implementados no curso

---

## Fontes

- [[sources/aws-course-01-mfa-iam-setup]]
- [[sources/aws-course-02-iam-policies-tags-credentials]]
- [[sources/aws-course-03-iam-user-login-inline-policy]]
- [[sources/aws-course-04-iam-groups]]
- [[sources/aws-course-05-iam-roles-custom-policies-lambda]]
- [[sources/aws-course-06-iam-permissions-validation-s3]]
- [[sources/aws-course-cognito-intro]]
- [[sources/aws-course-dynamo-01-table-lambda-intro]]
- [[sources/aws-course-dynamo-02-lambda-crud]]
- [[sources/aws-course-apigateway-01-api-routes]]
- [[sources/aws-course-apigateway-02-integration-postman]]
- [[sources/clf-c02-aulas1-6-seguranca-nuvem]]
