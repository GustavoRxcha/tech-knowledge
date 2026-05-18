---
title: "Inline Policy"
type: concept
tags: [aws, iam, policy, access-control]
created: 2026-05-18
updated: 2026-05-18
sources: 1
---

# Inline Policy

An [[iam-policy]] **embedded directly** in a single [[aws-iam|IAM]] identity (user, group, or role). It has no independent existence — when the identity is deleted, the policy goes with it.

---

## When to use vs managed policy

| Question | Use inline | Use managed |
|---|---|---|
| Is this permission unique to one user? | ✅ | |
| Will it be reused across identities? | | ✅ |
| Need strict 1:1 lifecycle binding? | ✅ | |
| Need centralized policy versioning? | | ✅ |

Inline policies are best for **exceptional, identity-specific** permissions that should never be applied elsewhere.

## Worked example (from [[aws-course-03-iam-user-login-inline-policy]])

Grant a single user the ability to put and get objects on one specific S3 bucket:

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": ["s3:PutObject", "s3:GetObject"],
      "Resource": "arn:aws:s3:::my-bucket/*"
    }
  ]
}
```

Created via: IAM → Users → user → Permissions → Add permissions → **Create inline policy**.

## Sources

- [[aws-course-03-iam-user-login-inline-policy]]

## Related

- [[iam-policy]]
- [[arn]]
- [[amazon-s3]]
