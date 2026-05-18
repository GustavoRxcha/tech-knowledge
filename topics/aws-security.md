---
title: "AWS Security"
type: topic
tags: [aws, security, iam, mfa]
created: 2026-05-18
updated: 2026-05-18
sources: 3
---

# AWS Security

Topic page grouping everything the wiki knows about securing an [[aws|AWS]] account. Currently focused on account bootstrapping and access management.

---

## Baseline checklist (from current sources)

- [x] Enable [[mfa]] on the root user immediately after account creation.
- [x] **Disable the root access key.**
- [x] Stop using root for day-to-day work — operate via [[aws-iam]] users.
- [x] Apply the [[principle-of-least-privilege]] to every identity.
- [x] Prefer [[iam-policy|policies]] scoped to specific actions and [[arn|ARNs]].
- [x] Use [[inline-policy|inline policies]] only for genuinely one-off, identity-specific permissions.
- [x] Reserve `AdministratorAccess` for genuine administrators only.
- [x] Download the credentials CSV at user creation — the Secret Access Key is shown only once.
- [x] Tag resources from day one for governance — see [[resource-tags]].

## Sub-areas

### Identity & access
- [[aws-iam]]
- [[iam-policy]] / [[inline-policy]]
- [[access-keys]]
- [[principle-of-least-privilege]]

### Authentication
- [[mfa]]
- [[google-authenticator]]

### Resource identification & governance
- [[arn]]
- [[resource-tags]]

## Gaps

- No coverage yet of: IAM **roles**, IAM **groups** (next lesson), service control policies (SCPs), AWS Organizations, KMS, Secrets Manager, GuardDuty, CloudTrail, Security Hub, IAM Access Analyzer.
- No coverage of bucket-level policies on [[amazon-s3]] or other resource-based policies.

## Sources

- [[aws-course-01-mfa-iam-setup]]
- [[aws-course-02-iam-policies-tags-credentials]]
- [[aws-course-03-iam-user-login-inline-policy]]
