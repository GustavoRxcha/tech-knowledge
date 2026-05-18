---
title: "Curso AWS 02 — IAM Policies, Tags e Credenciais de Usuário"
type: source
tags: [aws, iam, policies, tags, credenciais, curso]
created: 2026-05-18
updated: 2026-05-18
sources: 1
---

# Curso AWS 02 — IAM Policies, Tags e Credenciais de Usuário

Arquivo fonte: `raw/aula-02-policies-tags-credenciais-iam.md` (PT-BR)

Segunda aula do curso. Aprofunda a estrutura de [[iam-policy|policies IAM]], introduz [[resource-tags|tags]] de recursos e finaliza o processo de criação do usuário IAM com foco no manuseio das credenciais.

---

## Pontos-chave

- Policies IAM são documentos JSON com `Effect`, `Action`, `Resource`.
- `AdministratorAccess` ≈ `Action: "*"`, `Resource: "*"` — cobre ~300 serviços AWS. Reserve para administradores reais.
- [[resource-tags|Tags]] são pares chave/valor para classificar e organizar recursos (analogia: etiquetas de bagagem). Úteis para alocação de custo, governança e filtragem.
- Um novo usuário IAM gera dois conjuntos distintos de credenciais:
  - **Console**: username + senha (login web).
  - **Programático**: [[access-keys|Access Key ID + Secret Access Key]] (CLI/SDK/API).
- A **Secret Access Key é exibida apenas uma vez**. Se for perdida, a única opção é deletar e gerar um novo par.

## JSON da AdministratorAccess (exemplo canônico)

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": "*",
      "Resource": "*"
    }
  ]
}
```

## Casos de uso de tags mencionados

| Critério | Exemplo |
|---|---|
| Ambiente | `Env: Production` |
| Time | `Team: Backend` |
| Centro de custo | `CostCenter: 1042` |
| Projeto | `Project: Curso-AWS` |

## Passo operacional crítico

Baixar o CSV com as credenciais do novo usuário **antes de fechar a tela de criação**. Guardar em local seguro (gerenciador de senhas). Depois de fechar, a Secret Access Key é irrecuperável.

## Boas práticas declaradas

- Atribuir `AdministratorAccess` apenas a administradores reais.
- Preferir policies com menor privilégio — ver [[principle-of-least-privilege]].
- Marcar recursos com tags desde o dia 1 para governança e rastreio de custo.
- Baixar o CSV de credenciais no momento da criação.

---

## Entidades e conceitos tocados

- Entidades: [[aws]], [[aws-iam]]
- Conceitos: [[iam-policy]], [[access-keys]], [[resource-tags]], [[principle-of-least-privilege]]
- Tópicos: [[aws-security]]
