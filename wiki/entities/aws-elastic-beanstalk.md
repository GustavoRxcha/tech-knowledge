---
title: "AWS Elastic Beanstalk"
type: entity
tags: [aws, paas, deploy, elastic-beanstalk]
created: 2026-05-19
updated: 2026-05-20
sources: 2
---

# AWS Elastic Beanstalk

Serviço **[[concepts/paas|PaaS]]** da [[entities/aws|AWS]]. Faz upload do código e a plataforma cuida do provisionamento (EC2, load balancer, auto scaling, monitoramento) automaticamente.

---

## Posicionamento

- **Exemplo canônico de [[concepts/paas|PaaS]]** na AWS (citado nas fontes do curso CLF-C02).
- Você entrega o **artefato da aplicação** (JAR, WAR, container, código fonte). A plataforma cria a infra subjacente.
- Suporta múltiplas linguagens/plataformas: Java, .NET, Node.js, Python, Ruby, Go, PHP, Docker.

## Como funciona

1. Você empacota o código (ex: `.zip`) e fornece um arquivo de configuração indicando como a aplicação deve ser executada
2. O Elastic Beanstalk provisiona automaticamente toda a infra necessária

## O que ele faz por você

- Provisiona [[entities/amazon-ec2|EC2]] instances
- Configura Elastic Load Balancer
- Configura Auto Scaling
- Banco de dados (se configurado)
- Coleta métricas (CloudWatch)
- Gerencia versões da aplicação

> O Elastic Beanstalk usa [[entities/aws-cloudformation|AWS CloudFormation]] internamente para provisionar os recursos — os dois são complementares, não concorrentes.

## O que ainda é sua responsabilidade

- O **código da aplicação**.
- Configuração da própria aplicação (env vars, secrets).
- Dados (RDS / DynamoDB ficam separados).

## Comparação rápida

| | Você gerencia | AWS gerencia |
|---|---|---|
| EC2 (IaaS) | SO, runtime, app, escala | Hardware, virtualização |
| **Beanstalk (PaaS)** | App, dados | SO, runtime, escala, infra |
| Lambda (FaaS) | Função | Tudo o resto |

## Para a prova CLF-C02

Aparece como **resposta correta** quando o cenário diz: "Equipe quer fazer deploy sem gerenciar servidores, mas precisa de controle sobre a aplicação."

## Lacunas

- Não cobre EB Worker Environments, configuração avançada, ebextensions, blue/green deploy via EB.
- Será preenchido se aulas práticas chegarem.

> [!question] Apenas referência conceitual até agora.

## Fontes

- [[sources/clf-c02-aula03-service-models]]
- [[sources/clf-c02-aula08-provisioning]]

## Relações

- [[entities/aws]]
- [[concepts/paas]]
- [[entities/amazon-ec2]] — provisionado por baixo do EB
- [[entities/aws-cloudformation]] — usado internamente pelo EB
