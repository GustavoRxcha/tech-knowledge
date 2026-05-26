---
title: "AWS Shield"
type: entity
tags: [aws, segurança, shield, ddos, clf-c02]
created: 2026-05-26
updated: 2026-05-26
sources: 1
---

# AWS Shield

Serviço da [[entities/aws|AWS]] de **proteção contra ataques DDoS** (Distributed Denial of Service). Existe em duas versões: Standard (gratuita e ativa por padrão) e Advanced (paga).

---

## O que é DDoS

Atacante controla milhares de máquinas para sobrecarregar um serviço simultaneamente, impedindo que usuários legítimos acessem.

```
[Atacante controla 10.000 máquinas]
         ↓ todas chamam ao mesmo tempo
[Sua API]
    └── Sobrecarregada → usuários legítimos bloqueados
```

---

## Duas versões

### Shield Standard — Gratuito

- Incluso em **todos os serviços AWS** sem custo adicional
- Proteção contra ataques DDoS **mais comuns**
- Análise em tempo real de tráfego malicioso
- **Ativo por padrão** — não requer configuração

### Shield Advanced — Pago

- Custo mensal adicional
- Proteção contra ataques DDoS **mais elaborados e complexos**
- Diagnósticos detalhados de ataques
- Integração com [[entities/aws-waf|WAF]]
- **Suporte 24/7** de equipe especializada em DDoS

---

## Comparativo

| Aspecto | Standard | Advanced |
|---|---|---|
| Custo | **Gratuito** | Pago |
| Ataques comuns | ✅ | ✅ |
| Ataques complexos | ❌ | ✅ |
| Suporte 24/7 | ❌ | ✅ |
| Diagnóstico detalhado | ❌ | ✅ |
| Integração WAF | ❌ | ✅ |

---

## Palavra-gatilho na prova

| Enunciado | Resposta |
|---|---|
| "Proteger contra DDoS" | Shield |
| "DDoS gratuito, já incluso" | Shield Standard |
| "DDoS avançado com suporte 24/7" | Shield Advanced |

---

## Relações

- [[entities/aws]]
- [[entities/aws-waf]] — Shield Advanced integra com WAF
- [[topics/aws-security]]
- [[sources/clf-c02-aulas1-6-seguranca-nuvem]]
