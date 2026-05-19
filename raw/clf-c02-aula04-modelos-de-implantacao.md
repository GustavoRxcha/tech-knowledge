# Modelos de Implantação em Cloud: On-Premises, Híbrido e Cloud

> 📋 **Curso:** Introdução à Cloud — Preparatório AWS Cloud Practitioner (CLF-C02)
> 📌 **Aula:** Conceitual — Modelos de Implantação

---

## Visão Geral

O **modelo de implantação** define **onde os recursos de computação estão estruturados e hospedados** — ou seja, onde a sua solução está rodando. Existem três modelos principais:

| Modelo | Onde roda | Quem gerencia |
|---|---|---|
| **On-Premises** | Data center próprio / local | A própria organização |
| **Híbrido** | Parte local + parte na nuvem | Compartilhado |
| **Cloud** | Totalmente na nuvem (ex: AWS) | Provedor + organização |

---

## 1. On-Premises (Ambiente Local)

### O que é

Toda a infraestrutura está **fisicamente localizada** nas instalações da própria organização — seja em um servidor de escritório ou em um data center próprio.

### Características

- Hardware, rede, sistemas operacionais e aplicações são **comprados e gerenciados internamente**
- Total controle sobre a infraestrutura
- Altos custos de aquisição, manutenção e operação
- Escalabilidade lenta e cara

### Quando é usado

- Empresas com requisitos regulatórios que exigem dados locais
- Organizações que ainda não iniciaram a migração para a nuvem
- Sistemas legados que não foram modernizados

### Exemplo

> Uma instituição financeira com data center próprio, onde toda a infraestrutura de TI — servidores, bancos de dados, aplicações — está fisicamente nas dependências da empresa, gerenciada por uma equipe interna.

---

## 2. Híbrido (Hybrid Cloud)

### O que é

A solução está **parcialmente na nuvem e parcialmente on-premises** ao mesmo tempo. Os dois ambientes coexistem e se comunicam.

### Quando é usado

O modelo híbrido é muito comum em **cenários de migração gradual para a nuvem**:

```
Mês 1:  100% on-premises
Mês 3:  migrar primeiros 10.000 usuários → parte on-prem, parte cloud
Mês 6:  migrar mais serviços → equilíbrio híbrido
Mês 12: migração completa → 100% cloud
```

Durante esse processo de transição, a organização opera em modo híbrido — parte dos dados e aplicações ainda está no data center local, enquanto outra parte já foi migrada para a nuvem.

### Outros casos de uso do modelo híbrido

- Dados sensíveis que precisam permanecer locais por compliance, enquanto outros sistemas rodam na nuvem
- Sistemas legados que não podem ser migrados facilmente, integrados a novos serviços na nuvem
- Uso de nuvem apenas para picos de demanda (cloud bursting), mantendo infra local no restante

### Características

| Aspecto | Descrição |
|---|---|
| **Flexibilidade** | Combina o controle do on-premises com a escalabilidade da cloud |
| **Complexidade** | Maior complexidade de gerenciamento e integração |
| **Custo** | Mantém parte do custo de on-premises + custos da cloud |
| **Transição** | Modelo natural durante processos de migração |

---

## 3. Cloud (Nuvem Pública)

### O que é

Toda a infraestrutura e todos os serviços estão **hospedados e gerenciados por um provedor de nuvem** (como a AWS). Não há dependência de hardware próprio.

### Características

- Todos os recursos rodam em serviços cloud (ex: EC2, S3, RDS, Lambda)
- Sem necessidade de data center próprio
- Escalabilidade imediata, pagamento pelo uso
- Responsabilidade de infraestrutura física é do provedor

### Quando é usado

- Empresas nativas digitais (startups, SaaS)
- Organizações que concluíram a migração para a nuvem
- Novos projetos sem legado de infraestrutura

### Exemplo

> Uma empresa que usa EC2 para seus servidores, RDS para banco de dados, S3 para armazenamento e Lambda para processamento — tudo na AWS, sem nenhum servidor físico próprio.

---

## 4. Comparativo dos Modelos

| Critério | On-Premises | Híbrido | Cloud |
|---|---|---|---|
| **Localização** | Data center próprio | Local + Nuvem | Provedor cloud |
| **Controle** | Total | Parcial | Compartilhado |
| **Custo inicial** | Alto | Médio | Baixo/Zero |
| **Escalabilidade** | Lenta e cara | Parcial | Imediata |
| **Gerenciamento** | 100% interno | Compartilhado | Provedor + time |
| **Casos de uso** | Compliance, legado | Migração, compliance parcial | Novos projetos, nativas cloud |

---

## 5. Observação Importante: Nuvem Privada (Private Cloud)

> 📌 É possível construir uma **nuvem privada** usando tecnologias de nuvem, mas rodando **on-premises** (ex: VMware, OpenStack, AWS Outposts).

Isso significa que **nem todo ambiente on-premises é ausente de tecnologia cloud** — uma organização pode ter uma nuvem privada local, com características de elasticidade e automação, mas toda a infraestrutura física dentro de suas instalações.

Essa distinção é importante para não confundir:

| Conceito | Localização | Tecnologia |
|---|---|---|
| On-premises tradicional | Local | Sem cloud |
| Nuvem privada | Local | Com tecnologia cloud |
| Nuvem pública | Provedor (AWS, Azure, GCP) | Cloud |
| Nuvem híbrida | Local + Provedor | Misto |

---

## 6. Pergunta Diagnóstica

Uma forma prática de identificar o modelo de implantação:

> **"Onde está sua aplicação?"**
> - Está só no servidor local? → **On-Premises**
> - Está parte local, parte na nuvem? → **Híbrido**
> - Está toda na AWS/Azure/GCP? → **Cloud**

---

> 💡 **Dica para a prova CLF-C02:** Questões sobre modelos de implantação costumam descrever um **cenário de empresa** e pedir para identificar qual modelo está sendo usado. Foque nas palavras-chave: **"data center próprio"** → on-premises; **"migração gradual"** ou **"parte local"** → híbrido; **"tudo na nuvem"** → cloud.

---

## Links Úteis

- [Tipos de Cloud Computing — AWS (PT-BR)](https://aws.amazon.com/pt/types-of-cloud-computing/)
- Whitepaper AWS sobre modelos de implantação
- Artigo sobre diferença entre nuvem pública e privada

---

*Aula 04 — Módulo: Introdução à Cloud Computing | Curso Preparatório AWS Cloud Practitioner*
