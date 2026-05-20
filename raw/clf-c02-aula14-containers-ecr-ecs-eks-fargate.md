# Containers na AWS: ECR, ECS, EKS e Fargate

> 📋 **Curso:** Computação na AWS — Preparatório AWS Cloud Practitioner (CLF-C02)
> 📌 **Aula:** Conceitual — Containers e Serviços de Orquestração na AWS

---

## 1. O que são Containers?

**Containers** são uma forma padronizada de **empacotar uma aplicação e todas as suas dependências** em uma única unidade executável, isolada e portável.

### Características principais

- **Isolamento:** cada container roda como um processo isolado — não interfere em outros
- **Portabilidade:** "funciona na minha máquina" deixa de ser um problema — o container roda igual em qualquer ambiente
- **Leveza:** mais eficiente que máquinas virtuais completas — compartilham o kernel do SO do host
- **Padronização:** a ferramenta mais popular é o **Docker**

### O que um container resolve na prática

```
Sem containers:
"Funciona na minha máquina" ← problema clássico de desenvolvimento
Configurar banco de dados, dependências, variáveis de ambiente → trabalhoso

Com containers:
Configura UMA vez no Dockerfile → build da imagem
→ roda igual em qualquer máquina/servidor/nuvem
```

### Fluxo básico com Docker

```
[Dockerfile]         [Imagem Docker]      [Container em execução]
(instruções)  →  docker build  →  docker run  →  [Aplicação rodando]
```

### Casos de uso

- Empacotar e distribuir aplicações de forma consistente
- Executar bancos de dados localmente no desenvolvimento
- Escalabilidade de microsserviços
- Automação de testes e pipelines de CI/CD
- Deploy em qualquer ambiente (local, cloud, on-premises)

---

## 2. Os 4 Serviços de Containers na AWS

A AWS oferece quatro serviços principais relacionados a containers, cada um com um papel específico:

```
[ECR]  →  armazena imagens
  ↓
[ECS ou EKS]  →  orquestra e executa containers
  ↓
[Fargate]  →  elimina gerenciamento de infraestrutura (opcional)
```

---

## 3. Amazon ECR — Elastic Container Registry

### O que é

O **ECR** é o **repositório gerenciado de imagens Docker** da AWS — equivalente a um Docker Hub privado dentro da sua conta AWS.

### O que faz

- Armazena imagens Docker em diferentes versões
- Permite compartilhar imagens entre equipes e serviços AWS
- Integrado nativamente com ECS e EKS
- Suporta versionamento de imagens (tags)

### Fluxo de uso

```
1. Você escreve o Dockerfile (instruções da imagem)
2. Faz o build: docker build → gera a imagem
3. Faz o push para o ECR: a imagem fica armazenada na nuvem
4. ECS ou EKS fazem o pull da imagem do ECR para executar os containers
```

```
[Desenvolvedor]
      ↓ docker build + push
   [ECR]
      ↓ pull automático
[ECS / EKS] → executa os containers
```

> 📌 O ECR é o ponto de partida — sem uma imagem armazenada, não há container para executar.

---

## 4. Amazon ECS — Elastic Container Service

### O que é

O **ECS** é o serviço de **orquestração e execução de containers Docker** nativo da AWS. Ele gerencia onde e como os containers são executados dentro de um **cluster**.

### O que faz

- Executa containers a partir de imagens armazenadas no ECR
- Gerencia o ciclo de vida dos containers (start, stop, restart)
- Distribui containers entre instâncias do cluster
- Integra com ELB, Auto Scaling, IAM e outros serviços AWS

### Quando usar

- Quando você quer executar containers Docker na AWS
- Quando prefere a solução nativa e gerenciada da própria AWS
- Quando não precisa de Kubernetes

---

## 5. Amazon EKS — Elastic Kubernetes Service

### O que é

O **EKS** é o serviço gerenciado de **Kubernetes** da AWS. Kubernetes (K8s) é a plataforma open-source mais popular para orquestração de containers.

### O que faz

- Provisiona e gerencia um **cluster Kubernetes** na AWS
- Você faz o deploy dos seus containers conectando ao EKS
- Compatível com ferramentas e configurações padrão do ecossistema Kubernetes

### ECS vs EKS

| | ECS | EKS |
|---|---|---|
| **Tecnologia** | Nativa AWS | Kubernetes (open-source) |
| **Curva de aprendizado** | Menor | Maior |
| **Portabilidade** | Limitada à AWS | Alta — Kubernetes roda em qualquer nuvem |
| **Ecossistema** | AWS nativo | Kubernetes / CNCF |
| **Quando usar** | Solução simples, AWS-first | Time já usa K8s, multi-cloud |

> 📌 Para a prova CLF-C02, o importante é saber que **ECS = orquestrador nativo AWS** e **EKS = Kubernetes gerenciado na AWS**.

---

## 6. AWS Fargate

### O que é

O **AWS Fargate** é o motor de computação **serverless para containers** — elimina a necessidade de gerenciar a infraestrutura (servidores/instâncias EC2) que executa os containers.

### Como funciona

Sem Fargate, ao usar ECS ou EKS, você ainda precisa provisionar e gerenciar as instâncias EC2 que formam o cluster. Com Fargate:

```
Sem Fargate:
[ECS/EKS] → você provisiona e gerencia instâncias EC2 do cluster

Com Fargate:
[ECS/EKS + Fargate] → AWS gerencia toda a infraestrutura automaticamente
                       você só define CPU/memória por container
```

### Benefícios

| Benefício | Descrição |
|---|---|
| **Serverless** | Sem gerenciamento de servidores ou clusters |
| **Menos configuração** | Define apenas os recursos necessários por container |
| **Escalabilidade automática** | Infraestrutura escala conforme os containers precisam |
| **Pagamento por uso** | Paga pelo tempo de CPU e memória consumidos pelos containers |

### Quando usar

- Quando quer rodar containers sem gerenciar a infraestrutura subjacente
- Complementa tanto o ECS quanto o EKS

---

## 7. Visão Geral — Como os Serviços se Conectam

```
┌─────────────────────────────────────────────────────┐
│                   Sua aplicação                      │
│                                                     │
│  [Dockerfile] → build → [Imagem Docker]             │
│                              ↓                      │
│                           [ECR]                     │
│                    (repositório de imagens)         │
│                              ↓                      │
│              ┌───────────────┴──────────────┐        │
│           [ECS]                          [EKS]      │
│      (orquestrador nativo)         (Kubernetes)     │
│              └───────────────┬──────────────┘        │
│                              ↓                      │
│                         [Fargate]                   │
│               (infraestrutura serverless)           │
│                    (opcional, mas recomendado)      │
└─────────────────────────────────────────────────────┘
```

---

## 8. Comparativo dos 4 Serviços

| Serviço | Sigla | Função | Analogia |
|---|---|---|---|
| **Elastic Container Registry** | ECR | Armazena imagens Docker | Almoxarifado de imagens |
| **Elastic Container Service** | ECS | Orquestra e executa containers (nativo AWS) | Gerente de containers |
| **Elastic Kubernetes Service** | EKS | Kubernetes gerenciado na AWS | Gerente de containers (K8s) |
| **Fargate** | — | Infraestrutura serverless para ECS/EKS | Equipe de infra automática |

---

## 9. Containers vs Serverless (Lambda)

| | Containers (ECS/EKS) | Serverless (Lambda) |
|---|---|---|
| **Unidade** | Container (imagem Docker) | Função |
| **Controle** | Maior — você define o ambiente | Menor — AWS gerencia tudo |
| **Tempo de execução** | Longo (aplicações contínuas) | Curto (até 15 minutos) |
| **Casos de uso** | APIs, microsserviços, apps complexas | Processamento por evento, automações |

---

> 💡 **Dica para a prova CLF-C02:** Questões típicas sobre containers:
> - *"Onde armazenar imagens Docker na AWS?"* → **ECR**
> - *"Qual serviço executa containers Docker de forma nativa na AWS?"* → **ECS**
> - *"Qual serviço oferece Kubernetes gerenciado na AWS?"* → **EKS**
> - *"Qual serviço elimina a necessidade de gerenciar servidores para rodar containers?"* → **Fargate**
> - *"Qual a diferença entre ECS e EKS?"* → ECS é nativo AWS; EKS usa **Kubernetes**

---

## Links Úteis

- [Amazon ECR](https://aws.amazon.com/pt/ecr/)
- [Amazon ECS](https://aws.amazon.com/pt/ecs/)
- [Amazon EKS](https://aws.amazon.com/pt/eks/)
- [AWS Fargate](https://aws.amazon.com/pt/fargate/)

---

*Aula 06 — Módulo: Computação na AWS | Curso Preparatório AWS Cloud Practitioner*
