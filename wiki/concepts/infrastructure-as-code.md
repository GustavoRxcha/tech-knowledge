---
title: "Infraestrutura como Código (Infrastructure as Code — IaC)"
type: concept
tags: [aws, iac, cloudformation, terraform, devops, automacao, clf-c02]
created: 2026-05-20
updated: 2026-05-20
sources: 1
---

# Infraestrutura como Código (Infrastructure as Code — IaC)

**IaC** é a prática de definir e provisionar infraestrutura de TI através de **arquivos de código** (geralmente JSON ou YAML), ao invés de configurações manuais via interface gráfica ou terminal.

---

## Princípio central

A infraestrutura é tratada como código-fonte: versionada, revisável, reprodutível e automatizável.

```
Manual (tradicional):
Engenheiro clica no console → cria recurso → configuração só existe "na nuvem"

IaC:
Engenheiro escreve template → commita no Git → CI/CD aplica → ambiente criado
```

---

## Benefícios

| Benefício | Descrição |
|---|---|
| **Reprodutibilidade** | Mesmo arquivo cria ambientes idênticos (dev, staging, prod) |
| **Versionamento** | Histórico de mudanças na infraestrutura via Git |
| **Automação** | Criação e destruição de ambientes com um comando |
| **Consistência** | Elimina erros de configuração manual |
| **Rollback** | Em caso de falha, a ferramenta desfaz as mudanças automaticamente |
| **Colaboração** | Code review da infraestrutura como qualquer outro código |

---

## Implementações na AWS e no mercado

| Ferramenta | Escopo | Observação |
|---|---|---|
| [[entities/aws-cloudformation]] | Apenas AWS | Solução nativa da AWS; JSON ou YAML |
| Terraform | Multi-cloud | HCL (HashiCorp Configuration Language) |
| AWS CDK | Apenas AWS | IaC usando linguagens de programação (Python, TypeScript…) |
| Pulumi | Multi-cloud | IaC em linguagens de programação |

---

## Relações

- [[entities/aws-cloudformation]] — implementação nativa de IaC na AWS
- [[entities/aws-elastic-beanstalk]] — usa CloudFormation internamente
- [[concepts/paas]] — contraste: PaaS abstrai a infra; IaC dá controle total sobre ela

## Fontes

- [[sources/clf-c02-aula08-provisioning]]
