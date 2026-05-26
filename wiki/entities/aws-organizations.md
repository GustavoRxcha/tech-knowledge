---
title: "AWS Organizations"
type: entity
tags: [aws, multi-conta, organizations, scp, faturamento, clf-c02]
created: 2026-05-26
updated: 2026-05-26
sources: 1
---

# AWS Organizations

Serviço **gratuito** da [[entities/aws|AWS]] para gerenciar **múltiplas contas AWS** de forma centralizada. Resolve o problema de escala quando uma única conta não é mais suficiente.

---

## Problema resolvido

Uma única conta AWS cria dois problemas ao crescer:

1. **Custos** — impossível separar quanto cada time gasta
2. **Limites de serviço** — cada conta tem limites de VPCs, instâncias EC2, etc.

Múltiplas contas separadas resolvem os limites, mas criam novo problema: vários logins, vários consoles, vários faturamentos. Organizations resolve isso.

---

## Estrutura hierárquica

```
[Conta Gerenciadora (Management Account)]
        ↓
[Organização]
├── [OU: Produção]
│   ├── Conta Prod Web
│   └── Conta Prod API
├── [OU: Desenvolvimento]
│   ├── Conta Dev Web
│   └── Conta Dev API
└── [OU: Operações]
    └── Conta Monitoring
```

> OU = Organizational Unit (Unidade Organizacional)

---

## Recursos principais

### Gerenciamento Centralizado
- Uma **Management Account** gerencia todas as outras
- Visibilidade consolidada de todas as contas
- Criação de novas contas automatizada via API

### Faturamento Consolidado
- Uma única fatura para todas as contas da organização
- Relatórios de custo por conta e por serviço
- Volume de uso **combinado** pode gerar descontos da AWS

### SCP — Service Control Policies
Políticas aplicadas em nível de OU que **restringem** quais serviços podem ser usados.

```
[SCP aplicada ao OU: Operações]
├── Proibido: acessar S3
├── Proibido: criar EC2 fora de us-east-1
└── Permitido: apenas serviços necessários

→ Qualquer usuário novo no grupo herda essas restrições automaticamente
```

SCPs funcionam como teto de permissões — mesmo um administrador da conta-filha não pode ultrapassar o que a SCP permite.

---

## Comparativo

| Aspecto | Sem Organizations | Com Organizations |
|---|---|---|
| Contas | Gerenciadas individualmente | Gerenciadas centralmente |
| Faturamento | Múltiplas faturas | Fatura consolidada |
| Limites | Uma conta pode esgotar | Distribuído entre contas |
| Políticas | Por conta | Centralizadas via SCP |
| Custo | — | **Gratuito** |

---

## Palavra-gatilho na prova

| Enunciado | Resposta |
|---|---|
| "Gerenciar múltiplas contas AWS" | AWS Organizations |
| "Fatura única para várias contas" | Faturamento Consolidado (Organizations) |
| "Restringir serviços por unidade organizacional" | SCP |
| "É gratuito?" | SIM |

---

## Relações

- [[entities/aws]]
- [[concepts/shared-responsibility-model]]
- [[concepts/scp]] — Service Control Policies
- [[topics/aws-security]]
- [[sources/clf-c02-aulas1-6-seguranca-nuvem]]
