# Elastic Load Balancing (ELB)

> 📋 **Curso:** Computação na AWS — Preparatório AWS Cloud Practitioner (CLF-C02)
> 📌 **Aula:** Conceitual — Elastic Load Balancing

---

## 1. O Problema: Auto Scaling Sem Distribuição de Carga

Imagine o seguinte cenário:

```
[200.000 usuários]
        ↓ requisições
[EC2 #1] [EC2 #2] [EC2 #3] [EC2 #4] [EC2 #5]
```

O **EC2 Auto Scaling** resolveu o problema de escalar o número de instâncias. Mas surgiu um novo problema: **quem decide para qual instância cada requisição vai?**

### O problema sem Load Balancer

Sem um mecanismo de distribuição, as requisições podem ser direcionadas de forma **desequilibrada**:

```
[Usuários]
    ↓ todas as requisições vão para a mesma instância
[EC2 #1 — sobrecarregada 🔥]  [EC2 #2 — ociosa] [EC2 #3 — ociosa]
```

- Uma instância recebe tráfego excessivo → lenta ou indisponível
- Outras instâncias ficam ociosas → recursos desperdiçados
- O Auto Scaling criou mais instâncias, mas elas não estão sendo usadas de forma eficiente

---

## 2. O que é o Elastic Load Balancing?

O **Elastic Load Balancing (ELB)** é um serviço da AWS que **distribui automaticamente o tráfego de entrada** entre múltiplas instâncias EC2 (ou outros alvos), garantindo que nenhuma instância fique sobrecarregada enquanto outras ficam ociosas.

No fundo, o ELB é um **algoritmo de balanceamento de carga** que decide para qual instância cada requisição será enviada.

```
ANTES (sem ELB):
[Usuários] → diretamente para instâncias EC2 (desequilibrado)

DEPOIS (com ELB):
[Usuários] → [ELB] → distribui para instâncias EC2 (equilibrado)
```

---

## 3. Como o ELB Funciona na Prática

### Fluxo de uma requisição com ELB

```
[Cliente externo]
       ↓ requisição
  [Elastic Load Balancer]
       ↓ distribui de forma equilibrada
[EC2 #1] [EC2 #2] [EC2 #3] [EC2 #4]
```

### Integração com EC2 Auto Scaling

O ELB e o EC2 Auto Scaling **trabalham juntos de forma coordenada**:

| Situação | O que acontece |
|---|---|
| Auto Scaling **lança** uma nova instância | ELB automaticamente começa a enviar tráfego para ela |
| Auto Scaling **encerra** uma instância | ELB para de enviar requisições para ela antes do encerramento |
| Uma instância fica **indisponível** | ELB detecta e redireciona o tráfego para instâncias saudáveis |
| Tráfego **aumenta** muito | Auto Scaling lança mais instâncias; ELB distribui entre todas |
| Tráfego **diminui** | Auto Scaling encerra instâncias; ELB ajusta automaticamente |

> ✅ Essa integração é o que torna possível criar aplicações **altamente disponíveis e escaláveis** na AWS.

---

## 4. Tipos de Uso do ELB

### 4.1 Balanceamento de Carga Externo (Internet-facing)

O ELB fica entre os usuários externos (internet) e as instâncias EC2 internas:

```
[Internet / Usuários]
          ↓
    [ELB externo]
          ↓ distribui
[EC2 #1] [EC2 #2] [EC2 #3]
```

**Uso:** Aplicações web, APIs públicas, sites — qualquer serviço acessado pela internet.

---

### 4.2 Balanceamento de Carga Interno (Internal)

O ELB fica entre componentes **dentro da própria infraestrutura AWS**, sem exposição à internet:

```
[Frontend EC2]
      ↓
[ELB interno]
      ↓ distribui
[Backend EC2 #1] [Backend EC2 #2] [Backend EC2 #3]
```

**Uso:** Comunicação entre camadas da aplicação (frontend → backend, microsserviços).

---

## 5. Tipos de Load Balancer na AWS

O ELB oferece três tipos de balanceadores, cada um para um caso de uso específico:

| Tipo | Nome | Camada | Melhor para |
|---|---|---|---|
| **Application LB** | ALB | Camada 7 (HTTP/HTTPS) | Aplicações web, APIs REST, roteamento por URL |
| **Network LB** | NLB | Camada 4 (TCP/UDP) | Alto desempenho, baixa latência, jogos, IoT |
| **Gateway LB** | GWLB | Camada 3 (IP) | Appliances de segurança (firewalls, IDS/IPS) |

> 📌 Para a prova CLF-C02, o mais importante é saber que **ALB** é o mais comum para aplicações web e APIs.

---

## 6. Características do ELB

| Característica | Descrição |
|---|---|
| **Escopo Regional** | Opera no escopo da região — automaticamente distribuído entre AZs |
| **Alta disponibilidade** | Integrado com múltiplas AZs para tolerância a falhas |
| **Escalabilidade automática** | Escala sua própria capacidade conforme o volume de requisições aumenta |
| **Health checks** | Monitora a saúde das instâncias e para de enviar tráfego para as indisponíveis |
| **Integração com Auto Scaling** | Coordena automaticamente com grupos de Auto Scaling |

---

## 7. Arquitetura Completa: ELB + Auto Scaling

A combinação de **ELB + EC2 Auto Scaling** forma a base de aplicações escaláveis e altamente disponíveis na AWS:

```
                    [Usuários]
                         ↓
              [Elastic Load Balancer]
               /          |          \
         [EC2 #1]    [EC2 #2]    [EC2 #3]
            AZ-a        AZ-a       AZ-b
              \          |          /
         [EC2 Auto Scaling Group]
              ↑ monitora e ajusta
         [Métricas (CPU, tráfego...)]


Tráfego alto → Auto Scaling adiciona instâncias → ELB distribui para elas
Tráfego baixo → Auto Scaling remove instâncias → ELB para de enviar para elas
Instância falha → ELB detecta → redireciona tráfego → Auto Scaling repõe
```

---

## 8. Resumo dos Conceitos

| Conceito | Definição |
|---|---|
| **ELB** | Serviço que distribui tráfego entre múltiplas instâncias EC2 |
| **Balanceamento de carga** | Algoritmo que decide para qual instância cada requisição vai |
| **Health check** | Verificação periódica da saúde de cada instância |
| **ELB externo** | Distribui tráfego da internet para instâncias EC2 |
| **ELB interno** | Distribui tráfego entre componentes internos (ex: front → back) |
| **ALB** | Application Load Balancer — camada HTTP, ideal para apps web |
| **NLB** | Network Load Balancer — camada TCP, alto desempenho |

---

> 💡 **Dica para a prova CLF-C02:** Questões típicas sobre ELB:
> - *"Qual serviço distribui o tráfego entre múltiplas instâncias EC2?"* → **Elastic Load Balancing**
> - *"O que acontece quando uma instância EC2 fica indisponível com ELB configurado?"* → O ELB detecta via **health check** e redireciona o tráfego para instâncias saudáveis
> - *"Qual a combinação usada para criar aplicações altamente disponíveis e escaláveis?"* → **ELB + EC2 Auto Scaling**
> - *"Qual tipo de Load Balancer é ideal para aplicações web HTTP/HTTPS?"* → **Application Load Balancer (ALB)**

---

## Links Úteis

- [Elastic Load Balancing — Visão Geral](https://aws.amazon.com/pt/elasticloadbalancing/)
- [Tipos de Load Balancer](https://aws.amazon.com/pt/elasticloadbalancing/features/)

---

*Aula 03 — Módulo: Computação na AWS | Curso Preparatório AWS Cloud Practitioner*
