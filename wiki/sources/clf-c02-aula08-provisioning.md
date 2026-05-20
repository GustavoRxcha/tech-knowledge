---
title: "CLF-C02 Aula 08 — Provisionamento de Recursos na AWS"
type: source
tags: [aws, clf-c02, console, cli, sdk, elastic-beanstalk, cloudformation, iac]
created: 2026-05-20
updated: 2026-05-20
sources: 1
---

# CLF-C02 Aula 08 — Provisionamento de Recursos na AWS

Formas de interagir com as APIs da AWS (Console, CLI, SDKs) e ferramentas de provisionamento automatizado de infraestrutura (Elastic Beanstalk e CloudFormation).

---

## Origem

- **Arquivo:** `raw/clf-c02-aula08-provisionamento-console-cli-sdk-beanstalk-cloudformation.md`
- **Trilha:** CLF-C02 — Preparatório AWS Cloud Practitioner
- **Módulo:** Infraestrutura Global AWS (aula 04 do módulo / aula 08 do curso)

---

## Interagir com a AWS = chamadas de API

Toda interação com serviços AWS — seja pelo console web, CLI ou SDKs — acontece via **APIs da AWS**. As três formas a seguir são abstrações sobre essas APIs.

---

## 1. Console de Gerenciamento AWS

Interface **web** da AWS. Acesso visual e intuitivo a todos os serviços.

- Ideal para: exploração, aprendizado, tarefas manuais pontuais
- Limitação: não serve para automação ou repetição em escala

---

## 2. AWS CLI

Ferramenta instalada localmente para interagir com **todas as APIs da AWS via terminal**.

```bash
aws configure                                 # login (Access Key + Secret)
aws s3 ls                                     # listar buckets S3
aws ec2 describe-instances                    # listar instâncias EC2
aws s3 cp arquivo.txt s3://meu-bucket/        # upload para S3
```

- Compatível com Windows, macOS e Linux
- Ideal para: automação de tarefas repetitivas, scripts, CI/CD, administração em escala

---

## 3. SDKs (Software Development Kits)

Bibliotecas que permitem que **aplicações acessem recursos AWS pelo código**.

| Linguagem | SDK |
|---|---|
| Python | boto3 |
| JavaScript / Node.js | aws-sdk / @aws-sdk |
| Java | AWS SDK for Java |
| Go | AWS SDK for Go |
| C#/.NET | AWS SDK for .NET |

```python
import boto3
s3 = boto3.client('s3')
buckets = s3.list_buckets()
```

- Ideal para: microsserviços, Lambdas que acessam S3/DynamoDB, automação integrada ao código

---

## Comparativo das 3 formas

| Forma | Interface | Requer código? | Melhor para |
|---|---|---|---|
| Console | Web (visual) | ❌ | Exploração, tarefas manuais |
| CLI | Terminal | Parcialmente (scripts) | Automação, administração |
| SDK | Código | ✅ | Integração em aplicações |

---

## 4. AWS Elastic Beanstalk

Serviço **PaaS** que automatiza deploy e provisionamento de infraestrutura para aplicações.

### Como funciona

1. Você empacota o código (`.zip`)
2. Fornece arquivo de configuração indicando como a aplicação deve ser executada
3. Beanstalk provisiona automaticamente:
   - Instâncias EC2
   - Balanceador de carga
   - Auto Scaling
   - Banco de dados (se configurado)
   - Monitoramento

### Quando usar

- Focar no código, não na infra
- Deploy rápido de apps web sem configurar cada serviço manualmente
- Desenvolvedores sem experiência profunda em infraestrutura

---

## 5. AWS CloudFormation

Serviço de **IaC (Infrastructure as Code)** da AWS. Define e provisiona toda a infraestrutura via arquivo JSON ou YAML.

### Como funciona

1. Escreve template (JSON ou YAML) declarando todos os recursos
2. CloudFormation interpreta o template
3. Infraestrutura é criada, atualizada ou destruída automaticamente

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

### Benefícios

| Benefício | Descrição |
|---|---|
| Reprodutibilidade | Mesmo template cria ambientes idênticos (dev, staging, prod) |
| Versionamento | Template em Git → histórico de mudanças na infra |
| Automação | Criação e destruição de ambientes com um comando |
| Consistência | Elimina erros de configuração manual |
| Rollback | Em caso de falha, CloudFormation desfaz as mudanças automaticamente |

---

## Elastic Beanstalk vs CloudFormation

| | Elastic Beanstalk | CloudFormation |
|---|---|---|
| Foco | Deploy de aplicações | Provisionamento de infraestrutura |
| Abstração | Alta — não vê os detalhes | Baixa — declara tudo |
| Controle | Menor | Total |
| Linguagem | Configuração simplificada | JSON ou YAML |
| Perfil | Desenvolvedor | DevOps / Engenheiro de Infra |
| Modelo | PaaS | IaC |

> O próprio Elastic Beanstalk usa CloudFormation internamente — são complementares, não concorrentes.

---

## Conceitos/entidades relacionados

- [[entities/aws-elastic-beanstalk]]
- [[entities/aws-cloudformation]]
- [[concepts/infrastructure-as-code]]
- [[concepts/aws-cli]]
- [[concepts/paas]]
