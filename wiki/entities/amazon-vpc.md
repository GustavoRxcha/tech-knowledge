---
title: "Amazon VPC (Virtual Private Cloud)"
type: entity
tags: [aws, vpc, redes, sub-redes, infraestrutura]
created: 2026-05-20
updated: 2026-05-20
sources: 1
---

# Amazon VPC — Virtual Private Cloud

**Rede virtual privada** da AWS — permite construir redes isoladas dentro da cloud, equivalentes a redes físicas em data centers.

> "Tudo começa com uma VPC" — é o alicerce de qualquer infraestrutura na AWS. O primeiro recurso a configurar antes de EC2, RDS, ou qualquer outro serviço de rede.

---

## O que ela faz

- Isola recursos em uma rede virtual privada dentro da AWS
- Permite segmentar a infraestrutura em [[concepts/subnet|sub-redes]] públicas e privadas
- Controla conectividade entre recursos (EC2, RDS, Lambda, etc.)
- Base para configurar regras de tráfego via [[concepts/network-acl|NACLs]] e [[concepts/security-group|Security Groups]]

## Componentes de uma VPC

| Componente | Função |
|---|---|
| **[[concepts/subnet\|Sub-redes]]** | Segmentos de rede dentro da VPC (pública ou privada) |
| **[[entities/aws-internet-gateway\|Internet Gateway (IGW)]]** | Porta de entrada/saída para a internet pública |
| **[[concepts/network-acl\|Network ACL (NACL)]]** | Firewall de nível de sub-rede (stateless) |
| **[[concepts/security-group\|Security Group]]** | Firewall de nível de instância EC2 (stateful) |
| **Virtual Private Gateway (VGW)** | Endpoint para [[concepts/vpn\|VPN]] e [[entities/aws-direct-connect\|Direct Connect]] |
| **Router interno** | Roteia tráfego entre sub-redes da VPC |

## Sub-redes: pública vs privada

| Tipo | Acesso da internet | Uso típico |
|---|---|---|
| **Pública** | ✅ Sim (via IGW) | Servidores web, APIs, Load Balancers |
| **Privada** | ❌ Não | Bancos de dados, microserviços internos |

## Padrão de alta disponibilidade

Deploy em múltiplas AZs com sub-rede pública + privada em cada AZ:

```
Região
├── AZ-1 → Sub-rede pública (EC2) + Sub-rede privada (RDS)
└── AZ-2 → Sub-rede pública (EC2) + Sub-rede privada (RDS réplica)
```

Se uma AZ falhar, a outra continua atendendo.

## Fluxo de tráfego de fora para dentro

```
[Internet] → [IGW] → [NACL sub-rede] → [Security Group] → [EC2]
```

Dois checkpoints de segurança antes de chegar na instância.

## Relações

- [[entities/aws]]
- [[concepts/subnet]]
- [[entities/aws-internet-gateway]]
- [[concepts/network-acl]]
- [[concepts/security-group]]
- [[concepts/vpn]]
- [[entities/aws-direct-connect]]
- [[concepts/availability-zone]]
- [[concepts/high-availability]]
- [[entities/amazon-ec2]]
- [[topics/cloud-fundamentals]]

## Fontes

- [[sources/clf-c02-aula15-vpc]]
