---
title: "Overview"
type: overview
tags: [aws, iam, s3, serverless, cloud, clf-c02, segurança, infraestrutura-global, redes]
created: 2026-05-18
updated: 2026-05-20
sources: 28
---

# Tech Knowledge Wiki — Overview

Síntese evolutiva do panorama geral. Atualizada sempre que uma nova fonte muda o quadro.

---

## Estado atual

O wiki cobre AWS por **duas trilhas paralelas**:

1. **Trilha hands-on** (11 sources): curso prático com módulos IAM (6 aulas) e Serverless (5 aulas: Cognito intro + DynamoDB + API Gateway). Arquitetura CRUD completa rodando ponta-a-ponta.
2. **Trilha CLF-C02** (17 sources): preparatório conceitual para a certificação AWS Cloud Practitioner. Cobertura: definição de cloud, benefícios, modelos de serviço, modelos de implantação, infraestrutura global (Regiões, AZs, Edge Locations), formas de provisionamento, **módulo completo de Computação** (EC2 + Auto Scaling + ELB + SQS + SNS + Lambda + Containers), **módulo de Redes** (VPC, sub-redes, IGW, VPN, Direct Connect, NACLs, Security Groups).

As duas trilhas se cruzam — IaaS/PaaS/SaaS conceituais da CLF-C02 ancoram [[entities/amazon-ec2|EC2]], [[entities/aws-elastic-beanstalk|Elastic Beanstalk]] e [[entities/aws-lambda|Lambda]] da prática.

---

## Áreas rastreadas

| Área | Status | Páginas-chave |
|---|---|---|
| AI/ML & LLMs | — | — |
| Linguagens | 🌱 inicial (Node.js + Python via SDK) | [[sources/aws-course-dynamo-02-lambda-crud]] |
| Frameworks | — | — |
| Cloud — fundamentos / CLF-C02 | 🟢 17 aulas cobertas | [[topics/cloud-fundamentals]], [[concepts/aws-region]], [[entities/elastic-load-balancing]], [[entities/amazon-sqs]], [[entities/amazon-sns]], [[entities/amazon-ecs]], [[entities/aws-fargate]], [[entities/amazon-vpc]], [[concepts/network-acl]], [[concepts/security-group]] |
| Arquitetura — serverless | 🟢 cobertura prática | [[concepts/serverless]], [[entities/aws-lambda]], [[entities/amazon-api-gateway]], [[entities/amazon-dynamodb]] |
| Infraestrutura — cloud AWS | 🟢 sólida na faixa coberta | [[entities/aws]] e todos os serviços listados nele |
| Bancos de dados | 🟡 DynamoDB cobre o básico | [[entities/amazon-dynamodb]], [[concepts/nosql]] |
| Segurança — IAM/AWS | 🟢 módulo completo | [[topics/aws-security]], [[concepts/iam-role]], [[concepts/iam-policy]], [[concepts/s3-block-public-access]] |
| Autenticação de usuários | 🟡 conceitual | [[entities/aws-cognito]], [[concepts/user-pool]], [[concepts/jwt]] |
| Prática de engenharia | — | — |

---

## Modelos mentais consolidados

### IAM

Quatro perguntas:
1. **Quem?** — usuário, grupo, role, serviço
2. **O quê?** — actions (`s3:GetObject`, `dynamodb:PutItem`...)
3. **Em quê?** — resources identificados por [[concepts/arn|ARN]]
4. **Como?** — via [[concepts/iam-policy|policy]] (managed, customer-managed, inline)

Hierarquia recomendada: **policy → grupo → usuário**. Para serviços: **policy → role → serviço**.

### Stack serverless

```
[Cliente] → [Cognito (JWT)] → [API Gateway] → [Lambda (switch routeKey)] → [DynamoDB / S3]
```

Tudo serverless, mesma região, sem credenciais hardcodadas.

### Cloud (eixos da CLF-C02)

- **O quê é cloud**: pay-as-you-go via internet.
- **Por que cloud**: 5 benefícios (CapEx→OpEx, [[concepts/elasticity|elasticidade]], economias de escala, agilidade, alcance global).
- **Quanto gerencio**: [[concepts/iaas|IaaS]] / [[concepts/paas|PaaS]] / [[concepts/saas|SaaS]].
- **Onde roda**: [[concepts/on-premises]] / [[concepts/hybrid-cloud|Híbrido]] / Cloud / [[concepts/private-cloud|Privada]].
- **Como é organizado fisicamente**: [[concepts/aws-region|Regiões]] → [[concepts/availability-zone|AZs]] → Data Centers; [[concepts/edge-location|Edge Locations]] (400+) para entrega de conteúdo.
- **Como provisiono**: Console · [[concepts/aws-cli|CLI]] · SDKs · [[entities/aws-elastic-beanstalk|Beanstalk (PaaS)]] · [[entities/aws-cloudformation|CloudFormation (IaC)]].
- **Computação EC2**: 5 famílias · [[entities/amazon-ec2-auto-scaling|Auto Scaling]] (preditivo/dinâmico, multi-AZ) · [[entities/elastic-load-balancing|ELB]] (ALB/NLB/GWLB).
- **Mensageria**: [[entities/amazon-sqs|SQS]] (fila FIFO, one-to-one) + [[entities/amazon-sns|SNS]] (Pub/Sub, one-to-many) = fanout e desacoplamento de microsserviços.
- **Serverless e containers**: Lambda por evento · ECS/EKS orquestram containers via ECR · Fargate elimina gerenciamento de infra.
- **Redes**: [[entities/amazon-vpc|VPC]] é o alicerce · sub-redes públicas (IGW) vs privadas · IGW para internet · VPN para data center · Direct Connect para alto desempenho · [[concepts/network-acl|NACL]] (stateless, sub-rede) + [[concepts/security-group|Security Group]] (stateful, instância) = defesa em profundidade.

---

## Temas emergentes

- **Menor privilégio operacional**: validado com erros reais nas aulas 04, 06 e API Gateway 02.
- **Roles como padrão para serviços**: nunca hardcodar credenciais.
- **Customer-managed policies** preenchem o gap entre managed (genérica demais) e inline (não reutilizável).
- **Cognito ≠ IAM**: identidade de usuário final vs identidade operacional.
- **JWT como contrato** entre Cognito e API Gateway.
- **DocumentClient / boto3 resource** abstraem tipos internos do DynamoDB.
- **Constantes para nomes de recursos** — bug real do curso reforça a prática.
- **Pay-as-you-go + elasticidade** são o motor econômico que justifica todo o resto da cloud.
- **Distinguir modelos de serviço (gerenciamento) de modelos de implantação (localização)** — caem juntos e geram confusão.

---

## Próximas perguntas abertas

### Trilha hands-on
- Authorizer Cognito no API Gateway na prática.
- Identity Pool (vs User Pool) — quando entra?
- Cross-account role.
- `aws:ResourceTag` como condição.
- Bucket policies S3 × IAM policies.
- DynamoDB: GSIs, transactions, streams.
- Lambda: cold starts, layers, observabilidade.

### Trilha CLF-C02
- Well-Architected Framework.
- Shared Responsibility Model.
- Pricing & Support Plans.
- Catálogo de serviços por categoria.

---

## Lacunas do wiki

- **IAM avançado**: Roles cross-account, federação, SCPs, AWS Organizations, KMS, CloudTrail, IAM Access Analyzer.
- **S3**: Sem versionamento, criptografia, lifecycle, storage classes, presigned URLs, hospedagem estática.
- **Lambda**: triggers detalhados, layers, cold starts, VPC, observabilidade.
- **DynamoDB**: GSI/LSI, streams, transactions, capacity modes.
- **API Gateway**: custom domain, CORS, throttling, validação.
- **Cognito**: User Pool real, authorizer no API Gateway, Identity Pool, federação social.
- **EC2**: tudo além da menção conceitual e do "acesso negado".
- **CLF-C02**: tudo depois da aula 16.1 (Well-Architected, Shared Responsibility, billing, catálogo de serviços avançados). Redes avançadas: NAT Gateway, VPC Peering, PrivateLink.
- Tudo fora do tópico AWS — linguagens, frameworks, AI/ML, arquitetura clássica — ainda sem fontes.

---

## Candidatos a synthesis

1. **`synthesis/serverless-crud-architecture-aws`** — consolida as 5 últimas aulas hands-on em uma referência operacional única.
2. **`synthesis/iaas-paas-saas-decision-matrix`** — matriz decisória prática para CLF-C02, com cenários e palavras-gatilho.
3. **`synthesis/aws-baseline-account-setup`** — checklist único de bootstrap seguro de conta a partir das 6 aulas do módulo IAM.

Posso filar qualquer uma. Diga qual prioriza.
