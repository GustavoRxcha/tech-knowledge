---
title: "AWS CLI (Command Line Interface)"
type: concept
tags: [aws, cli, automacao, terminal, devops, clf-c02]
created: 2026-05-20
updated: 2026-05-20
sources: 1
---

# AWS CLI (Command Line Interface)

A **AWS CLI** é uma ferramenta instalada localmente que permite interagir com **todas as APIs da AWS via linha de comando**. É uma das três formas principais de acessar os serviços AWS (junto com o Console e os SDKs).

---

## Instalação e configuração

```bash
# Download: https://aws.amazon.com/pt/cli/

# Configuração inicial (Access Key + Secret + Região padrão)
aws configure
```

---

## Comandos comuns

```bash
aws s3 ls                                     # listar buckets S3
aws ec2 describe-instances                    # listar instâncias EC2
aws s3 cp arquivo.txt s3://meu-bucket/        # upload para S3
aws iam list-users                            # listar usuários IAM
```

---

## Compatibilidade

Disponível para **Windows, macOS e Linux**.

---

## Quando usar

- Automação de tarefas repetitivas via scripts (bash, PowerShell)
- Integração com pipelines de CI/CD
- Administração de recursos em grande escala
- Quando o Console web seria ineficiente ou não permite automação

---

## Comparativo com outras formas de acesso

| Forma | Interface | Melhor para |
|---|---|---|
| Console | Web (visual) | Exploração, tarefas manuais |
| **CLI** | Terminal | Automação, administração |
| SDK | Código da aplicação | Integração programática |

---

## Relações

- [[entities/aws]] — a CLI interage com todas as APIs da AWS
- [[concepts/infrastructure-as-code]] — complementa IaC em pipelines
- [[concepts/access-keys]] — a CLI usa Access Key + Secret para autenticação

## Fontes

- [[sources/clf-c02-aula08-provisioning]]
