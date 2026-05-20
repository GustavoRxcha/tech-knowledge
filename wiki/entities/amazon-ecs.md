---
title: "Amazon ECS (Elastic Container Service)"
type: entity
tags: [aws, ecs, containers, orquestracao, docker]
created: 2026-05-20
updated: 2026-05-20
sources: 1
---

# Amazon ECS — Elastic Container Service

Serviço de **orquestração e execução de containers Docker** nativo da [[entities/aws|AWS]]. Gerencia onde e como os containers são executados dentro de um cluster.

---

## O que faz

- Executa containers a partir de imagens armazenadas no [[entities/amazon-ecr|ECR]]
- Gerencia o ciclo de vida dos containers (start, stop, restart)
- Distribui containers entre instâncias do cluster
- Integra com ELB, Auto Scaling, IAM e outros serviços AWS

---

## Quando usar

- Quando quer executar containers Docker na AWS
- Quando prefere a solução **nativa e gerenciada** da própria AWS
- Quando não precisa de Kubernetes

---

## ECS vs EKS

| | ECS | EKS |
|---|---|---|
| Tecnologia | Nativa AWS | Kubernetes (open-source) |
| Curva de aprendizado | Menor | Maior |
| Portabilidade | Limitada à AWS | Alta — K8s roda em qualquer nuvem |
| Quando usar | Simples, AWS-first | Time já usa K8s, multi-cloud |

---

## Com ou sem Fargate

- **Sem Fargate:** você provisiona e gerencia as instâncias EC2 do cluster
- **Com [[entities/aws-fargate|Fargate]]:** AWS gerencia toda a infraestrutura; você define só CPU/memória por container

---

## Para a prova CLF-C02

- *"Qual serviço executa containers Docker de forma nativa na AWS?"* → **ECS**

---

## Relações

- [[entities/amazon-ecr]] — fonte das imagens Docker
- [[entities/aws-fargate]] — infraestrutura serverless opcional para o ECS
- [[entities/amazon-eks]] — alternativa com Kubernetes
- [[concepts/containers]] — o conceito base

## Fontes

- [[sources/clf-c02-aula14-containers-ecr-ecs-eks-fargate]]
