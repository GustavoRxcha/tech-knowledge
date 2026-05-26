---
title: "CLF-C02 Aulas 1-6 — Segurança na Nuvem com AWS"
type: source
tags: [aws, segurança, clf-c02, shared-responsibility, iam, kms, organizations, artifact, waf, shield, inspector, guardduty]
created: 2026-05-26
updated: 2026-05-26
sources: 1
---

# CLF-C02 Aulas 1-6 — Segurança na Nuvem com AWS

Módulo conceitual do preparatório AWS Cloud Practitioner (CLF-C02). Cobre os principais conceitos e serviços de segurança da AWS cobrados no exame.

---

## Aula 1 — Modelo de Responsabilidade Compartilhada

O conceito central do módulo: a segurança na cloud é dividida entre AWS e cliente.

```
[AWS]                          [Cliente]
Segurança DA nuvem    +    Segurança NA nuvem
(infraestrutura)          (o que você coloca lá)
```

### Responsabilidade da AWS (Segurança DA nuvem)
- Hardware físico dos data centers
- Rede física global
- Virtualização (hypervisor)
- Armazenamento físico
- Segurança física dos data centers

### Responsabilidade do Cliente (Segurança NA nuvem)
- Sistema Operacional das instâncias EC2 (patches, atualizações)
- Aplicações rodando nas instâncias
- Banco de dados (configuração e acesso)
- Dados armazenados
- Gerenciamento de identidades (IAM)
- Configuração de rede (VPC, Security Groups)
- Criptografia dos dados

### Varia conforme o serviço

| Serviço | Tipo | Responsabilidade do cliente |
|---|---|---|
| EC2 | IaaS | SO, runtime, app, dados |
| Elastic Beanstalk | PaaS | App e dados |
| Lambda | Serverless | Código e dados |

Quanto mais gerenciado o serviço, menos infraestrutura o cliente precisa proteger.

**Analogia:** AWS = Engenheiro Civil (constrói o prédio com segurança estrutural). Cliente = Morador (tranca a porta do apartamento, decide quem entra).

---

## Aula 2 — Criptografia e KMS

### Dados em Repouso (Data at Rest)
Dados **armazenados** — não trafegando. Exemplos: volume EBS, bucket S3, banco RDS, snapshots.

### Dados em Trânsito (Data in Transit)
Dados **sendo transmitidos**. Exemplos: login na aplicação, dados entre EC2 e RDS, upload para S3, comunicação entre APIs.

### AWS KMS — Key Management Service
Serviço gerenciado para criação e gestão de chaves criptográficas.

| Característica | Descrição |
|---|---|
| Gerenciado | Sem infraestrutura para provisionar |
| Centralizado | Gerencia todas as chaves em um lugar |
| Integrado | Funciona com EBS, S3, RDS, DynamoDB |
| Controle de acesso | Define quem pode usar cada chave |
| Auditoria | Logs de uso das chaves via CloudTrail |

- Dados em repouso → KMS criptografa os dados armazenados
- Dados em trânsito → SSL/TLS (HTTPS) criptografa o transporte

---

## Aula 3 — Gerenciamento de Acessos (IAM)

Revisão CLF-C02 do IAM. Consolida o que foi visto na trilha hands-on com perspectiva de certificação.

Componentes: Usuário Root (evitar usar, ativar MFA), Usuários IAM, Grupos, Políticas (JSON), Roles (identidades temporárias assumíveis).

Ver: [[entities/aws-iam]] para cobertura completa.

**Destaques CLF-C02:**
- IAM é **gratuito**
- Novo usuário tem acesso a **nada** por padrão (menor privilégio)
- Lambda acessa S3 via **IAM Role** (nunca credenciais hardcodadas)
- Grupos **não** podem ser aninhados

---

## Aula 4 — AWS Organizations

Serviço **gratuito** para gerenciar múltiplas contas AWS centralmente.

### Problema resolvido
Uma conta única cria problemas: impossível separar custos por time, limites de recursos compartilhados, múltiplos logins sem gerenciamento central.

### Componentes
- **Management Account** — conta central que gerencia todas as outras
- **OU (Organizational Unit)** — agrupamento hierárquico de contas
- **Faturamento Consolidado** — uma fatura única; volume combinado pode gerar descontos
- **SCP (Service Control Policies)** — políticas que restringem serviços por OU; herdadas por todos os usuários do grupo

```
[Conta Gerenciadora]
├── [OU: Produção]
│   ├── Conta Prod Web
│   └── Conta Prod API
├── [OU: Desenvolvimento]
│   └── Conta Dev
└── [OU: Operações]
    └── Conta Monitoring
```

---

## Aula 5 — Conformidade e AWS Artifact

### Conformidade
Aderir a regulações legais do setor: LGPD (Brasil), GDPR (Europa), HIPAA (EUA Saúde), SOC 1/2/3, ISO 27001. A responsabilidade de conformidade também é **compartilhada**.

### AWS Artifact
Serviço **gratuito** com dois componentes:

| Componente | O que faz |
|---|---|
| **Artifact Agreements** | Assinar contratos digitais com a AWS (LGPD, HIPAA, GDPR DPA) |
| **Artifact Reports** | Baixar relatórios de conformidade gerados por auditores externos independentes |

**Caso de uso:** Auditoria exige comprovação de conformidade da infraestrutura → baixar relatório no Artifact Reports e apresentar.

---

## Aula 6 — Serviços Adicionais de Segurança

### AWS WAF — Web Application Firewall
Firewall para aplicações web. Filtra tráfego HTTP/HTTPS malicioso **antes** que chegue à aplicação.

- Protege contra SQL Injection, XSS e outros ataques OWASP
- Integra com ALB, EC2, CloudFront
- Regras pré-configuradas e customizáveis

### AWS Shield — Proteção DDoS

| Versão | Custo | Proteção |
|---|---|---|
| Shield Standard | **Gratuito** (incluso) | DDoS comuns; ativo por padrão |
| Shield Advanced | Pago | DDoS avançados + suporte 24/7 + integração WAF + diagnósticos |

### Amazon Inspector
Escaneia automaticamente **vulnerabilidades** (CVEs) em instâncias EC2 e containers. Compara com banco de CVEs e benchmarks de segurança. Scan programado ou contínuo.

### Amazon GuardDuty
Detecta **atividades maliciosas** em tempo real usando Machine Learning. Monitora: logs DNS, fluxo VPC, eventos S3, CloudTrail, atividade RDS.

### Par Inspector vs GuardDuty (mais cobrado na prova)

| Aspecto | Amazon Inspector | Amazon GuardDuty |
|---|---|---|
| Foco | Vulnerabilidades conhecidas (CVEs) | Atividades maliciosas em tempo real |
| O que analisa | SO e software da instância | Tráfego de rede e eventos da conta |
| Fonte de dados | CVEs, benchmarks | Logs DNS, VPC, CloudTrail |
| Exemplo | "Seu SO tem CVE-2024-X" | "Alguém tenta invadir do IP Y" |

---

## Mapa de palavras-gatilho (prova CLF-C02)

| Palavra-gatilho | Resposta |
|---|---|
| "segurança física dos data centers" | AWS (Segurança DA nuvem) |
| "atualizar SO de uma EC2" | Cliente (Segurança NA nuvem) |
| "gerenciar chaves criptográficas" | KMS |
| "dados em repouso" | Dados armazenados (EBS, S3, RDS) |
| "dados em trânsito" | Dados sendo transmitidos (HTTPS, SSL) |
| "múltiplas contas AWS centralizadas" | AWS Organizations |
| "fatura única para várias contas" | Faturamento Consolidado (Organizations) |
| "restringir serviços por unidade organizacional" | SCP |
| "relatório de conformidade LGPD/GDPR" | AWS Artifact Reports |
| "assinar contrato HIPAA com AWS" | AWS Artifact Agreements |
| "proteger contra SQL Injection" | WAF |
| "proteger contra DDoS" | Shield |
| "DDoS gratuito" | Shield Standard |
| "escanear vulnerabilidades em EC2" | Amazon Inspector |
| "detectar atividades maliciosas com ML" | GuardDuty |

---

## Fontes

- Arquivo: `raw/clf-c02-seguranca-nuvem-aws-aulas-1-6-completo.md`
- Módulo: Segurança na Nuvem com AWS | Aulas 1-6 | CLF-C02
