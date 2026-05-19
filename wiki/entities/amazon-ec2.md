---
title: "Amazon EC2 (Elastic Compute Cloud)"
type: entity
tags: [aws, ec2, computação, vm, iaas]
created: 2026-05-18
updated: 2026-05-19
sources: 2
---

# Amazon EC2 — Elastic Compute Cloud

Serviço de **máquinas virtuais** da [[entities/aws|AWS]]. Exemplo canônico de **[[concepts/iaas|IaaS]]** — você escolhe o tamanho da instância, SO, configura rede e segurança, instala e mantém tudo acima da camada de virtualização.

---

## Posicionamento como [[concepts/iaas|IaaS]]

| Camada | Quem gerencia |
|---|---|
| Aplicação / dados / runtime / SO | Você |
| Virtualização / servidor físico / storage / rede | AWS |

Citado em [[sources/clf-c02-aula03-service-models]] como exemplo de IaaS na trilha CLF-C02.

## O que você decide

- **Tamanho** da instância (CPU, RAM, disco) — família de instâncias (t3.micro, m5.large, etc.).
- **Sistema operacional** — Amazon Linux, Ubuntu, Windows Server, etc.
- **Rede** — VPC, subnet, security groups.
- **Storage** — EBS volumes.
- **Patches e atualizações** do SO.
- **Software instalado** dentro da VM.

## Aparições anteriores no wiki

Em [[sources/aws-course-04-iam-groups]] o EC2 foi usado apenas como **exemplo de acesso negado**: o usuário do grupo `developers` (sem policy de EC2) recebeu `You are not authorized to perform this operation.` ao tentar acessar.

Isso ilustra dois conceitos simultâneos:
- [[concepts/principle-of-least-privilege]] em ação.
- Que [[entities/aws-iam|IAM]] controla acesso a serviços inteiros, não só ações dentro do serviço.

## Lacunas conhecidas

Sem cobertura ainda de:
- Tipos de instância detalhados (t3, m5, c5, r5, etc.)
- AMIs (Amazon Machine Images)
- Security Groups vs NACLs
- EBS (block storage)
- VPC, subnets, internet gateway
- Key pairs SSH
- Elastic IP
- Auto Scaling Groups
- Spot, Reserved, Savings Plans (pricing models)

> [!question] Aprofundar quando o curso cobrir EC2 dedicadamente — provável próximo módulo prático ou do CLF-C02.

## Fontes

- [[sources/aws-course-04-iam-groups]] — exemplo de acesso negado
- [[sources/clf-c02-aula03-service-models]] — citado como exemplo canônico de IaaS

## Relações

- [[entities/aws]]
- [[concepts/iaas]]
- [[concepts/virtualization]]
- [[concepts/principle-of-least-privilege]]
- [[entities/aws-elastic-beanstalk]] — provisiona EC2 por baixo
- [[topics/cloud-fundamentals]]
- [[topics/aws-security]]
