---
title: "Cloud Fundamentals (CLF-C02)"
type: topic
tags: [cloud, fundamentos, clf-c02, certificação, conceitual, segurança]
created: 2026-05-19
updated: 2026-05-26
sources: 18
---

# Cloud Fundamentals — Trilha CLF-C02

Página de tópico que agrupa todo o conteúdo conceitual do preparatório **AWS Cloud Practitioner (CLF-C02)** — fundamentos de cloud computing, modelos de serviço, modelos de implantação, benefícios.

> Esta trilha é **conceitual e voltada para certificação**. Complementa a trilha hands-on do outro curso, que está agrupada em [[topics/aws-security]] e nos serviços (EC2, S3, Lambda, etc.).

---

## Mapa do conteúdo

### Conceito raiz
- [[concepts/cloud-computing]] — definição AWS, pay-as-you-go, evolução pré-cloud

### Benefícios (5 oficiais)
- [[concepts/cloud-benefits]] — CapEx→OpEx, elasticidade, escala, agilidade, alcance global
- [[concepts/elasticity]] — em destaque, conceito muito cobrado

### Modelos de serviço (nível de gerenciamento)
- [[concepts/iaas]] — Infrastructure as a Service ([[entities/amazon-ec2|EC2]])
- [[concepts/paas]] — Platform as a Service ([[entities/aws-elastic-beanstalk|Elastic Beanstalk]])
- [[concepts/saas]] — Software as a Service (Gmail, Salesforce)

### Modelos de implantação (onde roda)
- [[concepts/on-premises]] — local, controle total, alto custo fixo
- [[concepts/hybrid-cloud]] — local + nuvem, migração ou compliance parcial
- [[concepts/private-cloud]] — local + tecnologia cloud (VMware, Outposts)
- Nuvem pública — coberto via [[concepts/cloud-computing]] e [[entities/aws]]

### Tecnologias de base
- [[concepts/virtualization]] — hypervisor, fundação técnica da cloud

### Infraestrutura Global AWS
- [[concepts/aws-region]] — Região: agrupamento geográfico, isolamento de dados, compliance (LGPD/GDPR), 4 critérios de escolha
- [[concepts/availability-zone]] — AZ: data center isolado dentro de uma Região; escopo de AZ vs regional
- [[concepts/edge-location]] — Ponto de Presença / Edge Location / Local de Borda: cache, CDN, DNS
- [[concepts/high-availability]] — serviço continua com falha parcial
- [[concepts/fault-tolerance]] — arquitetura resiste a falhas

### Serviços de borda e CDN
- [[entities/amazon-cloudfront]] — CDN da AWS; usa Edge Locations
- [[entities/amazon-route53]] — DNS gerenciado; opera nos Edge Locations

### Provisionamento e IaC
- [[concepts/aws-cli]] — CLI; automação via terminal; `aws configure`
- [[concepts/infrastructure-as-code]] — IaC: infra declarada em arquivo, versionável, reprodutível
- [[entities/aws-cloudformation]] — IaC nativo AWS; JSON/YAML templates; rollback automático

### Computação na AWS — EC2
- [[entities/amazon-ec2]] — VMs; 5 famílias (Geral, Computação, Memória, Acelerada, Armazenamento); AMI; lifecycle
- [[entities/amazon-ec2-auto-scaling]] — ASG; min/desejado/max; escalabilidade preditiva vs dinâmica; multi-AZ
- [[entities/elastic-load-balancing]] — ELB; ALB/NLB/GWLB; health checks; escopo regional
- [[concepts/auto-scaling]] — horizontal vs vertical; parâmetros de capacidade
- [[concepts/load-balancing]] — distribuição de tráfego entre instâncias

### Computação na AWS — Mensageria
- [[entities/amazon-sqs]] — fila FIFO; produtor/consumidor; resiliência
- [[entities/amazon-sns]] — Pub/Sub; tópicos; múltiplos assinantes simultâneos; fanout
- [[concepts/microservices]] — desacoplamento entre serviços independentes
- [[concepts/pub-sub]] — Publisher/Subscriber; padrão implementado pelo SNS

### Computação na AWS — Serverless e Containers
- [[entities/aws-lambda]] — execução por evento; triggers; pay-per-use; ecossistema serverless
- [[entities/amazon-ecr]] — repositório de imagens Docker
- [[entities/amazon-ecs]] — orquestrador nativo AWS
- [[entities/amazon-eks]] — Kubernetes gerenciado na AWS
- [[entities/aws-fargate]] — infraestrutura serverless para containers
- [[concepts/containers]] — Docker; portabilidade; imagens; Dockerfile

### Redes na AWS — VPC e Conectividade
- [[entities/amazon-vpc]] — Rede virtual privada; alicerce de toda infraestrutura; "tudo começa com uma VPC"
- [[concepts/subnet]] — Sub-rede pública (internet) vs privada (isolada)
- [[entities/aws-internet-gateway]] — IGW; porta de entrada/saída da VPC para internet pública
- [[concepts/vpn]] — Túnel criptografado; Virtual Private Gateway; conecta data center corporativo
- [[entities/aws-direct-connect]] — Fibra óptica dedicada; até 100 Gbps; baixíssima latência

### Redes na AWS — Segurança
- [[concepts/network-acl]] — NACL; firewall de sub-rede; stateless; padrão permissivo
- [[concepts/security-group]] — Firewall de instância EC2; stateful; padrão entrada bloqueada

---

## Atalho para a prova

### Mapeamento cenário → conceito

| Palavra-gatilho no enunciado | Resposta provável |
|---|---|
| "custo inicial", "investimento em hardware" | Benefício: CapEx → OpEx ([[concepts/cloud-benefits]]) |
| "Black Friday", "pico de tráfego", "auto scaling" | [[concepts/elasticity\|Elasticidade]] |
| "lançar MVP rápido" | Benefício: agilidade |
| "latência para usuários globais" | Benefício: alcance global |
| "controle sobre SO e runtime" | [[concepts/iaas\|IaaS]] |
| "deploy sem gerenciar infra" | [[concepts/paas\|PaaS]] |
| "pronto pra usar, só login" | [[concepts/saas\|SaaS]] |
| "data center próprio" | [[concepts/on-premises]] |
| "migração gradual", "parte local + nuvem" | [[concepts/hybrid-cloud]] |
| "VMware/OpenStack local" | [[concepts/private-cloud]] |
| "latência para usuários globais", "CDN" | [[entities/amazon-cloudfront\|CloudFront]] + [[concepts/edge-location\|Edge Locations]] |
| "tradução de domínio DNS" | [[entities/amazon-route53\|Route 53]] |
| "infra a partir de arquivo JSON/YAML" | [[entities/aws-cloudformation\|CloudFormation]] |
| "deploy de app sem gerenciar EC2" | [[entities/aws-elastic-beanstalk\|Elastic Beanstalk]] |
| "dados legais devem ficar no Brasil" | Compliance → Região `sa-east-1` |
| "tolerância a falhas de data center" | [[concepts/availability-zone\|Múltiplas AZs]] |
| "aplicação web genérica sem requisito específico" | EC2 [[entities/amazon-ec2\|Uso Geral]] |
| "banco de dados em memória, Redis, SAP HANA" | EC2 [[entities/amazon-ec2\|Memória]] |
| "ML, GPU, Deep Learning" | EC2 [[entities/amazon-ec2\|Acelerada]] |
| "data warehouse, OLTP com I/O intensivo" | EC2 [[entities/amazon-ec2\|Armazenamento]] |
| "escala automática, pico de tráfego" | [[entities/amazon-ec2-auto-scaling\|EC2 Auto Scaling]] |
| "distribuição de tráfego entre instâncias" | [[entities/elastic-load-balancing\|ELB]] |
| "comunicação assíncrona, fila de mensagens" | [[entities/amazon-sqs\|SQS]] |
| "notificar múltiplos sistemas simultaneamente" | [[entities/amazon-sns\|SNS]] |
| "armazenar imagens Docker na AWS" | [[entities/amazon-ecr\|ECR]] |
| "executar containers Docker (nativo AWS)" | [[entities/amazon-ecs\|ECS]] |
| "Kubernetes gerenciado" | [[entities/amazon-eks\|EKS]] |
| "containers sem gerenciar servidores" | [[entities/aws-fargate\|Fargate]] |
| "rede virtual privada na AWS" | [[entities/amazon-vpc\|VPC]] |
| "primeiro passo ao construir infraestrutura na AWS" | [[entities/amazon-vpc\|VPC]] (criar a VPC) |
| "banco de dados isolado da internet" | [[concepts/subnet\|Sub-rede privada]] |
| "EC2 precisa de acesso internet" | [[entities/aws-internet-gateway\|Internet Gateway (IGW)]] |
| "conectar data center corporativo com segurança" | [[concepts/vpn\|VPN com Virtual Private Gateway]] |
| "altíssima velocidade, fibra dedicada, data center" | [[entities/aws-direct-connect\|AWS Direct Connect]] |
| "controle de tráfego no nível da sub-rede" | [[concepts/network-acl\|Network ACL (NACL)]] — stateless |
| "controle de tráfego no nível da instância" | [[concepts/security-group\|Security Group]] — stateful |
| "stateless, firewall de sub-rede" | [[concepts/network-acl\|NACL]] |
| "stateful, firewall de instância" | [[concepts/security-group\|Security Group]] |

### Pares que mais caem

- **[[concepts/iaas|IaaS]] vs [[concepts/paas|PaaS]]** — quem gerencia SO + runtime?
- **[[concepts/on-premises|On-premises]] vs [[concepts/private-cloud|Private Cloud]]** — usa tecnologia cloud localmente?
- **[[concepts/hybrid-cloud|Híbrido]] vs Público** — tem componente local ou só na cloud?

---

## Estado da trilha

| Aula | Tema | Source |
|---|---|---|
| 01 | O que é Cloud Computing | ✅ [[sources/clf-c02-aula01-cloud-computing]] |
| 02 | Benefícios da Cloud | ✅ [[sources/clf-c02-aula02-cloud-benefits]] |
| 03 | Modelos de Serviço | ✅ [[sources/clf-c02-aula03-service-models]] |
| 04 | Modelos de Implantação | ✅ [[sources/clf-c02-aula04-deployment-models]] |
| 05 | Infraestrutura Global AWS | ✅ [[sources/clf-c02-aula05-global-infrastructure]] |
| 06 | Regiões e Zonas de Disponibilidade | ✅ [[sources/clf-c02-aula06-regions-az]] |
| 07 | Edge Locations, CloudFront e Route 53 | ✅ [[sources/clf-c02-aula07-edge-cloudfront-route53]] |
| 08 | Provisionamento: Console, CLI, SDK, EB, CloudFormation | ✅ [[sources/clf-c02-aula08-provisioning]] |
| 09 | EC2: AMI, lifecycle, 5 famílias de instância | ✅ [[sources/clf-c02-aula09-ec2-instance-types]] |
| 10 | EC2 Auto Scaling: ASG, preditivo vs dinâmico, multi-AZ | ✅ [[sources/clf-c02-aula10-ec2-auto-scaling]] |
| 11 | Elastic Load Balancing: ELB, ALB/NLB/GWLB, health checks | ✅ [[sources/clf-c02-aula11-elastic-load-balancing]] |
| 12 | Mensageria: SQS (fila), SNS (Pub/Sub), fanout | ✅ [[sources/clf-c02-aula12-messaging-sqs-sns]] |
| 13 | Serverless: Lambda, triggers, pricing, ecossistema | ✅ [[sources/clf-c02-aula13-serverless-lambda]] |
| 14 | Containers: Docker, ECR, ECS, EKS, Fargate | ✅ [[sources/clf-c02-aula14-containers-ecr-ecs-eks-fargate]] |
| 15 | VPC: sub-redes públicas/privadas, multi-AZ | ✅ [[sources/clf-c02-aula15-vpc]] |
| 16 | Conectividade: IGW, VPN (VGW), Direct Connect | ✅ [[sources/clf-c02-aula16-connectivity]] |
| 16.1 | Network ACLs (stateless) e Security Groups (stateful) | ✅ [[sources/clf-c02-aula16-1-nacl-security-groups]] |
| 17-24 | Armazenamento e Banco de Dados (EBS, S3, EFS, RDS, Aurora, DynamoDB, DocumentDB, Neptune, QLDB, DAX, ElastiCache, Redshift) | ✅ [[sources/clf-c02-aulas17-24-storage-databases]] |
| 1-6 (seg.) | Segurança na Nuvem: Shared Responsibility, KMS, IAM, Organizations, Artifact, WAF, Shield, Inspector, GuardDuty | ✅ [[sources/clf-c02-aulas1-6-seguranca-nuvem]] |
| próximos | (Well-Architected, Pricing, suporte) | 🔜 |

### Segurança na Nuvem AWS
- [[concepts/shared-responsibility-model]] — AWS: DA nuvem (infra); Cliente: NA nuvem (dados, acesso, config)
- [[entities/aws-kms]] — criptografia de chaves; dados em repouso e em trânsito
- [[concepts/encryption]] — data at rest vs data in transit
- [[entities/aws-organizations]] — múltiplas contas; faturamento consolidado; gratuito
- [[concepts/scp]] — Service Control Policies; teto de permissões por OU
- [[entities/aws-artifact]] — relatórios de conformidade (LGPD, GDPR, HIPAA) e contratos digitais
- [[entities/aws-waf]] — firewall L7 para apps web; SQL Injection, XSS
- [[entities/aws-shield]] — DDoS; Standard (gratuito) vs Advanced (pago)
- [[entities/amazon-inspector]] — scan de CVEs em EC2 e containers
- [[entities/amazon-guardduty]] — detecção de ameaças via ML; logs DNS, VPC, CloudTrail

## Lacunas

- Well-Architected Framework — sem cobertura ainda.
- Billing e AWS Pricing & Support Plans — sem cobertura.
- Redes avançadas: NAT Gateway, VPC Peering, PrivateLink, Route Tables detalhadas.
- CloudTrail — mencionado como fonte do GuardDuty, sem página própria.
- Secrets Manager, Security Hub, IAM Access Analyzer — sem cobertura.

## Fontes

- [[sources/clf-c02-aula01-cloud-computing]]
- [[sources/clf-c02-aula02-cloud-benefits]]
- [[sources/clf-c02-aula03-service-models]]
- [[sources/clf-c02-aula04-deployment-models]]
- [[sources/clf-c02-aula05-global-infrastructure]]
- [[sources/clf-c02-aula06-regions-az]]
- [[sources/clf-c02-aula07-edge-cloudfront-route53]]
- [[sources/clf-c02-aula08-provisioning]]
- [[sources/clf-c02-aula09-ec2-instance-types]]
- [[sources/clf-c02-aula10-ec2-auto-scaling]]
- [[sources/clf-c02-aula11-elastic-load-balancing]]
- [[sources/clf-c02-aula12-messaging-sqs-sns]]
- [[sources/clf-c02-aula13-serverless-lambda]]
- [[sources/clf-c02-aula14-containers-ecr-ecs-eks-fargate]]
- [[sources/clf-c02-aula15-vpc]]
- [[sources/clf-c02-aula16-connectivity]]
- [[sources/clf-c02-aula16-1-nacl-security-groups]]
- [[sources/clf-c02-aulas1-6-seguranca-nuvem]]
