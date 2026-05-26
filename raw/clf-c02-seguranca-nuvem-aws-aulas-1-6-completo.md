# Segurança na Nuvem com AWS — Módulo Completo

> 📋 **Curso:** Segurança na Nuvem com AWS — Preparatório AWS Cloud Practitioner (CLF-C02)
> 📌 **Módulo:** Conceitual | 6 aulas | Sem pré-requisitos

---

## Visão Geral do Módulo

Este módulo cobre todos os **principais conceitos e serviços de segurança AWS** que caem no exame CLF-C02. O foco é entender tanto os conceitos fundamentais quanto os serviços práticos de proteção.

**Percurso das 6 aulas:**
1. Modelo de Responsabilidade Compartilhada
2. Criptografia (KMS)
3. Gerenciamento de Acessos (IAM)
4. AWS Organizations
5. Conformidade e Suporte (AWS Artifact)
6. Serviços Adicionais (WAF, Shield, Inspector, GuardDuty)

---
---

# AULA 1: Modelo de Responsabilidade Compartilhada

## 1. A Pergunta Fundamental

> "Quando uso EC2, RDS ou Lambda — **quem é responsável pela segurança**? Eu ou a AWS?"

**Resposta:** Os **dois**. A responsabilidade é compartilhada entre cliente e AWS.

---

## 2. O que é o Modelo de Responsabilidade Compartilhada?

É a **definição clara de responsabilidades** entre cliente e AWS em relação à segurança na nuvem.

```
[AWS]                          [Cliente]
Segurança DA nuvem    +    Segurança NA nuvem
(infraestrutura)          (o que você coloca lá)
```

---

## 3. Responsabilidade da AWS (Segurança DA Nuvem)

A AWS é responsável por tudo que **sustenta a nuvem**:

```
[AWS cuida de:]
├── Hardware físico dos data centers
├── Rede física global
├── Virtualização (hypervisor)
├── Armazenamento físico
├── Computação física (servidores)
└── Segurança dos data centers (acesso físico, câmeras, etc.)
```

> ✅ Se alguém tentar invadir fisicamente um data center AWS — problema da AWS.

---

## 4. Responsabilidade do Cliente (Segurança NA Nuvem)

O cliente é responsável por tudo que **coloca e configura** na nuvem:

```
[Cliente cuida de:]
├── Sistema Operacional das instâncias EC2
│   └── Patches e atualizações de segurança
├── Aplicações rodando nas instâncias
├── Banco de dados (configuração e acesso)
├── Dados armazenados
├── Gerenciamento de identidades (IAM)
├── Configuração de rede (VPC, security groups)
└── Criptografia dos dados
```

> ⚠️ Se o Linux da sua EC2 tiver vulnerabilidade reportada — problema do **cliente** atualizar.

---

## 5. Analogia: O Prédio

| Papel | Responsabilidade |
|---|---|
| **Engenheiro Civil** (AWS) | Projetar e construir o prédio com segurança estrutural |
| **Morador** (Cliente) | Trancar as portas, controlar quem entra no apartamento |

```
[Prédio construído]
├── Fundação segura → AWS
├── Paredes e estrutura → AWS
├── Portaria do condomínio → AWS
└── Tranca do apartamento → Cliente
    └── Quem convidar para entrar → Cliente
```

---

## 6. Dois Termos Essenciais

| Termo | Definição | Responsável |
|---|---|---|
| **Segurança DA nuvem** | Segurança da infraestrutura física e virtualização | **AWS** |
| **Segurança NA nuvem** | Segurança do que o cliente configura e usa | **Cliente** |

---

## 7. Exemplo Prático: EC2

```
Instância EC2 em produção:

[Camada]          [O que é]             [Responsável]
Hardware          Servidor físico        AWS
Rede física       Cabos, switches        AWS
Virtualização     Hypervisor, VMware     AWS
─────────────────────────────────────────────────────
Sistema Op.       Linux / Windows        Cliente
Aplicação         Seu servidor web       Cliente
Banco de dados    MySQL instalado        Cliente
Dados             Arquivos do usuário    Cliente
Permissões        IAM, grupos, políticas Cliente
```

---

## 8. Varia Conforme o Serviço!

> 📌 A divisão muda dependendo do nível de abstração do serviço.

```
EC2 (IaaS) → Cliente gerencia SO, runtime, app
Elastic Beanstalk (PaaS) → AWS gerencia mais camadas
Lambda (Serverless) → AWS gerencia quase tudo de infra
```

Quanto mais gerenciado o serviço, menos o cliente precisa cuidar de segurança de infraestrutura.

---

> 💡 **Dica para a prova CLF-C02:**

- *"Quem é responsável pela segurança física dos data centers?"* → **AWS**
- *"Quem deve atualizar o SO de uma EC2?"* → **Cliente**
- *"Quem cuida da virtualização?"* → **AWS**
- *"Quem gerencia permissões de usuários?"* → **Cliente**
- *"O que é segurança DA nuvem?"* → Infraestrutura física — **responsabilidade AWS**

---
---

# AULA 2: Criptografia — KMS (Key Management Service)

## 1. O que é Criptografia?

**Criptografia** é a prática de proteger informações por meio de algoritmos codificados, hashes e assinaturas digitais.

**Objetivo:** Garantir que dados sensíveis só possam ser lidos por quem tem autorização.

```
[Dado Original]     [Criptografado]    [Descriptografado]
"senha123"    →    "x9#mK!2@qP"   →   "senha123"
                    ↑                    ↑
               Com a chave          Com a chave
               ninguém lê           autorizado lê
```

---

## 2. Quando Criptografar?

### Dados em Repouso (Data at Rest)

Dados **armazenados** — não estão trafegando.

```
[Exemplos:]
├── Volume EBS com dados do servidor
├── Objetos em buckets S3
├── Banco de dados RDS
└── Backups e snapshots
```

> ⚠️ Se alguém tiver acesso indevido ao disco — sem criptografia, lê tudo.

### Dados em Trânsito (Data in Transit)

Dados **sendo transmitidos** de um ponto a outro.

```
[Exemplos:]
├── Login em um aplicativo (usuário → servidor)
├── Dados entre EC2 e RDS
├── Upload de arquivo para S3
└── Comunicação entre APIs
```

> ⚠️ Se alguém interceptar a comunicação — sem criptografia, lê tudo.

---

## 3. AWS KMS — Key Management Service

**KMS** é o serviço gerenciado da AWS para **criação e gestão de chaves criptográficas**.

### Características

| Característica | Descrição |
|---|---|
| **Gerenciado** | Sem infraestrutura para provisionar |
| **Centralizado** | Gerencia todas as chaves em um lugar |
| **Integrado** | Funciona com EBS, S3, RDS, DynamoDB, etc. |
| **Controle de acesso** | Define quem pode usar cada chave |
| **Auditoria** | Logs de uso das chaves via CloudTrail |

---

## 4. Criptografia em Repouso com KMS

**Exemplo: DynamoDB com dados criptografados**

```
[Dados originais]
Nome: "João Silva"
CPF:  "123.456.789-00"
        ↓ KMS gera chave
[Dados criptografados no DynamoDB]
Nome: "a3#9xK@2mP"
CPF:  "8!nQ%7rZ#1"
        ↓ Apenas quem tem a chave
[Dados legíveis]
Nome: "João Silva"
CPF:  "123.456.789-00"
```

> ✅ Mesmo que alguém acesse o banco diretamente — sem a chave, dados são ilegíveis.

---

## 5. Criptografia em Trânsito com KMS

**Exemplo: Aplicação acessando bucket S3**

```
[Aplicação]
    ↓ HTTPS (SSL/TLS)
[Camada SSL + Certificado]
    ↓ Dados criptografados em trânsito
[Bucket S3]
```

### Como funciona

1. Conexão estabelecida via **HTTPS**
2. Certificado digital autentica o sistema
3. Dados trafegam criptografados
4. Apenas o sistema certificado pode descriptografar

---

## 6. Resumo: KMS

```
KMS (Key Management Service)
├── Cria e gerencia chaves criptográficas
├── Dados em Repouso → EBS, S3, RDS, DynamoDB
└── Dados em Trânsito → SSL/TLS, HTTPS
```

---

> 💡 **Dica para a prova CLF-C02:**

- *"Qual serviço gerencia chaves criptográficas na AWS?"* → **KMS**
- *"Como proteger dados em um volume EBS?"* → **Criptografia com KMS**
- *"O que são dados em repouso?"* → Dados **armazenados** (EBS, S3, RDS)
- *"O que são dados em trânsito?"* → Dados **sendo transmitidos** (HTTPS, SSL)

---
---

# AULA 3: Gerenciamento de Acessos — IAM

## 1. O que é IAM?

**IAM = Identity and Access Management** — Serviço **gratuito** da AWS para gerenciar **quem pode acessar o quê**.

```
IAM responde: "Quem pode fazer o quê na AWS?"
```

### Características

- Serviço **gratuito**
- Controle **granular** de permissões
- Gerencia usuários, grupos, políticas e roles
- Suporte a MFA (Multi-Factor Authentication)
- Federação de identidades (Google, AD, etc.)

---

## 2. Usuário Root

### O que é

O **usuário root** é criado automaticamente ao abrir uma conta AWS. Tem acesso irrestrito a **tudo**.

```
[Usuário Root]
├── Pode fazer QUALQUER coisa
├── Em QUALQUER recurso
├── Sem exceção
└── Sem limite
```

### ⚠️ Por que NÃO usar o root?

```
[Riscos do root]
├── Um erro acidental pode apagar tudo
├── Se comprometido, atacante controla tudo
├── Não há limitação nenhuma de ação
└── Dificulta auditoria
```

### Boas Práticas para o Root

1. **Nunca usar no dia a dia**
2. Criar usuários IAM com menor privilégio
3. **Ativar MFA obrigatoriamente** no root
4. Guardar as credenciais em local seguro

---

## 3. Usuários IAM

### O que é

**Usuários** são identidades criadas na AWS para representar pessoas ou aplicações.

```
[Usuário IAM]
├── Pode ser: Uma pessoa ou uma aplicação/sistema
├── Composto de: Nome + credenciais
└── Por padrão: Sem acesso a nada (princípio do menor privilégio)
```

### Princípio do Menor Privilégio

> Todo usuário novo **não tem acesso a nada** por padrão.

```
Usuário recém criado → Acesso: ZERO
    ↓ Você explicitamente adiciona permissões
Usuário com permissão → Acesso: Apenas o que você definiu
```

Você deve explicitamente conceder **apenas as permissões necessárias**.

---

## 4. Grupos IAM

### O que é

**Grupos** são conjuntos de usuários que compartilham as mesmas permissões.

```
[Grupo: developers]
├── Usuário: João
├── Usuário: Maria
└── Usuário: Pedro
└── Permissão: AWSLambdaFullAccess

[Grupo: admins]
├── Usuário: Carlos
└── Permissão: AdministratorAccess
```

### Regras dos Grupos

- Um usuário pode pertencer a **vários grupos**
- Grupos **NÃO** podem ser aninhados (grupo dentro de grupo)
- Permissões são herdadas do grupo pelo usuário

```
Nova permissão para grupo developers
    ↓ Todos os usuários do grupo
João ✅ | Maria ✅ | Pedro ✅
```

---

## 5. Políticas IAM (Policies)

### O que é

**Políticas** são documentos JSON que definem **o que** pode ser feito e **em quais recursos**.

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": "s3:ListBucket",
      "Resource": "arn:aws:s3:::exemplo-bucket"
    }
  ]
}
```

### Interpretando

```
Effect:   "Allow"         → Permite (ou Deny para negar)
Action:   "s3:ListBucket" → Listar objetos em um bucket S3
Resource: "arn:aws:s3:::exemplo-bucket" → Apenas nesse bucket específico
```

### Alto Nível de Granularidade

Uma política pode ser extremamente precisa:

```
[Aplicação de Upload]
├── Pode: PutObject (inserir)
├── NÃO pode: ListBucket (listar)
├── NÃO pode: GetObject (baixar)
└── NÃO pode: DeleteObject (deletar)

[Aplicação de Leitura]
├── Pode: GetObject (baixar)
├── Pode: ListBucket (listar)
└── NÃO pode: PutObject, DeleteObject
```

---

## 6. Roles (Funções)

### O que é

**Roles** são identidades com permissões específicas, **sem senha**, que podem ser **assumidas temporariamente** por usuários, aplicações ou serviços.

```
[Role: acesso-s3-fotos]
├── Sem senha (não é um usuário)
├── Pode ser assumida por: usuários, EC2, Lambda
└── Permissão: Acesso ao bucket fotos
```

### Analogia

> Role = Chapéu que você veste temporariamente.
> Quando tira o chapéu, volta às permissões normais.

```
[Desenvolvedor William]
Permissões normais: Acesso ao ambiente dev
    ↓ Assume role de deploy
Permissões com role: Acesso a produção
    ↓ Sessão expira / role removida
Permissões normais: Acesso ao ambiente dev (volta ao normal)
```

### Exemplo Prático: Aplicação em EC2 acessando S3

```
Passo 1: Admin cria Role com acesso ao bucket "fotos"
Passo 2: Desenvolvedor sobe EC2 com essa Role associada
Passo 3: Aplicação na EC2 solicita credenciais ao STS
Passo 4: STS retorna credenciais temporárias
Passo 5: Aplicação usa credenciais para acessar bucket "fotos"
```

### Role Switch

Um usuário pode ter múltiplas roles e alternar entre elas:

```
[Usuário: Carlos (infra)]
├── Role: conta-producao    → Acessa ambiente prod
├── Role: conta-desenvolvimento → Acessa ambiente dev
└── Role: conta-teste       → Acessa ambiente teste

Carlos faz "role switch" para acessar o ambiente que precisa.
```

---

## 7. Resumo IAM

| Conceito | Definição | Uso |
|---|---|---|
| **Usuário Root** | Conta original, acesso irrestrito | Evitar usar |
| **Usuário IAM** | Identidade para pessoa/sistema | Uso diário |
| **Grupo** | Conjunto de usuários com mesmas permissões | Organizar permissões |
| **Política** | Documento JSON com permissões | Definir o que pode fazer |
| **Role** | Identidade temporária assumível | Serviços, cross-account |
| **MFA** | Segundo fator de autenticação | Segurança extra |

---

> 💡 **Dica para a prova CLF-C02:**

- *"Qual serviço gerencia usuários e permissões?"* → **IAM**
- *"É gratuito?"* → **SIM**
- *"Por padrão, um novo usuário tem acesso a quê?"* → **Nada** (menor privilégio)
- *"Como dar permissão a 50 desenvolvedores de uma vez?"* → **Grupo IAM**
- *"Qual identidade um Lambda usa para acessar S3?"* → **Role (IAM Role)**
- *"O que é uma política IAM?"* → Documento **JSON** com permissões

---
---

# AULA 4: AWS Organizations

## 1. O Problema de uma Única Conta

Imagine uma empresa que cresce: devs, operações, usuários, ambientes múltiplos — tudo em **uma conta só**.

### Problemas

```
[Problema 1: Custos]
Todos os recursos na mesma conta → impossível separar
quanto cada time gasta

[Problema 2: Soft Limits]
Cada conta AWS tem limites de recursos:
├── Limite de VPCs por região
├── Limite de instâncias EC2
└── Alguns limites são hard (não podem ser aumentados)
```

---

## 2. Solução Inicial: Múltiplas Contas

```
[Conta Produção]          [Conta Não-Produção]
├── Ambiente real         ├── Ambiente de dev
├── Time operações        └── Time desenvolvimento
└── Usuários finais
```

**Melhora:** Separa limites e custos.

**Problema novo:** Agora tem dois logins, dois consoles, dois faturamentos — difícil de gerenciar.

---

## 3. AWS Organizations

**AWS Organizations** — Serviço **gratuito** para gerenciar **múltiplas contas AWS** de forma centralizada.

```
[Conta Gerenciadora (Management Account)]
        ↓
[Organização]
├── [OU: Produção]
│   ├── Conta Prod Web
│   └── Conta Prod API
│
├── [OU: Desenvolvimento]
│   ├── Conta Dev Web
│   └── Conta Dev API
│
└── [OU: Operações]
    └── Conta Monitoring
```

> OU = Organizational Unit (Unidade Organizacional)

---

## 4. Recursos do AWS Organizations

### Gerenciamento Centralizado

- Uma conta gerencia todas as outras
- Visibilidade consolidada de todas as contas
- Criação de novas contas automatizada

### Faturamento Consolidado

```
[Conta A] + [Conta B] + [Conta C]
           ↓
[Fatura Única Consolidada]
├── Total por conta
├── Total por serviço
└── Relatórios de custo por equipe
```

**Benefício extra:** Volume de uso combinado pode gerar **descontos** da AWS.

### Agrupamento Hierárquico

```
[Organização]
├── [Grupo: Desenvolvedores]
│   ├── Conta Dev 1
│   └── Conta Dev 2
└── [Grupo: Operações]
    └── Conta Prod
```

### SCP — Service Control Policies

**Políticas de Controle de Serviço** aplicadas em nível organizacional.

```
[SCP aplicada ao grupo Operações]
├── Proibido: Acessar S3
├── Proibido: Criar instâncias EC2 fora de us-east-1
└── Permitido: Apenas serviços necessários

Qualquer usuário novo que entrar nesse grupo
→ Já herda essas restrições automaticamente
```

---

## 5. Comparativo: Sem x Com Organizations

| Aspecto | Sem Organizations | Com Organizations |
|---|---|---|
| **Contas** | Gerenciadas individualmente | Gerenciadas centralmente |
| **Faturamento** | Múltiplas faturas | Fatura consolidada |
| **Limites** | Uma conta pode esgotar | Distribuído entre contas |
| **Políticas** | Por conta | Centralizadas via SCP |
| **Custo** | Pago | **Gratuito** |

---

> 💡 **Dica para a prova CLF-C02:**

- *"Como gerenciar múltiplas contas AWS?"* → **AWS Organizations**
- *"Como ter fatura única para várias contas?"* → **Faturamento Consolidado (Organizations)**
- *"O que é SCP?"* → Políticas de controle de acesso a serviços por unidade organizacional
- *"É gratuito?"* → **SIM**

---
---

# AULA 5: Conformidade e Suporte — AWS Artifact

## 1. Conformidade: O Que é?

**Conformidade** = Aderir às regulações e normas legais do seu setor/país.

```
[Regulações por contexto]
├── Brasil: LGPD (dados pessoais)
├── Europa: GDPR (dados pessoais)
├── EUA Saúde: HIPAA
├── EUA Financeiro: SOC 1/2/3
├── Japão Financeiro: FISC
└── Global: ISO 27001 (segurança da informação)
```

**Na prática:** Auditorias podem exigir comprovação de que sua infraestrutura é aderente a essas normas.

---

## 2. Responsabilidade da Conformidade: Também Compartilhada

```
[AWS cumpre:]
├── Conformidade da infraestrutura física
├── Segurança dos data centers
├── Redundância da rede
└── Certificações ISO, SOC, PCI-DSS da infra

[Cliente cumpre:]
├── Criptografar dados pessoais (LGPD/GDPR)
├── Controle de acesso correto (IAM)
├── Retenção de dados
└── Processos da sua aplicação
```

---

## 3. AWS Artifact

**AWS Artifact** — Serviço para **acessar documentos de conformidade** e assinar contratos com a AWS.

### Dois Componentes Principais

#### Artifact Agreements (Contratos)

- Assinar contratos com a AWS sobre uso de serviços
- Exemplo: Contrato de conformidade com LGPD ou HIPAA
- Tudo feito via console, de forma digital

```
[Console AWS Artifact]
    ↓
Agreements disponíveis:
├── BAA (HIPAA Business Associate Agreement)
├── GDPR DPA
├── LGPD
└── Outros contratos específicos
    ↓
Você lê e assina digitalmente
```

#### Artifact Reports (Relatórios de Auditoria)

- Baixar documentos que **comprovam** que a AWS está em conformidade
- Gerados por **auditores externos independentes** (não pela AWS)
- Usados para responder a auditorias de sua empresa

```
[Cenário real:]
Auditoria chega na sua empresa e pergunta:
"Vocês usam AWS? Precisamos de um relatório de
conformidade com LGPD da infraestrutura da AWS."

Você vai ao AWS Artifact Reports
    ↓
Solicita o documento de conformidade LGPD
    ↓
Baixa o relatório gerado por auditores externos
    ↓
Apresenta para os auditores ✅
```

---

## 4. Como Fica a Divisão

```
[Auditoria pede:] "Sua infraestrutura atende ao LGPD?"

[Parte AWS] → AWS Artifact Reports comprova
[Parte Cliente] → Você comprova com sua config de IAM, criptografia, etc.
```

---

> 💡 **Dica para a prova CLF-C02:**

- *"Onde baixar relatórios de conformidade da AWS?"* → **AWS Artifact Reports**
- *"Como assinar contratos de conformidade com a AWS?"* → **AWS Artifact Agreements**
- *"A conformidade é responsabilidade de quem?"* → **Compartilhada** (AWS + Cliente)

---
---

# AULA 6: Serviços Adicionais de Segurança

## 1. AWS WAF — Web Application Firewall

### O que é

**WAF** é um **firewall para aplicações web** que filtra tráfego HTTP/HTTPS malicioso antes que chegue à sua aplicação.

### Características

- Protege contra ataques web comuns (SQL Injection, XSS, etc.)
- Regras pré-configuradas e customizáveis
- Integra nativamente com ALB, EC2, CloudFront

### Exemplo: SQL Injection

```
[Atacante]
    ↓ Requisição: GET /api?id=1; DROP TABLE users; --
[WAF]
    ↓ Regra: "SQL Injection detectado"
    ✖ Bloqueia a requisição
[Load Balancer]
    ↓ Nunca recebe a requisição maliciosa
[EC2 + Banco de dados]
    ↓ Protegidos
```

### Sem WAF:

```
[Atacante]
    ↓ SQL Injection
[Load Balancer]
    ↓ Distribui para EC2
[EC2]
    ↓ Executa query maliciosa
[Banco de Dados] ← Dados apagados/comprometidos ❌
```

---

## 2. AWS Shield — Proteção contra DDoS

### O que é DDoS?

**DDoS (Distributed Denial of Service)** = Atacante controla milhares de máquinas para sobrecarregar seu serviço simultaneamente.

```
[Atacante controla 10.000 máquinas]
         ↓ todas chamam ao mesmo tempo
[Sua API]
    └── Sobrecarregada → usuários legítimos não conseguem acessar
```

### AWS Shield Standard (Gratuito)

- **Sem custo adicional** — já incluso em todos os serviços AWS
- Proteção contra ataques DDoS **mais comuns**
- Análise em tempo real de tráfego malicioso
- Ativo por padrão

### AWS Shield Advanced (Pago)

- **Pago** com custo mensal
- Diagnósticos detalhados de ataques
- Proteção contra ataques **mais elaborados e complexos**
- Integração com WAF
- **Suporte 24/7** de equipe especializada em DDoS

| Aspecto | Standard | Advanced |
|---|---|---|
| **Custo** | Gratuito | Pago |
| **Ataques comuns** | ✅ | ✅ |
| **Ataques complexos** | ❌ | ✅ |
| **Suporte 24/7** | ❌ | ✅ |
| **Diagnóstico detalhado** | ❌ | ✅ |
| **Integração WAF** | ❌ | ✅ |

---

## 3. Amazon Inspector

### O que é

**Amazon Inspector** — Serviço de segurança que **escaneia automaticamente** vulnerabilidades em suas instâncias EC2 e containers.

### Como funciona

```
[Amazon Inspector ativado]
    ↓ Scanneia suas instâncias EC2
    ↓ Compara com banco de CVEs (Common Vulnerabilities and Exposures)
    ↓ Compara com benchmarks de segurança

[Relatório de vulnerabilidades]
├── EC2-Instância-1: Sistema operacional desatualizado
│   └── CVE-2024-XXXX: Vulnerabilidade crítica no kernel Linux
├── EC2-Instância-2: OK
└── Recomendação: Atualizar pacote X para versão Y
```

### Por que é importante?

Diariamente, **novas vulnerabilidades** são descobertas em sistemas operacionais e softwares. O Inspector automatiza essa verificação.

```
[Sem Inspector]
Você mesmo precisa acompanhar boletins de CVE
Verificar manualmente cada instância
Risco de falhar em alguma

[Com Inspector]
Verificação automática e contínua
Relatório centralizado
Notificação imediata de problemas
```

---

## 4. Amazon GuardDuty

### O que é

**GuardDuty** — Serviço de **detecção inteligente de ameaças** que monitora continuamente a atividade da sua conta AWS.

### Como funciona

```
[GuardDuty habilitado]
    ↓ Monitora continuamente:
    ├── Logs DNS
    ├── Logs de fluxo VPC
    ├── Eventos no S3
    ├── Dados em volumes EBS
    ├── Atividade de login no RDS
    └── Eventos CloudTrail
    ↓
[Análise com Machine Learning]
    ↓ Detecta padrões anômalos
    ↓ Identifica atividades suspeitas
[Alerta para o usuário]
```

### Exemplo de Detecção

```
[Situação:]
Instância EC2 que normalmente só processa dados
começa a enviar requisições para IPs na lista negra
e recebe respostas incomuns.

[GuardDuty identifica:]
"Comunicação com IP malicioso conhecido"
"Possível comprometimento da instância i-0abc1234"
"Recomendação: isolar instância e investigar"
```

### Inspector vs GuardDuty

| Aspecto | Amazon Inspector | Amazon GuardDuty |
|---|---|---|
| **Foco** | Vulnerabilidades conhecidas | Atividades maliciosas em tempo real |
| **O que analisa** | Sistema operacional e software | Tráfego de rede e eventos da conta |
| **Quando age** | Scan programado ou contínuo | Monitoramento contínuo |
| **Fonte de dados** | CVEs, benchmarks | Logs DNS, VPC, CloudTrail |
| **Exemplo** | "Seu SO tem CVE-2024-X" | "Alguém está tentando invadir de IP Y" |

---

## 5. Resumo: Todos os Serviços de Segurança

```
[Proteção de Aplicação Web]
WAF → Filtra HTTP/HTTPS malicioso (SQL Injection, XSS)

[Proteção contra Ataques de Volume]
Shield Standard → DDoS básico (gratuito)
Shield Advanced → DDoS avançado (pago, com suporte 24/7)

[Proteção de Dados]
KMS → Criptografia (dados em repouso e em trânsito)

[Verificação de Vulnerabilidades]
Inspector → Escaneia EC2 buscando CVEs e problemas no SO

[Detecção de Ameaças]
GuardDuty → Monitora rede e conta buscando atividades suspeitas
```

---

> 💡 **Dica para a prova CLF-C02:**

- *"Qual protege contra SQL Injection?"* → **WAF**
- *"Qual protege contra DDoS?"* → **Shield**
- *"Qual é gratuito contra DDoS?"* → **Shield Standard**
- *"Qual escaneia vulnerabilidades em EC2?"* → **Amazon Inspector**
- *"Qual detecta atividades maliciosas na conta?"* → **GuardDuty**
- *"Qual usa Machine Learning para detectar ameaças?"* → **GuardDuty**

---
---

# Resumo Geral do Módulo

## Mapa Conceitual

```
SEGURANÇA NA NUVEM AWS
│
├── Fundamento
│   └── Modelo de Responsabilidade Compartilhada
│       ├── AWS: Segurança DA nuvem (infraestrutura)
│       └── Cliente: Segurança NA nuvem (dados, apps, acesso)
│
├── Controle de Acesso
│   └── IAM (Identity and Access Management)
│       ├── Usuários (pessoas e aplicações)
│       ├── Grupos (conjuntos de usuários)
│       ├── Políticas (JSON com permissões)
│       └── Roles (identidades temporárias)
│
├── Proteção de Dados
│   └── KMS (Key Management Service)
│       ├── Dados em Repouso (EBS, S3, RDS)
│       └── Dados em Trânsito (SSL/TLS, HTTPS)
│
├── Organização de Contas
│   └── AWS Organizations
│       ├── Múltiplas contas centralizadas
│       ├── Faturamento consolidado
│       └── SCP (Service Control Policies)
│
├── Conformidade
│   └── AWS Artifact
│       ├── Agreements (assinar contratos)
│       └── Reports (baixar relatórios de auditoria)
│
└── Serviços de Proteção Avançada
    ├── WAF → Firewall para apps web
    ├── Shield → Proteção DDoS
    ├── Inspector → Scan de vulnerabilidades
    └── GuardDuty → Detecção de ameaças
```

---

## Tabela Completa de Serviços

| Serviço | Categoria | O que faz | Custo |
|---|---|---|---|
| **IAM** | Controle de Acesso | Gerencia usuários, grupos, políticas, roles | Gratuito |
| **KMS** | Criptografia | Gerencia chaves criptográficas | Pago |
| **Organizations** | Multi-conta | Gerencia múltiplas contas AWS | Gratuito |
| **AWS Artifact** | Conformidade | Contratos e relatórios de auditoria | Gratuito |
| **WAF** | Proteção Web | Firewall contra ataques web | Pago |
| **Shield Standard** | Anti-DDoS | Proteção DDoS básica | **Gratuito** |
| **Shield Advanced** | Anti-DDoS | Proteção DDoS avançada + suporte | Pago |
| **Inspector** | Vulnerabilidades | Escaneia CVEs em EC2 | Pago |
| **GuardDuty** | Detecção de Ameaças | Monitora atividade maliciosa | Pago |

---

## Questões Típicas da Prova (CLF-C02)

1. *"Quem é responsável pela segurança física dos data centers?"* → **AWS**
2. *"Quem deve atualizar o SO de uma EC2?"* → **Cliente**
3. *"O que é segurança DA nuvem vs NA nuvem?"* → DA = AWS, NA = Cliente
4. *"Qual serviço gerencia usuários e permissões?"* → **IAM**
5. *"Por padrão, um novo usuário IAM tem acesso a quê?"* → **Nada**
6. *"O que é o princípio do menor privilégio?"* → Dar apenas permissões necessárias
7. *"Como uma Lambda acessa um S3 de forma segura?"* → **IAM Role**
8. *"Qual serviço gerencia chaves de criptografia?"* → **KMS**
9. *"Como centralizar múltiplas contas AWS?"* → **AWS Organizations**
10. *"Como obter relatório de conformidade da AWS?"* → **AWS Artifact Reports**
11. *"Qual protege contra SQL Injection?"* → **WAF**
12. *"Qual protege contra DDoS sem custo extra?"* → **Shield Standard**
13. *"Qual escaneia vulnerabilidades em EC2?"* → **Amazon Inspector**
14. *"Qual detecta atividades maliciosas usando ML?"* → **GuardDuty**

---

*Módulo Completo: Segurança na Nuvem com AWS | Aulas 1-6 | Curso Preparatório AWS Cloud Practitioner (CLF-C02)*
