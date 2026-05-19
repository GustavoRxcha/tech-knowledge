---
title: "Curso AWS 06 — Validação de Permissões no S3 e Encerramento do Módulo IAM"
type: source
tags: [aws, iam, s3, permissões, segurança]
created: 2026-05-18
updated: 2026-05-18
sources: 1
---

# Curso AWS 06 — Validação de Permissões no S3 e Encerramento do Módulo IAM

Aula de encerramento do módulo IAM. Foco prático: editar a policy `policy-s3-developers` para adicionar `s3:ListAllMyBuckets`, validar cada permissão no console com usuário developer, e introduzir [[concepts/s3-block-public-access|Block Public Access]] como boa prática de segurança.

---

## Atualização da policy

- Acesso: **IAM → Policies → policy-s3-developers → Edit policy**
- Ação adicionada: `s3:ListAllMyBuckets` — lista todos os buckets da conta
- Resource: `arn:aws:s3:::*`

---

## Validação prática (usuário developer G1)

| Ação S3 | Permissão | Resultado |
|---|---|---|
| Listar buckets da conta | `s3:ListAllMyBuckets` | ✅ |
| Acessar bucket específico | `s3:ListBucket` | ✅ |
| Upload de arquivo | `s3:PutObject` | ✅ |
| Download de objeto | `s3:GetObject` | ✅ |
| Deletar objeto | `s3:DeleteObject` | ✅ |
| Versionamento | `s3:PutObjectVersioning` | ❌ (não configurado) |

> Princípio do menor privilégio confirmado: usuário acessa apenas o que está explicitamente permitido.

---

## Block Public Access

Identificado durante os testes: bucket sem **Block Public Access** habilitado ficaria exposto publicamente.

- Habilitar por padrão em qualquer bucket que não precise ser público
- Controle de acesso deve ser via **bucket policies** e **ACLs**, não exposição aberta

Ver: [[concepts/s3-block-public-access]]

---

## Resumo do módulo IAM (aulas 01–06)

| Aula | Conteúdo |
|---|---|
| 01 | Console AWS, MFA no root, criação de usuário IAM |
| 02 | Policies, Tags, tipos de acesso, CSV de credenciais |
| 03 | Login com usuário IAM, inline policies, ARN, permissões S3 |
| 04 | Grupos, managed policies, testes com EC2 e Lambda |
| 05 | Roles, policies personalizadas, Lambda acessando S3 |
| 06 | Atualização de policies, validação prática de permissões |

---

## Boas práticas consolidadas do módulo

- Ativar **MFA** no root imediatamente
- Nunca usar root para operações diárias
- Organizar usuários em **grupos** com políticas bem definidas
- Sempre aplicar [[concepts/principle-of-least-privilege|menor privilégio]]
- Usar **roles** para comunicação entre serviços (nunca hardcodar credenciais)
- Usar [[concepts/resource-tags|tags]] para organizar recursos
- Fazer download do CSV de credenciais imediatamente após criar usuários
- Manter buckets com [[concepts/s3-block-public-access|Block Public Access]] ativado por padrão

---

## Próximo módulo

**Amazon S3 — Armazenamento de Objetos**

---

## Relações

- [[concepts/s3-block-public-access]] — configuração de segurança do S3
- [[entities/amazon-s3]] — serviço central desta aula
- [[concepts/iam-policy]] — editada para adicionar ListAllMyBuckets
- [[concepts/principle-of-least-privilege]] — validado na prática
- [[topics/aws-security]] — encerramento do baseline de segurança IAM
