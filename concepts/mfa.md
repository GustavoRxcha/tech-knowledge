---
title: "Multi-Factor Authentication (MFA)"
type: concept
tags: [security, authentication, mfa, totp]
created: 2026-05-18
updated: 2026-05-18
sources: 1
---

# Multi-Factor Authentication (MFA)

Authentication that requires **two or more** independent factors — something you know (password), something you have (device/token), or something you are (biometric).

---

## In the AWS context

- Strongly recommended on the [[aws|AWS]] root user immediately after account creation.
- Once enabled, every login requires a TOTP code in addition to the password.
- Setup uses a **virtual MFA device** (an authenticator app such as [[google-authenticator]]).
- Pairing flow: scan QR code → enter two sequential codes → device is bound.

## TOTP at a glance

- Codes are short-lived (typically 30s).
- The QR code encodes a shared secret; the client and server derive the same time-based code from that secret.
- Any TOTP-compatible app works — [[google-authenticator]] is just the most common one.

## Sources

- [[aws-course-01-mfa-iam-setup]]

## Related

- [[aws-iam]]
- [[aws-security]]
- [[principle-of-least-privilege]]
