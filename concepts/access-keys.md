---
title: "AWS Access Keys"
type: concept
tags: [aws, iam, credentials, access-keys, security]
created: 2026-05-18
updated: 2026-05-18
sources: 2
---

# AWS Access Keys

Long-lived credentials for **programmatic access** to [[aws|AWS]] (CLI, SDKs, APIs). An access key is a pair:

- **Access Key ID** — public identifier.
- **Secret Access Key** — the secret half; signs API requests.

---

## Lifecycle

- Generated when an [[aws-iam|IAM user]] is created with programmatic access (or later via IAM → Security credentials).
- The Secret Access Key is shown **exactly once** at creation. Download the credentials CSV before closing the screen.
- If lost: the key cannot be recovered. Delete the existing key and create a new pair.
- Each user can have up to 2 active key pairs (to enable rotation).

## Root vs IAM user keys

- The **root user**'s access key should be **disabled** as a baseline security practice (see [[aws-security]]).
- IAM user keys should follow the [[principle-of-least-privilege]] — scoped to only what the user needs.

## CSV contents (at user creation)

| Column | Use |
|---|---|
| Console login link | Web sign-in URL (pre-fills account ID) |
| Username | Console login |
| Password | Initial console password (reset on first login) |
| Access Key ID | Programmatic identifier |
| Secret Access Key | Programmatic secret |

## Sources

- [[aws-course-01-mfa-iam-setup]]
- [[aws-course-02-iam-policies-tags-credentials]]

## Related

- [[aws-iam]]
- [[mfa]]
- [[principle-of-least-privilege]]
