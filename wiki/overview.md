---
title: "Overview"
type: overview
tags: [aws, iam, segurança]
created: 2026-05-18
updated: 2026-05-18
sources: 4
---

# Tech Knowledge Wiki — Overview

Síntese evolutiva do panorama geral. Atualizada sempre que uma nova fonte muda o quadro.

---

## Estado atual

O wiki cobre, no momento, **fundamentos de segurança e IAM na AWS**, ingeridos a partir das quatro primeiras aulas de um curso AWS (PT-BR). Foco operacional: bootstrappar uma conta com baseline de segurança, criar usuários IAM, organizar permissões em [[iam-group|grupos]] e validar [[principle-of-least-privilege|menor privilégio]] na prática.

---

## Áreas rastreadas

| Área | Status | Páginas-chave |
|---|---|---|
| AI/ML & LLMs | — | — |
| Linguagens | — | — |
| Frameworks | — | — |
| Arquitetura | — | — |
| Infraestrutura — cloud AWS | 🌱 inicial | [[aws]], [[aws-iam]], [[amazon-s3]], [[aws-lambda]] (stub), [[amazon-ec2]] (stub), [[amazon-dynamodb]] (stub) |
| Bancos de dados | 🔴 só stub | [[amazon-dynamodb]] |
| Segurança — IAM/AWS | 🟢 cobertura sólida do baseline | [[aws-security]], [[mfa]], [[iam-policy]], [[iam-group]] |
| Prática de engenharia | — | — |

---

## Perguntas em aberto

- **IAM Roles** (próxima aula): assume-role, uso por serviços/usuários, vs usuários com [[access-keys]] de longa duração.
- **Customer-managed policies** (próxima aula): quando criar do zero em vez de usar managed da AWS.
- Como [[iam-policy|policies]] de identidade interagem com bucket policies em [[amazon-s3]]?
- Como usar [[resource-tags|tags]] como condição em policies (`aws:ResourceTag`)?
- Limites práticos de grupos (máximo de policies por grupo, etc.) — ainda não declarados nas fontes.

---

## Temas emergentes

- **Menor privilégio como princípio operacional**: cada aula reforça e a aula 4 valida com erros reais (`You are not authorized to perform this operation.`).
- **Hierarquia de anexação**: o caminho recomendado de permissão é **policy → grupo → usuário**, não policy direta no usuário.
- **Managed primeiro, inline como exceção**: para casos padrão a AWS já tem ~centenas de managed policies; criar do zero só quando necessário.
- O par **identidade + recurso**, mediado por [[arn|ARNs]], é o modelo central de autorização da AWS.
- Operações sensíveis (criação de access key) são **one-shot e irreversíveis** — falhar em baixar o CSV implica regerar credenciais.

---

## Lacunas

- **IAM Roles, customer-managed policies, SCPs, AWS Organizations, KMS, CloudTrail** — nada coberto.
- [[amazon-s3]] tem só duas actions ilustrativas; o resto do serviço (versionamento, criptografia, lifecycle etc.) está em aberto.
- [[aws-lambda]], [[amazon-ec2]], [[amazon-dynamodb]] estão como stubs — apenas posicionados no modelo mental, sem profundidade.
- Tudo fora do tópico AWS — outras linguagens, frameworks, AI/ML, arquitetura — ainda sem fontes.
