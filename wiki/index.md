---
title: "Index"
type: overview
updated: 2026-05-19
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

### Arquitetura
- [[concepts/serverless]] — Modelo sem provisionar servidor, escala automática
- [[concepts/nosql]] — Bancos não-relacionais

## Topics
- [[topics/aws-security]] — Trilha hands-on: IAM completo + auth via Cognito
- [[topics/cloud-fundamentals]] — Trilha CLF-C02: fundamentos para a certificação

## Synthesis
*(ainda vazio — candidato natural: "Arquitetura Serverless CRUD na AWS" sintetizando os 5 sources do módulo serverless)*
