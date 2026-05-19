# AWS Cognito: Gerenciamento de Usuários e Autenticação

## Visão Geral

Esta aula apresenta o **AWS Cognito**, serviço responsável pelo gerenciamento de usuários, autenticação e controle de acesso em aplicações. O Cognito é mencionado como um componente relevante no contexto da arquitetura que será construída ao longo do curso, que também envolve **DynamoDB**, **Lambda** e **API Gateway**.

> 📌 O Cognito não será implementado diretamente neste módulo prático, mas é apresentado conceitualmente por ser parte importante do ecossistema AWS para aplicações com autenticação de usuários.

---

## 1. Contexto da Arquitetura do Curso

A solução prática que será construída envolve os seguintes serviços:

| Serviço | Função |
|---|---|
| **DynamoDB** | Banco de dados NoSQL — armazenar dados/tabelas |
| **Lambda** | Funções serverless — lógica de negócio |
| **API Gateway** | Rotas HTTP que integram com as funções Lambda |
| **Cognito** | Gerenciamento de usuários e autenticação |
| **IAM** | Permissões e roles entre os serviços |

### Atenção: Regiões AWS

> ⚠️ Todos os serviços de uma solução devem estar na **mesma região AWS**. Se a solução foi criada para a região de São Paulo (`sa-east-1`), todos os recursos (Lambda, DynamoDB, API Gateway, etc.) devem ser criados nessa região. Misturar regiões exige configurações adicionais de **multi-região**, aumentando a complexidade.

---

## 2. O que é o AWS Cognito?

O **AWS Cognito** é um serviço gerenciado de **identidade e autenticação** para aplicações. Ele cuida de todo o fluxo de autenticação de usuários, eliminando a necessidade de implementar essa lógica manualmente.

### Principais funcionalidades

- Cadastro (sign-up) e login (sign-in) de usuários
- Recuperação e alteração de senha
- Validação de e-mail e número de telefone
- Suporte a **MFA (Multi-Factor Authentication)**
- Integração com provedores externos (Google, Facebook, etc.)
- Geração de **tokens de acesso temporários** (JWT)
- Interface de login hospedada (**Hosted UI**) pronta para uso

---

## 3. User Pools (Grupos de Usuários)

O conceito central do Cognito são os **User Pools** — grupos de usuários com acesso a determinados recursos da aplicação.

### O que um User Pool gerencia

- **Atributos de cadastro:** e-mail, username, telefone, e atributos customizados
- **Políticas de senha:** tamanho mínimo, caracteres especiais, letras maiúsculas/minúsculas
- **MFA:** suporte ao Google Authenticator e outros apps TOTP
- **Claims:** atributos incluídos no token JWT que identificam e descrevem o usuário
- **Fluxo de autenticação:** cadastro, login, troca de senha, validação

### Criando um User Pool (exemplo básico)

1. Acessar o console AWS → **Cognito** → **Create user pool**
2. Definir o **nome** do pool
3. Configurar os **atributos de login** (e-mail, username ou telefone)
4. Definir **políticas de senha**
5. Habilitar **MFA** se necessário
6. Configurar **atributos requeridos** para cadastro
7. Configurar integração com **aplicações clientes**
8. Opcionalmente configurar um **domínio** e a **Hosted UI**

---

## 4. Autenticação e Tokens

Após um login bem-sucedido, o Cognito retorna tokens no padrão **JWT (JSON Web Token)**:

| Token | Uso |
|---|---|
| **ID Token** | Contém os **claims** (atributos do usuário como e-mail, nome, grupos) |
| **Access Token** | Autoriza o acesso a recursos protegidos |
| **Refresh Token** | Permite renovar os tokens sem novo login |

> 📌 Esses tokens são temporários e expiram após um período configurável. O **Refresh Token** é usado para renovar o acesso sem solicitar nova autenticação ao usuário.

---

## 5. Integração com IAM

O Cognito atua em **parceria com o IAM**:

- Usuários autenticados pelo Cognito podem **assumir roles IAM** criadas especificamente para eles
- As roles definem quais operações esses usuários podem executar nos serviços AWS (ex: ler do S3, escrever no DynamoDB)
- Essa integração permite controle de acesso **granular** baseado no perfil do usuário autenticado

```
Usuário → Cognito (autenticação) → Token JWT → Role IAM → Acesso ao serviço AWS
```

> 📌 Cognito e IAM podem ser usados **isoladamente ou em conjunto** — a escolha depende da arquitetura e das regras de negócio da aplicação.

---

## 6. Hosted UI — Interface de Login Pronta

O Cognito oferece uma **Hosted UI**: uma interface de login e cadastro pronta, hospedada pela AWS, que pode ser:

- Utilizada diretamente com personalização básica (logo, cores)
- Substituída por uma interface própria desenvolvida pelo time
- Integrada com provedores de identidade externos (Google, Facebook, Apple)

---

## 7. Configurações Avançadas Disponíveis

| Configuração | Descrição |
|---|---|
| **Atributos customizados** | Campos extras além dos padrão (ex: empresa, cargo) |
| **Triggers Lambda** | Executar funções Lambda em eventos do Cognito (ex: pós-confirmação) |
| **Domínio customizado** | Usar domínio próprio na Hosted UI |
| **Grupos dentro do User Pool** | Segmentar usuários com diferentes níveis de acesso |
| **Provedores federados** | Login social (Google, Facebook) ou corporativo (SAML, OIDC) |

---

## 8. Quando usar o Cognito?

| Cenário | Cognito indicado? |
|---|---|
| Aplicação com cadastro e login de usuários finais | ✅ Sim |
| API protegida que requer autenticação | ✅ Sim |
| Acesso de serviços AWS entre si | ❌ Usar IAM Roles |
| Acesso de desenvolvedores ao console AWS | ❌ Usar IAM Users |

---

*Aula — AWS Cognito (Introdução) | Curso AWS*
