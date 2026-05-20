---
title: "Amazon EKS (Elastic Kubernetes Service)"
type: entity
tags: [aws, eks, kubernetes, containers, orquestracao, k8s]
created: 2026-05-20
updated: 2026-05-20
sources: 1
---

# Amazon EKS — Elastic Kubernetes Service

Serviço de **Kubernetes gerenciado** da [[entities/aws|AWS]]. Kubernetes (K8s) é a plataforma open-source mais popular para orquestração de containers.

---

## O que faz

- Provisiona e gerencia um **cluster Kubernetes** na AWS
- Você faz deploy conectando ao EKS com as ferramentas padrão do ecossistema K8s
- Compatível com ferramentas, configs e padrões CNCF do ecossistema Kubernetes

---

## EKS vs ECS

| | ECS | EKS |
|---|---|---|
| Tecnologia | Nativa AWS | Kubernetes (open-source) |
| Curva de aprendizado | Menor | Maior |
| Portabilidade | Limitada à AWS | Alta — K8s roda em qualquer nuvem |
| Ecossistema | AWS nativo | Kubernetes / CNCF |
| Quando usar | Simples, AWS-first | Time já usa K8s, multi-cloud |

---

## Quando usar

- O time já usa Kubernetes e quer manter as ferramentas e workflows
- Quando a portabilidade multi-cloud é um requisito
- Quando o ecossistema CNCF é necessário

---

## Com ou sem Fargate

Assim como ECS, pode ser combinado com [[entities/aws-fargate|Fargate]] para eliminar o gerenciamento da infraestrutura do cluster.

---

## Para a prova CLF-C02

- *"Qual serviço oferece Kubernetes gerenciado na AWS?"* → **EKS**
- *"Qual a diferença entre ECS e EKS?"* → ECS é nativo AWS; EKS usa **Kubernetes**

---

## Relações

- [[entities/amazon-ecr]] — fonte das imagens Docker
- [[entities/aws-fargate]] — infraestrutura serverless opcional
- [[entities/amazon-ecs]] — alternativa nativa AWS
- [[concepts/containers]] — o conceito base

## Fontes

- [[sources/clf-c02-aula14-containers-ecr-ecs-eks-fargate]]
