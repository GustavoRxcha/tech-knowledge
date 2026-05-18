---
title: "IAM Policy"
type: concept
tags: [aws, iam, policy, access-control, json]
created: 2026-05-18
updated: 2026-05-18
sources: 3
---

# IAM Policy

JSON document that defines what an [[aws-iam]] identity is allowed (or denied) to do on which resources.

---

## Anatomy

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::my-bucket/*"
    }
  ]
}
```

| Field | Meaning |
|---|---|
| `Version` | Policy language version. `2012-10-17` is the current standard. |
| `Effect` | `Allow` or `Deny`. |
| `Action` | One or more service actions, e.g. `s3:GetObject`. Wildcards allowed. |
| `Resource` | One or more [[arn|ARNs]] the statement applies to. |

## Policy types

| Type | Created by | Reusable | Notes |
|---|---|---|---|
| **AWS-managed** | AWS | Yes | Maintained by AWS. Example: `AdministratorAccess`. |
| **Customer-managed** | Account | Yes | Reusable across users/groups/roles in the account. |
| **[[inline-policy|Inline]]** | Account | No | Embedded in a single identity; deleted with it. |

## `AdministratorAccess` — the canonical "all access" policy

```json
{
  "Version": "2012-10-17",
  "Statement": [
    { "Effect": "Allow", "Action": "*", "Resource": "*" }
  ]
}
```

Covers ~300 AWS services. Should be attached only to genuine administrators — see [[principle-of-least-privilege]].

## Sources

- [[aws-course-01-mfa-iam-setup]]
- [[aws-course-02-iam-policies-tags-credentials]]
- [[aws-course-03-iam-user-login-inline-policy]]

## Related

- [[inline-policy]]
- [[arn]]
- [[access-keys]]
- [[principle-of-least-privilege]]
