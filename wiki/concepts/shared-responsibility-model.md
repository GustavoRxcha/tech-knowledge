---
title: "Modelo de Responsabilidade Compartilhada"
type: concept
tags: [aws, segurança, shared-responsibility, clf-c02]
created: 2026-05-26
updated: 2026-05-26
sources: 1
---

# Modelo de Responsabilidade Compartilhada

Definição clara de **quem é responsável por quê** em relação à segurança na nuvem AWS. A responsabilidade é dividida entre a AWS e o cliente.

```
[AWS]                          [Cliente]
Segurança DA nuvem    +    Segurança NA nuvem
(infraestrutura)          (o que você coloca lá)
```

---

## Responsabilidade da AWS — Segurança DA nuvem

A AWS cuida de tudo que **sustenta a infraestrutura**:

- Hardware físico dos data centers
- Rede física global
- Virtualização (hypervisor)
- Armazenamento físico
- Computação física (servidores)
- Segurança física dos data centers (acesso, câmeras, etc.)

> Se alguém invadir fisicamente um data center AWS → problema da AWS.

---

## Responsabilidade do Cliente — Segurança NA nuvem

O cliente cuida de tudo que **configura e coloca** na nuvem:

- Sistema Operacional das instâncias EC2 (patches, atualizações)
- Aplicações rodando nas instâncias
- Banco de dados (configuração e acesso)
- Dados armazenados
- Gerenciamento de identidades ([[entities/aws-iam|IAM]])
- Configuração de rede ([[entities/amazon-vpc|VPC]], [[concepts/security-group|Security Groups]])
- Criptografia dos dados ([[entities/aws-kms|KMS]])

> Se o Linux da EC2 tiver vulnerabilidade reportada → problema do cliente atualizar.

---

## Analogia: O Prédio

| Papel | Responsabilidade |
|---|---|
| **Engenheiro Civil** (AWS) | Construir o prédio com segurança estrutural |
| **Morador** (Cliente) | Trancar as portas, controlar quem entra |

```
[Prédio]
├── Fundação e estrutura → AWS
├── Portaria do condomínio → AWS
└── Tranca do apartamento → Cliente
    └── Quem convidar para entrar → Cliente
```

---

## Varia conforme o nível de abstração

| Serviço | Tipo | O cliente gerencia |
|---|---|---|
| [[entities/amazon-ec2\|EC2]] | IaaS | SO, runtime, app, dados, permissões |
| [[entities/aws-elastic-beanstalk\|Elastic Beanstalk]] | PaaS | App e dados |
| [[entities/aws-lambda\|Lambda]] | Serverless | Código e dados |

**Regra:** quanto mais gerenciado o serviço, menos infraestrutura o cliente precisa proteger.

---

## Conformidade também é compartilhada

A mesma lógica se aplica a regulações (LGPD, GDPR, HIPAA):

- AWS usa [[entities/aws-artifact|AWS Artifact]] para comprovar conformidade da infraestrutura
- Cliente precisa comprovar suas próprias configurações (IAM, KMS, retenção de dados)

---

## Palavra-gatilho na prova

| Enunciado | Resposta |
|---|---|
| "Segurança física dos data centers" | AWS |
| "Atualizar SO de uma EC2" | Cliente |
| "Gerenciar virtualização/hypervisor" | AWS |
| "Gerenciar permissões de usuários (IAM)" | Cliente |
| "Segurança DA nuvem" | Infraestrutura física — AWS |
| "Segurança NA nuvem" | Dados, apps, acesso — Cliente |

---

## Relações

- [[entities/aws-iam]] — gerenciamento de acesso é responsabilidade do cliente
- [[entities/aws-kms]] — criptografia é responsabilidade do cliente
- [[entities/amazon-ec2]] — exemplo onde a divisão é clara (SO = cliente)
- [[entities/aws-artifact]] — relatórios que comprovam conformidade da parte AWS
- [[entities/amazon-inspector]] — ajuda o cliente a cumprir sua parte (scan de vulnerabilidades)
- [[topics/aws-security]]
- [[sources/clf-c02-aulas1-6-seguranca-nuvem]]
