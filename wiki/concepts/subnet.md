---
title: "Sub-rede (Subnet)"
type: concept
tags: [vpc, redes, sub-rede, subnet, aws]
created: 2026-05-20
updated: 2026-05-20
sources: 1
---

# Sub-rede (Subnet)

Segmento de rede **dentro de uma [[entities/amazon-vpc|VPC]]** que divide a infraestrutura em zonas lógicas. Toda instância EC2, RDS ou recurso de rede reside dentro de uma sub-rede.

---

## Tipos

### Sub-rede Pública

- Possui **rota para o [[entities/aws-internet-gateway|Internet Gateway]]**
- Recursos podem receber e enviar tráfego da internet
- Ideal para: servidores web, APIs públicas, Load Balancers

### Sub-rede Privada

- **Sem rota para Internet Gateway**
- Recursos isolados da internet; comunicam-se apenas dentro da VPC
- Ideal para: bancos de dados, microserviços internos, recursos sensíveis

## Por que separar?

```
❌ Banco de dados em sub-rede pública:
   Acessível da internet → risco de segurança

✅ Banco de dados em sub-rede privada:
   Isolado da internet → só aplicações internas acessam
```

> **Regra de ouro:** bancos de dados e recursos sensíveis **nunca** em sub-redes públicas.

## Escopo de AZ

Cada sub-rede reside em **uma única [[concepts/availability-zone|Zona de Disponibilidade]]**. Para [[concepts/high-availability|alta disponibilidade]], crie pares de sub-redes em múltiplas AZs.

Padrão multi-AZ:

```
AZ-1: sub-rede pública + sub-rede privada
AZ-2: sub-rede pública + sub-rede privada
```

## Controles de tráfego por camada

| Nível | Controle | Estado |
|---|---|---|
| Sub-rede | [[concepts/network-acl\|Network ACL (NACL)]] | Stateless |
| Instância | [[concepts/security-group\|Security Group]] | Stateful |

## Relações

- [[entities/amazon-vpc]]
- [[concepts/network-acl]]
- [[concepts/security-group]]
- [[entities/aws-internet-gateway]]
- [[concepts/availability-zone]]
- [[concepts/high-availability]]
- [[entities/amazon-ec2]]

## Fontes

- [[sources/clf-c02-aula15-vpc]]
