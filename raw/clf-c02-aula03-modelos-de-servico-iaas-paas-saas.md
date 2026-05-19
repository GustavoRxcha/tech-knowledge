# Modelos de Serviço em Cloud: IaaS, PaaS e SaaS

> 📋 **Curso:** Introdução à Cloud — Preparatório AWS Cloud Practitioner (CLF-C02)
> 📌 **Aula:** Conceitual — Modelos de Computação em Nuvem

---

## Visão Geral

Os **modelos de serviço** (também chamados de **modelos de computação em nuvem**) definem **o nível de responsabilidade** que o usuário assume sobre a infraestrutura. A escolha do modelo depende do **objetivo** e do **perfil** de quem está consumindo o serviço.

Existem três modelos:

| Modelo | Nome completo | Analogia |
|---|---|---|
| **IaaS** | Infrastructure as a Service | Você aluga o terreno e constrói |
| **PaaS** | Platform as a Service | Você aluga o espaço e decora |
| **SaaS** | Software as a Service | Você aluga pronto e usa |

---

## 1. IaaS — Infrastructure as a Service (Infraestrutura como Serviço)

### O que é

O provedor disponibiliza os **componentes básicos de TI**: servidores virtuais, armazenamento e rede. O usuário é responsável por **gerenciar e configurar** tudo acima disso.

### Quando usar

- Quando você precisa de **controle total** sobre a infraestrutura
- Quando a equipe tem capacidade técnica para configurar e manter servidores
- Quando as necessidades são muito específicas e não cabem em plataformas prontas

### Exemplo na AWS

**EC2 (Elastic Compute Cloud)** — você:
- Escolhe o tamanho da instância (CPU, memória, disco)
- Seleciona o sistema operacional
- Configura regras de rede e segurança
- Instala e mantém o software necessário
- É responsável por atualizações e patches do SO

### O que você gerencia vs o que o provedor gerencia

| Camada | Responsável |
|---|---|
| Aplicação | ✅ Você |
| Dados | ✅ Você |
| Runtime | ✅ Você |
| Sistema Operacional | ✅ Você |
| Virtualização | ☁️ AWS |
| Servidores físicos | ☁️ AWS |
| Armazenamento físico | ☁️ AWS |
| Rede física | ☁️ AWS |

---

## 2. PaaS — Platform as a Service (Plataforma como Serviço)

### O que é

O provedor oferece uma **plataforma completa** para implantação de aplicações. O usuário faz o **deploy do código** e a plataforma cuida automaticamente de toda a infraestrutura subjacente.

### Quando usar

- Quando você é **desenvolvedor** e quer focar no código, não na infraestrutura
- Quando não quer gerenciar sistema operacional, runtime ou configuração de rede
- Quando a prioridade é **velocidade de entrega** da aplicação

### Exemplo na AWS

**AWS Elastic Beanstalk** — você:
- Faz o upload do código da aplicação
- A plataforma provisiona automaticamente os servidores, balanceadores de carga, banco de dados, etc.
- Não precisa configurar nada de infraestrutura

### O que você gerencia vs o que o provedor gerencia

| Camada | Responsável |
|---|---|
| Aplicação | ✅ Você |
| Dados | ✅ Você |
| Runtime | ☁️ AWS |
| Sistema Operacional | ☁️ AWS |
| Virtualização | ☁️ AWS |
| Servidores físicos | ☁️ AWS |
| Armazenamento físico | ☁️ AWS |
| Rede física | ☁️ AWS |

---

## 3. SaaS — Software as a Service (Software como Serviço)

### O que é

Um produto **completo e pronto para uso**, executado e gerenciado inteiramente pelo provedor. O usuário apenas **consome** o serviço, sem se preocupar com nenhum aspecto técnico.

### Quando usar

- Quando o objetivo é simplesmente **usar** uma funcionalidade
- Sem necessidade de implantação, configuração ou manutenção
- Quando qualquer usuário final (técnico ou não) precisa acessar o serviço

### Exemplos

- **Gmail** (e-mail como serviço)
- **Slack**, **Microsoft Teams** (mensagens instantâneas)
- **Salesforce** (CRM como serviço)
- **Dropbox**, **Google Drive** (armazenamento como serviço)

### O que você gerencia vs o que o provedor gerencia

| Camada | Responsável |
|---|---|
| Uso da aplicação | ✅ Você |
| Aplicação | ☁️ Provedor |
| Dados (infraestrutura) | ☁️ Provedor |
| Runtime | ☁️ Provedor |
| Sistema Operacional | ☁️ Provedor |
| Virtualização | ☁️ Provedor |
| Servidores físicos | ☁️ Provedor |
| Rede física | ☁️ Provedor |

---

## 4. Comparativo Completo: Do On-Premises ao SaaS

A tabela abaixo mostra como a responsabilidade migra do usuário para o provedor conforme o modelo:

| Camada | On-Premises | IaaS | PaaS | SaaS |
|---|---|---|---|---|
| Aplicação | ✅ Você | ✅ Você | ✅ Você | ☁️ Provedor |
| Dados | ✅ Você | ✅ Você | ✅ Você | ☁️ Provedor |
| Runtime | ✅ Você | ✅ Você | ☁️ Provedor | ☁️ Provedor |
| Sistema Operacional | ✅ Você | ✅ Você | ☁️ Provedor | ☁️ Provedor |
| Virtualização | ✅ Você | ☁️ Provedor | ☁️ Provedor | ☁️ Provedor |
| Servidores | ✅ Você | ☁️ Provedor | ☁️ Provedor | ☁️ Provedor |
| Armazenamento | ✅ Você | ☁️ Provedor | ☁️ Provedor | ☁️ Provedor |
| Rede | ✅ Você | ☁️ Provedor | ☁️ Provedor | ☁️ Provedor |

> 📌 **Regra geral:** Quanto mais à direita na tabela, **menos você gerencia** e **mais o provedor cuida**.

---

## 5. Resumo por Perfil de Usuário

| Perfil | Modelo recomendado | Foco |
|---|---|---|
| Equipe de infraestrutura / SysAdmin | **IaaS** | Controle total, configuração granular |
| Desenvolvedor / DevOps | **PaaS** | Deploy rápido sem gerenciar infra |
| Usuário final / Negócio | **SaaS** | Apenas usar o produto |

---

## 6. Analogia para Fixar

Pense em **pizza**:

| Cenário | Equivalente Cloud |
|---|---|
| Você faz tudo em casa (compra ingredientes, assa) | **On-Premises** |
| Você compra a massa pronta e monta | **IaaS** |
| Você pede para montar e só escolhe os ingredientes | **PaaS** |
| Você pede a pizza pronta e só come | **SaaS** |

---

> 💡 **Dica para a prova CLF-C02:** Questões sobre modelos de serviço geralmente apresentam um **cenário de usuário** e perguntam qual modelo se aplica. Foque em identificar **quem gerencia o quê** em cada modelo, especialmente a distinção entre **IaaS e PaaS**, que é a mais cobrada.

---

## Links Úteis

- [Tipos de Cloud Computing — AWS (PT-BR)](https://aws.amazon.com/pt/types-of-cloud-computing/)

---

*Aula 03 — Módulo: Introdução à Cloud Computing | Curso Preparatório AWS Cloud Practitioner*
