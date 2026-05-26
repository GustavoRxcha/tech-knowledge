---
title: "Amazon GuardDuty"
type: entity
tags: [aws, segurança, guardduty, detecção-ameaças, machine-learning, clf-c02]
created: 2026-05-26
updated: 2026-05-26
sources: 1
---

# Amazon GuardDuty

Serviço da [[entities/aws|AWS]] de **detecção inteligente de ameaças** que monitora continuamente a atividade da conta AWS usando Machine Learning para identificar comportamentos suspeitos.

---

## Como funciona

```
[GuardDuty habilitado]
    ↓ Monitora continuamente:
    ├── Logs DNS
    ├── Logs de fluxo VPC
    ├── Eventos no S3
    ├── Dados em volumes EBS
    ├── Atividade de login no RDS
    └── Eventos CloudTrail
    ↓
[Análise com Machine Learning]
    ↓ Detecta padrões anômalos
[Alerta para o usuário]
```

---

## Exemplo de detecção

```
[Situação:]
EC2 que normalmente só processa dados começa a
enviar requisições para IPs em lista negra.

[GuardDuty identifica:]
"Comunicação com IP malicioso conhecido"
"Possível comprometimento da instância i-0abc1234"
"Recomendação: isolar instância e investigar"
```

---

## Inspector vs GuardDuty (par mais cobrado)

| Aspecto | Amazon Inspector | Amazon GuardDuty |
|---|---|---|
| **Foco** | Vulnerabilidades conhecidas | Atividades maliciosas em tempo real |
| **O que analisa** | SO e software da instância | Tráfego de rede e eventos da conta |
| **Fonte de dados** | CVEs, benchmarks | Logs DNS, VPC, CloudTrail |
| **Exemplo** | "Seu SO tem CVE-2024-X" | "IP Y está tentando invadir" |

> Inspector = **o que está vulnerável** no sistema. GuardDuty = **o que está acontecendo** na rede.

---

## Palavra-gatilho na prova

| Enunciado | Resposta |
|---|---|
| "Detectar atividades maliciosas na conta AWS" | GuardDuty |
| "Machine Learning para detectar ameaças" | GuardDuty |
| "Monitorar tráfego de rede por anomalias" | GuardDuty |

---

## Relações

- [[entities/aws]]
- [[entities/amazon-inspector]] — par complementar; Inspector verifica vulnerabilidades estáticas
- [[entities/amazon-vpc]] — monitora logs de fluxo VPC
- [[entities/amazon-s3]] — monitora eventos no S3
- [[concepts/shared-responsibility-model]] — detectar ameaças é responsabilidade do cliente
- [[topics/aws-security]]
- [[sources/clf-c02-aulas1-6-seguranca-nuvem]]
