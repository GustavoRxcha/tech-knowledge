---
title: "AWS CloudFormation"
type: entity
tags: [aws, cloudformation, iac, infraestrutura-como-codigo, devops, yaml, json]
created: 2026-05-20
updated: 2026-05-20
sources: 1
---

# AWS CloudFormation

O **AWS CloudFormation** é o serviço de **[[concepts/infrastructure-as-code|Infraestrutura como Código (IaC)]]** nativo da [[entities/aws|AWS]]. Permite definir e provisionar toda a infraestrutura através de um arquivo de código (JSON ou YAML), chamado de **template**.

---

## Como funciona

1. Você escreve um **template** (JSON ou YAML) declarando todos os recursos necessários
2. O CloudFormation interpreta o template e determina a ordem de criação
3. A infraestrutura é criada, atualizada ou destruída automaticamente

### Exemplo de template (YAML)

```yaml
Resources:
  MinhaTabelaDynamo:
    Type: AWS::DynamoDB::Table
    Properties:
      TableName: "products"
      AttributeDefinitions:
        - AttributeName: "id"
          AttributeType: "S"
      KeySchema:
        - AttributeName: "id"
          KeyType: "HASH"

  MinhaFuncaoLambda:
    Type: AWS::Lambda::Function
    Properties:
      FunctionName: "getProducts"
      Runtime: "python3.12"

  MeuBucketS3:
    Type: AWS::S3::Bucket
    Properties:
      BucketName: "meu-bucket-produtos"
```

---

## Benefícios

| Benefício | Descrição |
|---|---|
| **Reprodutibilidade** | Mesmo template cria ambientes idênticos (dev, staging, prod) |
| **Versionamento** | Template em Git → histórico de mudanças na infra |
| **Automação** | Criação e destruição de ambientes com um comando |
| **Consistência** | Elimina erros de configuração manual |
| **Rollback automático** | Em caso de falha, desfaz as mudanças automaticamente |

---

## Relação com Elastic Beanstalk

> O próprio [[entities/aws-elastic-beanstalk|Elastic Beanstalk]] usa CloudFormation internamente para provisionar os recursos — são complementares, não concorrentes.

| | Elastic Beanstalk | CloudFormation |
|---|---|---|
| Foco | Deploy de aplicações | Provisionamento de infraestrutura |
| Abstração | Alta — não vê os detalhes | Baixa — declara tudo |
| Controle | Menor | Total |
| Perfil | Desenvolvedor | DevOps / Engenheiro de Infra |
| Modelo | PaaS | IaC |

---

## Quando usar

- Ambientes complexos com múltiplos serviços interdependentes
- Times que precisam recriar ambientes de forma consistente
- Pipelines de CI/CD com infraestrutura automatizada
- Quando versionamento da infraestrutura é necessário

---

## Para a prova CLF-C02

- *"Qual ferramenta permite criar infraestrutura AWS a partir de um arquivo JSON/YAML?"* → **CloudFormation**

---

## Relações

- [[concepts/infrastructure-as-code]] — o conceito que o CloudFormation implementa
- [[entities/aws-elastic-beanstalk]] — usa CloudFormation internamente
- [[entities/aws-lambda]] — pode ser provisionada via template CloudFormation
- [[entities/amazon-dynamodb]] — pode ser provisionada via template
- [[entities/amazon-s3]] — pode ser provisionada via template

## Fontes

- [[sources/clf-c02-aula08-provisioning]]
