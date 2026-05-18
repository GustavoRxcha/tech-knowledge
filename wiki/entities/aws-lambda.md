---
title: "AWS Lambda"
type: entity
tags: [aws, lambda, serverless, computação]
created: 2026-05-18
updated: 2026-05-18
sources: 1
---

# AWS Lambda

Serviço **serverless** de computação da [[aws|AWS]]. Permite executar funções sem provisionar ou gerenciar servidores.

---

## O que sabemos até agora

- Categoria: computação serverless / FaaS (Function-as-a-Service).
- Citado em [[aws-course-04-iam-groups]] como serviço típico do perfil de desenvolvedor — o grupo `developers` recebeu `AWSLambdaFullAccess`.
- Será coberto em módulo dedicado mais à frente no curso.

## Managed policy referenciada

| Policy | Efeito |
|---|---|
| `AWSLambdaFullAccess` | Acesso total ao serviço Lambda |

## Fontes

- [[aws-course-04-iam-groups]]

## Lacunas

- Sem cobertura ainda de: estrutura de função, runtimes, triggers/event sources, layers, limites de execução, pricing model, cold starts.

> [!question] Revisitar quando o módulo dedicado de Lambda for ingerido.

## Relacionados

- [[aws]]
- [[iam-policy]]
