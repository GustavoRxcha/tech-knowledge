---
title: "Amazon ECR (Elastic Container Registry)"
type: entity
tags: [aws, ecr, containers, docker, registro-de-imagens]
created: 2026-05-20
updated: 2026-05-20
sources: 1
---

# Amazon ECR — Elastic Container Registry

**Repositório gerenciado de imagens Docker** da [[entities/aws|AWS]]. Equivalente a um Docker Hub privado dentro da sua conta AWS.

---

## O que faz

- Armazena imagens Docker em diferentes versões (tags)
- Permite compartilhar imagens entre equipes e serviços AWS
- Integrado nativamente com [[entities/amazon-ecs|ECS]] e [[entities/amazon-eks|EKS]]
- Suporta versionamento de imagens

---

## Fluxo de uso

```
1. Você escreve o Dockerfile
2. docker build → gera a imagem localmente
3. docker push → imagem vai para o ECR (na nuvem)
4. ECS ou EKS fazem pull do ECR → executam os containers
```

```
[Desenvolvedor]
      ↓ docker build + push
   [ECR]
      ↓ pull automático
[ECS / EKS] → containers em execução
```

> O ECR é o ponto de partida — sem uma imagem armazenada, não há container para executar.

---

## Relações

- [[entities/amazon-ecs]] — consome imagens do ECR para execução
- [[entities/amazon-eks]] — consome imagens do ECR para execução
- [[concepts/containers]] — o conceito base

## Fontes

- [[sources/clf-c02-aula14-containers-ecr-ecs-eks-fargate]]
