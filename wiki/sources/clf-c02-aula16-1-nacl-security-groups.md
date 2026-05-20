---
title: "CLF-C02 Aula 16.1 — Network ACLs e Security Groups"
type: source
tags: [aws, vpc, nacl, security-group, redes, segurança, clf-c02]
created: 2026-05-20
updated: 2026-05-20
sources: 1
---

# CLF-C02 Aula 16.1 — Network ACLs e Security Groups

Terceira aula do módulo **Redes em AWS**. Cobre as duas camadas de segurança de rede na AWS.

**Arquivo raw:** `raw/clf-c02-aula16.1-network-acls-security-groups.md`

---

## Duas camadas de segurança

| Camada | Recurso | Escopo |
|---|---|---|
| Nível de sub-rede | [[concepts/network-acl\|Network ACL (NACL)]] | Sub-rede inteira |
| Nível de instância | [[concepts/security-group\|Security Group]] | Instância EC2 |

## Network ACL (NACL)

- **Stateless** — não lembra conexões; verifica regras para **entrada e saída separadamente**
- Opera na **sub-rede** inteira
- Padrão: permite TODO tráfego (permissivo)
- Regras avaliadas em ordem numérica (menor número = maior prioridade)
- Regra de saída explícita necessária mesmo que a entrada seja permitida

## Security Group

- **Stateful** — lembra conexões; saída automática se a entrada foi permitida
- Opera na **instância EC2** (granular)
- Padrão entrada: **bloqueia tudo**; padrão saída: permite tudo
- Só precisa configurar regras de **entrada** — saída para conexões aceitas é automática

## Comportamento stateful vs stateless (conceito mais cobrado)

```
NACL (stateless):
  Entrada porta 80 → precisa regra de ENTRADA explícita
  Resposta sai porta 80 → precisa regra de SAÍDA explícita
  (NACL não sabe que é uma resposta — verifica novamente)

Security Group (stateful):
  Entrada porta 80 → precisa regra de ENTRADA
  Resposta sai porta 80 → AUTOMÁTICO (SG lembrou a conexão aceita)
```

## Fluxo completo de um pacote

```
[Internet]
   ↓
[IGW]
   ↓
[NACL Sub-rede] → verifica regra de entrada
   ↓ se permitido
[Security Group da instância] → verifica regra de entrada
   ↓ se permitido
[Aplicação na EC2]
   ↓ resposta
[Security Group] → automático (stateful)
   ↓
[NACL Sub-rede] → verifica regra de saída (stateless)
   ↓ se permitido
[IGW → Internet]
```

> Um pacote bloqueado pela NACL **não chega** ao Security Group.

## Comparativo NACL vs Security Group

| Aspecto | NACL | Security Group |
|---|---|---|
| Escopo | Sub-rede | Instância EC2 |
| Estado | **Stateless** | **Stateful** |
| Entrada padrão | ✅ Permite tudo | ❌ Bloqueia tudo |
| Saída padrão | ✅ Permite tudo | ✅ Permite tudo |
| Granularidade | Grosseira (sub-rede) | Granular (instância) |
| Regra de saída | Explícita obrigatória | Automática (stateful) |

## Boas práticas

- Use NACL para controle amplo na sub-rede (bloquear IPs suspeitos, faixas de portas)
- Use Security Group para controle granular por instância (porta específica, origem específica)
- As duas camadas se complementam — defesa em profundidade

## Conceitos cobrados na prova

- *"Controla tráfego no nível da sub-rede?"* → NACL
- *"Controla tráfego no nível da instância?"* → Security Group
- *"Qual é stateless?"* → NACL
- *"Qual é stateful?"* → Security Group
- *"Qual permite TODO tráfego de entrada por padrão?"* → NACL
- *"Qual bloqueia TODO tráfego de entrada por padrão?"* → Security Group
- *"Pacote bloqueado na NACL pode passar no Security Group?"* → NÃO

## Relações

- [[concepts/network-acl]]
- [[concepts/security-group]]
- [[entities/amazon-vpc]]
- [[concepts/subnet]]
- [[entities/aws-internet-gateway]]
- [[topics/aws-security]]
- [[topics/cloud-fundamentals]]
