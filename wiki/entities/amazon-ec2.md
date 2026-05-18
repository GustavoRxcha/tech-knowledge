---
title: "Amazon EC2 (Elastic Compute Cloud)"
type: entity
tags: [aws, ec2, computação, vm]
created: 2026-05-18
updated: 2026-05-18
sources: 1
---

# Amazon EC2 — Elastic Compute Cloud

Serviço de máquinas virtuais (instâncias) da [[aws|AWS]].

---

## O que sabemos até agora

- Apenas mencionado em [[aws-course-04-iam-groups]] como **exemplo de acesso negado**: o novo usuário developer (grupo `developers`, sem policy de EC2) recebeu `You are not authorized to perform this operation.` ao tentar acessar o console do serviço.
- A própria interface do console EC2 não carregou completamente para um usuário sem permissão — comportamento esperado.

## Fontes

- [[aws-course-04-iam-groups]]

## Lacunas

- Sem cobertura conceitual do serviço: tipos de instância, AMIs, security groups, EBS, VPC, key pairs, pricing, regions/AZs.

> [!question] Pendente de ingest dedicado.

## Relacionados

- [[aws]]
- [[principle-of-least-privilege]]
