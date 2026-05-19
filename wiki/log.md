# Log

Registro append-only de atividade do wiki. Entradas mais recentes no topo.

---

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
