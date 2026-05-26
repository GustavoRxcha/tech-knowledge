---
title: "AWS WAF — Web Application Firewall"
type: entity
tags: [aws, segurança, waf, firewall, sql-injection, xss, clf-c02]
created: 2026-05-26
updated: 2026-05-26
sources: 1
---

# AWS WAF — Web Application Firewall

Firewall da [[entities/aws|AWS]] para **aplicações web**. Filtra tráfego HTTP/HTTPS malicioso **antes** que chegue à aplicação, bloqueando ataques comuns como SQL Injection e XSS.

---

## Como funciona

```
[Atacante]
    ↓ GET /api?id=1; DROP TABLE users; --
[WAF]
    ↓ Regra: "SQL Injection detectado" → BLOQUEIA
[Load Balancer / CloudFront]
    ↓ Nunca recebe a requisição maliciosa
[EC2 + Banco de dados] ← Protegidos
```

### Sem WAF

```
[Atacante] → SQL Injection → [Load Balancer] → [EC2] → [Banco] ← Dados comprometidos ❌
```

---

## Características

- Protege contra ataques OWASP Top 10 (SQL Injection, XSS, CSRF, etc.)
- Regras **pré-configuradas** (managed rules) e **customizáveis**
- Integra nativamente com: ALB ([[entities/elastic-load-balancing|ELB]]), [[entities/amazon-cloudfront|CloudFront]], EC2
- Opera na camada 7 (aplicação HTTP/HTTPS)

---

## Diferença em relação a outros firewalls do wiki

| Serviço | Nível | Protege contra |
|---|---|---|
| [[concepts/network-acl\|NACL]] | Sub-rede (L3/L4) | Tráfego IP/porta |
| [[concepts/security-group\|Security Group]] | Instância EC2 (L4) | Tráfego IP/porta |
| **WAF** | Aplicação web (L7) | Ataques HTTP (SQL Injection, XSS) |

WAF complementa NACL e Security Group — atua em uma camada mais alta, entendendo o conteúdo das requisições HTTP.

---

## Palavra-gatilho na prova

| Enunciado | Resposta |
|---|---|
| "Proteger contra SQL Injection" | WAF |
| "Proteger contra XSS em aplicação web" | WAF |
| "Firewall para aplicações web" | WAF |

---

## Relações

- [[entities/aws]]
- [[entities/aws-shield]] — WAF integra com Shield Advanced
- [[entities/elastic-load-balancing]] — WAF protege na frente do ALB
- [[entities/amazon-cloudfront]] — WAF integra com CloudFront
- [[concepts/network-acl]] — complementar (camada de sub-rede)
- [[concepts/security-group]] — complementar (camada de instância)
- [[topics/aws-security]]
- [[sources/clf-c02-aulas1-6-seguranca-nuvem]]
