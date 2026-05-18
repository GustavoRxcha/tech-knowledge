---
title: "Resource Tags (AWS)"
type: concept
tags: [aws, tags, governança, custos]
created: 2026-05-18
updated: 2026-05-18
sources: 1
---

# Resource Tags

Pares chave/valor de metadados anexados a recursos da [[aws|AWS]] para classificação, filtragem, governança e alocação de custos.

---

## Modelo mental

Pense em tags como etiquetas de bagagem: pares arbitrários chave/valor que permitem fatiar o inventário de recursos pelos critérios que importam pra você.

## Esquemas típicos

| Chave | Valores exemplo |
|---|---|
| `Env` | `Production`, `Staging`, `Development` |
| `Team` | `Backend`, `Data`, `Platform` |
| `CostCenter` | `1042` |
| `Project` | `Curso-AWS` |
| `Owner` | `alice@empresa.com` |

## Por que tags importam

- **Alocação de custo** — filtrar gastos no AWS Cost Explorer por tag.
- **Governança** — aplicar policies baseadas em valores de tag (ex.: exigir `Env`).
- **Descoberta** — encontrar todos os recursos de um projeto ou time.
- **Automação** — scripts e IaC podem filtrar por tag.

## Fontes

- [[aws-course-02-iam-policies-tags-credentials]]

## Relacionados

- [[aws-iam]]
- [[aws]]

> [!question] Precisa de verificação — a fonte cobre tags apenas conceitualmente. Condições de policy baseadas em tag (`aws:RequestTag`, `aws:ResourceTag`) e boas práticas de tagging ainda não foram ingeridas.
