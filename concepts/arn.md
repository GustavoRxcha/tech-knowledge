---
title: "ARN — Amazon Resource Name"
type: concept
tags: [aws, arn, identifiers]
created: 2026-05-18
updated: 2026-05-18
sources: 1
---

# ARN — Amazon Resource Name

Unique identifier for any resource in [[aws|AWS]]. Used as the `Resource` field in [[iam-policy|IAM policies]] to scope permissions.

---

## Format

```
arn:aws:<service>:<region>:<account>:<resource-type>/<resource-name>
```

Some services omit `region` and/or `account` when the namespace is global.

## Examples

| Resource | ARN |
|---|---|
| S3 bucket | `arn:aws:s3:::my-bucket` |
| All objects in a bucket | `arn:aws:s3:::my-bucket/*` |
| EC2 instance | `arn:aws:ec2:us-east-1:123456789012:instance/i-abc123` |
| IAM user | `arn:aws:iam::123456789012:user/alice` |

> [!note] S3 bucket names are globally unique, so the region and account segments are blank for S3 ARNs.

## Common patterns

- **Wildcard suffix** `/*` — applies to all objects/sub-resources within a parent.
- **Service wildcard** `arn:aws:s3:::*` — every S3 bucket (dangerous outside admin policies).

## How to find an ARN

In the AWS console, every resource detail page exposes its ARN. The CLI usually returns it in `describe-*` calls.

## Sources

- [[aws-course-03-iam-user-login-inline-policy]]

## Related

- [[iam-policy]]
- [[inline-policy]]
- [[amazon-s3]]
- [[aws-iam]]
