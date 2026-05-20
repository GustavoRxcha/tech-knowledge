---
title: "Amazon EC2 (Elastic Compute Cloud)"
type: entity
tags: [aws, ec2, computação, vm, iaas]
created: 2026-05-18
updated: 2026-05-20
sources: 5
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

## Contexto de rede

Toda instância EC2 reside dentro de uma [[concepts/subnet|sub-rede]] de uma [[entities/amazon-vpc|VPC]]. A segurança de rede é gerenciada em duas camadas:

- **[[concepts/security-group|Security Group]]** — firewall de nível de instância (stateful), associado diretamente à EC2
- **[[concepts/network-acl|NACL]]** — firewall de nível de sub-rede (stateless), aplica-se automaticamente

Para acesso público, a EC2 deve estar em sub-rede pública com rota para um [[entities/aws-internet-gateway|Internet Gateway]].

## Lacunas conhecidas

Sem cobertura ainda de:
- Tipos de instância por nome de família (t3, m5, c5, r5, etc.)
- EBS (block storage) em detalhe
- Key pairs SSH / Elastic IP
- Spot, Reserved, Savings Plans (modelos de pricing)
- NAT Gateway (saída internet de sub-redes privadas)

## Fontes

- [[sources/aws-course-04-iam-groups]] — exemplo de acesso negado
- [[sources/clf-c02-aula03-service-models]] — citado como exemplo canônico de IaaS
- [[sources/clf-c02-aula06-regions-az]] — escopo de AZ
- [[sources/clf-c02-aula09-ec2-instance-types]] — AMI, lifecycle, 5 famílias de instância, pricing

## AMI — Amazon Machine Image

"Molde" a partir do qual uma instância é criada. Define: SO (Amazon Linux, Ubuntu, Windows...), configurações iniciais, softwares pré-instalados (em AMIs customizadas).

## Ciclo de vida de uma instância

| Estado | Descrição |
|---|---|
| **Pendente** | Inicializando após ser lançada |
| **Executando** | Rodando e disponível |
| **Reiniciando** | Reboot — mantém IP e dados |
| **Parada** | Desligada — não cobra por compute, mas cobra pelo armazenamento |
| **Hibernada** | Salva o estado da memória em disco e para; retoma do ponto parado |
| **Encerrada** | Destruída permanentemente — não pode ser recuperada |

## 5 famílias de instância

| Família | Foco | Palavra-chave | Exemplos de uso |
|---|---|---|---|
| **Uso Geral** | Equilíbrio CPU/RAM/Rede | "padrão", "balanceado" | Web servers, apps gerais |
| **Computação** | Alto desempenho de CPU | "processamento", "lote" | Batch, jogos, modelagem científica |
| **Memória** | Grande quantidade de RAM | "em memória", "tempo real" | Redis, SAP HANA, grandes datasets |
| **Acelerada** | GPU / hardware especializado | "gráficos", "ML", "GPU" | Deep Learning, rendering |
| **Armazenamento** | I/O de disco intensivo | "leitura/gravação", "OLTP" | Data warehouses, OLTP |

## Modelo de precificação

Paga por hora ou por segundo conforme o uso. Instância **parada = sem cobrança por computação** (mas cobra pelo armazenamento EBS).

## Escopo de infraestrutura

O EC2 é um serviço de **escopo de AZ** — cada instância roda em uma [[concepts/availability-zone|Zona de Disponibilidade]] específica. Se a AZ falhar, a instância nela hospedada fica indisponível.

> Boa prática: sempre provisionar instâncias em **pelo menos 2 AZs** para garantir alta disponibilidade.

## Relações

- [[entities/aws]]
- [[concepts/iaas]]
- [[concepts/virtualization]]
- [[concepts/principle-of-least-privilege]]
- [[concepts/availability-zone]] — EC2 tem escopo de AZ
- [[concepts/high-availability]] — requer múltiplas AZs
- [[entities/amazon-ec2-auto-scaling]] — escala instâncias EC2 automaticamente
- [[entities/elastic-load-balancing]] — distribui tráfego entre instâncias EC2
- [[entities/aws-elastic-beanstalk]] — provisiona EC2 por baixo
- [[entities/amazon-vpc]] — EC2 reside dentro de uma VPC
- [[concepts/subnet]] — EC2 está em sub-rede pública ou privada
- [[concepts/security-group]] — firewall de nível de instância
- [[concepts/network-acl]] — firewall de nível de sub-rede
- [[topics/cloud-fundamentals]]
- [[topics/aws-security]]
