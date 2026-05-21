# Armazenamento e Banco de Dados na AWS — Módulo Completo

> 📋 **Curso:** Armazenamento e Banco de Dados — Preparatório AWS Cloud Practitioner (CLF-C02)
> 📌 **Módulo:** Conceitual | 8 aulas | Sem pré-requisitos

---

## Visão Geral do Módulo

Este módulo cobre os **principais serviços de armazenamento e banco de dados** da AWS que caem no exame CLF-C02. O objetivo é conhecer os serviços, suas características principais e quando usar cada um.

**Percurso das 8 aulas:**
1. Tipos de Armazenamento (objetos, arquivos, blocos)
2. Amazon EBS (Elastic Block Store)
3. Amazon S3 (Simple Storage Service)
4. Amazon EFS (Elastic File System)
5. Amazon RDS (Relational Database Service)
6. Amazon DynamoDB (NoSQL)
7. Outros Serviços de Banco de Dados
8. Amazon Redshift (Big Data & Data Warehouse)

---

---

# AULA 17: Tipos de Armazenamento na AWS

## 1. O Problema: Onde Ficam os Dados?

Você já sabe como estruturar a infraestrutura (VPCs, subnets, segurança), como rodar instâncias EC2, como escalar com Auto Scaling. Mas **onde os dados são armazenados?**

- Vídeos e mídias — onde?
- Arquivos de configuração — onde?
- Bancos de dados — onde?
- Dados de usuários — onde?

> 📌 O armazenamento é **tão importante quanto a computação**. Uma boa estratégia de armazenamento é fundamental para qualquer solução AWS.

---

## 2. Os Três Tipos de Armazenamento

A AWS oferece três tipos principais de armazenamento, cada um com características diferentes:

```
┌──────────────────────────┐
│   Tipos de Armazenamento  │
├──────────────────────────┤
│ 1. Armazenamento de      │
│    Objetos (Object)      │
├──────────────────────────┤
│ 2. Armazenamento de      │
│    Arquivos (File)       │
├──────────────────────────┤
│ 3. Armazenamento de      │
│    Blocos (Block)        │
└──────────────────────────┘
```

### Ponto Importante: Mesmo dado, diferentes formatos

> ⚠️ **A mesma informação pode ser armazenada de 3 formas diferentes!**

```
[Vídeo de 100MB]
    ↓
[Pode ser armazenado como]
    ├── Objeto (S3)
    ├── Arquivo (EFS)
    └── Bloco (EBS)
```

Cada tipo serve a **finalidades e casos de uso diferentes**.

---

## 3. Armazenamento de Objetos (Object Storage)

### O que é

Dados armazenados como **objetos auto-contidos**. Um objeto = arquivo + metadados + permissões.

**Característica chave:** Dados **não estruturados**.

### Estrutura

```
Objeto = {
  Arquivo: (conteúdo)
  Metadados: (tipo, tamanho, encoding, tags, autor...)
  URL: (endereço acessível)
  Permissões: (quem pode acessar)
}
```

### Casos de Uso

- Mídias (vídeos, áudios, imagens)
- Backup e recuperação de arquivos
- Armazenamento de logs
- Data lakes
- Hospedagem de conteúdo

### Serviço AWS

**Amazon S3 (Simple Storage Service)** — visto em detalhes na Aula 19.

---

## 4. Armazenamento de Arquivos (File Storage)

### O que é

Sistema de arquivos **compartilhado** em rede. Similar a pastas compartilhadas em um escritório.

**Característica chave:** Hierarquia de diretórios e permissões de compartilhamento.

### Analogia

```
[Escritório físico]
Servidor de arquivos → compartilha pastas
├── /documentos
├── /planilhas
└── /fotos

[Escritório na cloud]
EFS (Elastic File System) → compartilha arquivos
├── /documentos
├── /planilhas
└── /fotos
```

### Casos de Uso

- Diretórios compartilhados em equipe
- Ferramentas de desenvolvimento (código, assets)
- Armazenamento de diretórios pessoais
- Backup centralizado

### Serviço AWS

**Amazon EFS (Elastic File System)** — visto em detalhes na Aula 20.

---

## 5. Armazenamento de Blocos (Block Storage)

### O que é

Armazenamento tradicional de **disco (HD/SSD)**, dividido em blocos.

**Característica chave:** Estrutura de blocos de dados — como um disco rígido funciona fisicamente.

### Como funciona

```
[Arquivo de texto]
    ↓
[Convertido em blocos]
├── Bloco 1: primeiras linhas
├── Bloco 2: próximas linhas
├── Bloco 3: últimas linhas
└── ...
```

### Casos de Uso

- Sistemas operacionais (SO em EC2)
- Bancos de dados (RDS, DynamoDB)
- Aplicações de alta performance
- Containers

### Serviços AWS

- **Amazon EBS (Elastic Block Store)** — para EC2
- **Amazon RDS** — para bancos relacionais
- **DynamoDB** — para NoSQL

---

## 6. Resumo Comparativo

| Aspecto | Objetos | Arquivos | Blocos |
|---|---|---|---|
| **Formato** | Dados auto-contidos | Sistema hierárquico | Blocos de dados |
| **Estrutura** | Não estruturada | Estruturada em diretórios | Estrutura de disco |
| **Acesso** | Via URL/API | Via NFS/SMB | Via mount point |
| **Caso comum** | Mídias, backups | Compartilhamento | Discos, BD |
| **Serviço AWS** | S3 | EFS | EBS, RDS |

---

## 7. Decisão: Qual Tipo Escolher?

```
Tenho arquivo/mídia para armazenar?
├─ SIM → Armazenamento de Objetos (S3)
└─ NÃO → próxima pergunta

Preciso compartilhar arquivos em rede?
├─ SIM → Armazenamento de Arquivos (EFS)
└─ NÃO → próxima pergunta

Preciso de disco para EC2 ou BD?
└─ SIM → Armazenamento de Blocos (EBS/RDS)
```

---

> 💡 **Dica para a prova CLF-C02:** Questões sobre tipos de armazenamento:

- *"Qual tipo de armazenamento para vídeos em uma aplicação web?"* → **Objetos (S3)**
- *"Como compartilhar arquivos entre instâncias EC2?"* → **Arquivos (EFS)**
- *"Qual tipo para adicionar disco a uma instância EC2?"* → **Blocos (EBS)**
- *"Qual tipo é não estruturado?"* → **Objetos**
- *"Qual tipo usa diretórios hierárquicos?"* → **Arquivos**

---

---

# AULA 18: Amazon EBS — Elastic Block Store

## 1. Virtualização em EC2

### O Problema

Quando você cria uma instância EC2, ela não ocupa um espaço **físico dedicado**. Ela é **virtualizada** — múltiplas instâncias rodam no mesmo hardware.

```
[Servidor Físico 1]
├── Instância A (rodando)
└── Instância B (rodando)

[Servidor Físico 2]
└── Instância C (rodando)
```

### O Risco

Se uma instância para ou é encerrada, os **dados podem ser perdidos** porque estão no disco local daquele servidor.

```
Instância A rodava no Servidor 1
    ↓ para de rodar
Instância A é movida para Servidor 2
    ↓ dados do Servidor 1 perdidos!
```

---

## 2. Instance Store Volumes (Armazenamento Temporário)

### O que é

**Volumes de instância** — armazenamento **efêmero** anexado ao servidor físico.

### Características

- Muito rápido (local, sem latência de rede)
- Dados **perdidos se**:
  - Instância parar
  - Instância for hibernada
  - Servidor físico falhar
  - Instância for movida para outro servidor

### Quando usar

- Buffers e caches temporários
- Dados que podem ser recriados
- Processamento de curta duração

> ⚠️ **NUNCA use para dados importantes!**

---

## 3. Amazon EBS — Armazenamento Persistente

### O que é

**Elastic Block Store** — volume de armazenamento **persistente** e dedicado que se conecta a uma instância EC2.

### Diferença Crítica

```
Instance Store Volume (temporário):
Instância EC2 → 停止 → Dados perdidos

EBS Volume (persistente):
Instância EC2 ⟷ [EBS] → Dados persistem
                    ↓
                Mesmo após parar/reiniciar
```

### Características do EBS

- **Persistente** — dados sobrevivem a reboots, hibernação, falhas
- **Dedicado** — anexado a uma instância específica
- **Escalável** — tamanho configurável
- **Configurável** — tipo de disco (SSD, HDD), performance
- **Multi-AZ** — dados replicados automaticamente

---

## 4. Tipos de Volumes EBS

### Comparativo: SSD vs HDD

| Tipo | Velocidade | Custo | Melhor Para |
|---|---|---|---|
| **SSD** | Rápido | Caro | Aplicações, BD |
| **HDD** | Lento | Barato | Backup, logs |

### Tipos Específicos

#### SSD (Solid State Drive)

**gp3 (General Purpose 3):**
- Uso geral, equilibrado
- Para a maioria das aplicações

**io2 (Provisioned IOPS):**
- Alto desempenho garantido
- Para bancos de dados críticos
- Você escolhe o IOPS

#### HDD (Hard Disk Drive)

**st1 (Throughput Optimized):**
- Otimizado para leitura/escrita sequencial
- Para data warehouses, logs

**sc1 (Cold Storage):**
- Armazenamento frio de dados acessados raramente
- Backup antigos

---

## 5. Snapshots (Backups Incrementais)

### O que é

**Snapshot** = foto do estado do volume EBS em um momento específico.

### Característica: Incremental

```
Dia 1: Snapshot 1 (copia TUDO — 10 GB)
        ├── Arquivo 1: 5 GB
        ├── Arquivo 2: 3 GB
        └── Arquivo 3: 2 GB

Dia 2: Arquivo 2 foi modificado (3 GB → 7 GB, mudou 4 GB)
        Snapshot 2 (copia SÓ O QUE MUDOU — 4 GB)

Dia 3: Arquivo 3 foi adicionado (2 GB novo)
        Snapshot 3 (copia SÓ O NOVO — 2 GB)
```

### Benefícios

- **Economia de espaço** — copia apenas mudanças
- **Histórico** — múltiplos snapshots de diferentes datas
- **Recuperação** — restaurar volume antigo a partir de snapshot
- **Cross-region** — copiar snapshot para outra região

---

## 6. Exemplo: Timeline de Snapshots

```
[Volume Original: 10 GB]
    ↓
[Snapshot 1] → 10 GB (conteúdo completo)
    ↓
[Modificação: 4 GB alterados]
    ↓
[Snapshot 2] → 4 GB (só as alterações + referência ao Snapshot 1)
    ↓
[Adição: 2 GB novos]
    ↓
[Snapshot 3] → 2 GB (só o novo + referência aos anteriores)

Total armazenado: 10 + 4 + 2 = 16 GB
(em vez de 10 + 10 + 10 = 30 GB se fossem completos)
```

### Restauração

```
[Snapshot 1 (10 GB)] → [Novo Volume A: 10 GB]
[Snapshot 2 (4 GB alterados)] → [Novo Volume B: 10 GB + 4 GB novos = 14 GB]
```

---

## 7. Resumo: EBS em Produção

| Aspecto | Instance Store | EBS |
|---|---|---|
| **Persistência** | ❌ Efêmero | ✅ Persistente |
| **Ciclo de vida** | Perdido ao parar | Sobrevive tudo |
| **Backup** | ❌ Nenhum | ✅ Snapshots |
| **Uso** | Temp cache | Dados permanentes |
| **Custo** | Incluído | Pago por GB |

---

> 💡 **Dica para a prova CLF-C02:**

- *"Qual tipo de armazenamento é perdido se a instância parar?"* → **Instance Store**
- *"Como fazer backup de um volume EBS?"* → **Snapshots**
- *"Qual tipo de disco é mais rápido?"* → **SSD**
- *"Qual é mais barato?"* → **HDD**

---

---

# AULA 19: Amazon S3 — Simple Storage Service

## 1. O que é S3?

**S3 = Simple Storage Service** — Serviço de armazenamento de **objetos** gerenciado.

### Conceitos Fundamentais

**Objeto** = Arquivo + Metadados + Chave (nome)

```
Objeto S3 = {
  Chave: "meu-video.mp4"
  Conteúdo: (dados do vídeo)
  Metadados: {
    Tamanho: 500 MB
    Tipo: video/mp4
    Criado: 2026-05-21
    Tags: {"categoria": "tutorial"}
  }
  URL: https://bucket.s3.amazonaws.com/meu-video.mp4
}
```

---

## 2. Buckets (Contêineres)

### O que é um Bucket

**Bucket** = Contêiner onde objetos são armazenados. Analogia: pastas em um disco rígido.

```
[Bucket: meu-bucket-aws]
├── meu-video.mp4
├── documento.pdf
├── /imagens/
│   ├── foto1.jpg
│   └── foto2.png
└── /backups/
    └── backup-2026-05.tar.gz
```

### Regras

- **Obrigatório:** Você deve criar um bucket antes de fazer upload
- **Nomes únicos globalmente:** Nomes de buckets são únicos em toda a AWS
- **Número:** Até 100 buckets por conta (pode solicitar aumento)
- **Tamanho de objeto:** 0 até 5 TB por arquivo
- **Quantidade:** Ilimitado de objetos por bucket

---

## 3. Classes de Armazenamento S3

A escolha da classe afeta **custo** e **recuperação**. Escolha com base em:
- Com que frequência você acessa os dados?
- Quanto tempo pode esperar para recuperar?

### S3 Standard

- **Acesso:** Frequente
- **Disponibilidade:** Multi-AZ (3+ zonas)
- **Custo:** Mais caro
- **Casos:** Websites, aplicações ativas, análise de dados
- **Recuperação:** Imediata

---

### S3 Standard-IA (Infrequent Access)

- **Acesso:** Pouco frequente
- **Disponibilidade:** Multi-AZ
- **Custo:** Barato que Standard (menos acessos = menos custo)
- **Casos:** Backup, dados acessados < 1x/mês
- **Recuperação:** Imediata

---

### S3 One Zone-IA

- **Acesso:** Pouco frequente
- **Disponibilidade:** UMA ÚNICA zona (mais risco!)
- **Custo:** Mais barato que Standard-IA
- **Casos:** Backup local, dados recriáveis
- **Recuperação:** Imediata
- **Risco:** Se a AZ falhar, dados perdidos

---

### S3 Intelligent-Tiering

- **Acesso:** Desconhecido ou variável
- **Como funciona:** Move objetos automaticamente entre classes baseado em padrão de acesso
  - Não acessado 30 dias → move para Infrequent Access
  - Não acessado 90 dias → move para Archive Instant
  - Não acessado 180+ dias → move para Deep Archive

- **Custo:** Taxa pequena de monitoramento, mas economiza no longo prazo
- **Melhor para:** Dados com padrão de acesso incerto

---

### S3 Glacier (Arquivamento)

#### Instant Retrieval
- **Acesso:** Raro mas recuperação rápida
- **Custo:** Barato
- **Recuperação:** Instantânea
- **Casos:** Backup de longa duração, compliance

#### Flexible Retrieval
- **Acesso:** Raro
- **Custo:** Muito barato
- **Recuperação:** 1-5 minutos
- **Casos:** Backups, disaster recovery não-urgente

#### Deep Archive
- **Acesso:** Arquivamento puro (compliance legal 7-10 anos)
- **Custo:** Mais barato possível
- **Recuperação:** 12 horas
- **Casos:** Retenção legal, conformidade

---

## 4. Versionamento de Objetos

### O que é

Histórico de versões do mesmo objeto.

```
documento.txt
├── Versão 1 (criado)
├── Versão 2 (editado)
├── Versão 3 (editado novamente)
└── Versão 4 (atual)
```

### Benefícios

- Recuperar versão anterior
- Auditoria de mudanças
- Proteção contra exclusões acidentais

---

## 5. Decisão: Qual Classe Escolher?

```
Dados acessados frequentemente?
├─ SIM → S3 Standard
└─ NÃO → próxima pergunta

Preciso de recuperação rápida?
├─ SIM → S3 Standard-IA ou Intelligent-Tiering
├─ NÃO → próxima pergunta

Posso esperar algumas horas/dias?
├─ SIM → S3 Glacier Flexible Retrieval
└─ NÃO → S3 Deep Archive (compliance/legal)
```

---

## 6. Casos de Uso

- **Data lakes:** S3 Standard (acesso frequente a análises)
- **Backup diário:** S3 Standard-IA (acesso raro)
- **Compliance legal:** S3 Deep Archive (retenção 7-10 anos)
- **Padrão desconhecido:** S3 Intelligent-Tiering (otimiza automaticamente)
- **Website estático:** S3 Standard (com CloudFront)

---

> 💡 **Dica para a prova CLF-C02:**

- *"Qual classe para dados acessados raramente mas que precisam estar prontos?"* → **Standard-IA**
- *"Qual para backup de conformidade legal por 10 anos?"* → **Deep Archive**
- *"Qual move automaticamente os dados baseado em acesso?"* → **Intelligent-Tiering**
- *"Qual é mais caro?"* → **S3 Standard**
- *"Qual tamanho máximo de arquivo?"* → **5 TB**

---

---

# AULA 20: Amazon EFS — Elastic File System

## 1. O que é EFS?

**Elastic File System** — Sistema de arquivos **compartilhado, gerenciado e elástico** na nuvem.

### Analogia

```
[Escritório]                    [Nuvem]
Servidor de arquivos        EFS
├── /docs (compartilhado)   ├── /docs
├── /fotos                  ├── /fotos
└── /projetos               └── /projetos

Qualquer máquina pode acessar via protocolo de rede
```

---

## 2. Características Principais

| Característica | Descrição |
|---|---|
| **Serverless** | Totalmente gerenciado — você não provisiona |
| **Elástico** | Cresce/diminui automaticamente com dados |
| **Multi-AZ** | Disponível em múltiplas zonas de disponibilidade |
| **Protocolo** | NFS (Network File System) |
| **Acesso** | EC2, Lambda, ECS podem acessar |
| **Compartilhado** | Múltiplas instâncias acessam simultaneamente |

---

## 3. Classes de Armazenamento EFS

### Standard

- **Disponibilidade:** Multi-AZ regional
- **Acesso:** Normal
- **Custo:** Mais alto

### Standard-IA (Infrequent Access)

- **Disponibilidade:** Multi-AZ regional
- **Acesso:** Raro
- **Custo:** Mais baixo

### One Zone

- **Disponibilidade:** UMA ÚNICA AZ
- **Acesso:** Normal
- **Custo:** Reduzido
- **Risco:** Se AZ falhar, dados perdidos

---

## 4. Arquitetura Exemplo: EFS Multi-AZ

```
[VPC]
│
├── [AZ-a]
│   ├── Subnet Pública
│   │   └── EC2 Web Server 1 → [EFS Mount Point]
│   │
│   └── Subnet Privada
│       └── EC2 App Server 1 → [EFS Mount Point]
│
├── [AZ-b]
│   ├── Subnet Pública
│   │   └── EC2 Web Server 2 → [EFS Mount Point]
│   │
│   └── Subnet Privada
│       └── EC2 App Server 2 → [EFS Mount Point]
│
└── [EFS] ← Único sistema de arquivos compartilhado
    ├── /app
    ├── /dados
    └── /configuração
```

Todos os servidores acessam os **mesmos arquivos** via NFS.

---

## 5. Casos de Uso

- **Compartilhamento de código:** Times acessam mesmo repositório
- **Diretório home compartilhado:** Arquivos pessoais acessíveis de qualquer máquina
- **Configurações centralizadas:** Todos os servidores usam mesma config
- **Backup centralizado:** Um local para todos os dados
- **Desenvolvimento colaborativo:** Múltiplos devs no mesmo projeto

---

## 6. Exemplo: Data Center + Cloud

```
[Data Center Corporativo]
├── Firewall
├── Rede local
└── Direct Connect
         ↓
    [EFS na AWS]
         ↓
    [VPC Privada]
    ├── EC2 App Servers
    └── Ponto de montagem EFS
```

Funcionários no data center podem acessar os mesmos arquivos que instâncias na cloud.

---

> 💡 **Dica para a prova CLF-C02:**

- *"Qual serviço para compartilhar arquivos entre múltiplas EC2?"* → **EFS**
- *"Qual protocolo usa EFS?"* → **NFS**
- *"Qual é serverless?"* → **EFS**
- *"Qual tipo de armazenamento para diretórios compartilhados?"* → **Arquivos (EFS)**

---

---

# AULA 21: Amazon RDS — Relational Database Service

## 1. Bancos de Dados Relacionais

### O que é

Banco de dados que armazena dados em **tabelas relacionadas**.

### Exemplo: E-commerce

```
[Tabela: Lojas]
ID | Nome
---|------
1  | Loja Centro
2  | Loja Norte

[Tabela: Produtos]
ID | Nome      | Preço
---|-----------|------
1  | Tênis     | 150
2  | Sandália  | 80

[Tabela: Estoque] (Relaciona Lojas + Produtos)
Loja_ID | Produto_ID | Quantidade
--------|------------|----------
1       | 1          | 30
1       | 2          | 20
2       | 1          | 10
2       | 2          | 0
```

As tabelas se relacionam através de **chaves estrangeiras**.

---

## 2. O Problema: Banco em EC2 vs RDS

### Banco em EC2 (Você gerencia)

```
[EC2 com SQL Server]
├── Você instala o BD
├── Você configura
├── Você faz backup (ou não!)
├── Você gerencia armazenamento
├── Você otimiza performance
└── Você trata falhas
```

**Desvantagens:**
- Muita responsabilidade
- Risco de perda de dados
- Complexo de escalar
- Pode falhar sem backup

### RDS (AWS gerencia)

```
[RDS Service]
├── AWS instala o BD
├── AWS configura
├── AWS faz backup automático
├── AWS escala armazenamento
├── AWS otimiza
└── AWS trata failover
```

**Vantagens:**
- Foco no BD, não em infraestrutura
- Backups automáticos
- Fácil replicação
- Multi-AZ automático
- Recuperação de desastres

---

## 3. RDS — Características

| Característica | Descrição |
|---|---|
| **Gerenciado** | AWS cuida da infraestrutura |
| **Multi-AZ** | Replicação automática para outra AZ |
| **Backup** | Automático com retenção configurável |
| **Failover** | Falha automática para réplica |
| **Performance** | Otimização automática |
| **Escalabilidade** | Aumentar/diminuir recursos sem downtime |
| **Read Replicas** | Criar cópias de leitura em outras regiões |

---

## 4. Engines Suportados pelo RDS

| Engine | Descrição |
|---|---|
| **MySQL** | Open-source, muito utilizado |
| **PostgreSQL** | Open-source, poderoso |
| **MariaDB** | Fork do MySQL |
| **Oracle** | Enterprise, pago |
| **SQL Server** | Microsoft |

---

## 5. Quando Escolher RDS?

```
Precisa de banco relacional?
├─ SIM → RDS (melhor que EC2)
└─ NÃO → próxima pergunta

Quer gerenciar infraestrutura do BD?
├─ NÃO → RDS
├─ SIM → EC2 + seu BD
└─ DEPENDE → Aurora (melhor do RDS)
```

---

## 6. Amazon Aurora (Evolução do RDS)

### O que é

**Aurora** = RDS melhorado, feito pela AWS especificamente para cloud.

### Vantagens

| Aurora | RDS |
|---|---|
| Compatível com MySQL/PostgreSQL | Vários engines |
| **1/10 do custo** | Mais caro |
| Multi-region automático | Precisa configurar |
| Até 15 read replicas | Menos replicas |
| Auto-scaling | Manual |
| Backup contínuo em S3 | Snapshots |

---

> 💡 **Dica para a prova CLF-C02:**

- *"Qual serviço para banco relacional gerenciado?"* → **RDS**
- *"Como fazer backup automático de BD?"* → **RDS (automático)**
- *"Qual tem menor custo entre RDS e Aurora?"* → **Aurora (1/10)**
- *"Como proteger um BD contra falha de AZ?"* → **RDS Multi-AZ**

---

---

# AULA 22: Amazon DynamoDB — NoSQL

## 1. O que é DynamoDB?

**DynamoDB** — Banco de dados **NoSQL** (não-relacional) gerenciado pela AWS.

### Comparação: Relacional vs NoSQL

| Aspecto | RDS (Relacional) | DynamoDB (NoSQL) |
|---|---|---|
| **Modelo** | Tabelas com relações | Documentos/Items |
| **Estrutura** | Rígida, schema fixo | Flexível, sem schema |
| **Escalabilidade** | Manual | Automática |
| **Performance** | Bom | Excelente (< 10ms) |
| **Custo** | Padrão | Paga por uso |

---

## 2. Estrutura DynamoDB

```
[Tabela: People]
│
├── Item 1: {
│   ├── id: 103 (Partition Key)
│   ├── name: "João"
│   ├── email: "joao@email.com"
│   └── age: 30
│
├── Item 2: {
│   ├── id: 104 (Partition Key)
│   ├── name: "Maria"
│   ├── email: "maria@email.com"
│   └── phone: "11987654321"  ← DIFERENTE! Flexibilidade
│
└── Item 3: {
    ├── id: 105
    ├── name: "Pedro"
    └── address: "Rua X, 123"
```

**Cada item pode ter atributos diferentes** — isso é flexibilidade NoSQL.

### Conceitos

| Conceito | Descrição |
|---|---|
| **Tabela** | Coleção de items |
| **Item** | Linha/documento individual |
| **Atributo** | Campo/coluna (nome-valor) |
| **Partition Key** | ID único do item |
| **Sort Key** | Ordenação secundária (opcional) |

---

## 3. Características DynamoDB

- **Serverless:** Sem provisionar servidores
- **Auto-scaling:** Escala automaticamente com demanda
- **Multi-AZ:** Replicação regional automática
- **Baixa latência:** < 10 milissegundos
- **Flexível:** Itens com diferentes atributos
- **Global:** Replicação global disponível

---

## 4. Casos de Uso

- **Aplicações de alta performance:** Jogos, apps em tempo real
- **IoT:** Dispositivos enviando dados constantemente
- **Mobile:** Apps com acesso rápido a dados
- **Catálogos:** Produtos com diferentes atributos
- **Sessões de usuário:** Login, carrinho de compras
- **Análise em tempo real:** Stream de dados

---

## 5. RDS vs DynamoDB

```
Dados estruturados com relações?
├─ SIM → RDS (relacional)
└─ NÃO → próxima pergunta

Alta performance necessária?
├─ SIM → DynamoDB (< 10ms)
├─ NÃO → RDS é ok
└─ MUITA ESCALA → DynamoDB
```

---

> 💡 **Dica para a prova CLF-C02:**

- *"Qual BD para NoSQL?"* → **DynamoDB**
- *"Qual tem latência < 10ms?"* → **DynamoDB**
- *"Qual é serverless?"* → **DynamoDB**
- *"Qual permite items com atributos diferentes?"* → **DynamoDB**

---

---

# AULA 23: Outros Serviços de Banco de Dados

## 1. Quando Escolher o Banco Certo

> **Regra de Ouro:** A escolha do banco passa por **necessidades de negócio**, não por tecnologia.

```
Perguntas para fazer:
1. Qual é a estrutura dos dados?
2. Como os dados são acessados?
3. Qual é a escala?
4. Preciso de conformidade?
```

---

## 2. Amazon DocumentDB (Document Database)

### O que é

Banco de dados de **documentos** NoSQL, compatível com **MongoDB**.

### Estrutura

```
{
  "user_id": "u123",
  "name": "João",
  "preferences": {
    "language": "pt-BR",
    "theme": "dark"
  },
  "tags": ["vip", "active"]
}
```

### Casos de Uso

- Gerenciamento de conteúdo
- Catálogos de produtos
- Perfis de usuário

---

## 3. Amazon Neptune (Graph Database)

### O que é

Banco de dados de **grafos** — armazena relacionamentos entre dados.

### Estrutura

```
[Usuário A] ─ amigo de ─ [Usuário B]
     │                       │
     └─ segue ─ [Página]─ curtida de ─ [Usuário C]
```

### Casos de Uso

- Redes sociais (conexões entre usuários)
- Detecção de fraude
- Mecanismos de recomendação
- Gráfico de conhecimento

---

## 4. Amazon QLDB (Quantum Ledger Database)

### O que é

Banco de dados **imutável** — dados **não podem ser modificados**, apenas novos registros adicionados.

### Características

- Auditoria completa
- Conformidade legal
- Histórico imutável

### Casos de Uso

- Registros financeiros
- Histórico de transações (blockchain-like)
- Conformidade regulatória

---

## 5. DAX (DynamoDB Accelerator) — Cache

### O que é

**Cache layer** na frente do DynamoDB para melhorar performance.

```
[Aplicação]
    ↓ consulta
[DAX Cache] ← se encontrado, retorna rápido
    ↓ se não encontrado
[DynamoDB] ← busca e armazena em cache
```

### Benefício

- **Microsegundos** vs milissegundos
- Ideal para leituras repetidas

---

## 6. ElastiCache — Cache para RDS

### O que é

**Cache layer** para bancos relacionais (MySQL, PostgreSQL).

### Compatibilidade

- Memcached
- Redis

### Uso

```
[Aplicação]
    ↓ "SELECT * FROM users WHERE id=1" (frequente)
[ElastiCache]
    ├─ Primeira vez → vai ao BD, armazena
    └─ Próximas vezes → retorna do cache
```

---

## 7. Decisão: Qual Banco Escolher?

```
Dados relacionais estruturados?
├─ SIM → RDS
└─ NÃO → próxima pergunta

Documentos JSON?
├─ SIM → DocumentDB
└─ NÃO → próxima pergunta

Grafos e relacionamentos complexos?
├─ SIM → Neptune
└─ NÃO → próxima pergunta

Dados imutáveis (compliance)?
├─ SIM → QLDB
└─ NÃO → próxima pergunta

NoSQL de alta performance?
└─ SIM → DynamoDB (com DAX se cache)
```

---

> 💡 **Dica para a prova CLF-C02:**

- *"Qual para documentos JSON?"* → **DocumentDB**
- *"Qual para redes sociais?"* → **Neptune**
- *"Qual para blockchain/imutável?"* → **QLDB**
- *"Como acelerar DynamoDB?"* → **DAX**
- *"Como acelerar RDS?"* → **ElastiCache**

---

---

# AULA 24: Amazon Redshift — Big Data & Data Warehouse

## 1. O Problema: Big Data

Na realidade, os dados vêm de **muitas fontes**:

```
[Infraestrutura]
├── EC2 → logs
├── S3 → arquivos, mídias
├── Lambda → eventos
├── RDS → transações
├── DynamoDB → dados NoSQL
├── EFS → documentos
└── Internet → dados externos (APIs, web)
```

**Problemas:**
- Muita **variedade** de dados
- Muita **velocidade** de geração
- Muito **volume**
- Precisa responder perguntas de negócio rapidamente

> **Big Data = Volume + Variedade + Velocidade**

---

## 2. Perguntas de Negócio Difíceis

```
"Quantas vendas fizemos desde o lançamento?"
"Quantos usuários se cadastraram na última hora?"
"Qual é a tendência de crescimento?"
"Como prever demanda?"
```

Essas perguntas exigem análise de **MUITO DADO** de **múltiplas fontes**.

---

## 3. O que é Redshift?

**Amazon Redshift** — **Data Warehouse** (armazém de dados) para análise de Big Data.

### Características

- **Coleta** de dados de múltiplas fontes
- **Armazenamento** centralizado
- **Análise** com SQL
- **Performance** otimizada para analytics
- **Escalável** até petabytes

---

## 4. Arquitetura Redshift

```
[Múltiplas Fontes]
├── S3 (arquivos)
├── RDS (transações)
├── DynamoDB (NoSQL)
├── EFS (documentos)
└── APIs externas
        ↓
[Redshift Cluster]
├── Nó 1: dados + computação
├── Nó 2: dados + computação
└── Nó 3: dados + computação
        ↓
[Redshift Spectrum]
└── Consultar S3 diretamente via SQL
        ↓
[Respostas & Analytics]
```

---

## 5. Redshift Spectrum

### O que é

Permite consultar S3 diretamente usando **SQL**, sem precisar copiar dados.

```
[S3 com 1000 arquivos]
    ↑
[Redshift Spectrum]
Executa: SELECT * FROM s3_data WHERE condition
    ↓
[Resultado da consulta]
```

---

## 6. Casos de Uso

- **Data lakes:** Analisar grande volume
- **Analytics em tempo real:** Responder perguntas de negócio
- **Business intelligence:** Dashboards e relatórios
- **Machine learning:** Treinar modelos com muitos dados
- **Detecção de fraude:** Padrões em grande escala

---

## 7. Redshift vs RDS

| Aspecto | RDS | Redshift |
|---|---|---|
| **Propósito** | Transações (OLTP) | Analytics (OLAP) |
| **Dados** | Estruturados | Multi-fonte |
| **Volume** | GB-TB | PB+ |
| **Velocidade** | Resposta rápida (ms) | Análise em batch |
| **Query** | Simples (select/insert) | Complexa (análises) |
| **Uso** | Aplicação web | Data warehouse |

---

> 💡 **Dica para a prova CLF-C02:**

- *"Qual serviço para analisar Big Data?"* → **Redshift**
- *"Qual para data warehouse?"* → **Redshift**
- *"Qual permite consultar S3 com SQL?"* → **Redshift Spectrum**
- *"Qual para volume de petabytes?"* → **Redshift**

---

---

## Resumo Geral: Decidindo entre Serviços

```
COMPUTAÇÃO vs ARMAZENAMENTO

┌─ Dados em Disco?
│  ├─ EC2: EBS (blocos) ou Instance Store
│  ├─ Arquivos compartilhados: EFS
│  └─ Objetos (mídias): S3
│
├─ Banco de Dados?
│  ├─ Relacional estruturado: RDS ou Aurora
│  ├─ NoSQL (documentos): DocumentDB ou DynamoDB
│  ├─ Grafos: Neptune
│  ├─ Imutável: QLDB
│  └─ Cache: DAX ou ElastiCache
│
└─ Big Data?
   ├─ Análise em larga escala: Redshift
   └─ Consultar S3: Redshift Spectrum
```

---

> 💡 **Questões Finais para a Prova:**

1. *"Qual serviço escolher para backup de 100GB?"* → **S3 Glacier Deep Archive**
2. *"Qual para diretórios compartilhados em rede?"* → **EFS**
3. *"Qual para disco de EC2?"* → **EBS**
4. *"Qual para dados com padrão de acesso desconhecido?"* → **S3 Intelligent-Tiering**
5. *"Qual para aplicação web com BD?"* → **RDS**
6. *"Qual para chat em tempo real?"* → **DynamoDB**
7. *"Qual para descobrir fraude?"* → **Neptune**
8. *"Qual para relatório de vendas históricas?"* → **Redshift**

---

*Módulo Completo: Armazenamento e Banco de Dados | Aulas 17-24 | Curso Preparatório AWS Cloud Practitioner*
