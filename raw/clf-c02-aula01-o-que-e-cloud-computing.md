# O que é Cloud Computing?

> 📋 **Curso:** Introdução à Cloud — Preparatório AWS Cloud Practitioner (CLF-C02)
> 📌 **Aula:** Conceitual — sem pré-requisitos técnicos

---

## 1. Objetivos da Aula

- Entender o que é **Cloud Computing** e seus principais benefícios
- Descrever os **modelos de serviço** (IaaS, PaaS, SaaS)
- Descrever os **modelos de implantação** (Public, Private, Hybrid)
- Contextualizar o mundo **pré-cloud** para entender a evolução

---

## 2. O Mundo Antes da Cloud (Pré-Cloud)

Para entender o valor da computação em nuvem, é importante entender como a infraestrutura de TI funcionava antes dela. Três conceitos marcam essa era:

### 2.1 Modelo Cliente-Servidor

A arquitetura mais básica e comum:

```
[Clientes] → [Roteador] → [Servidor] → [Banco de Dados]
```

- Computadores clientes se conectavam a um servidor local
- O servidor centralizava dados e aplicações
- Funcionava bem para empresas pequenas com necessidades simples

### 2.2 Ambientes On-Premises (On-Prem)

Com o crescimento das empresas, um único servidor deixou de ser suficiente. As organizações passaram a construir sua própria infraestrutura física:

- **Data centers** próprios com dezenas ou centenas de servidores
- Toda a infraestrutura era **comprada, instalada e gerenciada** pela própria empresa
- Responsabilidades incluíam:
  - Aquisição e configuração de hardware
  - Atualização de sistemas operacionais
  - Configuração de redes
  - Controle de temperatura e refrigeração
  - Segurança física
  - Manutenção contínua

> ⚠️ Tudo isso gera **alto custo**, **alta complexidade** e necessidade de equipes dedicadas apenas para manter a infraestrutura funcionando — antes mesmo de pensar no negócio em si.

### 2.3 Virtualização

Um avanço tecnológico que preparou o terreno para a cloud:

- Tecnologia de **hypervisor** permite que um único servidor físico rode **múltiplas instâncias** de máquinas virtuais simultaneamente
- Melhor aproveitamento dos recursos de hardware
- Base tecnológica sobre a qual a computação em nuvem foi construída

```
[Servidor Físico]
    ↓ Hypervisor
├── Máquina Virtual 1
├── Máquina Virtual 2
└── Máquina Virtual 3
```

---

## 3. O que Mudou: A Chegada da Cloud

Com a massificação da internet e a evolução tecnológica (conectividade 3G/4G, dispositivos móveis, IoT), a demanda por infraestrutura escalável explodiu:

- Smartphones, tablets, carros conectados, sensores — todos precisam de backend
- Conectar tudo isso a um data center físico e local deixou de ser viável
- Surgiu a necessidade de um **ambiente distribuído, acessível via internet**

### A solução: Cloud Computing

Ao invés de manter data centers próprios, as empresas passam a consumir infraestrutura de **provedores especializados** (como a AWS) via internet:

```
Antes:  [Dispositivos] → [Data Center próprio]
Depois: [Dispositivos] → [Internet] → [Provedor Cloud (AWS)]
```

O provedor mantém a infraestrutura física; o cliente consome os serviços sob demanda.

---

## 4. Definição Formal de Cloud Computing

> *"Entrega de recursos de TI sob demanda, por meio da internet, com precificação baseada em pagamento conforme o uso."*
>
> — **Amazon Web Services**

### Palavras-chave da definição

| Termo | Significado |
|---|---|
| **Recursos de TI** | Servidores, armazenamento, banco de dados, redes, software, etc. |
| **Sob demanda** | Disponíveis imediatamente, sem necessidade de compra prévia |
| **Por meio da internet** | Acessíveis de qualquer lugar com conexão |
| **Pagamento conforme o uso** | Você paga apenas pelo que consome, sem custos fixos de infraestrutura |

---

## 5. Benefício-Chave: Pay-as-you-go

O principal benefício da cloud é o modelo de **pagamento pelo uso** (*pay-as-you-go*):

| Aspecto | On-Premises | Cloud |
|---|---|---|
| **Custo inicial** | Alto (hardware, instalação) | Zero |
| **Custo operacional** | Alto (equipe, energia, refrigeração) | Proporcional ao uso |
| **Escalabilidade** | Lenta e cara | Imediata e elástica |
| **Gerenciamento** | Responsabilidade da empresa | Compartilhado ou gerenciado pelo provedor |
| **Tempo para provisionar** | Semanas/meses | Segundos/minutos |

---

## 6. Próximos Temas do Curso

| Tema | Descrição |
|---|---|
| **Benefícios da Cloud** | Elasticidade, agilidade, alcance global, alta disponibilidade |
| **Modelos de Serviço** | IaaS, PaaS, SaaS — níveis de gerenciamento e responsabilidade |
| **Modelos de Implantação** | Public Cloud, Private Cloud, Hybrid Cloud |

---

## 7. Links e Referências Úteis

- [História da Computação em Nuvem](https://aws.amazon.com/pt/what-is-cloud-computing/)
- [Overview da AWS](https://aws.amazon.com/pt/about-aws/)
- Fórum e comunidade da plataforma do curso

---

> 💡 **Dica para a prova CLF-C02:** A definição formal de Cloud Computing e o conceito de *pay-as-you-go* são temas recorrentes no exame. Memorize a definição da AWS e saiba diferenciar os ambientes **on-premises**, **cloud** e **híbrido**.

---

*Aula 01 — Módulo: Introdução à Cloud Computing | Curso Preparatório AWS Cloud Practitioner*
