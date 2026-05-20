# Regiões e Zonas de Disponibilidade (AZs)

> 📋 **Curso:** Infraestrutura Global AWS — Preparatório AWS Cloud Practitioner (CLF-C02)
> 📌 **Aula:** Conceitual — Regiões e Zonas de Disponibilidade

---

## 1. Regiões (Regions)

### Definição

Uma **Região** é um agrupamento de data centers da AWS em uma **localização geográfica específica** no mundo. Cada região é identificada por um nome e um código:

| Região | Código |
|---|---|
| São Paulo | `sa-east-1` |
| Virgínia do Norte (EUA) | `us-east-1` |
| Irlanda (Europa) | `eu-west-1` |
| Tóquio (Ásia) | `ap-northeast-1` |

### Características das Regiões

#### Isolamento de Dados
Dados armazenados em uma região **não saem dela automaticamente**. Para mover dados entre regiões, é necessário configurar explicitamente um serviço que faça isso (ex: replicação S3 cross-region).

> ✅ Isso garante que você tem controle total sobre onde seus dados estão fisicamente.

#### Conectividade entre Regiões
Todas as regiões são interconectadas por uma **rede de fibra óptica de alta velocidade** da própria AWS, que atravessa oceanos e continentes — garantindo comunicação rápida entre regiões quando necessário.

#### Conformidade Legal e Soberania de Dados
Cada região está sujeita às **leis e regulamentações locais** de proteção de dados. Isso é um fator crítico na escolha de onde hospedar sua solução.

| País / Região | Regulamentação |
|---|---|
| **Brasil** | LGPD (Lei Geral de Proteção de Dados) |
| **Europa** | GDPR (General Data Protection Regulation) |
| **China** | Legislação local de soberania de dados |
| **EUA** | Diversas leis federais e estaduais (HIPAA, CCPA, etc.) |

---

## 2. Como Escolher uma Região

A escolha da região deve considerar quatro fatores principais:

| Critério | Pergunta-chave |
|---|---|
| **Conformidade (Compliance)** | Há requisitos legais que exigem que os dados fiquem em um país específico? |
| **Latência** | Onde estão os usuários finais? Qual região está mais próxima? |
| **Disponibilidade de serviços** | O serviço AWS que preciso está disponível nessa região? |
| **Custo** | O preço dos serviços varia entre regiões — qual tem o melhor custo-benefício? |

> 📌 **Compliance sempre tem prioridade.** Se uma lei exige que os dados fiquem no Brasil, a região `sa-east-1` é obrigatória, independente de outros fatores.

---

## 3. Zonas de Disponibilidade (Availability Zones — AZs)

### Definição

Dentro de cada Região, existem múltiplas **Zonas de Disponibilidade (AZs)** — agrupamentos de um ou mais data centers fisicamente **separados**, com infraestrutura **independente** de:

- Energia elétrica
- Refrigeração
- Rede e conectividade
- Localização física

```
Região: sa-east-1 (São Paulo)
├── AZ: sa-east-1a  (data center A)
├── AZ: sa-east-1b  (data center B)
└── AZ: sa-east-1c  (data center C)
```

### O Equilíbrio das AZs

As AZs são posicionadas de forma estratégica:

```
Distância entre AZs:
├── Longe o suficiente → um desastre (tornado, enchente, falha elétrica)
│                        afeta apenas UMA AZ, não as outras
└── Perto o suficiente → latência de comunicação entre AZs permanece baixa
                         (dezenas de milissegundos)
```

> 📌 Esse equilíbrio é o que torna as AZs eficazes: **isolamento de falhas sem penalidade de performance**.

### Por que múltiplas AZs existem — Tolerância a Falhas

**Cenário sem AZs:**
```
Região com 1 data center
    ↓ tornado / falha elétrica / desastre
Serviço indisponível + risco de perda de dados
```

**Cenário com AZs:**
```
Região com 3 AZs — aplicação rodando nas AZs A e B
    ↓ AZ-a fica indisponível (desastre localizado)
AZ-b continua operando normalmente
→ Serviço continua disponível sem interrupção
```

---

## 4. Escopo de Serviços: Regional vs AZ

Os serviços AWS operam em dois escopos diferentes:

### Serviços de Escopo de AZ
São serviços que **rodam dentro de uma AZ específica**. Se a AZ falhar, o serviço nela hospedado fica indisponível.

- **EC2** (instâncias de máquinas virtuais)
- **EBS** (volumes de disco)

> ✅ **Boas práticas:** Para esses serviços, sempre provisionar instâncias em **pelo menos 2 AZs** para garantir disponibilidade.

```
EC2 na AZ-a  +  EC2 na AZ-b
     ↓ AZ-a falha
EC2 na AZ-b continua atendendo as requisições
```

### Serviços de Escopo Regional
São serviços que **operam no escopo da região inteira**, automaticamente distribuídos entre as AZs. Não requerem configuração manual de redundância entre AZs.

- **S3** (armazenamento de objetos)
- **DynamoDB** (banco NoSQL)
- **IAM** (gestão de identidades)

> 📌 A lista completa de serviços por escopo está disponível na documentação oficial da AWS.

---

## 5. Resumo Visual da Hierarquia

```
┌─────────────────────────────────────────────┐
│           INFRAESTRUTURA GLOBAL AWS          │
│                                             │
│  ┌──────────────────────────────────────┐   │
│  │         REGIÃO (ex: sa-east-1)       │   │
│  │                                      │   │
│  │  ┌──────────┐  ┌──────────┐          │   │
│  │  │  AZ - A  │  │  AZ - B  │   ...    │   │
│  │  │          │  │          │          │   │
│  │  │ EC2  EBS │  │ EC2  EBS │          │   │
│  │  └──────────┘  └──────────┘          │   │
│  │                                      │   │
│  │  S3, DynamoDB, IAM (escopo regional) │   │
│  └──────────────────────────────────────┘   │
│                                             │
│  Edge Locations (CloudFront, Route 53)      │
└─────────────────────────────────────────────┘
```

---

## 6. Conceitos-Chave para a Prova

| Conceito | Definição |
|---|---|
| **Região** | Agrupamento geográfico de data centers AWS |
| **AZ** | Data center(s) isolado(s) dentro de uma região |
| **Isolamento de dados** | Dados não saem da região sem configuração explícita |
| **Soberania de dados** | Dados seguem a legislação local da região |
| **Alta disponibilidade** | Serviço continua rodando mesmo com falha em uma AZ |
| **Tolerância a falhas** | Arquitetura que resiste a falhas sem interrupção |
| **Escopo de AZ** | Serviço vinculado a uma AZ específica (ex: EC2) |
| **Escopo regional** | Serviço distribuído automaticamente na região (ex: S3) |

---

> 💡 **Dica para a prova CLF-C02:** Questões típicas sobre esse tema:
> - *"O que garante que um desastre em um data center não derrube o serviço?"* → **Múltiplas AZs**
> - *"Por que os dados de uma região não aparecem em outra?"* → **Isolamento de dados por região**
> - *"Qual critério deve ser priorizado ao escolher uma região?"* → **Compliance/conformidade legal**
> - *"Qual serviço AWS precisa ser configurado em múltiplas AZs?"* → Serviços de **escopo de AZ** como EC2

---

## Links Úteis

- [Regiões e AZs — AWS](https://aws.amazon.com/pt/about-aws/global-infrastructure/regions_az/)
- [Lista de serviços por região](https://aws.amazon.com/pt/about-aws/global-infrastructure/regional-product-services/)
- [Infraestrutura Global AWS](https://infrastructure.aws/)

---

*Aula 03 — Módulo: Infraestrutura Global AWS | Curso Preparatório AWS Cloud Practitioner*
