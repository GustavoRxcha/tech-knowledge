---
title: "AWS Internet Gateway (IGW)"
type: entity
tags: [aws, vpc, igw, redes, internet, conectividade]
created: 2026-05-20
updated: 2026-05-20
sources: 1
---

# AWS Internet Gateway (IGW)

**Porta de entrada e saída** da [[entities/amazon-vpc|VPC]] para a internet pública. Componente necessário para qualquer instância EC2 que precise de acesso direto à internet.

---

## O que faz

- Recebe requisições externas (entrada) e as direciona para instâncias em sub-redes públicas
- Permite que instâncias façam requisições para a internet (saída)
- Bidirecional: entrada e saída
- Um IGW por VPC

## Pré-requisitos para acesso internet via IGW

Para uma instância EC2 acessar a internet:
1. Estar em uma **[[concepts/subnet|sub-rede pública]]**
2. A sub-rede deve ter **rota para o IGW** na tabela de roteamento
3. A instância deve ter **IP público ou Elastic IP**

## Quando usar vs não usar

| Situação | Usar IGW? |
|---|---|
| Servidor web que recebe requisições externas | ✅ Sim |
| API pública | ✅ Sim |
| Load Balancer público | ✅ Sim |
| Banco de dados | ❌ Não — sub-rede privada |
| Serviço interno | ❌ Não — comunicação interna não precisa de IGW |

## Comparativo com os outros serviços de conectividade

| Serviço | Propósito | Quando usar |
|---|---|---|
| **IGW** | Internet pública → VPC | Recursos que precisam de acesso internet |
| **VPN (VGW)** | Data center → VPC criptografado | Dados sensíveis, escritório corporativo |
| **Direct Connect** | Data center → VPC fibra dedicada | Grande volume, baixíssima latência |

## Relações

- [[entities/amazon-vpc]]
- [[concepts/subnet]]
- [[entities/amazon-ec2]]
- [[concepts/vpn]]
- [[entities/aws-direct-connect]]
- [[topics/cloud-fundamentals]]

## Fontes

- [[sources/clf-c02-aula16-connectivity]]
