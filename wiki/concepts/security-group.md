---
title: "Security Group"
type: concept
tags: [vpc, redes, segurança, security-group, firewall, stateful]
created: 2026-05-20
updated: 2026-05-20
sources: 1
---

# Security Group

**Firewall virtual de nível de instância** dentro de uma [[entities/amazon-vpc|VPC]]. Filtra tráfego de entrada e saída de **recursos individuais** (EC2, RDS, etc.). Opera de forma **stateful**.

---

## Características

| Característica | Valor |
|---|---|
| Escopo | Instância EC2 (ou recurso AWS) |
| Stateless / Stateful | **Stateful** |
| Entrada padrão | ❌ Bloqueia todo tráfego |
| Saída padrão | ✅ Permite todo tráfego |
| Associação | Manual — um recurso pode ter múltiplos Security Groups |

## Stateful — o conceito crítico

Security Group guarda estado de conexões. Se uma **entrada** é permitida, a **saída correspondente** é automática:

```
Requisição chega na porta 80:
  → SG verifica regra de ENTRADA: porta 80 permitida? → SIM
  → Conexão é "lembrada"

Resposta sai pela porta 80:
  → SG já sabe: "conexão aceita" → saída AUTOMÁTICA
  → Sem verificar regra de saída
```

> Contraste com [[concepts/network-acl|NACL]] (stateless): a NACL precisa de regra de saída **explícita** para cada direção.

## Comportamento padrão

Security Group recém-criado bloqueia **todo** tráfego de entrada. Você adiciona regras para cada tipo de acesso desejado.

## Exemplo de regras de entrada

```
| Protocolo | Porta | Origem         | Descrição            |
| TCP       | 80    | 0.0.0.0/0      | HTTP de qualquer IP  |
| TCP       | 443   | 0.0.0.0/0      | HTTPS                |
| TCP       | 22    | 10.0.0.0/8     | SSH interno apenas   |
| TCP       | 3306  | <SG-WebServer> | MySQL só do app web  |
```

## NACL vs Security Group

| Aspecto | NACL | Security Group |
|---|---|---|
| Escopo | Sub-rede | Instância EC2 |
| Estado | Stateless | **Stateful** |
| Entrada padrão | Permite tudo | **Bloqueia tudo** |
| Regra de saída | Explícita obrigatória | Automática |
| Granularidade | Grosseira (sub-rede) | Granular (instância) |

## Posição no fluxo de tráfego

```
[Internet] → [IGW] → [NACL Sub-rede] → [Security Group] → [EC2]
```

Segundo checkpoint — opera após a NACL.

## Relações

- [[entities/amazon-vpc]]
- [[concepts/subnet]]
- [[concepts/network-acl]]
- [[entities/amazon-ec2]]
- [[topics/cloud-fundamentals]]
- [[topics/aws-security]]

## Fontes

- [[sources/clf-c02-aula16-1-nacl-security-groups]]
