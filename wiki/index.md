---
title: "Index"
type: overview
updated: 2026-05-20
---

# Index

Catálogo principal de todas as páginas do wiki. O LLM lê isto primeiro para navegar.

---

## Sources

### Trilha hands-on — Módulo IAM
- [[sources/aws-course-01-mfa-iam-setup]] — Setup inicial: MFA no root e criação do primeiro usuário IAM (2026-05-18)
- [[sources/aws-course-02-iam-policies-tags-credentials]] — Estrutura de policies, tags e manuseio de credenciais IAM (2026-05-18)
- [[sources/aws-course-03-iam-user-login-inline-policy]] — Login com usuário IAM e criação de inline policy para S3 (2026-05-18)
- [[sources/aws-course-04-iam-groups]] — Grupos IAM, atribuição de permissões por grupo e validação de menor privilégio (2026-05-18)
- [[sources/aws-course-05-iam-roles-custom-policies-lambda]] — IAM Roles, policies personalizadas e Lambda acessando S3 (2026-05-18)
- [[sources/aws-course-06-iam-permissions-validation-s3]] — Validação prática de permissões no S3 e encerramento do módulo IAM (2026-05-18)

### Trilha hands-on — Módulo Serverless (DynamoDB + Lambda + API Gateway)
- [[sources/aws-course-cognito-intro]] — AWS Cognito conceitual: User Pools, JWT, integração com IAM (2026-05-19)
- [[sources/aws-course-dynamo-01-table-lambda-intro]] — Criação de tabela DynamoDB e introdução à função Lambda (2026-05-19)
- [[sources/aws-course-dynamo-02-lambda-crud]] — Lambda Node.js (+Python) com CRUD completo no DynamoDB (2026-05-19)
- [[sources/aws-course-apigateway-01-api-routes]] — Criação de HTTP API e rotas no API Gateway (2026-05-19)
- [[sources/aws-course-apigateway-02-integration-postman]] — Integração Lambda, correção de IAM e testes com Postman (2026-05-19)

### Trilha CLF-C02 — Fundamentos de Cloud
- [[sources/clf-c02-aula01-cloud-computing]] — O que é Cloud Computing: definição AWS, pré-cloud, pay-as-you-go (2026-05-19)
- [[sources/clf-c02-aula02-cloud-benefits]] — Os 5 benefícios oficiais da cloud pela AWS (2026-05-19)
- [[sources/clf-c02-aula03-service-models]] — Modelos de serviço: IaaS, PaaS, SaaS (2026-05-19)
- [[sources/clf-c02-aula04-deployment-models]] — Modelos de implantação: on-premises, híbrido, cloud, privada (2026-05-19)

### Trilha CLF-C02 — Infraestrutura Global AWS
- [[sources/clf-c02-aula05-global-infrastructure]] — Hierarquia da infra global: Regiões, AZs, Edge Locations, formas de provisionar (2026-05-20)
- [[sources/clf-c02-aula06-regions-az]] — Regiões: isolamento, compliance (LGPD/GDPR), 4 critérios; AZs: escopo de serviço (2026-05-20)
- [[sources/clf-c02-aula07-edge-cloudfront-route53]] — Edge Locations, CloudFront (CDN), Route 53 (DNS) (2026-05-20)
- [[sources/clf-c02-aula08-provisioning]] — Console, CLI, SDKs (boto3), Elastic Beanstalk, CloudFormation (IaC) (2026-05-20)

### Trilha CLF-C02 — Computação na AWS
- [[sources/clf-c02-aula09-ec2-instance-types]] — EC2: AMI, lifecycle (6 estados), 5 famílias de instância (2026-05-20)
- [[sources/clf-c02-aula10-ec2-auto-scaling]] — Auto Scaling Group: min/desejado/max, preditivo vs dinâmico, multi-AZ (2026-05-20)
- [[sources/clf-c02-aula11-elastic-load-balancing]] — ELB: ALB/NLB/GWLB, health checks, integração Auto Scaling (2026-05-20)
- [[sources/clf-c02-aula12-messaging-sqs-sns]] — SQS (fila FIFO) e SNS (Pub/Sub), desacoplamento de microsserviços, fanout (2026-05-20)
- [[sources/clf-c02-aula13-serverless-lambda]] — Serverless e Lambda: triggers, pricing, ecossistema serverless (2026-05-20)
- [[sources/clf-c02-aula14-containers-ecr-ecs-eks-fargate]] — Containers: Docker, ECR, ECS, EKS, Fargate (2026-05-20)

### Trilha CLF-C02 — Redes na AWS
- [[sources/clf-c02-aula15-vpc]] — VPC: rede virtual privada, sub-redes públicas/privadas, multi-AZ (2026-05-20)
- [[sources/clf-c02-aula16-connectivity]] — Conectividade: IGW, VPN com Virtual Private Gateway, AWS Direct Connect (2026-05-20)
- [[sources/clf-c02-aula16-1-nacl-security-groups]] — Network ACLs (stateless, sub-rede) e Security Groups (stateful, instância) (2026-05-20)

### Trilha CLF-C02 — Segurança na Nuvem
- [[sources/clf-c02-aulas1-6-seguranca-nuvem]] — Shared Responsibility Model, KMS, IAM (CLF-C02), Organizations, Artifact, WAF, Shield, Inspector, GuardDuty (2026-05-26)

## Entities
- [[entities/aws]] — A plataforma de nuvem da Amazon
- [[entities/aws-iam]] — Serviço de identidade e acesso da AWS
- [[entities/amazon-s3]] — Serviço de armazenamento de objetos da AWS
- [[entities/aws-lambda]] — Serviço serverless de computação; handler, execution role, CRUD
- [[entities/amazon-dynamodb]] — Banco NoSQL gerenciado; modelo de dados + operações CRUD
- [[entities/amazon-api-gateway]] — API HTTP/REST/WS na frente de backends; rotas + integrations
- [[entities/aws-cognito]] — Auth de usuários finais; User Pools + JWT
- [[entities/amazon-ec2]] — VMs (IaaS canônico da AWS)
- [[entities/aws-elastic-beanstalk]] — PaaS da AWS (deploy sem gerenciar infra)
- [[entities/google-authenticator]] — App TOTP usado para MFA
- [[entities/postman]] — Cliente GUI para testar APIs HTTP
- [[entities/amazon-cloudfront]] — CDN da AWS; usa Edge Locations para entregar conteúdo com baixa latência
- [[entities/amazon-route53]] — Serviço DNS gerenciado; opera nos Edge Locations
- [[entities/aws-cloudformation]] — IaC nativo da AWS; templates JSON/YAML; rollback automático
- [[entities/amazon-ec2-auto-scaling]] — Escala instâncias EC2 automaticamente; ASG com min/desejado/max; preditivo vs dinâmico
- [[entities/elastic-load-balancing]] — Distribui tráfego entre instâncias; ALB/NLB/GWLB; health checks
- [[entities/amazon-sqs]] — Fila de mensagens gerenciada; FIFO; desacoplamento de microsserviços
- [[entities/amazon-sns]] — Pub/Sub; tópicos; notificações para múltiplos assinantes; fanout
- [[entities/amazon-ecr]] — Repositório gerenciado de imagens Docker
- [[entities/amazon-ecs]] — Orquestrador nativo AWS para containers Docker
- [[entities/amazon-eks]] — Kubernetes gerenciado na AWS
- [[entities/aws-fargate]] — Infraestrutura serverless para containers (ECS/EKS)
- [[entities/amazon-vpc]] — Rede virtual privada; alicerce de toda infraestrutura na AWS
- [[entities/aws-internet-gateway]] — Porta de entrada da VPC para internet pública (IGW)
- [[entities/aws-direct-connect]] — Conexão de fibra óptica dedicada; até 100 Gbps
- [[entities/aws-kms]] — Gerencia chaves criptográficas; dados em repouso e em trânsito
- [[entities/aws-organizations]] — Gerencia múltiplas contas AWS; faturamento consolidado; SCPs; gratuito
- [[entities/aws-artifact]] — Relatórios de conformidade (LGPD, GDPR, HIPAA) e contratos digitais; gratuito
- [[entities/aws-waf]] — Firewall L7 para apps web; bloqueia SQL Injection e XSS
- [[entities/aws-shield]] — Proteção DDoS; Standard (gratuito) vs Advanced (pago)
- [[entities/amazon-inspector]] — Scan automático de CVEs em EC2 e containers
- [[entities/amazon-guardduty]] — Detecção de ameaças em tempo real via Machine Learning

## Concepts

### Cloud — fundamentos
- [[concepts/cloud-computing]] — Definição AWS + pay-as-you-go + evolução
- [[concepts/cloud-benefits]] — Os 5 benefícios oficiais
- [[concepts/elasticity]] — Escalar/encolher automaticamente conforme demanda
- [[concepts/virtualization]] — Hypervisor, base técnica da cloud

### Modelos de serviço
- [[concepts/iaas]] — Infrastructure as a Service
- [[concepts/paas]] — Platform as a Service
- [[concepts/saas]] — Software as a Service

### Modelos de implantação
- [[concepts/on-premises]] — Infra local, controle total
- [[concepts/hybrid-cloud]] — Local + nuvem coexistindo
- [[concepts/private-cloud]] — Cloud tech rodando localmente

### IAM & autorização
- [[concepts/iam-policy]] — Estrutura JSON das policies IAM
- [[concepts/inline-policy]] — Policy embutida em uma única identidade
- [[concepts/customer-managed-policy]] — Policy criada pelo usuário; reutilizável
- [[concepts/iam-group]] — Coleção de usuários IAM compartilhando permissões
- [[concepts/iam-role]] — Identidade assumida temporariamente por serviços ou usuários
- [[concepts/access-keys]] — Credenciais de longa duração para acesso programático
- [[concepts/principle-of-least-privilege]] — Princípio do menor privilégio
- [[concepts/arn]] — Amazon Resource Name
- [[concepts/resource-tags]] — Tags chave/valor para classificação e custo

### Auth de usuário final
- [[concepts/mfa]] — Multi-Factor Authentication (TOTP)
- [[concepts/user-pool]] — Diretório de usuários do Cognito
- [[concepts/jwt]] — JSON Web Token

### Storage & segurança
- [[concepts/s3-block-public-access]] — Configuração que impede exposição pública de buckets

### Infraestrutura Global AWS
- [[concepts/aws-region]] — Região: agrupamento geográfico, isolamento de dados, 4 critérios de escolha (compliance > latência > serviços > custo)
- [[concepts/availability-zone]] — AZ: data center isolado dentro de uma Região; escopo AZ vs regional
- [[concepts/edge-location]] — Ponto de Presença / Edge Location: cache, CDN, DNS; 400+ locais
- [[concepts/high-availability]] — Serviço continua operando com falha parcial
- [[concepts/fault-tolerance]] — Arquitetura que resiste a falhas sem interrupção

### Provisionamento e DevOps
- [[concepts/infrastructure-as-code]] — IaC: infra declarada em código, versionável, reprodutível
- [[concepts/aws-cli]] — CLI da AWS: terminal, automação, `aws configure`

### Computação e escalabilidade
- [[concepts/auto-scaling]] — Escalabilidade horizontal automática; parâmetros min/desejado/max
- [[concepts/load-balancing]] — Distribuição de tráfego entre instâncias; health checks

### Mensageria e eventos
- [[concepts/microservices]] — Arquitetura de microsserviços; desacoplamento via mensageria
- [[concepts/pub-sub]] — Publisher/Subscriber; one-to-many; implementado pelo SNS

### Containers
- [[concepts/containers]] — Docker; portabilidade; imagens; Dockerfile; VMs vs containers

### Arquitetura
- [[concepts/serverless]] — Modelo sem provisionar servidor, escala automática
- [[concepts/nosql]] — Bancos não-relacionais

### Redes e segurança de rede
- [[concepts/subnet]] — Sub-rede pública (internet) vs privada (isolada) dentro de uma VPC
- [[concepts/network-acl]] — Firewall stateless de nível de sub-rede; padrão permissivo
- [[concepts/security-group]] — Firewall stateful de nível de instância EC2; padrão entrada bloqueada
- [[concepts/vpn]] — Túnel criptografado; Virtual Private Gateway; conecta data center à AWS

### Segurança na nuvem
- [[concepts/shared-responsibility-model]] — AWS: segurança DA nuvem (infra); Cliente: segurança NA nuvem (dados, acesso)
- [[concepts/encryption]] — Criptografia: data at rest (EBS, S3, RDS) vs data in transit (HTTPS, SSL/TLS)
- [[concepts/scp]] — Service Control Policies; teto de permissões por OU no Organizations

## Topics
- [[topics/aws-security]] — Trilha hands-on: IAM completo + auth via Cognito
- [[topics/cloud-fundamentals]] — Trilha CLF-C02: fundamentos para a certificação

## Synthesis
*(ainda vazio — candidato natural: "Arquitetura Serverless CRUD na AWS" sintetizando os 5 sources do módulo serverless)*
