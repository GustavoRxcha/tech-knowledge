---
title: "AWS Artifact"
type: entity
tags: [aws, conformidade, artifact, lgpd, gdpr, hipaa, clf-c02]
created: 2026-05-26
updated: 2026-05-26
sources: 1
---

# AWS Artifact

Serviço **gratuito** da [[entities/aws|AWS]] para acesso a **documentos de conformidade** e assinatura digital de contratos. Usado quando auditorias exigem comprovação de que a infraestrutura atende a regulações legais.

---

## Dois componentes

### Artifact Agreements (Contratos)

Assinar contratos com a AWS sobre uso de serviços em conformidade com regulações específicas.

```
[Console AWS Artifact]
    ↓
Agreements disponíveis:
├── BAA (HIPAA Business Associate Agreement)
├── GDPR DPA
├── LGPD
└── Outros contratos específicos
    ↓
Você lê e assina digitalmente
```

### Artifact Reports (Relatórios de Auditoria)

Baixar documentos que **comprovam** que a infraestrutura da AWS está em conformidade com normas globais. Gerados por **auditores externos independentes** — não pela própria AWS.

```
[Cenário real:]
Auditoria chega na empresa e pede:
"Comprovem que a infraestrutura atende ao LGPD."

Você → AWS Artifact Reports
    ↓
Solicita relatório de conformidade LGPD
    ↓
Baixa documento gerado por auditor externo
    ↓
Apresenta para auditores ✅
```

---

## Regulações cobertas

| Regulação | Contexto |
|---|---|
| LGPD | Brasil — dados pessoais |
| GDPR | Europa — dados pessoais |
| HIPAA | EUA — saúde |
| SOC 1/2/3 | EUA — financeiro/operacional |
| ISO 27001 | Global — segurança da informação |
| FISC | Japão — financeiro |

---

## Conformidade é compartilhada

```
[Auditoria pede:] "Sua infra atende ao LGPD?"

[Parte AWS] → AWS Artifact Reports comprova a infra física
[Parte Cliente] → Você comprova com sua config de IAM, KMS, etc.
```

Ver [[concepts/shared-responsibility-model]] — a conformidade segue a mesma lógica de responsabilidade compartilhada.

---

## Palavra-gatilho na prova

| Enunciado | Resposta |
|---|---|
| "Baixar relatório de conformidade LGPD/GDPR da AWS" | AWS Artifact Reports |
| "Assinar contrato HIPAA com a AWS" | AWS Artifact Agreements |
| "Conformidade é responsabilidade de quem?" | Compartilhada (AWS + Cliente) |

---

## Relações

- [[entities/aws]]
- [[concepts/shared-responsibility-model]]
- [[entities/aws-organizations]] — Organizations pode exigir conformidade por OU
- [[topics/aws-security]]
- [[sources/clf-c02-aulas1-6-seguranca-nuvem]]
