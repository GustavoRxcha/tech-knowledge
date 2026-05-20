# Infraestrutura Global AWS

> 📋 **Curso:** Infraestrutura Global AWS — Preparatório AWS Cloud Practitioner (CLF-C02)
> 📌 **Aula:** Conceitual — Sem pré-requisitos

---

## Visão Geral

A **Infraestrutura Global AWS** é o conjunto de data centers, redes e recursos físicos distribuídos pelo mundo que torna possível o uso de todos os serviços da AWS — como EC2, S3, RDS, Lambda, entre outros.

É o "chão" sobre o qual toda a plataforma AWS está construída.

### Percurso do módulo

1. O que é a Infraestrutura Global AWS
2. **Regiões** e **Zonas de Disponibilidade**
3. **Pontos de Presença** (Edge Locations)
4. **Provisionamento** de recursos e interação com as APIs da AWS

---

## 1. Por que a Infraestrutura Global Existe?

Diferente do modelo on-premises — onde cada empresa constrói e mantém sua própria infraestrutura — a AWS construiu uma infraestrutura física global que permite a qualquer cliente consumir recursos de TI via internet, sem se preocupar com hardware.

### O que ela provê

- **Rede** de alta velocidade e baixa latência entre data centers
- **Conectividade** entre regiões e com o usuário final
- **Serviços** disponíveis globalmente (EC2, S3, DynamoDB, etc.)
- **Alta disponibilidade** e **tolerância a falhas** por design

---

## 2. Regiões (Regions)

### O que é uma Região

Uma **região** é uma área geográfica específica no mundo onde a AWS mantém um conjunto de data centers. Cada região é **independente** das demais — tem sua própria infraestrutura, energia, rede e conectividade.

### Características

- Cada região possui um **nome** (ex: `sa-east-1` para São Paulo) e um identificador geográfico
- Os serviços e dados de uma região **não são automaticamente replicados** para outras
- A escolha da região afeta **latência**, **custo**, **disponibilidade de serviços** e **conformidade legal (compliance)**

### Como escolher uma Região

| Critério | Consideração |
|---|---|
| **Latência** | Escolher a região mais próxima dos usuários finais |
| **Compliance** | Alguns países exigem que dados fiquem em território nacional |
| **Disponibilidade de serviços** | Nem todos os serviços AWS estão disponíveis em todas as regiões |
| **Custo** | O preço dos serviços pode variar entre regiões |

> 📌 **Números de referência (momento da gravação):** 27 regiões ao redor do mundo, com expansão contínua. Consulte [aws.amazon.com/pt/about-aws/global-infrastructure](https://aws.amazon.com/pt/about-aws/global-infrastructure/) para os números atualizados.

---

## 3. Zonas de Disponibilidade (Availability Zones — AZs)

### O que é uma AZ

Cada região é composta por **múltiplas Zonas de Disponibilidade (AZs)**. Uma AZ é um ou mais data centers fisicamente separados dentro da mesma região, com:

- Energia independente
- Refrigeração independente
- Rede independente
- Localização geográfica distinta (separadas por dezenas de quilômetros)

```
Região: sa-east-1 (São Paulo)
├── AZ: sa-east-1a
├── AZ: sa-east-1b
└── AZ: sa-east-1c
```

### Por que as AZs existem — Tolerância a Falhas

Se um data center sofrer uma falha (desastre natural, falha elétrica, etc.), as outras AZs da mesma região continuam operando normalmente. Isso garante:

- **Alta disponibilidade** — o serviço continua rodando mesmo com falha em uma AZ
- **Tolerância a falhas** — a aplicação sobrevive a desastres localizados
- **Recuperação de desastres** — dados replicados entre AZs ficam protegidos

> 📌 **Números de referência (momento da gravação):** 87 zonas de disponibilidade distribuídas entre as regiões. Expansão contínua.

### Boas práticas

> ✅ Sempre arquitetar aplicações para rodar em **pelo menos 2 AZs** — isso garante que uma falha em uma zona não derrube o serviço.

---

## 4. Pontos de Presença (Points of Presence / Edge Locations)

### O que são

Os **Pontos de Presença** (PoPs ou Edge Locations) são locais físicos distribuídos globalmente — em número muito maior que as regiões — usados para **entregar conteúdo ao usuário final com baixíssima latência**.

### Para que servem

- **Amazon CloudFront** (CDN — Content Delivery Network): distribui conteúdo estático (imagens, vídeos, páginas) a partir do ponto de presença mais próximo do usuário
- **AWS Global Accelerator**: otimiza o roteamento de tráfego para aplicações globais
- **Route 53** (DNS): resolução de nomes de domínio com alta performance

```
Usuário em Lisboa
    ↓
Edge Location em Frankfurt (mais próxima)
    ↓ cache do conteúdo
Resposta rápida — sem precisar ir até a região original
```

---

## 5. Visão Geral da Hierarquia

```
Infraestrutura Global AWS
│
├── Regiões (27+)
│   └── ex: sa-east-1 (São Paulo), us-east-1 (Virgínia)
│       │
│       └── Zonas de Disponibilidade (87+ no total)
│           └── ex: sa-east-1a, sa-east-1b, sa-east-1c
│               │
│               └── Data Centers físicos
│
└── Pontos de Presença / Edge Locations (400+)
    └── ex: São Paulo, Buenos Aires, Frankfurt, Tóquio...
```

---

## 6. Provisionamento de Recursos e APIs AWS

Toda interação com os serviços da AWS — seja pelo console web, CLI ou SDKs — acontece por meio das **APIs da AWS**. Ao criar um recurso (ex: uma instância EC2), você está fazendo uma chamada de API para a infraestrutura global da AWS na região escolhida.

### Formas de provisionar recursos

| Método | Descrição |
|---|---|
| **Console AWS** | Interface web, visual e intuitiva |
| **AWS CLI** | Linha de comando — ideal para automação |
| **SDKs** | Bibliotecas para Python (boto3), JS, Java, etc. |
| **CloudFormation / Terraform** | Infraestrutura como código (IaC) |

---

## 7. Resumo dos Conceitos

| Conceito | Definição resumida |
|---|---|
| **Infraestrutura Global** | Conjunto de data centers, redes e recursos físicos da AWS no mundo |
| **Região** | Área geográfica com múltiplos data centers isolados |
| **Zona de Disponibilidade (AZ)** | Data center(s) isolado(s) dentro de uma região |
| **Ponto de Presença** | Local de borda para entrega de conteúdo com baixa latência |
| **Alta Disponibilidade** | Sistema continua funcionando mesmo com falha parcial |
| **Tolerância a Falhas** | Capacidade de resistir a falhas sem interrupção do serviço |

---

> 💡 **Dica para a prova CLF-C02:** Região, AZ e Edge Location são conceitos **muito cobrados** no exame. Saiba diferenciar os três e entender a relação hierárquica entre eles. Questões comuns:
> - *"O que garante alta disponibilidade em caso de falha de um data center?"* → **Múltiplas AZs**
> - *"O que reduz a latência para usuários globais?"* → **Edge Locations / CloudFront**
> - *"Onde os dados ficam armazenados por padrão?"* → **Na região escolhida**

---

## Links Úteis

- [Infraestrutura Global AWS](https://aws.amazon.com/pt/about-aws/global-infrastructure/)
- [Mapa interativo de regiões e AZs](https://infrastructure.aws/)

---

*Aula 01 — Módulo: Infraestrutura Global AWS | Curso Preparatório AWS Cloud Practitioner*
