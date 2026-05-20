# Log

Registro append-only de atividade do wiki. Entradas mais recentes no topo.

---

## [2026-05-20] ingest | CLF-C02 Aula 16.1 — Network ACLs e Security Groups
Fonte: `raw/clf-c02-aula16.1-network-acls-security-groups.md`. Criados: [[concepts/network-acl]] (stateless, sub-rede), [[concepts/security-group]] (stateful, instância). Par stateless/stateful documentado com fluxo completo de pacote.

## [2026-05-20] ingest | CLF-C02 Aula 16 — Conectividade com AWS: IGW, VPN e Direct Connect
Fonte: `raw/clf-c02-aula16-conectividade-igw-vpn-directconnect.md`. Criados: [[entities/aws-internet-gateway]], [[entities/aws-direct-connect]], [[concepts/vpn]]. Árvore de decisão IGW vs VPN vs Direct Connect documentada.

## [2026-05-20] ingest | CLF-C02 Aula 15 — Amazon VPC: Virtual Private Cloud
Fonte: `raw/clf-c02-aula15-amazon-vpc.md`. Criados: [[entities/amazon-vpc]], [[concepts/subnet]]. Módulo Redes na AWS iniciado. Atualizado: [[entities/amazon-ec2]] (contexto de rede, Security Group, sub-rede), [[topics/cloud-fundamentals]] (17 sources), [[wiki/overview]], [[wiki/index]].

## [2026-05-20] ingest | CLF-C02 Aula 14 — Containers na AWS: ECR, ECS, EKS e Fargate
Fonte: `raw/clf-c02-aula14-containers-ecr-ecs-eks-fargate.md`. Criados: [[concepts/containers]], [[entities/amazon-ecr]], [[entities/amazon-ecs]], [[entities/amazon-eks]], [[entities/aws-fargate]].

## [2026-05-20] ingest | CLF-C02 Aula 13 — Serverless e AWS Lambda
Fonte: `raw/clf-c02-aula13-serverless-lambda.md`. Atualizado: [[entities/aws-lambda]] (triggers completo, pricing, ecossistema serverless, fonte CLF-C02 adicionada).

## [2026-05-20] ingest | CLF-C02 Aula 12 — Mensageria: SQS e SNS
Fonte: `raw/clf-c02-aula12-mensageria-sqs-sns.md`. Criados: [[entities/amazon-sqs]], [[entities/amazon-sns]], [[concepts/microservices]], [[concepts/pub-sub]]. Padrão fanout documentado.

## [2026-05-20] ingest | CLF-C02 Aula 11 — Elastic Load Balancing
Fonte: `raw/clf-c02-aula11-elastic-load-balancing.md`. Criados: [[entities/elastic-load-balancing]], [[concepts/load-balancing]]. Arquitetura ELB + Auto Scaling documentada.

## [2026-05-20] ingest | CLF-C02 Aula 10 — EC2 Auto Scaling
Fonte: `raw/clf-c02-aula10-ec2-auto-scaling.md`. Criados: [[entities/amazon-ec2-auto-scaling]], [[concepts/auto-scaling]]. Parâmetros ASG, escalabilidade preditiva vs dinâmica, multi-AZ documentados.

## [2026-05-20] ingest | CLF-C02 Aula 09 — EC2 e Tipos de Instância
Fonte: `raw/clf-c02-aula09-ec2-tipos-instancia.md`. Atualizado: [[entities/amazon-ec2]] (AMI, 6 estados de lifecycle, 5 famílias de instância, pricing). Módulo Computação na AWS iniciado.

## [2026-05-20] ingest | CLF-C02 Aula 08 — Provisionamento: Console, CLI, SDK, Beanstalk, CloudFormation
Fonte: `raw/clf-c02-aula08-provisionamento-console-cli-sdk-beanstalk-cloudformation.md`. Criados: [[concepts/infrastructure-as-code]], [[concepts/aws-cli]], [[entities/aws-cloudformation]]. Atualizado: [[entities/aws-elastic-beanstalk]] (detalhe do fluxo de deploy + relação com CloudFormation).

## [2026-05-20] ingest | CLF-C02 Aula 07 — Edge Locations, CloudFront e Route 53
Fonte: `raw/clf-c02-aula07-edge-locations-cloudfront-route53.md`. Criados: [[entities/amazon-cloudfront]], [[entities/amazon-route53]]. Atualizado: [[concepts/edge-location]] (detalhe de cache, CDN, DNS).

## [2026-05-20] ingest | CLF-C02 Aula 06 — Regiões e Zonas de Disponibilidade
Fonte: `raw/clf-c02-aula06-regioes-zonas-disponibilidade.md`. Adicionados à [[concepts/aws-region]]: isolamento de dados, LGPD/GDPR, 4 critérios de escolha (compliance prioritário). Adicionado a [[concepts/availability-zone]]: escopo AZ vs regional (EC2/EBS = AZ; S3/DynamoDB/IAM = regional). Atualizado: [[entities/amazon-ec2]], [[topics/cloud-fundamentals]].

## [2026-05-20] ingest | CLF-C02 Aula 05 — Infraestrutura Global AWS
Fonte: `raw/clf-c02-aula05-infraestrutura-global-aws.md`. Criados: [[concepts/aws-region]], [[concepts/availability-zone]], [[concepts/edge-location]], [[concepts/high-availability]], [[concepts/fault-tolerance]]. Atualizados: [[topics/cloud-fundamentals]], [[wiki/overview]], [[wiki/index]]. Módulo de Infraestrutura Global iniciado.

## [2026-05-19] ingest | CLF-C02 Aula 04 — Modelos de Implantação
Fonte: `raw/clf-c02-aula04-modelos-de-implantacao.md`. Criados: [[concepts/hybrid-cloud]], [[concepts/private-cloud]]. Atualizado: [[concepts/on-premises]] (consolidado).

## [2026-05-19] ingest | CLF-C02 Aula 03 — Modelos de Serviço (IaaS, PaaS, SaaS)
Fonte: `raw/clf-c02-aula03-modelos-de-servico-iaas-paas-saas.md`. Criados: [[concepts/iaas]], [[concepts/paas]], [[concepts/saas]], [[entities/aws-elastic-beanstalk]]. Atualizado: [[entities/amazon-ec2]] (saiu de stub puro, agora ancorado como exemplo de IaaS).

## [2026-05-19] ingest | CLF-C02 Aula 02 — Benefícios do Cloud Computing
Fonte: `raw/clf-c02-aula02-beneficios-cloud-computing.md`. Criados: [[concepts/cloud-benefits]] (5 benefícios oficiais), [[concepts/elasticity]].

## [2026-05-19] ingest | CLF-C02 Aula 01 — O que é Cloud Computing
Fonte: `raw/clf-c02-aula01-o-que-e-cloud-computing.md`. Início da nova trilha CLF-C02 (preparatório certificação Cloud Practitioner). Criados: [[concepts/cloud-computing]], [[concepts/on-premises]], [[concepts/virtualization]], [[topics/cloud-fundamentals]]. Atualizados: [[entities/aws]], [[wiki/overview]], [[wiki/index]]. Wiki agora rastreia duas trilhas paralelas (hands-on + CLF-C02).

## [2026-05-19] ingest | Curso AWS — API Gateway 02: Integração Lambda, Permissões e Testes com Postman
Fonte: `raw/aula-apigateway-02-integracao-lambda-testes-postman.md`. Criada: [[entities/postman]] (stub). Atualizadas: [[entities/aws-lambda]], [[entities/amazon-api-gateway]], [[entities/amazon-dynamodb]], [[topics/aws-security]], [[wiki/overview]]. Capturado erro real de IAM (`dynamodb:PutItem`) e padrão de testes CRUD com Postman.

## [2026-05-19] ingest | Curso AWS — API Gateway 01: Criação de API HTTP e Rotas
Fonte: `raw/aula-apigateway-01-criacao-api-rotas.md`. Criada: [[entities/amazon-api-gateway]]. Definidas rotas CRUD que casam com `event.routeKey` da Lambda.

## [2026-05-19] ingest | Curso AWS — DynamoDB 02: Lambda CRUD no DynamoDB
Fonte: `raw/aula-dynamo-02-lambda-crud-dynamodb.md`. Atualizada: [[entities/aws-lambda]] (handler completo, switch por routeKey, JS + Python). [[entities/amazon-dynamodb]] ganha as operações via SDK.

## [2026-05-19] ingest | Curso AWS — DynamoDB 01: Criação de Tabela e Introdução ao Lambda
Fonte: `raw/aula-dynamo-01-tabela-e-introducao-lambda.md`. Criados: [[concepts/serverless]], [[concepts/nosql]]. Upgrade de stub: [[entities/amazon-dynamodb]] (modelo de dados, chaves, Query vs Scan).

## [2026-05-19] ingest | Curso AWS — Introdução ao Cognito
Fonte: `raw/aula-cognito-introducao.md`. Criados: [[entities/aws-cognito]], [[concepts/user-pool]], [[concepts/jwt]]. Conceitual — não implementado ainda. Distinção Cognito (usuários finais) vs IAM (identidades operacionais) consolidada.

## [2026-05-18] ingest | Curso AWS 06 — Validação de Permissões no S3 e Encerramento do Módulo IAM
Fonte: `raw/aula-06-validacao-permissoes-s3-encerramento-iam.md`. Criadas: [[concepts/s3-block-public-access]]. Atualizadas: [[entities/amazon-s3]], [[entities/aws-iam]], [[topics/aws-security]], [[wiki/overview]]. Módulo IAM encerrado. Total: 6 páginas tocadas.

## [2026-05-18] ingest | Curso AWS 05 — IAM Roles, Policies Personalizadas e Lambda
Fonte: `raw/aula-05-roles-policies-personalizadas-lambda.md`. Criadas: [[concepts/iam-role]], [[concepts/customer-managed-policy]]. Upgrade de stub: [[entities/aws-lambda]]. Atualizadas: [[entities/aws-iam]], [[entities/amazon-s3]], [[topics/aws-security]], [[wiki/overview]]. Total: 9 páginas tocadas.

## [2026-05-18] ingest | Curso AWS 04 — Grupos de Usuários IAM
Fonte: `raw/aula-04-grupos-usuarios-iam.md`. Criadas: [[iam-group]] (conceito), [[aws-lambda]], [[amazon-ec2]], [[amazon-dynamodb]] (stubs). Atualizadas: [[aws-iam]], [[aws]], [[iam-policy]], [[inline-policy]], [[principle-of-least-privilege]], [[aws-security]], [[overview]]. Total: 14 páginas tocadas.

## [2026-05-18] update | Idioma do wiki alterado para PT-BR
Schema atualizado (`CLAUDE.md`) e todas as páginas existentes reescritas em português. Termos técnicos canônicos (Inline Policy, Access Key, ARN etc.) mantidos no original.

## [2026-05-18] ingest | Curso AWS 03 — Login com Usuário IAM e Inline Policies para S3
Fonte: `raw/aula-03-login-usuario-iam-inline-policy-s3.md`. Criadas páginas para [[amazon-s3]], [[inline-policy]], [[arn]]. Atualizadas: [[aws-iam]], [[iam-policy]], [[access-keys]], [[aws-security]], [[overview]].

## [2026-05-18] ingest | Curso AWS 02 — IAM Policies, Tags e Credenciais
Fonte: `raw/aula-02-policies-tags-credenciais-iam.md`. Criadas páginas para [[resource-tags]], [[principle-of-least-privilege]]. Aprofundadas: [[iam-policy]], [[access-keys]], [[aws-iam]].

## [2026-05-18] ingest | Curso AWS 01 — MFA e Criação de Usuário IAM
Fonte: `raw/aula-01-mfa-e-iam-aws.md`. Bootstrap do wiki: páginas criadas para [[aws]], [[aws-iam]], [[google-authenticator]], [[mfa]], [[iam-policy]], [[access-keys]], [[principle-of-least-privilege]], [[aws-security]].

## [2026-05-18] init | Tech Knowledge Wiki
Wiki inicializado. Estrutura de diretórios criada, schema `CLAUDE.md` escrito, `index.md` e `log.md` em bootstrap. Foco do domínio: tecnologia (linguagens, frameworks, AI/ML, arquitetura, infraestrutura, bancos, segurança, prática de engenharia).
