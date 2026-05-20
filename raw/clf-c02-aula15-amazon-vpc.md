# Amazon VPC: Virtual Private Cloud

> 📋 **Curso:** Redes em AWS — Preparatório AWS Cloud Practitioner (CLF-C02)
> 📌 **Aula:** Conceitual — Introdução à Amazon VPC | Sem pré-requisitos

---

## Visão Geral

O objetivo deste módulo é cobrir os **principais conceitos de redes relacionados à AWS** que caem no exame CLF-C02. Não cobriremos tudo sobre redes, apenas os assuntos essenciais para a prova.

**Percurso do módulo:**
1. Amazon VPC (esta aula)
2. Conectividade com AWS
3. Sub-redes
4. Network ACLs (Listas de Controle de Acesso)

---

## 1. O Problema: Como Organizar Redes na Cloud?

### Analogia com o mundo físico

Imagine um **escritório tradicional**:

```
[Laptops] [Smartphones]
    ↓          ↓
   [Roteador] ← coordena e roteia tráfego
    ↓
[Impressora] [Data Center Local] [Servidores]
```

Cada dispositivo está conectado através de um roteador. Existem **regras de rede** que determinam:
- Quem acessa o quê?
- Qual tráfego é permitido?
- Quais recursos são acessíveis de fora?

### Na cloud: os mesmos desafios

Quando você monta infraestrutura na AWS, enfrenta desafios similares:

- **Como conectar instâncias EC2** entre si?
- **Como fazer uma instância acessar a internet** enquanto isola outra?
- **Como proteger um banco de dados** de acesso não autorizado?
- **Como estruturar tudo de forma organizada** e segura?

> ⚠️ A solução é a **Amazon VPC** — sua rede virtual na cloud.

---

## 2. O que é Amazon VPC?

**VPC = Virtual Private Cloud** — Acrônimo para **Nuvem Privada Virtual**

A VPC permite que você:

- **Construa redes virtuais** que funcionam como redes físicas na nuvem
- **Configure conectividade** entre recursos AWS (EC2, RDS, Lambda, etc.)
- **Segmente a infraestrutura** em sub-redes públicas (acessíveis da internet) e privadas (isoladas)
- **Implemente regras de segurança** para controlar tráfego
- **Crie a estrutura de seu "escritório virtual"** na AWS

### Princípio Central: "Tudo Começa com uma VPC"

Um dos primeiros passos ao montar qualquer infraestrutura na AWS é:

```
1. Criar a VPC
2. Organizar sub-redes
3. Provisionar recursos (EC2, RDS, etc.) dentro das sub-redes
```

A VPC é o **alicerce** de toda a arquitetura de rede da sua aplicação.

---

## 3. Sub-redes: Pública vs Privada

### O Conceito

Dentro de uma VPC, você cria **sub-redes** — segmentos de rede isolados que dividem a infraestrutura em zonas lógicas.

### 3.1 Sub-rede Pública

```
[Internet / Usuários]
     ↓
[Sub-rede Pública]
     ↓
[EC2 — Servidor HTTP]
```

**Características:**
- **Acessível da internet** — recebe requisições externas
- **Pode enviar para a internet** — comunica-se com o mundo externo
- **Ideal para:** servidores web, APIs públicas, qualquer recurso que fale com usuários externos

**Exemplo:** Um servidor HTTP que recebe requisições de um aplicativo mobile ou navegador web.

### 3.2 Sub-rede Privada

```
[Sub-rede Privada]
     ↓
[EC2 — Database Server]
     ↓
[Não acessível da internet]
```

**Características:**
- **Isolada da internet** — ninguém de fora pode iniciar conexão
- **Acessa recursos internos** — comunica-se com outras sub-redes da VPC
- **Ideal para:** bancos de dados, aplicações internas, recursos sensíveis

**Exemplo:** Um servidor de banco de dados que é acessado **apenas por aplicações internas** — nunca exposto diretamente na internet.

### 3.3 Por que Essa Separação?

**Caso real:** Uma instância EC2 que acessa um banco de dados

```
❌ ERRADO:
[EC2 Database] → Sub-rede pública
         ↑
Acessível da internet — RISCO DE SEGURANÇA!
Qualquer um pode tentar conectar

✅ CORRETO:
[EC2 Database] → Sub-rede privada
         ↑
Isolada da internet — SEGURA!
Só aplicações internas acessam
```

> 📌 **Regra de ouro:** Bancos de dados e recursos sensíveis **nunca devem estar** em sub-redes públicas.

---

## 4. Arquitetura com Múltiplas AZs (Multi-AZ)

### O Padrão de Alta Disponibilidade

Para garantir **alta disponibilidade** e **tolerância a falhas**, distribua recursos em múltiplas **Zonas de Disponibilidade (AZs)**:

```
Região AWS
│
├── AZ-1
│   ├── Sub-rede Pública
│   │   └── [EC2 Web Server]
│   └── Sub-rede Privada
│       └── [RDS Database]
│
└── AZ-2
    ├── Sub-rede Pública
    │   └── [EC2 Web Server]
    └── Sub-rede Privada
        └── [RDS Database - Replica]
```

### Fluxo de Requisições

```
[Cliente]
   ↓ requisição HTTP
[Load Balancer] ← distribui para ambas as AZs
  ↙         ↘
[AZ-1]    [AZ-2]
  ↓         ↓
[EC2]     [EC2]
  │         │
  └────┬────┘
       ↓
   [Database]
   (privado)
```

### Benefícios

| Benefício | Descrição |
|---|---|
| **Alta disponibilidade** | Se uma AZ cair, a outra continua atendendo |
| **Tolerância a falhas** | Desastres localizados não derrubam tudo |
| **Distribuição de carga** | Requisições distribuídas entre múltiplas instâncias |
| **Resiliência** | Arquitectura robusta e confiável |

> 📌 Multi-AZ é **essencial** para aplicações críticas na produção.

---

## 5. Caso de Uso Completo: Aplicação Web Moderna

### Cenário

Uma aplicação web que:
- Recebe requisições de usuários externos
- Processa as requisições em servidores
- Armazena dados em banco de dados
- Precisa estar sempre disponível

### Arquitetura

```
[Internet]
   ↓
[Load Balancer (ALB)]
   ↙              ↘
[AZ-1]          [AZ-2]
   │              │
[Sub-rede]    [Sub-rede]
 Pública       Pública
   │              │
[EC2#1]        [EC2#2]
   ↘              ↙
    [Sub-redes Privadas]
           ↓
    [RDS Database]
    (Multi-AZ)
```

### Como Funciona

1. **Usuários** fazem requisições HTTP
2. **Load Balancer** distribui entre EC2#1 e EC2#2
3. Ambos os servidores acessam o **mesmo banco de dados** (privado)
4. Se **AZ-1 falhar** → AZ-2 continua atendendo
5. Se **um servidor cair** → o outro absorve o tráfego
6. Se **a internet cair** para uma AZ → a outra continua operando

> ✅ Resultado: **Aplicação altamente disponível e resiliente**.

---

## 6. Estrutura Completa do Módulo

```
Redes em AWS
│
├── Amazon VPC (esta aula)
│   ├── Conceito e propósito
│   ├── Sub-redes públicas e privadas
│   └── Multi-AZ para alta disponibilidade
│
├── Conectividade com AWS (próxima)
│   ├── Internet Gateway
│   ├── NAT Gateway
│   └── VPN / Direct Connect
│
├── Sub-redes (seguinte)
│   └── Planejamento e configuração
│
└── Network ACLs (final)
    └── Controle de acesso em nível de rede
```

---

## 7. Conceitos-Chave

| Conceito | Definição |
|---|---|
| **VPC** | Rede virtual isolada dentro da AWS |
| **Sub-rede** | Segmento de rede dentro da VPC |
| **Sub-rede pública** | Acessível da internet, com roteamento para IGW |
| **Sub-rede privada** | Isolada da internet, sem acesso direto |
| **AZ (Availability Zone)** | Zona de disponibilidade — data center isolado |
| **Multi-AZ** | Implantação em múltiplas zonas de disponibilidade |
| **Alta disponibilidade** | Serviço continua operando mesmo com falhas |
| **Tolerância a falhas** | Arquitetura resistente a desastres localizados |
| **Roteador (Router)** | Dispositivo que coordena tráfego de rede |

---

## 8. "Tudo Começa com uma VPC"

Quando você planeja qualquer infraestrutura na AWS:

```
Passo 1: Criar VPC
         └─ Definir intervalo de IPs
         
Passo 2: Criar sub-redes
         ├─ Sub-rede pública (AZ-1)
         ├─ Sub-rede privada (AZ-1)
         ├─ Sub-rede pública (AZ-2)
         └─ Sub-rede privada (AZ-2)
         
Passo 3: Provisionar recursos
         ├─ EC2 nas sub-redes públicas
         ├─ RDS nas sub-redes privadas
         └─ Load Balancer
         
Passo 4: Configurar conectividade
         ├─ Internet Gateway (IGW)
         ├─ NAT Gateway
         └─ Regras de roteamento
```

> 📌 A VPC é o primeiro recurso que você configura — antes de criar **qualquer outro** recurso na AWS.

---

> 💡 **Dica para a prova CLF-C02:** Questões típicas sobre VPC:

- *"O que é uma Amazon VPC?"* → **Rede virtual privada na cloud que permite organizar e conectar recursos AWS**
- *"Qual a diferença entre sub-rede pública e privada?"* → **Pública:** acessível da internet. **Privada:** isolada da internet
- *"Por que usar múltiplas AZs?"* → Para garantir **alta disponibilidade** e **tolerância a falhas**
- *"Onde deve estar um banco de dados?"* → Em uma **sub-rede privada** — nunca em uma pública
- *"Qual é o primeiro passo ao construir infraestrutura na AWS?"* → **Criar a VPC e planejar as sub-redes**
- *"O que garante resiliência em uma aplicação na AWS?"* → **Implantação multi-AZ com Load Balancer**

---

## Links Úteis

- [Amazon VPC — Documentação Oficial](https://docs.aws.amazon.com/pt_br/vpc/)
- [Amazon VPC — Página do Produto](https://aws.amazon.com/pt/vpc/)
- [Tutorial VPC: Sub-redes, IGW e NAT](https://docs.aws.amazon.com/pt_br/vpc/latest/userguide/VPC_Getting_Started.html)

---

*Aula 01 — Módulo: Redes em AWS | Curso Preparatório AWS Cloud Practitioner*
