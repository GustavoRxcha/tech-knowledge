---
title: "S3 Block Public Access"
type: concept
tags: [aws, s3, segurança, acesso-público]
created: 2026-05-18
updated: 2026-05-18
sources: 1
---

# S3 Block Public Access

Configuração de segurança do [[entities/amazon-s3|Amazon S3]] que impede que objetos e buckets fiquem **expostos publicamente na internet**, mesmo que políticas ou ACLs mal configuradas tentem torná-los públicos.

---

## Por que importa

Por padrão (contas novas), a AWS bloqueia acesso público. Mas buckets podem ser configurados para remover esse bloqueio — e isso é um risco de segurança se feito sem intenção.

Um bucket sem Block Public Access habilitado pode ser acessado por qualquer pessoa na internet, expondo dados sensíveis.

---

## Configurações disponíveis

| Opção | O que bloqueia |
|---|---|
| `BlockPublicAcls` | Impede ACLs que concedam acesso público |
| `IgnorePublicAcls` | Ignora ACLs públicas existentes |
| `BlockPublicPolicy` | Impede bucket policies que concedam acesso público |
| `RestrictPublicBuckets` | Restringe acesso público mesmo com policy permissiva |

> Habilitar todas as quatro opções é o baseline de segurança recomendado.

---

## Boas práticas

- Habilitar Block Public Access **por padrão** em todos os buckets
- Tornar um bucket público deve ser uma decisão **deliberada e documentada**
- Usar **bucket policies** e [[concepts/iam-policy|IAM policies]] para controle granular de acesso
- Nunca deixar bucket aberto sem necessidade operacional clara

---

## Acesso legítimo a buckets

Para servir conteúdo publicamente (ex: site estático, assets), use:
- **CloudFront com Origin Access Control (OAC)** — bucket permanece privado, CloudFront acessa via role
- **Bucket policy restrita** a origens específicas

---

## Relações

- [[entities/amazon-s3]] — serviço ao qual esta configuração pertence
- [[concepts/iam-policy]] — forma correta de controlar acesso ao S3
- [[concepts/principle-of-least-privilege]] — princípio que motiva manter Block Public Access ativo
- [[topics/aws-security]] — contexto mais amplo de segurança AWS
