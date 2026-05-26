---
title: "AWS KMS — Key Management Service"
type: entity
tags: [aws, segurança, criptografia, kms, clf-c02]
created: 2026-05-26
updated: 2026-05-26
sources: 1
---

# AWS KMS — Key Management Service

Serviço gerenciado da [[entities/aws|AWS]] para **criação e gestão de chaves criptográficas**. Protege dados em repouso e em trânsito em toda a infraestrutura AWS.

---

## Características

| Característica | Descrição |
|---|---|
| Gerenciado | Sem infraestrutura para provisionar |
| Centralizado | Gerencia todas as chaves em um lugar |
| Integrado | Funciona com EBS, S3, RDS, DynamoDB, Lambda |
| Controle de acesso | Define quem pode usar cada chave via IAM |
| Auditoria | Logs de uso das chaves via CloudTrail |

---

## Dois tipos de proteção

### Dados em Repouso (Data at Rest)

Dados **armazenados** — não estão trafegando.

```
[Dado original: CPF "123.456.789-00"]
        ↓ KMS criptografa com chave
[Dado no DynamoDB: "8!nQ%7rZ#1"]
        ↓ Apenas quem tem a chave
[Dado legível: "123.456.789-00"]
```

Serviços integrados: [[entities/amazon-dynamodb|DynamoDB]], [[entities/amazon-s3|S3]], RDS, EBS, snapshots.

### Dados em Trânsito (Data in Transit)

Dados **sendo transmitidos** de um ponto a outro.

```
[Aplicação]
    ↓ HTTPS (SSL/TLS)
[KMS + Certificado digital]
    ↓ Dados criptografados em trânsito
[Bucket S3]
```

Protocolo: HTTPS/SSL/TLS — conexão estabelecida, certificado autentica, dados trafegam criptografados.

---

## Quando usar KMS

- Armazenar dados sensíveis (CPF, dados financeiros, segredos) no S3, RDS ou DynamoDB
- Garantir que volumes EBS não possam ser lidos se o disco for removido
- Cumprir requisitos de conformidade (LGPD, HIPAA, SOC) que exigem criptografia

---

## Palavra-gatilho na prova

| Enunciado | Resposta |
|---|---|
| "Gerenciar chaves criptográficas na AWS" | KMS |
| "Proteger dados em volume EBS" | Criptografia com KMS |
| "Dados em repouso" | Dados armazenados (EBS, S3, RDS) |
| "Dados em trânsito" | Dados sendo transmitidos (HTTPS, SSL) |

---

## Relações

- [[entities/aws]]
- [[concepts/shared-responsibility-model]] — criptografia é responsabilidade do cliente
- [[concepts/encryption]] — conceito base
- [[entities/amazon-s3]]
- [[entities/amazon-dynamodb]]
- [[topics/aws-security]]
- [[sources/clf-c02-aulas1-6-seguranca-nuvem]]
