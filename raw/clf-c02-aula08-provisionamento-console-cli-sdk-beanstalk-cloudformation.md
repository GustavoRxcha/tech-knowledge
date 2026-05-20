# Provisionamento de Recursos na AWS

> 📋 **Curso:** Infraestrutura Global AWS — Preparatório AWS Cloud Practitioner (CLF-C02)
> 📌 **Aula:** Conceitual — Formas de Interagir com a AWS e Provisionamento de Infraestrutura

---

## Visão Geral

Para utilizar qualquer serviço AWS, é preciso **interagir com as APIs da AWS**. Existem três formas principais de fazer isso, e dois serviços específicos para **automatizar o provisionamento de infraestrutura**.

---

## 1. Formas de Interagir com a AWS

### 1.1 Console de Gerenciamento AWS (Management Console)

A interface **web** da AWS — o portal acessado pelo navegador.

- Acesso visual e intuitivo a todos os serviços
- Ideal para exploração, aprendizado e tarefas manuais pontuais
- Disponível em: [console.aws.amazon.com](https://console.aws.amazon.com)

**Quando usar:**
- Criar recursos manualmente (ex: lançar uma instância EC2)
- Visualizar métricas e dashboards
- Configurações iniciais e exploração de serviços

**Limitação:** Não é adequado para automação ou repetição de tarefas em escala.

---

### 1.2 AWS CLI (Command Line Interface)

Ferramenta instalada na máquina local que permite interagir com **todas as APIs da AWS via linha de comando**.

**Instalação e uso:**
1. Baixar e instalar o pacote da CLI no [site da AWS](https://aws.amazon.com/pt/cli/)
2. Fazer login com `aws configure` (Access Key + Secret)
3. Executar comandos para interagir com qualquer serviço

```bash
# Exemplos de comandos AWS CLI
aws s3 ls                          # listar buckets S3
aws ec2 describe-instances         # listar instâncias EC2
aws s3 cp arquivo.txt s3://meu-bucket/  # upload para S3
```

**Compatibilidade:** Windows, macOS e Linux

**Quando usar:**
- Automação de tarefas repetitivas via scripts
- Integração com pipelines de CI/CD
- Administração de recursos em grande escala

> 📌 Exige conhecimento dos comandos e da documentação, mas é essencial para automação.

---

### 1.3 SDKs (Software Development Kits)

Bibliotecas disponíveis em diversas linguagens de programação que permitem que **aplicações acessem recursos AWS diretamente pelo código**.

**Linguagens suportadas (principais):**

| Linguagem | SDK |
|---|---|
| **Python** | boto3 |
| **JavaScript / Node.js** | aws-sdk / @aws-sdk |
| **Java** | AWS SDK for Java |
| **Go** | AWS SDK for Go |
| **C#/.NET** | AWS SDK for .NET |
| E muitas outras... | |

**Exemplo de uso (Python/boto3):**
```python
import boto3
s3 = boto3.client('s3')
buckets = s3.list_buckets()
```

**Quando usar:**
- Quando uma aplicação precisa interagir com serviços AWS programaticamente
- Microsserviços, APIs, funções Lambda que acessam S3, DynamoDB, etc.
- Automação integrada ao código da aplicação

---

### Comparativo das 3 Formas

| Forma | Interface | Requer código? | Melhor para |
|---|---|---|---|
| **Console** | Web (visual) | ❌ | Exploração, tarefas manuais |
| **CLI** | Terminal | Parcialmente (scripts) | Automação, administração |
| **SDK** | Código | ✅ | Integração em aplicações |

---

## 2. Provisionamento de Infraestrutura

Além de interagir com serviços individuais, a AWS oferece ferramentas para **provisionar e gerenciar infraestrutura de forma automatizada e padronizada**.

---

### 2.1 AWS Elastic Beanstalk

Serviço de **plataforma gerenciada (PaaS)** que automatiza o processo de deploy e provisionamento de infraestrutura para aplicações.

**Como funciona:**
1. Você empacota seu código (ex: `.zip` com a aplicação)
2. Fornece um arquivo de configuração indicando como quer que a aplicação seja executada
3. O Elastic Beanstalk automaticamente provisiona:
   - Instâncias EC2
   - Balanceador de carga
   - Auto Scaling
   - Banco de dados (se necessário)
   - Monitoramento

```
[Seu código + configuração]
         ↓
[Elastic Beanstalk]
         ↓ provisiona automaticamente
[EC2] [Load Balancer] [Auto Scaling] [RDS]
```

**Quando usar:**
- Quando você quer focar no código, não na infraestrutura
- Deploy rápido de aplicações web sem configurar cada serviço manualmente
- Ideal para desenvolvedores sem experiência profunda em infraestrutura

---

### 2.2 AWS CloudFormation

Serviço de **Infraestrutura como Código (IaC — Infrastructure as Code)** da AWS. Permite definir e provisionar **toda a infraestrutura através de um arquivo de código** (JSON ou YAML).

**Como funciona:**
1. Você escreve um arquivo de template (JSON ou YAML) declarando todos os recursos necessários
2. O CloudFormation interpreta o template
3. A infraestrutura é criada, atualizada ou destruída automaticamente

**Exemplo de template CloudFormation (YAML):**
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
      ...

  MeuBucketS3:
    Type: AWS::S3::Bucket
    Properties:
      BucketName: "meu-bucket-produtos"
```

**Benefícios:**

| Benefício | Descrição |
|---|---|
| **Reprodutibilidade** | Mesmo template cria ambientes idênticos (dev, staging, prod) |
| **Versionamento** | Template armazenado em Git — histórico de mudanças na infraestrutura |
| **Automação** | Criação e destruição de ambientes com um comando |
| **Consistência** | Elimina erros de configuração manual |
| **Rollback** | Em caso de falha, o CloudFormation desfaz as mudanças automaticamente |

**Quando usar:**
- Ambientes complexos com múltiplos serviços interdependentes
- Times que precisam recriar ambientes de forma consistente
- Pipelines de CI/CD com infraestrutura automatizada
- Quando versionamento da infraestrutura é necessário

---

### Diferença entre Elastic Beanstalk e CloudFormation

| | Elastic Beanstalk | CloudFormation |
|---|---|---|
| **Foco** | Deploy de aplicações | Provisionamento de infraestrutura |
| **Abstração** | Alta — você não vê os detalhes | Baixa — você declara tudo |
| **Controle** | Menor | Total |
| **Linguagem** | Configuração simplificada | JSON ou YAML |
| **Perfil** | Desenvolvedor | DevOps / Engenheiro de Infraestrutura |
| **Modelo** | PaaS | IaC |

> 📌 O próprio Elastic Beanstalk usa CloudFormation internamente para provisionar os recursos — são complementares, não concorrentes.

---

## 3. Resumo Geral

```
COMO INTERAGIR COM A AWS
├── Console (web) → visual, manual
├── CLI → terminal, scripts, automação
└── SDKs → código da aplicação (Python, JS, Java...)

COMO PROVISIONAR INFRAESTRUTURA
├── Elastic Beanstalk → deploy de apps (PaaS, alto nível)
└── CloudFormation → infraestrutura como código (IaC, controle total)
```

---

> 💡 **Dica para a prova CLF-C02:** Questões típicas:
> - *"Qual ferramenta permite criar infraestrutura AWS a partir de um arquivo JSON/YAML?"* → **CloudFormation**
> - *"Qual serviço provisiona automaticamente a infraestrutura para uma aplicação web?"* → **Elastic Beanstalk**
> - *"Como um desenvolvedor acessa recursos AWS de dentro de uma aplicação Python?"* → **SDK (boto3)**
> - *"Qual forma de acesso à AWS é compatível com Windows, Mac e Linux via terminal?"* → **AWS CLI**

---

## Links Úteis

- [Console de Gerenciamento AWS](https://console.aws.amazon.com)
- [AWS CLI — Instalação e documentação](https://aws.amazon.com/pt/cli/)
- [AWS SDKs](https://aws.amazon.com/pt/developer/tools/)
- [AWS Elastic Beanstalk](https://aws.amazon.com/pt/elasticbeanstalk/)
- [AWS CloudFormation](https://aws.amazon.com/pt/cloudformation/)

---

*Aula 04 — Módulo: Infraestrutura Global AWS | Curso Preparatório AWS Cloud Practitioner*
