# Computação Sem Servidor: AWS Lambda

> 📋 **Curso:** Computação na AWS — Preparatório AWS Cloud Practitioner (CLF-C02)
> 📌 **Aula:** Conceitual — Serverless e AWS Lambda

---

## 1. O que é Computação Sem Servidor (Serverless)?

**Serverless** (computação sem servidor) é um modelo de execução de código onde:

- O código **é** executado em servidores — mas você **não precisa** provisionar, configurar ou gerenciar esses servidores
- Toda a infraestrutura subjacente (CPU, memória, sistema operacional, rede) é **gerenciada automaticamente** pelo provedor cloud
- A capacidade é **ajustada automaticamente** conforme necessário — sem nenhuma configuração manual

### Serverless vs EC2

| Aspecto | EC2 (IaaS) | Lambda (Serverless) |
|---|---|---|
| **Provisionar servidor** | ✅ Você configura | ❌ Não necessário |
| **Gerenciar SO** | ✅ Você atualiza | ❌ Não necessário |
| **Configurar CPU/RAM** | ✅ Você escolhe | ❌ Automático |
| **Escalabilidade** | Manual ou Auto Scaling | Automática e instantânea |
| **Cobrança** | Por hora da instância ligada | Por tempo de execução do código |
| **Foco do desenvolvedor** | Infra + código | Apenas o código |

> 📌 O nome "sem servidor" não significa que não há servidores — significa que você **não precisa se preocupar** com eles.

---

## 2. AWS Lambda — O Principal Serviço Serverless da AWS

O **AWS Lambda** é o serviço de execução de código serverless da AWS. Você escreve o código, define quando ele deve ser executado, e o Lambda cuida de todo o resto.

### Características principais

- **Execução baseada em eventos** — o código só executa quando acionado por um trigger
- **Suporte a múltiplas linguagens** — Python, Node.js, Java, Go, Ruby, C#/.NET, entre outras
- **Escalabilidade automática** — executa múltiplas instâncias em paralelo conforme a demanda
- **Sem gerenciamento de servidor** — você não vê, não configura e não se preocupa com a infraestrutura
- **Pagamento por uso** — cobra apenas pelo tempo de CPU consumido durante a execução

---

## 3. Como o Lambda Funciona

O fluxo de uso do Lambda segue três etapas:

```
1. ESCREVER          2. CONFIGURAR         3. EXECUTAR
O código             O trigger             Automaticamente
(qualquer            (o que dispara        quando o evento
linguagem)           a função)             ocorre
```

### Passo a passo

```
[Você escreve o código]
         ↓
[Faz upload para o Lambda]
         ↓
[Configura um Trigger]
         ↓
[Evento ocorre] → Lambda executa o código → Resultado
                  (AWS provisiona tudo)
```

---

## 4. Triggers — O que Pode Acionar uma Função Lambda

Uma função Lambda **não executa sozinha** — ela precisa ser acionada por um **trigger (gatilho)**. Exemplos comuns:

| Trigger | Descrição |
|---|---|
| **Upload no S3** | Um arquivo cai em um bucket S3 → Lambda processa o arquivo |
| **Chamada HTTP** | Uma requisição chega via API Gateway → Lambda processa e responde |
| **Mensagem no SQS** | Uma mensagem entra na fila → Lambda a consome e processa |
| **Evento do SNS** | Um tópico SNS publica → Lambda é notificada |
| **Agendamento (EventBridge)** | Executar em horários definidos (ex: todo dia às 8h) |
| **Mudança no DynamoDB** | Um item é inserido/atualizado → Lambda reage ao evento |

> 📌 O Lambda é naturalmente o "cola" entre serviços AWS — conecta eventos de um serviço a ações em outro.

---

## 5. Modelo de Cobrança

O Lambda cobra com base em **dois fatores**:

| Fator | Descrição |
|---|---|
| **Número de invocações** | Cada vez que a função é chamada |
| **Tempo de execução (duração)** | Medido em milissegundos × memória configurada |

> ✅ O Lambda tem um **nível gratuito generoso**: 1 milhão de invocações e 400.000 GB-segundos de computação por mês — permanentemente.

> ⚠️ **Atenção ao custo:** Ao escrever funções Lambda, fique atento ao tempo de execução e aos recursos necessários — quanto mais processamento e tempo, maior o custo.

---

## 6. Casos de Uso Comuns

| Caso de Uso | Exemplo |
|---|---|
| **Processamento de arquivos** | Redimensionar imagens ao fazer upload no S3 |
| **APIs e backends** | Processar requisições HTTP via API Gateway |
| **Automação** | Executar tarefas agendadas (backup, relatórios) |
| **Processamento de streams** | Consumir mensagens do SQS ou DynamoDB Streams |
| **Integração entre serviços** | Reagir a eventos e orquestrar ações entre serviços AWS |

---

## 7. Lambda na Arquitetura do Curso Prático

> 📌 O Lambda já foi usado extensivamente no módulo prático anterior. Conectando com o que foi visto:

```
[API Gateway]          [Lambda]              [DynamoDB]
POST /items    →   processa requisição  →   PutItem
GET /items     →   consulta tabela      →   Scan
DELETE /items  →   remove item          →   DeleteItem
PUT /items     →   atualiza item        →   UpdateItem

Trigger: chamada HTTP via API Gateway
Linguagem: Node.js (no curso prático) / Python com boto3 (equivalente)
```

---

## 8. Outros Serviços Serverless na AWS

O Lambda é o principal, mas existem outros serviços serverless:

| Serviço | Função |
|---|---|
| **AWS Lambda** | Execução de código por evento |
| **Amazon API Gateway** | API HTTP serverless (visto no curso prático) |
| **Amazon DynamoDB** | Banco NoSQL serverless |
| **Amazon S3** | Armazenamento serverless |
| **AWS Fargate** | Containers serverless (sem gerenciar o cluster) |
| **Amazon EventBridge** | Barramento de eventos serverless |

---

## 9. Resumo dos Conceitos

| Conceito | Definição |
|---|---|
| **Serverless** | Execução de código sem provisionar ou gerenciar servidores |
| **AWS Lambda** | Principal serviço serverless da AWS |
| **Função Lambda** | Unidade de código executável no Lambda |
| **Trigger** | Evento que aciona a execução de uma função Lambda |
| **Invocação** | Cada execução de uma função Lambda |
| **Pay-per-use** | Paga pelo tempo de CPU usado na execução |

---

> 💡 **Dica para a prova CLF-C02:** Questões típicas sobre Lambda:
> - *"Qual serviço executa código sem provisionar servidores?"* → **AWS Lambda**
> - *"O que é necessário para executar uma função Lambda?"* → Um **trigger** (evento)
> - *"Como o Lambda é cobrado?"* → Por **número de invocações** e **tempo de execução**
> - *"Qual a diferença entre EC2 e Lambda?"* → EC2 exige gerenciamento de servidor; Lambda é **serverless**
> - *"Um arquivo foi enviado ao S3 e precisa ser processado automaticamente. Qual serviço usar?"* → **Lambda** com trigger no S3

---

## Links Úteis

- [AWS Lambda — Visão Geral](https://aws.amazon.com/pt/lambda/)
- [Preços do Lambda](https://aws.amazon.com/pt/lambda/pricing/)
- [Triggers suportados pelo Lambda](https://docs.aws.amazon.com/pt_br/lambda/latest/dg/lambda-services.html)

---

*Aula 05 — Módulo: Computação na AWS | Curso Preparatório AWS Cloud Practitioner*
