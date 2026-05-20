---
title: "VPN (Virtual Private Network)"
type: concept
tags: [vpc, redes, vpn, segurança, conectividade, criptografia]
created: 2026-05-20
updated: 2026-05-20
sources: 1
---

# VPN — Virtual Private Network

**Túnel criptografado** criado sobre a internet pública para conectar redes privadas de forma segura. Na AWS, implementada via **Virtual Private Gateway (VGW)**.

---

## Como funciona na AWS

```
[Data Center Corporativo]
       ↓ dados criptografados
  [Túnel VPN pela internet pública]
       ↓
[Virtual Private Gateway (VGW)]
       ↓
[VPC — Sub-rede privada]
```

## Características

| Característica | Valor |
|---|---|
| Meio físico | Internet pública (criptografada) |
| Criptografia | ✅ Sim — dados protegidos em trânsito |
| Velocidade | Limitada pela velocidade da internet |
| Custo | Baixo (usa infraestrutura de internet já existente) |
| Setup | Horas |

## Virtual Private Gateway (VGW)

O **Virtual Private Gateway** é o componente AWS que termina o túnel VPN no lado da VPC. Ele:

- Aceita conexões VPN do data center corporativo ou de clientes remotos
- Roteia o tráfego para as sub-redes privadas da VPC
- Suporta múltiplas conexões VPN simultâneas

## Quando usar

- ✅ Conectar data centers corporativos à AWS com segurança
- ✅ Trabalho remoto de funcionários
- ✅ Dados sensíveis que precisam de criptografia
- ❌ Quando velocidade máxima é crítica → use [[entities/aws-direct-connect|Direct Connect]]

## Comparativo com Direct Connect

| Aspecto | VPN | Direct Connect |
|---|---|---|
| Infraestrutura | Internet pública | Fibra óptica dedicada |
| Velocidade | Variável | Até 100 Gbps |
| Custo | Baixo | Alto |
| Setup | Horas | Semanas |
| Quando usar | Segurança + flexibilidade | Volume + latência |

## Relações

- [[entities/amazon-vpc]]
- [[entities/aws-direct-connect]]
- [[entities/aws-internet-gateway]]
- [[topics/cloud-fundamentals]]

## Fontes

- [[sources/clf-c02-aula16-connectivity]]
