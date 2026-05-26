---
title: "Amazon Inspector"
type: entity
tags: [aws, segurança, inspector, vulnerabilidades, cve, clf-c02]
created: 2026-05-26
updated: 2026-05-26
sources: 1
---

# Amazon Inspector

Serviço da [[entities/aws|AWS]] que **escaneia automaticamente vulnerabilidades** em instâncias EC2 e containers, comparando com bancos de CVEs (Common Vulnerabilities and Exposures) e benchmarks de segurança.

---

## Como funciona

```
[Amazon Inspector ativado]
    ↓ Escaneia instâncias EC2 e containers
    ↓ Compara com banco de CVEs
    ↓ Compara com benchmarks de segurança

[Relatório]
├── EC2-1: SO desatualizado — CVE-2024-XXXX (crítico)
│   └── Recomendação: atualizar pacote X para versão Y
└── EC2-2: OK
```

---

## Por que é importante

Diariamente, novas vulnerabilidades são descobertas em SOs e softwares. Sem automação, é necessário acompanhar manualmente boletins de CVE e verificar cada instância — arriscado em escala.

| Sem Inspector | Com Inspector |
|---|---|
| Verificação manual por instância | Automática e contínua |
| Risco de falhar em alguma | Cobertura centralizada |
| Sem notificação imediata | Alerta imediato |

---

## Inspector vs GuardDuty (par mais cobrado)

| Aspecto | Amazon Inspector | Amazon GuardDuty |
|---|---|---|
| **Foco** | Vulnerabilidades conhecidas | Atividades maliciosas em tempo real |
| **O que analisa** | SO e software da instância | Tráfego de rede e eventos da conta |
| **Quando age** | Scan programado ou contínuo | Monitoramento contínuo |
| **Fonte de dados** | CVEs, benchmarks | Logs DNS, VPC, CloudTrail |
| **Exemplo** | "Seu SO tem CVE-2024-X" | "IP Y está tentando invadir" |

> Inspector = **o que está vulnerável** no sistema. GuardDuty = **o que está acontecendo** na rede.

---

## Palavra-gatilho na prova

| Enunciado | Resposta |
|---|---|
| "Escanear vulnerabilidades em EC2" | Amazon Inspector |
| "Verificar CVEs automaticamente" | Amazon Inspector |
| "Auditoria de segurança de SO" | Amazon Inspector |

---

## Relações

- [[entities/aws]]
- [[entities/amazon-guardduty]] — par complementar; GuardDuty detecta ameaças ativas
- [[entities/amazon-ec2]] — principal alvo dos scans
- [[concepts/shared-responsibility-model]] — atualizar SO da EC2 é responsabilidade do cliente; Inspector automatiza a verificação
- [[topics/aws-security]]
- [[sources/clf-c02-aulas1-6-seguranca-nuvem]]
