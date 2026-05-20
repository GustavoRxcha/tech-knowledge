---
title: "AWS Fargate"
type: entity
tags: [aws, fargate, serverless, containers, ecs, eks]
created: 2026-05-20
updated: 2026-05-20
sources: 1
---

# AWS Fargate

Motor de computação **serverless para containers** — elimina a necessidade de provisionar e gerenciar as instâncias EC2 que formam o cluster do [[entities/amazon-ecs|ECS]] ou [[entities/amazon-eks|EKS]].

---

## O que resolve

Ao usar ECS ou EKS **sem** Fargate, você ainda precisa gerenciar as instâncias EC2 do cluster. O Fargate remove essa responsabilidade:

```
Sem Fargate:
[ECS/EKS] → você provisiona e gerencia instâncias EC2 do cluster

Com Fargate:
[ECS/EKS + Fargate] → AWS gerencia toda a infraestrutura
                       Você define apenas CPU/memória por container
```

---

## Benefícios

| Benefício | Descrição |
|---|---|
| **Serverless** | Sem gerenciamento de servidores ou clusters |
| **Menos configuração** | Define apenas os recursos necessários por container |
| **Escalabilidade automática** | Infraestrutura escala conforme os containers precisam |
| **Pay-per-use** | Paga pelo tempo de CPU e memória consumidos pelos containers |

---

## Posicionamento no ecossistema

```
[ECR] → armazena imagens
  ↓
[ECS ou EKS] → orquestra e executa containers
  ↓
[Fargate] → elimina gerenciamento de infraestrutura (opcional, mas recomendado)
```

---

## Fargate vs Lambda (serverless)

| | Fargate (containers) | Lambda (funções) |
|---|---|---|
| Unidade | Container (imagem Docker) | Função |
| Controle | Maior — define o ambiente via imagem | Menor — AWS gerencia tudo |
| Tempo de execução | Longo (aplicações contínuas) | Curto (até 15 minutos) |
| Casos de uso | APIs, microsserviços contínuos | Processamento por evento |

---

## Para a prova CLF-C02

- *"Qual serviço elimina a necessidade de gerenciar servidores para rodar containers?"* → **Fargate**

---

## Relações

- [[entities/amazon-ecs]] — Fargate é infraestrutura opcional para o ECS
- [[entities/amazon-eks]] — Fargate é infraestrutura opcional para o EKS
- [[entities/aws-lambda]] — outra abordagem serverless (funções vs containers)
- [[concepts/containers]] — base do que Fargate executa
- [[concepts/serverless]] — Fargate aplica serverless à camada de infraestrutura de containers

## Fontes

- [[sources/clf-c02-aula14-containers-ecr-ecs-eks-fargate]]
