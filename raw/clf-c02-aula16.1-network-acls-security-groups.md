# Network ACLs e Security Groups: Camadas de Segurança na AWS

> 📋 **Curso:** Redes em AWS — Preparatório AWS Cloud Practitioner (CLF-C02)
> 📌 **Aula:** Conceitual — Network ACLs e Security Groups | Sem pré-requisitos

---

## Visão Geral

Agora que você sabe como conectar a VPC à internet (IGW, VPN, Direct Connect), precisa aprender **como controlar qual tráfego é permitido**. Existem **duas camadas de segurança** na AWS:

1. **Network ACLs (NACLs)** — Segurança no nível da sub-rede
2. **Security Groups** — Segurança no nível da instância EC2

---

## 1. O Problema: Quem Pode Acessar Minhas Recursos?

### Cenário

```
[Internet]
   ↓ requisição HTTP
[IGW]
   ↓
[Sub-rede Pública]
   ↓
[EC2 — Servidor Web]
```

**Perguntas críticas:**
- Toda requisição que chega pela internet deve ser aceita?
- Se um pacote entra na sub-rede, ele automaticamente sai?
- Como proteger instâncias de acessos não autorizados?

> ⚠️ A resposta é: **NÃO**. Você precisa configurar regras de segurança.

---

## 2. Network ACLs (NACLs)

### O que é

Uma **Network ACL (NACL)** é uma **lista de controle de acesso de rede** que filtra o tráfego de **entrada e saída de uma sub-rede**.

Cada sub-rede (pública ou privada) tem uma NACL associada que funciona como um **firewall no nível da sub-rede**.

```
[Internet]
   ↓
[NACL — Sub-rede A]
   ↓ bloqueia/permite
[Instâncias dentro da sub-rede]
```

### Características da NACL

| Característica | Descrição |
|---|---|
| **Escopo** | Opera no nível da **sub-rede** |
| **Stateless** | Não guarda estado — verifica **todas as entradas e saídas** contra as regras |
| **Regras de entrada** | Definem qual tráfego **pode entrar** na sub-rede |
| **Regras de saída** | Definem qual tráfego **pode sair** da sub-rede |
| **Ordem de avaliação** | Regras são avaliadas em **ordem numérica** (primeira match vence) |

### Comportamento Stateless

A palavra-chave é **stateless** — a NACL não "lembra" de conexões anteriores.

**Exemplo:**

```
1. Cliente envia requisição para porta 80 (HTTP)
   ↓ NACL verifica: "Entrada na porta 80 é permitida?"
   → SIM → Pacote entra na sub-rede

2. Servidor responde pela mesma porta 80
   ↓ NACL verifica NOVAMENTE: "Saída pela porta 80 é permitida?"
   → Precisa de regra de saída explícita
   → SIM → Resposta sai; NÃO → Resposta bloqueada
```

> 📌 **Ponto crítico:** Mesmo que a entrada seja permitida, a saída **precisa ser explicitamente permitida** também.

### Comportamento Padrão

Por padrão, uma NACL recém-criada:

```
Entrada:  ✅ Permite TODO tráfego
Saída:    ✅ Permite TODO tráfego
```

> ⚠️ Isso significa que você precisa **customizar a NACL** para seu cenário real — o padrão é muito permissivo.

### Exemplo de Regra NACL

```
Inbound Rules (Entrada):
┌─────────┬──────────┬─────────┬──────────────┬─────────────┐
│ Priority│ Protocol │ Port    │ Source       │ Action      │
├─────────┼──────────┼─────────┼──────────────┼─────────────┤
│ 100     │ TCP      │ 80      │ 0.0.0.0/0    │ Allow (HTTP)│
│ 110     │ TCP      │ 443     │ 0.0.0.0/0    │ Allow(HTTPS)│
│ 120     │ TCP      │ 22      │ 10.0.0.0/8   │ Allow (SSH) │
│ 32767   │ ALL      │ ALL     │ 0.0.0.0/0    │ Deny ()*    │
└─────────┴──────────┴─────────┴──────────────┴─────────────┘
* Regra final implícita — bloqueia tudo que não foi permitido
```

### Quando usar NACL

- ✅ Bloquear ataques em **nível de sub-rede**
- ✅ Controlar tráfego entre sub-redes
- ✅ Implementar firewall básico
- ❌ Não é granular o suficiente para controle por instância (use Security Groups)

---

## 3. Security Groups

### O que é

Um **Security Group** é um **firewall virtual** que filtra tráfego de **entrada e saída no nível da instância EC2**.

Enquanto a NACL protege a **sub-rede inteira**, o Security Group protege **uma instância específica** ou um grupo delas.

```
[Internet]
   ↓
[NACL — Sub-rede]
   ↓ permitido
[EC2 Instância]
   ↓
[Security Group]
   ↓ bloqueia/permite
[Processo dentro da EC2]
```

### Características do Security Group

| Característica | Descrição |
|---|---|
| **Escopo** | Opera no nível da **instância EC2** (ou recurso) |
| **Stateful** | **Guarda estado** — se entrada é permitida, saída é automaticamente permitida |
| **Regras de entrada** | Definem qual tráfego pode chegar à instância |
| **Regras de saída** | Definem qual tráfego pode sair da instância |
| **Padrão** | Por padrão: entrada **bloqueada**, saída **permitida** |

### Comportamento Stateful

A palavra-chave é **stateful** — o Security Group "lembra" de conexões.

**Exemplo:**

```
1. Cliente envia requisição para porta 80
   ↓ Security Group verifica: "Entrada na porta 80 é permitida?"
   → SIM → Pacote entra; conexão é "lembrada"

2. Servidor responde pela mesma porta 80
   ↓ Security Group já sabe: "Esta é uma resposta para conexão estabelecida"
   → Automaticamente PERMITIDA (sem verificar regra de saída)
```

> 📌 **Vantagem:** Você só precisa definir regras de **entrada**; as de saída funcionam automaticamente.

### Comportamento Padrão

Por padrão, um Security Group recém-criado:

```
Entrada:  ❌ Bloqueia TODO tráfego
Saída:    ✅ Permite TODO tráfego
```

> ⚠️ Você precisa **adicionar regras de entrada** para cada acesso que deseja permitir.

### Exemplo de Regra Security Group

```
Inbound Rules (Entrada):
┌──────────┬────────┬──────────┬─────────────────────┐
│ Protocol │ Port   │ Source   │ Descrição           │
├──────────┼────────┼──────────┼─────────────────────┤
│ TCP      │ 80     │ 0.0.0.0/0│ HTTP de qualquer IP │
│ TCP      │ 443    │ 0.0.0.0/0│ HTTPS de qualquer IP│
│ TCP      │ 3306   │ 10.0.1.0 │ MySQL da sub-rede 1 │
│ TCP      │ 22     │ 10.0.0.0 │ SSH interno apenas  │
└──────────┴────────┴──────────┴─────────────────────┘

Outbound Rules (Saída):
[Padrão] TODO tráfego permitido
```

### Quando usar Security Group

- ✅ Controlar acesso **por instância**
- ✅ Permitir HTTP/HTTPS para servidores web
- ✅ Permitir SSH apenas de IPs internos
- ✅ Permitir MySQL apenas de aplicações específicas
- ✅ Implementar segurança **granular**

---

## 4. Fluxo Completo de um Pacote

```
[Cliente na Internet]
   ↓ requisição HTTP para porta 80
[Internet Gateway]
   ↓
[NACL — Sub-rede]
   ├─ Regra de entrada: "TCP 80 permitido?"
   ├─ SIM → continua
   └─ NÃO → pacote bloqueado aqui
   ↓
[EC2 Instância]
   ↓
[Security Group]
   ├─ Regra de entrada: "TCP 80 permitido?"
   ├─ SIM → pacote aceito
   └─ NÃO → pacote bloqueado aqui
   ↓
[Servidor Web dentro da EC2]
   ↓ resposta
[Security Group]
   ├─ Stateful: "Esta é resposta a requisição aceita?"
   ├─ SIM → Automaticamente permitida (sem regra explícita)
   └─
   ↓
[NACL — Sub-rede]
   ├─ Regra de saída: "TCP 80 permitido?"
   ├─ SIM → resposta sai
   └─ NÃO → resposta bloqueada aqui
   ↓
[Internet Gateway]
   ↓
[Cliente]
```

---

## 5. Comparativo: NACL vs Security Group

| Aspecto | NACL | Security Group |
|---|---|---|
| **Escopo** | Sub-rede | Instância EC2 |
| **Stateless/Stateful** | **Stateless** | **Stateful** |
| **Entrada padrão** | ✅ Permite tudo | ❌ Bloqueia tudo |
| **Saída padrão** | ✅ Permite tudo | ✅ Permite tudo |
| **Número de regras** | Limitado | Muitas regras possíveis |
| **Granularidade** | Coarse (grosseira) | Fine (granular) |
| **Aplicação** | Automática em sub-rede | Manual por recurso |
| **Overhead** | Baixo | Muito baixo |

---

## 6. Exemplo Prático: Web Server com Banco de Dados

### Arquitetura

```
[Internet]
   ↓
[NACL Sub-rede Pública]
   ↓ permite HTTP/HTTPS
[EC2 Web Server]
   ↓ Security Group permite entrada 80/443
   └─ faz conexão com banco de dados
   ↓
[NACL Sub-rede Privada]
   ↓ permite MySQL apenas da sub-rede pública
[RDS Database]
   └─ Security Group permite entrada apenas do Web Server
```

### Regras Necessárias

**NACL Sub-rede Pública:**
```
Entrada:
  - TCP 80 (HTTP): 0.0.0.0/0 ✅ Allow
  - TCP 443 (HTTPS): 0.0.0.0/0 ✅ Allow
  - TCP 3306 (MySQL resposta): 10.0.1.0/24 ✅ Allow (from private subnet)

Saída:
  - TCP 3306 (MySQL): 10.0.1.0/24 ✅ Allow
  - TODO: ✅ Allow (padrão)
```

**Security Group Web Server:**
```
Entrada:
  - TCP 80: 0.0.0.0/0 ✅ Allow
  - TCP 443: 0.0.0.0/0 ✅ Allow

Saída:
  - TODO: ✅ Allow (padrão)
```

**NACL Sub-rede Privada:**
```
Entrada:
  - TCP 3306 (MySQL): 10.0.0.0/24 ✅ Allow (from public subnet)

Saída:
  - TODO: ✅ Allow (padrão)
```

**Security Group RDS:**
```
Entrada:
  - TCP 3306: <SG Web Server> ✅ Allow

Saída:
  - TODO: ✅ Allow (padrão)
```

---

## 7. Resumo das Duas Camadas

| Camada | Recurso | Função |
|---|---|---|
| **Nível de Sub-rede** | Network ACL | Controle geral de tráfego da sub-rede |
| **Nível de Instância** | Security Group | Controle granular por instância |

> 📌 **Boas práticas:** Use NACL para controle de sub-rede amplo + Security Group para controle específico por instância.

---

## 8. Conceitos-Chave

| Conceito | Definição |
|---|---|
| **Network ACL (NACL)** | Firewall de nível de sub-rede |
| **Security Group** | Firewall de nível de instância |
| **Stateless** | Verifica entrada E saída contra regras |
| **Stateful** | Lembra de conexões; saída automática se entrada permitida |
| **Regra de entrada** | Define qual tráfego pode entrar |
| **Regra de saída** | Define qual tráfego pode sair |
| **Padrão permissivo** | Por padrão permite (NACL) |
| **Padrão restritivo** | Por padrão bloqueia entrada (Security Group) |

---

> 💡 **Dica para a prova CLF-C02:** Questões típicas sobre segurança:

- *"Qual recurso controla tráfego no nível da sub-rede?"* → **Network ACL (NACL)**
- *"Qual recurso controla tráfego no nível da instância EC2?"* → **Security Group**
- *"Qual é stateless?"* → **NACL** (verifica entrada E saída)
- *"Qual é stateful?"* → **Security Group** (lembra conexões)
- *"Por padrão, qual permite TODO tráfego de entrada?"* → **NACL**
- *"Por padrão, qual bloqueia TODO tráfego de entrada?"* → **Security Group**
- *"Um pacote que é bloqueado pela NACL pode passar no Security Group?"* → **NÃO** — bloqueado na NACL já não chega lá

---

## Links Úteis

- [Network ACLs — Documentação AWS](https://docs.aws.amazon.com/pt_br/vpc/latest/userguide/vpc-network-acls.html)
- [Security Groups — Documentação AWS](https://docs.aws.amazon.com/pt_br/vpc/latest/userguide/VPC_SecurityGroups.html)

---

*Aula 16 — Módulo: Redes em AWS | Curso Preparatório AWS Cloud Practitioner*
