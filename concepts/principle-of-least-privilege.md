---
title: "Principle of Least Privilege"
type: concept
tags: [security, access-control, best-practice]
created: 2026-05-18
updated: 2026-05-18
sources: 2
---

# Principle of Least Privilege

Grant every identity (user, service, process) **only the permissions it needs to do its job — and nothing more**. A foundational security principle in access-control design.

---

## Why

- Limits the blast radius of a compromised credential.
- Reduces accidental damage from operator error.
- Makes auditing tractable — fewer permissions = clearer review.

## How it shows up in [[aws|AWS]] sources

- Avoid using the root user for daily work — see [[aws-security]].
- Disable the root access key.
- Prefer narrow [[iam-policy|IAM policies]] (specific actions, specific [[arn|ARNs]]) over broad ones like `AdministratorAccess`.
- Use [[inline-policy|inline policies]] for one-off, identity-specific exceptions.
- Reserve `AdministratorAccess` for genuine administrators only.

## Sources

- [[aws-course-01-mfa-iam-setup]]
- [[aws-course-02-iam-policies-tags-credentials]]

## Related

- [[aws-iam]]
- [[iam-policy]]
- [[mfa]]
- [[aws-security]]
