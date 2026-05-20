# Computação na AWS: Amazon EC2 e Tipos de Instância

> 📋 **Curso:** Computação na AWS — Preparatório AWS Cloud Practitioner (CLF-C02)
> 📌 **Aula:** Conceitual — Sem pré-requisitos | Nível: Foundation

---

## Visão Geral do Módulo

Este módulo aborda os principais serviços de computação da AWS. As etapas previstas são:

| Etapa | Serviço | Descrição |
|---|---|---|
| **1** | Amazon EC2 | Computação em nuvem (máquinas virtuais) |
| **2** | EC2 Auto Scaling | Escalabilidade automática de instâncias |
| **3** | Elastic Load Balancing (ELB) | Distribuição de tráfego entre instâncias |
| **4** | Computação Serverless | Lambda e outros serviços sem servidor |
| **5** | Containers na AWS | ECS, EKS e outros |

---

## 1. Por que o EC2 Existe? O Problema do Data Center Próprio

Antes de entender o EC2, é importante entender o problema que ele resolve.

### O custo de montar infraestrutura própria

Hospedar uma aplicação em um data center próprio exige:

- **Segurança física e operacional** do ambiente
- **Analistas de rede** para cabeamento e estrutura lógica
- **Energia elétrica redundante** (geradores de backup)
- **Refrigeração** dos servidores
- **Data center de backup** em localização geográfica distinta
- **Racks de servidores** e todo o hardware associado

> ⚠️ Tudo isso é extremamente **caro**, **complexo** e exige equipes dedicadas apenas para manter a infraestrutura — antes mesmo de pensar no produto ou negócio em si.

### O dilema da capacidade

| Cenário | Problema |
|---|---|
| Compra hardware **além do necessário** | Paga por capacidade ociosa — prejuízo |
| Compra hardware **abaixo do necessário** | Sistema não suporta a demanda — queda |
| Negócio **cresce rápido** | Comprar mais racks leva semanas ou meses |
| Negócio **não cresce** | Investimento em data center desperdiçado |

### A solução ideal

O que as empresas precisam é de uma solução com:

| Necessidade | Conceito |
|---|---|
| Pagar apenas pelo que usa | **Economia de recursos** |
| Aumentar ou diminuir capacidade conforme a demanda | **Elasticidade** |
| Crescer a infraestrutura de forma rápida e coordenada | **Escalabilidade** |
| Garantir que o serviço esteja sempre disponível | **Disponibilidade** |

> ✅ É exatamente isso que o **Amazon EC2** oferece.

---

## 2. O que é o Amazon EC2?

**EC2 = Elastic Compute Cloud**

> 📌 O nome EC2 vem de: **E**lastic **C**ompute **C**loud — três "C"s, por isso o número **2** no nome.

O EC2 fornece **capacidade computacional segura e redimensionável** na nuvem. Em vez de comprar servidores físicos, você aluga **instâncias** (servidores virtuais) na infraestrutura da AWS.

### O que você pode configurar em uma instância EC2

- **CPU** (número de núcleos e arquitetura)
- **Memória RAM**
- **Armazenamento** (tipo e tamanho do disco)
- **Rede** (largura de banda, IP, grupos de segurança)
- **Sistema Operacional** (Linux, Windows, etc.)

> ✅ Tudo pode ser **alterado a qualquer momento** pelo console de gerenciamento — sem necessidade de comprar novo hardware.

### Modelo de precificação

Você paga **conforme o uso** — por hora ou por segundo, dependendo do tipo de instância e da modalidade escolhida. Quando a instância está parada, você não paga por computação.

---

## 3. AMI — Amazon Machine Image

Ao criar uma instância EC2, você escolhe uma **AMI (Amazon Machine Image)** — uma imagem pré-configurada disponível na infraestrutura da AWS que define:

- Sistema operacional (ex: Amazon Linux, Ubuntu, Windows Server)
- Configurações iniciais do sistema
- Softwares pré-instalados (em AMIs customizadas)

> 📌 A AMI é o "molde" a partir do qual a instância é criada.

---

## 4. Ciclo de Vida de uma Instância EC2

```
[AMI selecionada]
      ↓
  PENDENTE → aguardando inicialização
      ↓
  EXECUTANDO → instância rodando e disponível
      ↓
┌─────┴──────┐
REINICIANDO  PARANDO
(reboot)         ↓
             PARADA → instância desligada (não cobra por compute)
                 ↓
             HIBERNADA → estado salvo em disco, retoma do ponto parado
                 ↓
             ENCERRADA → instância destruída permanentemente
```

| Estado | Descrição |
|---|---|
| **Pendente** | Inicializando após ser lançada |
| **Executando** | Rodando e disponível |
| **Reiniciando** | Reboot — mantém IP e dados |
| **Parada** | Desligada — não cobra por compute, mas cobra pelo armazenamento |
| **Hibernada** | Salva o estado da memória em disco e para |
| **Encerrada** | Destruída permanentemente — não pode ser recuperada |

---

## 5. Tipos de Instância EC2

A AWS oferece diferentes **famílias de instâncias**, cada uma otimizada para um tipo específico de carga de trabalho. Conhecer os 5 tipos principais é essencial para a prova.

### 5.1 Uso Geral (General Purpose)

**Características:** Equilíbrio entre CPU, memória e rede — configuração mais versátil.

**Casos de uso:**
- Servidores de aplicação web
- Servidores de jogos
- Back-ends de aplicações
- Bancos de dados pequenos

> 💡 Escolha padrão quando não há um requisito específico de performance.

---

### 5.2 Otimizadas para Computação (Compute Optimized)

**Características:** Alto desempenho de CPU — ideal quando o processador é o gargalo.

**Casos de uso:**
- Processamento em lote de alto volume
- Servidores web de alto tráfego
- Servidores de jogos dedicados
- Modelagem científica e simulações

> 💡 Use quando precisa de mais poder de CPU do que as instâncias de uso geral oferecem.

---

### 5.3 Otimizadas para Memória (Memory Optimized)

**Características:** Grande quantidade de RAM — ideal para processar grandes volumes de dados em memória.

**Casos de uso:**
- Bancos de dados de alto desempenho (ex: Redis, SAP HANA)
- Processamento em tempo real de grandes datasets
- Cache de alto desempenho
- Aplicações que carregam grandes estruturas de dados na memória

> 💡 Use quando a memória RAM é o recurso crítico da sua carga de trabalho.

---

### 5.4 Computação Acelerada (Accelerated Computing)

**Características:** Usa **aceleradores de hardware** (GPUs, FPGAs) para executar funções específicas com muito mais eficiência do que CPUs convencionais.

**Casos de uso:**
- Processamento gráfico (rendering, jogos)
- Cálculos de ponto flutuante (simulações físicas, financeiras)
- Machine Learning e Deep Learning
- Matching de padrões em grandes volumes de dados

> 💡 Use quando sua carga de trabalho se beneficia de aceleração por GPU ou hardware especializado.

---

### 5.5 Otimizadas para Armazenamento (Storage Optimized)

**Características:** Acesso de leitura e gravação com alto throughput e baixa latência diretamente no disco local.

**Casos de uso:**
- Sistemas de arquivos distribuídos
- Data warehouses
- Sistemas de transações online (OLTP) de alto volume
- Bancos de dados que exigem I/O intensivo

> 💡 Use quando o disco e o I/O são os recursos críticos — não a CPU ou memória.

---

## 6. Resumo dos Tipos de Instância

| Tipo | Foco | Palavra-chave | Exemplo de uso |
|---|---|---|---|
| **Uso Geral** | Equilíbrio CPU/RAM/Rede | "padrão", "balanceado" | Web servers, apps gerais |
| **Computação** | Alto desempenho de CPU | "processamento", "lote" | Batch processing, jogos |
| **Memória** | Grande quantidade de RAM | "em memória", "tempo real" | Bancos de alto desempenho |
| **Acelerada** | GPU / hardware especializado | "gráficos", "ML", "GPU" | Deep Learning, rendering |
| **Armazenamento** | I/O de disco intensivo | "leitura/gravação", "OLTP" | Data warehouses, OLTP |

---

> 💡 **Dica para a prova CLF-C02:** Questões sobre tipos de instância geralmente descrevem uma carga de trabalho e perguntam qual tipo é mais adequado. Use a tabela acima como guia. As mais cobradas são:
> - *"Qual tipo para banco de dados em memória?"* → **Memória**
> - *"Qual tipo para Machine Learning com GPU?"* → **Computação Acelerada**
> - *"Qual tipo para aplicação web genérica?"* → **Uso Geral**
> - *"Qual tipo para data warehouse com muito I/O?"* → **Armazenamento**

---

## Links Úteis

- [Amazon EC2 — Visão Geral](https://aws.amazon.com/pt/ec2/)
- [Tipos de instâncias EC2](https://aws.amazon.com/pt/ec2/instance-types/)
- [Ciclo de vida das instâncias EC2](https://docs.aws.amazon.com/pt_br/AWSEC2/latest/UserGuide/ec2-instance-lifecycle.html)

---

*Aula 01 — Módulo: Computação na AWS | Curso Preparatório AWS Cloud Practitioner*
