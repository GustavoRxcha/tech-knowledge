# Segurança na AWS: Configuração de MFA e Criação de Usuários IAM

## Visão Geral

Esta aula aborda as primeiras e mais importantes práticas de segurança ao configurar uma conta AWS: a ativação do MFA (Multi-Factor Authentication) no usuário root e a criação de usuários IAM com permissões adequadas.

---

## 1. Interface do Console AWS

Ao acessar o console da AWS, a interface apresenta informações como:

- Quantidade de políticas (policies) ativas
- Número de usuários cadastrados
- Grupos e identidades configuradas

---

## 2. MFA no Usuário Root

### Por que ativar?

O usuário **root** é a conta principal da AWS com acesso irrestrito a todos os recursos. É **fortemente recomendado** ativar o MFA nessa conta como camada extra de proteção.

### Como ativar

1. No console AWS, localizar a opção de **MFA** nas configurações de segurança do usuário root
2. Clicar na opção para ativar o MFA
3. Escolher o tipo de dispositivo virtual (recomendado: **aplicativo autenticador**)
4. Escanear o **QR Code** exibido na tela com o aplicativo

### Aplicativos compatíveis

- **Google Authenticator** (mais comum)
- Outros autenticadores TOTP compatíveis

### Processo de pareamento

1. Escanear o QR Code com o aplicativo
2. Inserir **dois códigos sequenciais** gerados pelo aplicativo para confirmar o pareamento
3. Aguardar a validação — após confirmação, o console AWS estará vinculado ao aplicativo
4. A partir desse momento, todo login solicitará o código gerado pelo autenticador

---

## 3. Chave de Acesso do Root (Access Key)

> ⚠️ **Atenção:** A AWS exibe um alerta recomendando que a **chave de acesso do usuário root não seja utilizada**. Esta é uma boa prática de segurança — a chave root deve permanecer desativada.

---

## 4. Criação de Usuários IAM

### O que é IAM?

**IAM (Identity and Access Management)** é o serviço da AWS para gerenciar identidades e permissões de acesso de forma granular e segura.

### Criando um usuário

1. Acessar o serviço **IAM** no console
2. Navegar até **Users** e clicar em criar novo usuário
3. Definir o **nome do usuário** (ex: `curso`)
4. Selecionar o **tipo de acesso**:

| Tipo de Acesso | Descrição |
|---|---|
| **Acesso programático** | Gera credenciais (Access Key + Secret) para uso via terminal/API/SDK |
| **Acesso ao console** | Permite login na interface web da AWS |
| **Ambos** | Usuário com acesso ao console e à API |

5. Configurar a senha:
   - Auto-gerada pela AWS, ou
   - Definida manualmente
   - Opção de exigir troca de senha no primeiro acesso

---

## 5. Permissões de Usuário

Existem **três formas** de atribuir permissões a um usuário IAM:

### 5.1 Grupo de Usuários
- Criar um grupo com permissões definidas
- Adicionar o usuário ao grupo
- Ideal para gerenciar múltiplos usuários com o mesmo perfil

### 5.2 Herdar permissões de outro usuário
- Copiar as permissões de um usuário existente
- Útil quando há um perfil de referência já configurado

### 5.3 Permissões diretas (Attach Policies)
- Atribuir políticas diretamente ao usuário
- Indicado para casos específicos (ex: único administrador)

---

## 6. Políticas (Policies)

As políticas definem **o que** um usuário pode ou não fazer na AWS.

### Tipos de políticas

| Tipo | Descrição |
|---|---|
| **Gerenciadas pela AWS** | Identificadas com ícone laranja/amarelo; criadas e mantidas pela própria AWS |
| **Gerenciadas pelo cliente** | Criadas e personalizadas pela sua conta |

### Estrutura de uma política

As políticas são escritas em formato **JSON** e definem:
- **Effect**: `Allow` ou `Deny`
- **Action**: quais ações são permitidas/negadas (ex: `s3:GetObject`)
- **Resource**: em quais recursos a política se aplica

> 📌 **Exemplo prático:** A política `AdministratorAccess` concede acesso total a todos os serviços e recursos da AWS.

---

## Boas Práticas Resumidas

- ✅ Ativar MFA no usuário **root** imediatamente após criar a conta
- ✅ **Não utilizar** o usuário root para operações do dia a dia
- ✅ **Desativar** a chave de acesso do root
- ✅ Criar usuários IAM com permissões mínimas necessárias (**princípio do menor privilégio**)
- ✅ Organizar usuários em **grupos** com políticas bem definidas

---

*Aula 01 — Curso AWS | Continuação na próxima aula*
