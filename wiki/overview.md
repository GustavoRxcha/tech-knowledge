---
title: "Overview"
type: overview
tags: [aws, iam, s3, segurança]
created: 2026-05-18
updated: 2026-05-18
sources: 6
---

# Tech Knowledge Wiki — Overview

Síntese evolutiva do panorama geral. Atualizada sempre que uma nova fonte muda o quadro.

---

## Estado atual

O wiki concluiu o **módulo completo de IAM da AWS** (aulas 01–06). Cobre desde o bootstrap inicial da conta até roles, policies personalizadas e validação prática de permissões no S3. O próximo módulo do curso é **Amazon S3 — Armazenamento de Objetos**.

---

## Áreas rastreadas

| Área | Status | Páginas-chave |
|---|---|---|
| AI/ML & LLMs | — | — |
| Linguagens | — | — |
| Frameworks | — | — |
| Arquitetura | — | — |
| Infraestrutura — cloud AWS | 🟡 módulo IAM completo | [[entities/aws]], [[entities/aws-iam]], [[entities/amazon-s3]], [[entities/aws-lambda]], [[entities/amazon-ec2]] (stub), [[entities/amazon-dynamodb]] (stub) |
| Bancos de dados | 🔴 só stub | [[entities/amazon-dynamodb]] |
| Segurança — IAM/AWS | 🟢 cobertura sólida do baseline | [[topics/aws-security]], [[concepts/mfa]], [[concepts/iam-policy]], [[concepts/iam-group]], [[concepts/iam-role]], [[concepts/customer-managed-policy]], [[concepts/s3-block-public-access]] |
| Prática de engenharia | — | — |

---

## Modelo mental do IAM (consolidado)

O IAM organiza acesso em torno de quatro perguntas:

1. **Quem?** — usuário, grupo, role, serviço
2. **O quê?** — actions (`s3:GetObject`, `lambda:InvokeFunction`...)
3. **Em quê?** — resources identificados por [[concepts/arn|ARN]]
4. **Como?** — via policy (managed, customer-managed, inline)

A hierarquia recomendada de permissão: **policy → grupo → usuário**. Para serviços: **policy → role → serviço**.

---

## Temas emergentes

- **Menor privilégio como prática operacional**: validado com erros reais em aulas 4 e 6 (`You are not authorized to perform this operation.`).
- **Roles como padrão para serviços**: Lambda + S3 demonstrou o modelo — nenhum serviço deve usar access keys hardcodadas.
- **Block Public Access como default**: configuração de segurança S3 essencial, deve ser habilitada por padrão em qualquer bucket.
- **Customer-managed policies** para casos não cobertos pelas managed da AWS.

---

## Próximas perguntas abertas

- Como funciona cross-account role (assume-role entre contas)?
- Como usar `aws:ResourceTag` como condição em policies?
- Limites de grupos (máximo de policies por grupo, usuários por grupo)?
- Bucket policies e ACLs do S3 — como interagem com as IAM policies?
- Módulo S3: versionamento, criptografia, lifecycle, storage classes, presigned URLs, hospedagem estática.

---

## Lacunas do wiki

- **IAM**: Roles cross-account, federação de identidade, SCPs, AWS Organizations, KMS, CloudTrail, IAM Access Analyzer — não cobertos.
- **S3**: Apenas ações IAM básicas e Block Public Access. Módulo dedicado a ser ingerido.
- **EC2, DynamoDB**: Stubs apenas.
- Tudo fora do tópico AWS — linguagens, frameworks, AI/ML, arquitetura — ainda sem fontes.
