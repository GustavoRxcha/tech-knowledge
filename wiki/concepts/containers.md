---
title: "Containers"
type: concept
tags: [containers, docker, portabilidade, microsservicos, devops]
created: 2026-05-20
updated: 2026-05-20
sources: 1
---

# Containers

**Containers** são uma forma padronizada de **empacotar uma aplicação e todas as suas dependências** (bibliotecas, configs, runtime) em uma única unidade executável, isolada e portável.

---

## Características

| Característica | Descrição |
|---|---|
| **Isolamento** | Cada container roda como processo isolado — não interfere em outros |
| **Portabilidade** | Roda igual em qualquer ambiente (local, staging, produção, qualquer nuvem) |
| **Leveza** | Mais eficiente que VMs completas — compartilham o kernel do SO do host |
| **Padronização** | A ferramenta mais popular é o **Docker** |

---

## O problema que resolve

```
SEM containers:
"Funciona na minha máquina" ← problema clássico
Configurar dependências em cada ambiente → trabalhoso e propenso a erros

COM containers:
Configura UMA vez no Dockerfile → build da imagem
→ roda igual em qualquer máquina / servidor / nuvem
```

---

## Fluxo básico com Docker

```
[Dockerfile]          [Imagem Docker]       [Container em execução]
(instruções)  →  docker build  →  docker run  →  [Aplicação rodando]
```

- **Dockerfile:** arquivo de instruções para construir a imagem
- **Imagem Docker:** snapshot imutável da aplicação + dependências
- **Container:** instância em execução de uma imagem

---

## Containers vs VMs

| | Container | VM |
|---|---|---|
| Isolamento | Processo isolado | Sistema operacional inteiro |
| Overhead | Mínimo (compartilha kernel) | Alto (SO próprio por VM) |
| Inicialização | Segundos | Minutos |
| Portabilidade | Alta | Média |

---

## Containers vs Serverless (Lambda)

| | Containers | Lambda |
|---|---|---|
| Controle | Maior — você define o ambiente | Menor |
| Tempo de execução | Longo (apps contínuas) | Curto (até 15 min) |
| Casos de uso | APIs, microsserviços | Processamento por evento |

---

## Casos de uso

- Empacotar e distribuir aplicações de forma consistente
- Escalabilidade de microsserviços
- Pipelines de CI/CD e testes automatizados
- Deploy em qualquer ambiente (local, cloud, on-premises)

---

## Relações

- [[entities/amazon-ecr]] — repositório de imagens Docker na AWS
- [[entities/amazon-ecs]] — orquestração de containers na AWS (nativo)
- [[entities/amazon-eks]] — orquestração via Kubernetes na AWS
- [[entities/aws-fargate]] — infraestrutura serverless para containers
- [[concepts/serverless]] — alternativa para workloads de curta duração
- [[concepts/microservices]] — containers são o empacotamento padrão de microsserviços

## Fontes

- [[sources/clf-c02-aula14-containers-ecr-ecs-eks-fargate]]
