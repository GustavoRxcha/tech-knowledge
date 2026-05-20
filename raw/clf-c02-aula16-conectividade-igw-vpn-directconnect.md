# Conectividade com AWS: IGW, VPN e Direct Connect

> 📋 **Curso:** Redes em AWS — Preparatório AWS Cloud Practitioner (CLF-C02)
> 📌 **Aula:** Conceitual — Conectividade com AWS | Sem pré-requisitos

---

## Visão Geral

Agora que você conhece a **estrutura interna de uma VPC** (sub-redes públicas e privadas), esta aula aborda **como conectar a VPC com o mundo externo**. Existem três formas principais de conectividade na AWS, cada uma com um propósito específico.

---

## 1. O Problema: Como Conectar a VPC à Internet?

### Cenário base

Você tem uma VPC com sub-redes públicas e privadas, mas como os usuários externos acessam sua aplicação?

```
[Internet / Usuários]
         ↓ requisição HTTP
[VPC com sub-rede pública]
         ↓
[EC2 — Servidor Web]
```

Precisa de algo que **receba requisições da internet** e as **dirija para a VPC**. Isso é o **Internet Gateway**.

---

## 2. Internet Gateway (IGW)

### O que é

O **Internet Gateway** é um serviço AWS que funciona como uma "porta de entrada" para a VPC. Ele conecta a VPC diretamente à internet.

### Funcionalidades

- **Recebe requisições externas** — de usuários na internet
- **Direciona para sub-redes públicas** — roteia o tráfego para as instâncias EC2 apropriadas
- **Permite saída para a internet** — instâncias podem fazer requisições para fora

### Diagrama: Internet Gateway

```
[Internet]
   ↓ requisição HTTP (entrada)
[Internet Gateway (IGW)]
   ↓ roteia
[Sub-rede Pública — VPC]
   ↓
[EC2 — Servidor Web]
   ↓ resposta
[Internet Gateway]
   ↓
[Internet / Cliente]
```

### Arquitetura com IGW

```
[Região AWS]
     ↓
[VPC]
  │
  ├── [Internet Gateway] ← conecta à internet
  │   ↓
  ├── [Sub-rede Pública]
  │   └── [EC2 Web Server] ← acessível da internet
  │
  └── [Sub-rede Privada]
      └── [RDS Database] ← não acessível da internet
```

### Quando usar

- ✅ Servidores web, APIs públicas, qualquer recurso que precisa de acesso direto da internet
- ❌ Bancos de dados, serviços internos (use sub-rede privada)

> 📌 **Regra:** Instâncias EC2 que precisam de acesso à internet **devem estar em sub-redes públicas com IGW configurado**.

---

## 3. Virtual Private Gateway (VPG) e VPN

### O Problema: Conectar Data Center Corporativo à AWS

Imagine um cenário realista:

```
[Data Center Corporativo]
  ├── Firewall
  ├── Rede privada
  └── Dados sensíveis (banco de dados)
         ↓ precisa conectar com segurança
       [Internet]
         ↓ risco — tráfego aberto
[AWS VPC]
  └── Sub-rede privada com RDS
```

**O desafio:** Conectar dados entre o data center e a AWS **sem expor os dados na internet aberta**.

### A solução: VPN (Virtual Private Network)

Uma **VPN (Rede Privada Virtual)** cria um **túnel criptografado** através da internet:

```
[Data Center Corporativo]
         ↓ criptografado
    [Túnel VPN]
         ↓ pela internet (mas protegido)
[AWS VPC — Sub-rede privada]
         ↓
[RDS Database]
```

### Virtual Private Gateway (VGW)

O **Virtual Private Gateway** é o serviço AWS que implementa VPN para conectar sua VPC a:

- Data centers corporativos
- Escritórios remotos
- Sua máquina pessoal
- Outra VPC

### Características da VPN

| Característica | Descrição |
|---|---|
| **Criptografia** | Dados trafegam criptografados através da internet |
| **Segurança** | Protege dados sensíveis durante a transmissão |
| **Custo-efetivo** | Usa a internet pública, sem custo extra de infraestrutura |
| **Velocidade** | Limitada pela velocidade da internet |
| **Sempre disponível** | Conecta através da internet pública |

### Arquitetura com VPN

```
[Data Center Corporativo]
  ├── Rede local
  └── Firewall
         ↓ VPN criptografada
[Virtual Private Gateway]
         ↓
[VPC — Sub-rede Privada]
  └── RDS Database (seguro)
```

### Quando usar VPN

- ✅ Conectar data centers corporativos à AWS
- ✅ Trabalho remoto seguro para funcionários
- ✅ Dados sensíveis que precisam de criptografia
- ❌ Quando precisa de altíssima velocidade (use Direct Connect)

---

## 4. AWS Direct Connect

### O Problema: Velocidade e Dedicação

A **VPN é segura**, mas usa a internet pública — não é ideal para:

- Transferências de **grande volume de dados**
- Aplicações que precisam de **baixíssima latência**
- Conexões que precisam de **garantia de largura de banda**

### A Solução: AWS Direct Connect

**AWS Direct Connect** é uma conexão de **fibra óptica dedicada** entre o seu data center e a AWS.

```
[Data Center Corporativo]
         ↓ fibra óptica dedicada
    [AWS Direct Connect]
         ↓ alta velocidade
[AWS VPC]
```

### Características do Direct Connect

| Característica | Descrição |
|---|---|
| **Velocidade** | Altíssima — até 100 Gbps |
| **Dedicado** | Conexão exclusiva, não compartilhada |
| **Latência baixa** | Conexão ponto a ponto direto |
| **Confiabilidade** | SLA de 99,99% de uptime |
| **Custo** | Mais caro que VPN, mas justificado para grandes volumes |

### Como funciona

1. **Locais de conexão:** AWS tem **Direct Connect locations** em vários provedores de internet
2. **Buscar parceiro próximo:** Você identifica o parceiro Direct Connect na sua região
3. **Conectar fibra óptica:** Construir conexão de fibra óptica dedicada do seu data center até o local AWS
4. **Resultado:** Conexão de altíssima velocidade, ponto a ponto, sem passar pela internet pública

### Diagrama: Direct Connect

```
[Seu Data Center]
       ↓ fibra óptica ponto a ponto
  [Local AWS Direct Connect]
       ↓
[AWS VPC — Qualquer sub-rede]
```

### Quando usar Direct Connect

- ✅ Transferências massivas de dados (TB+)
- ✅ Aplicações que requerem latência muito baixa
- ✅ Conexão permanente de data center corporativo
- ❌ Trabalho ocasional remoto (use VPN)
- ❌ Pequenas transferências (overkill de custo)

---

## 5. Comparativo: IGW vs VPN vs Direct Connect

| Aspecto | Internet Gateway | VPN | Direct Connect |
|---|---|---|---|
| **Propósito** | Acesso internet público | Conectar privado seguro | Conexão dedicada de alto desempenho |
| **Tipo de conexão** | Pública | Criptografada pela internet | Fibra óptica dedicada |
| **Velocidade** | Variável (depende internet) | Variável (depende internet) | Até 100 Gbps |
| **Latência** | Variável | Variável | Muito baixa |
| **Criptografia** | ❌ Não (HTTP/HTTPS faz isso) | ✅ Sim (tunnel criptografado) | Pode adicionar criptografia |
| **Custo** | Incluído no IGW | Barato (usa internet) | Caro (infraestrutura dedicada) |
| **Caso de uso** | Servidores web públicos | Data center corporativo | Grande volume de dados |
| **Setup** | Rápido (minutos) | Médio (horas) | Lento (semanas) |

---

## 6. Arquitetura Completa: Conectividade em Camadas

```
[Internet]                    [Data Center Corporativo]
   ↓                              ↓
[IGW]                        [VPN Criptografada]
   ↓                              ↓
[Sub-rede Pública]      [Virtual Private Gateway]
   ↓                              ↓
[EC2 Web Server]         [Sub-rede Privada]
   ↓                              ↓
   └────────────────────────────┘
                  ↓
[Sub-rede Privada com RDS]

Alternativa para alto desempenho:
[Data Center] ─── fibra óptica ─── [Direct Connect] ─── [AWS VPC]
```

---

## 7. Conceitos-Chave

| Conceito | Definição |
|---|---|
| **Internet Gateway (IGW)** | Porta de entrada da VPC para a internet pública |
| **Virtual Private Gateway (VGW)** | Serviço que implementa VPN para conexão privada e segura |
| **VPN (Virtual Private Network)** | Túnel criptografado para comunicação segura |
| **AWS Direct Connect** | Conexão dedicada de fibra óptica para alto desempenho |
| **Túnel VPN** | Caminho criptografado através da internet |
| **Ponto a ponto** | Conexão direta entre dois pontos sem intermediários |

---

## 8. Decisão: Qual Usar?

```
Precisa de acesso à internet pública?
├─ SIM → Use Internet Gateway (IGW)
└─ NÃO → Próxima pergunta

Precisa conectar data center corporativo com segurança?
├─ SIM + dados sensíveis → Use VPN (VGW)
├─ SIM + grande volume + baixa latência → Use Direct Connect
└─ NÃO → Próxima pergunta

Só precisa de sub-redes privadas internas?
└─ SIM → Nenhum dos três (apenas roteamento interno)
```

---

> 💡 **Dica para a prova CLF-C02:** Questões típicas sobre conectividade:

- *"Qual serviço permite que instâncias EC2 acessem a internet?"* → **Internet Gateway (IGW)**
- *"Como conectar um data center corporativo à AWS de forma segura?"* → **VPN com Virtual Private Gateway**
- *"Qual serviço oferece altíssima velocidade dedicada?"* → **AWS Direct Connect**
- *"Qual é mais barato: VPN ou Direct Connect?"* → **VPN** (usa internet pública)
- *"Um desenvolvedor precisa acessar a VPC do escritório. Qual usar?"* → **VPN com Virtual Private Gateway**
- *"Transferir 10TB entre data center e AWS. Qual é mais adequado?"* → **Direct Connect** (mais rápido e confiável)

---

## Links Úteis

- [Internet Gateway — Documentação AWS](https://docs.aws.amazon.com/pt_br/vpc/latest/userguide/VPC_Internet_Gateway.html)
- [Virtual Private Gateway (VPN) — Documentação AWS](https://docs.aws.amazon.com/pt_br/vpn/latest/s2svpn/VPC_VPN.html)
- [AWS Direct Connect — Documentação AWS](https://docs.aws.amazon.com/pt_br/directconnect/)

---

*Aula 15 — Módulo: Redes em AWS | Curso Preparatório AWS Cloud Practitioner*
