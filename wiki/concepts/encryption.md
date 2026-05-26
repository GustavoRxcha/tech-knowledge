---
title: "Criptografia (Encryption)"
type: concept
tags: [segurança, criptografia, encryption, kms, ssl, tls, clf-c02]
created: 2026-05-26
updated: 2026-05-26
sources: 1
---

# Criptografia (Encryption)

Prática de proteger informações por meio de algoritmos codificados, tornando os dados ilegíveis para quem não tem a chave de acesso.

```
[Dado Original]     [Criptografado]    [Descriptografado]
"senha123"    →    "x9#mK!2@qP"   →   "senha123"
                    ↑                    ↑
               Com a chave          Com a chave
               ninguém lê           autorizado lê
```

---

## Dois contextos de criptografia

### Dados em Repouso (Data at Rest)

Dados **armazenados** — não estão trafegando.

| Serviço | O que é criptografado |
|---|---|
| [[entities/amazon-s3\|S3]] | Objetos no bucket |
| EBS | Dados no volume de disco |
| [[entities/amazon-dynamodb\|DynamoDB]] | Items nas tabelas |
| RDS | Dados no banco relacional |
| Snapshots | Backups EBS |

Serviço AWS: [[entities/aws-kms|KMS]] gerencia as chaves.

### Dados em Trânsito (Data in Transit)

Dados **sendo transmitidos** de um ponto a outro.

| Exemplo | Como é protegido |
|---|---|
| Login em aplicação | HTTPS (SSL/TLS) |
| EC2 ↔ RDS | SSL na conexão |
| Upload para S3 | HTTPS |
| Comunicação entre APIs | HTTPS/TLS |

Protocolo: **HTTPS** usa **SSL/TLS** — certificado digital autentica o sistema, dados trafegam criptografados.

---

## Responsabilidade

Criptografia é **responsabilidade do cliente** no [[concepts/shared-responsibility-model|Modelo de Responsabilidade Compartilhada]]. A AWS oferece as ferramentas ([[entities/aws-kms|KMS]]), mas o cliente decide se e como as usa.

---

## Palavra-gatilho na prova

| Enunciado | Resposta |
|---|---|
| "Dados em repouso" | Dados armazenados (EBS, S3, RDS) |
| "Dados em trânsito" | Dados transmitidos (HTTPS, SSL) |
| "Gerenciar chaves de criptografia" | [[entities/aws-kms\|KMS]] |
| "Proteger dados armazenados no DynamoDB" | Criptografia com KMS |

---

## Relações

- [[entities/aws-kms]] — serviço que implementa criptografia na AWS
- [[concepts/shared-responsibility-model]] — criptografia é responsabilidade do cliente
- [[topics/aws-security]]
- [[sources/clf-c02-aulas1-6-seguranca-nuvem]]
