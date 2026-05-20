---
title: "Network ACL (NACL)"
type: concept
tags: [vpc, redes, segurança, nacl, firewall, stateless]
created: 2026-05-20
updated: 2026-05-20
sources: 1
---

# Network ACL (NACL)

**Firewall de nível de sub-rede** dentro de uma [[entities/amazon-vpc|VPC]]. Filtra tráfego de entrada e saída de uma [[concepts/subnet|sub-rede]] inteira. Opera de forma **stateless**.

---

## Características

| Característica | Valor |
|---|---|
| Escopo | Sub-rede inteira |
| Stateless / Stateful | **Stateless** |
| Entrada padrão | ✅ Permite todo tráfego |
| Saída padrão | ✅ Permite todo tráfego |
| Avaliação de regras | Ordem numérica (menor = maior prioridade) |
| Associação | Automática a todas as instâncias da sub-rede |

## Stateless — o conceito crítico

NACL não guarda estado de conexões. Para cada pacote, verifica as regras **de forma independente**:

```
Requisição chega na porta 80:
  → NACL verifica regra de ENTRADA: porta 80 permitida? → SIM → entra

Resposta sai pela porta 80:
  → NACL verifica NOVAMENTE regra de SAÍDA: porta 80 permitida?
  → Precisa de regra de saída explícita
```

> Contraste com [[concepts/security-group|Security Group]] (stateful): se a entrada é permitida, a saída correspondente é **automática**.

## Comportamento padrão

NACL padrão (recém-criada) permite **todo** tráfego de entrada e saída. Customização necessária para restringir acesso.

## Estrutura de uma regra

```
| Prioridade | Protocolo | Porta | Origem      | Ação  |
| 100        | TCP       | 80    | 0.0.0.0/0   | Allow |
| 110        | TCP       | 443   | 0.0.0.0/0   | Allow |
| 120        | TCP       | 22    | 10.0.0.0/8  | Allow |
| 32767      | ALL       | ALL   | 0.0.0.0/0   | Deny  | ← regra final implícita
```

## NACL vs Security Group

| Aspecto | NACL | Security Group |
|---|---|---|
| Escopo | Sub-rede | Instância EC2 |
| Estado | **Stateless** | Stateful |
| Entrada padrão | Permite tudo | Bloqueia tudo |
| Regra de saída | Explícita obrigatória | Automática |
| Granularidade | Grosseira | Granular |

## Posição no fluxo de tráfego

```
[Internet] → [IGW] → [NACL Sub-rede] → [Security Group] → [EC2]
```

Primeiro checkpoint. Se bloquear, o pacote não chega ao Security Group.

## Relações

- [[entities/amazon-vpc]]
- [[concepts/subnet]]
- [[concepts/security-group]]
- [[topics/cloud-fundamentals]]
- [[topics/aws-security]]

## Fontes

- [[sources/clf-c02-aula16-1-nacl-security-groups]]
