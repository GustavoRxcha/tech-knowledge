---
title: "CLF-C02 Aula 16 — Conectividade com AWS: IGW, VPN e Direct Connect"
type: source
tags: [aws, vpc, igw, vpn, direct-connect, redes, clf-c02]
created: 2026-05-20
updated: 2026-05-20
sources: 1
---

# CLF-C02 Aula 16 — Conectividade com AWS: IGW, VPN e Direct Connect

Segunda aula do módulo **Redes em AWS**. Cobre as três formas de conectar uma VPC ao mundo externo.

**Arquivo raw:** `raw/clf-c02-aula16-conectividade-igw-vpn-directconnect.md`

---

## Internet Gateway (IGW)

[[entities/aws-internet-gateway|Internet Gateway]] — "porta de entrada" da VPC para a internet pública.

- Recebe requisições externas e as direciona para instâncias em sub-redes públicas
- Permite que instâncias façam requisições para a internet (saída)
- Necessário para qualquer acesso internet bidirecional

## VPN via Virtual Private Gateway (VGW)

[[concepts/vpn|VPN]] cria um **túnel criptografado** através da internet pública para conectar data centers corporativos à AWS.

- **Virtual Private Gateway (VGW)** — serviço AWS que implementa a VPN no lado da VPC
- Conexão segura, mas usa a internet pública (velocidade variável)
- Custo-efetivo: sem infraestrutura dedicada
- Casos: data centers corporativos, trabalho remoto, dados sensíveis

## AWS Direct Connect

[[entities/aws-direct-connect|AWS Direct Connect]] — conexão de **fibra óptica dedicada** entre data center e AWS.

- Até 100 Gbps de largura de banda
- Conexão exclusiva e dedicada (não compartilhada)
- Latência muito baixa, SLA de 99,99%
- Setup lento (semanas) e custo elevado
- Casos: transferências massivas (TB+), requisito de baixíssima latência

## Comparativo: IGW vs VPN vs Direct Connect

| Aspecto | IGW | VPN | Direct Connect |
|---|---|---|---|
| Propósito | Acesso internet público | Conexão privada segura | Alto desempenho dedicado |
| Tipo | Pública | Criptografada via internet | Fibra óptica dedicada |
| Velocidade | Variável | Variável | Até 100 Gbps |
| Custo | Incluído | Barato | Caro |
| Setup | Minutos | Horas | Semanas |

## Árvore de decisão

```
Precisa de acesso internet pública?
└─ SIM → Internet Gateway (IGW)

Conectar data center corporativo com segurança?
├─ Dados sensíveis → VPN com Virtual Private Gateway
└─ Grande volume + baixa latência → Direct Connect

Só sub-redes privadas internas?
└─ Nenhum dos três (roteamento interno)
```

## Conceitos cobrados na prova

- *"Qual serviço permite que EC2 acesse a internet?"* → Internet Gateway (IGW)
- *"Como conectar data center corporativo à AWS com segurança?"* → VPN com Virtual Private Gateway
- *"Qual oferece altíssima velocidade dedicada?"* → AWS Direct Connect
- *"Qual é mais barato: VPN ou Direct Connect?"* → VPN (usa internet pública)
- *"Transferir 10TB de data center para AWS. Qual usar?"* → Direct Connect (mais rápido e confiável)
- *"Um desenvolvedor precisa acessar a VPC do escritório. Qual usar?"* → VPN com Virtual Private Gateway

## Relações

- [[entities/aws-internet-gateway]]
- [[entities/aws-direct-connect]]
- [[concepts/vpn]]
- [[entities/amazon-vpc]]
- [[concepts/subnet]]
- [[topics/cloud-fundamentals]]
