# Amazon EC2 Auto Scaling

> 📋 **Curso:** Computação na AWS — Preparatório AWS Cloud Practitioner (CLF-C02)
> 📌 **Aula:** Conceitual — EC2 Auto Scaling

---

## 1. O Problema: Dimensionar Capacidade é Difícil

Imagine um e-commerce com variação de tráfego ao longo da semana:

```
Segunda a Quarta: Alto volume de acessos (pico)
Quinta a Sexta:   Volume médio
Sábado e Domingo: Volume baixo
```

Como configurar a infraestrutura para esse cenário?

### Opção 1: Escalar para a capacidade total (máximo)

- ✅ Todos os usuários são atendidos mesmo no pico
- ❌ Nos dias de baixo movimento, a capacidade fica **ociosa** — você paga por recursos que não usa

### Opção 2: Configurar para a capacidade média

- ✅ Custo equilibrado
- ❌ Nos dias de pico, as instâncias ficam sobrecarregadas → **experiência ruim para o usuário**

### Opção 3: Escalar conforme a necessidade ✅

- ✅ Nos dias de pico: adiciona instâncias automaticamente
- ✅ Nos dias tranquilos: remove instâncias para economizar
- ✅ O usuário é sempre bem atendido
- ✅ Você paga apenas pelo que usa

> 📌 É exatamente essa terceira opção que o **EC2 Auto Scaling** implementa.

---

## 2. O que é o EC2 Auto Scaling?

O **Amazon EC2 Auto Scaling** é o serviço que adiciona ou remove **instâncias EC2 automaticamente** com base na demanda atual, garantindo que você sempre tenha a quantidade certa de capacidade computacional.

### Tipo de escalabilidade: Horizontal

O Auto Scaling trabalha com **escalabilidade horizontal** — em vez de aumentar o tamanho de uma instância (vertical), ele **adiciona mais instâncias** com a mesma configuração para dividir a carga.

```
Escalabilidade Vertical (sem Auto Scaling):
[Instância pequena] → [Instância maior] (requer downtime)

Escalabilidade Horizontal (Auto Scaling):
[1 instância] → [2 instâncias] → [4 instâncias] (sem downtime)
```

---

## 3. Benefícios do Auto Scaling

| Benefício | Descrição |
|---|---|
| **Elasticidade** | Ajusta a capacidade automaticamente conforme a demanda |
| **Tolerância a falhas** | Detecta instâncias indisponíveis e as substitui automaticamente |
| **Alta disponibilidade** | Suporte a implantação **multi-AZ** — instâncias em múltiplas zonas de disponibilidade |
| **Melhor gerenciamento de custos** | Escala para baixo nos períodos de baixa demanda, pagando só pelo necessário |

---

## 4. Configurando um Auto Scaling Group (ASG)

A configuração do Auto Scaling é feita através de um **Auto Scaling Group (Grupo de Auto Scaling)**. Os principais parâmetros são:

### Parâmetros de capacidade

| Parâmetro | Descrição | Exemplo |
|---|---|---|
| **Capacidade mínima** | Número mínimo de instâncias sempre em execução, independente da demanda | `1` |
| **Capacidade desejada** | Número de instâncias que o grupo tenta manter por padrão | `2` |
| **Capacidade máxima** | Número máximo de instâncias que podem ser lançadas | `4` |

```
Capacidade mínima:  [■]          → sempre 1 instância rodando
Capacidade desejada: [■][■]      → normalmente 2 instâncias
Capacidade máxima:  [■][■][■][■] → no pico, até 4 instâncias
```

> 📌 A capacidade máxima é importante para **controlar custos** — evita que o Auto Scaling crie instâncias indefinidamente em caso de pico extremo ou configuração incorreta.

---

## 5. Abordagens de Escalabilidade

O EC2 Auto Scaling oferece duas abordagens que podem ser usadas **individualmente ou combinadas**:

### 5.1 Escalabilidade Preditiva (Predictive Scaling)

Usa **histórico e machine learning** para prever quando o pico vai acontecer e **provisiona instâncias antecipadamente**.

**Como funciona:**
- Analisa padrões históricos de uso (últimas semanas/meses)
- Prevê os momentos de maior carga
- Lança instâncias **antes** do pico acontecer

**Exemplo:**
```
Todo fim de semana às 20h o tráfego aumenta 80%
→ Auto Scaling preditivo sobe mais instâncias às 19h30
→ Sistema já está pronto quando o pico chega
```

**Requisito:** Os dados históricos de uso devem ser **consistentes e representativos** do padrão real de uso.

**Melhor para:** Serviços com padrões de uso **previsíveis e regulares** (ex: e-commerce com picos semanais conhecidos).

---

### 5.2 Escalabilidade Dinâmica (Dynamic Scaling)

Reage a **métricas em tempo real** para escalar conforme a demanda atual.

**Como funciona:**
- Monitora métricas continuamente (ex: uso de CPU, número de requisições)
- Quando a métrica ultrapassa um **limite (threshold)** configurado, escala para cima
- Quando a métrica cai abaixo do limite, escala para baixo

**Exemplo:**
```
CPU da instância atingiu 70% por 5 minutos
→ Auto Scaling lança mais uma instância
→ Carga dividida entre as duas instâncias
→ CPU de cada uma cai para ~35%
```

**Melhor para:** Serviços com variações de demanda **imprevisíveis ou irregulares**.

---

### Comparativo das Abordagens

| | Preditiva | Dinâmica |
|---|---|---|
| **Base** | Histórico + previsão | Métricas em tempo real |
| **Reação** | Antecipada (proativa) | Reativa |
| **Requisito** | Padrão histórico consistente | Definição de métricas e thresholds |
| **Melhor para** | Picos previsíveis | Variações imprevisíveis |
| **Podem ser combinadas?** | ✅ Sim | ✅ Sim |

---

## 6. Multi-AZ com Auto Scaling

Para maximizar **tolerância a falhas** e **disponibilidade**, o Auto Scaling deve ser configurado para distribuir instâncias em **múltiplas Zonas de Disponibilidade (AZs)**:

```
Auto Scaling Group
├── AZ-a: [instância 1] [instância 2]
└── AZ-b: [instância 3] [instância 4]
         ↓ AZ-a falha
├── AZ-a: ❌ indisponível
└── AZ-b: [instância 3] [instância 4] → continuam atendendo
           + Auto Scaling lança novas instâncias na AZ-b
```

> ✅ Com implantação multi-AZ, mesmo que uma zona de disponibilidade inteira fique fora do ar, o serviço continua funcionando.

---

## 7. Resumo Visual

```
DEMANDA BAIXA          DEMANDA MÉDIA          DEMANDA ALTA
    ↓                       ↓                      ↓
[instância 1]    [inst. 1][inst. 2]    [inst.1][inst.2][inst.3][inst.4]
 (mínimo = 1)      (desejada = 2)           (máximo = 4)
```

---

> 💡 **Dica para a prova CLF-C02:** Questões típicas sobre Auto Scaling:
> - *"Qual serviço adiciona e remove instâncias EC2 automaticamente?"* → **EC2 Auto Scaling**
> - *"Qual abordagem escala com base em padrões históricos?"* → **Escalabilidade Preditiva**
> - *"Qual abordagem reage a métricas em tempo real?"* → **Escalabilidade Dinâmica**
> - *"O que garante disponibilidade mesmo com falha em uma AZ?"* → **Auto Scaling com implantação multi-AZ**
> - *"Qual parâmetro garante que sempre haja pelo menos X instâncias rodando?"* → **Capacidade mínima**

---

## Links Úteis

- [EC2 Auto Scaling — Visão Geral](https://aws.amazon.com/pt/ec2/autoscaling/)
- [Tipos de escalabilidade do Auto Scaling](https://docs.aws.amazon.com/pt_br/autoscaling/ec2/userguide/scaling-overview.html)

---

*Aula 02 — Módulo: Computação na AWS | Curso Preparatório AWS Cloud Practitioner*
