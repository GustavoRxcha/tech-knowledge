---
title: "CLF-C02 Aula 14 — Containers na AWS: ECR, ECS, EKS e Fargate"
type: source
tags: [aws, clf-c02, containers, docker, ecr, ecs, eks, fargate, kubernetes]
created: 2026-05-20
updated: 2026-05-20
sources: 1
---

# CLF-C02 Aula 14 — Containers na AWS: ECR, ECS, EKS e Fargate

O que são containers (Docker), os 4 serviços AWS para containers (ECR, ECS, EKS, Fargate) e suas relações. Comparativo Containers vs Serverless (Lambda).

---

## Origem

- **Arquivo:** `raw/clf-c02-aula14-containers-ecr-ecs-eks-fargate.md`
- **Trilha:** CLF-C02 — Preparatório AWS Cloud Practitioner
- **Módulo:** Computação na AWS (aula 06 do módulo / aula 14 do curso)

---

## O que são containers

Forma padronizada de **empacotar uma aplicação e todas as suas dependências** em uma única unidade executável, isolada e portável.

**Características:** isolamento · portabilidade ("funciona na minha máquina" eliminado) · leveza (compartilham kernel do SO) · padronização (Docker)

**Fluxo básico:**
```
[Dockerfile] → docker build → [Imagem Docker] → docker run → [Container em execução]
```

---

## Os 4 serviços AWS para containers

```
[ECR] → armazena imagens
  ↓
[ECS ou EKS] → orquestra e executa containers
  ↓
[Fargate] → elimina gerenciamento de infra (opcional)
```

---

## Amazon ECR — Elastic Container Registry

**Repositório gerenciado de imagens Docker** — Docker Hub privado dentro da conta AWS.

- Armazena imagens em diferentes versões (tags)
- Integrado nativamente com ECS e EKS
- Fluxo: `docker build` → `docker push para ECR` → ECS/EKS fazem pull e executam

---

## Amazon ECS — Elastic Container Service

**Orquestrador nativo AWS** para containers Docker. Gerencia onde e como os containers são executados em um cluster.

- Gerencia ciclo de vida dos containers (start, stop, restart)
- Integra com ELB, Auto Scaling, IAM
- Quando usar: solução simples, AWS-first, sem necessidade de Kubernetes

---

## Amazon EKS — Elastic Kubernetes Service

**Kubernetes gerenciado na AWS**. Kubernetes (K8s) é a plataforma open-source mais popular para orquestração de containers.

- Provisiona e gerencia cluster Kubernetes na AWS
- Compatível com ferramentas padrão do ecossistema K8s

**ECS vs EKS:**

| | ECS | EKS |
|---|---|---|
| Tecnologia | Nativa AWS | Kubernetes (open-source) |
| Curva de aprendizado | Menor | Maior |
| Portabilidade | Limitada à AWS | Alta — roda em qualquer nuvem |
| Quando usar | Simples, AWS-first | Time já usa K8s, multi-cloud |

---

## AWS Fargate

**Motor de computação serverless para containers** — elimina o gerenciamento de instâncias EC2 que formam o cluster.

```
Sem Fargate: [ECS/EKS] → você provisiona e gerencia as instâncias EC2 do cluster
Com Fargate: [ECS/EKS + Fargate] → AWS gerencia tudo; você define CPU/memória por container
```

**Benefícios:** sem gerenciamento de servidores · menos configuração · escalabilidade automática · paga por uso (CPU + memória dos containers)

---

## Containers vs Serverless (Lambda)

| | Containers (ECS/EKS) | Serverless (Lambda) |
|---|---|---|
| Unidade | Container (imagem Docker) | Função |
| Controle | Maior — você define o ambiente | Menor — AWS gerencia tudo |
| Tempo de execução | Longo (aplicações contínuas) | Curto (até 15 minutos) |
| Casos de uso | APIs, microsserviços, apps complexas | Processamento por evento, automações |

---

## Conceitos/entidades relacionados

- [[concepts/containers]]
- [[entities/amazon-ecr]]
- [[entities/amazon-ecs]]
- [[entities/amazon-eks]]
- [[entities/aws-fargate]]
- [[concepts/serverless]]
- [[entities/aws-lambda]]
