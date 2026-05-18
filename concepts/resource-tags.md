---
title: "Resource Tags (AWS)"
type: concept
tags: [aws, tags, governance, cost-management]
created: 2026-05-18
updated: 2026-05-18
sources: 1
---

# Resource Tags

Key/value metadata pairs attached to [[aws|AWS]] resources for classification, filtering, governance, and cost allocation.

---

## Mental model

Think of tags like luggage labels: arbitrary key/value pairs that let you slice and dice the resource inventory by whatever criteria matter to you.

## Typical schemes

| Key | Example values |
|---|---|
| `Env` | `Production`, `Staging`, `Development` |
| `Team` | `Backend`, `Data`, `Platform` |
| `CostCenter` | `1042` |
| `Project` | `Curso-AWS` |
| `Owner` | `alice@company.com` |

## Why tags matter

- **Cost allocation** — filter spend in AWS Cost Explorer by tag.
- **Governance** — apply policies based on tag values (e.g. require `Env`).
- **Discoverability** — find all resources for a project or team.
- **Automation** — scripts and IaC can filter by tag.

## Sources

- [[aws-course-02-iam-policies-tags-credentials]]

## Related

- [[aws-iam]]
- [[aws]]

> [!question] Needs verification — the source covers tags only conceptually. Tag-based policy conditions (`aws:RequestTag`, `aws:ResourceTag`) and tagging best practices not yet ingested.
