# IAM na AWS: Criação de Grupos de Usuários e Gerenciamento de Permissões

## Visão Geral

Esta é a penúltima aula do módulo de IAM. O foco é a criação de **grupos de usuários** no IAM, a atribuição de permissões por grupo, e a validação prática das restrições de acesso entre diferentes serviços da AWS.

---

## 1. O que são Grupos de Usuários IAM?

**Grupos** são coleções de usuários IAM que **compartilham o mesmo conjunto de permissões**. Em vez de atribuir políticas individualmente a cada usuário, você define as permissões no grupo e todos os membros herdam essas políticas.

### Caso de uso clássico

Em uma empresa, diferentes setores têm perfis de acesso distintos:

| Grupo | Acesso típico |
|---|---|
| **Developers** | Lambda, S3, DynamoDB |
| **Admins** | Acesso total (AdministratorAccess) |
| **RH / Financeiro** | Apenas serviços internos relevantes |

### Vantagens

- Facilita o **gerenciamento em escala** — alterar a permissão do grupo afeta todos os membros
- Permissões **dinâmicas** — o administrador pode ajustar o grupo conforme necessário
- Segue o **princípio do menor privilégio** — cada grupo acessa apenas o que precisa

---

## 2. Passo a Passo: Criando Grupos no Console IAM

### Fluxo geral

1. Acessar o console AWS → serviço **IAM**
2. Navegar até **User Groups**
3. Criar o grupo
4. Atribuir **políticas de permissão** ao grupo
5. Adicionar **usuários** ao grupo
6. Testar as permissões

---

## 3. Criando o Grupo "Developers"

### Configuração

- **Nome do grupo:** `developers`
- **Usuários adicionados:** usuário developer criado anteriormente
- **Políticas atribuídas:**
  - `AWSLambdaFullAccess` — acesso total ao serviço Lambda (funções serverless)
  - Outras políticas relacionadas ao perfil de desenvolvimento

> 📌 **Lambda** é o serviço de computação **serverless** da AWS — permite executar funções sem necessidade de provisionar ou gerenciar servidores. Será estudado em módulo dedicado no curso.

> 📌 **DynamoDB** é o banco de dados **NoSQL** (não relacional) gerenciado da AWS. Também será abordado em módulo posterior.

---

## 4. Criando o Grupo "Admins"

### Configuração

- **Nome do grupo:** `admins`
- **Usuários adicionados:** usuário administrador
- **Políticas atribuídas:**
  - `AdministratorAccess` — acesso total a todos os serviços da AWS

### Removendo permissão direta do usuário admin

Com o usuário agora pertencendo ao grupo `admins`, a permissão `AdministratorAccess` que havia sido atribuída **diretamente** ao usuário (inline) na aula anterior foi **removida**.

> ✅ Boas práticas: permissões devem vir do **grupo**, não diretamente do usuário. Isso facilita o gerenciamento e evita inconsistências.

### Resultado

O usuário administrador passa a receber suas permissões **exclusivamente pelo grupo**, e não mais por atribuição direta.

---

## 5. Criando um Novo Usuário Developer

Para o teste de permissões, foi criado um segundo usuário com perfil developer:

- **Tipo de acesso:** console web + acesso programático (CLI)
- **Grupo:** `developers`
- Sem necessidade de criar nova senha manualmente — gerada automaticamente
- Adicionado diretamente ao grupo `developers` durante a criação

---

## 6. Testando as Permissões na Prática

Login realizado com o **novo usuário developer** para validar o comportamento das permissões.

### ✅ Acesso permitido: Lambda

- O usuário tem `AWSLambdaFullAccess`
- Consegue visualizar, criar e gerenciar funções Lambda normalmente

### ❌ Acesso negado: EC2

- O usuário **não tem** permissão para o serviço EC2
- Ao tentar acessar, recebe o erro:

```
You are not authorized to perform this operation.
```

- Nem a interface do serviço é carregada completamente
- Qualquer tentativa de executar operações retorna erro de permissão negada

### ❌ Acesso negado: IAM

- O usuário não pode criar outros usuários
- Não pode atribuir ou modificar políticas de acesso
- Tentativas retornam o mesmo erro de autorização

> 📌 Esse comportamento demonstra na prática o **princípio do menor privilégio**: o usuário acessa **somente** os serviços para os quais tem permissão explícita.

---

## 7. Managed Policies x Inline Policies — Revisão

Nesta aula foram usadas **managed policies da AWS** (as pré-criadas com ícone laranja no console):

- São políticas prontas, mantidas pela AWS
- Cobrem os casos de uso mais comuns
- Não é necessário (nem recomendado) criar políticas do zero para cenários padrão

> ⚠️ Existem centenas de managed policies disponíveis. Não é esperado conhecer todas — o importante é saber pesquisar e entender o que cada uma cobre.

---

## 8. Próximos Passos

Na próxima aula, o módulo de IAM será concluído com:

- Criação de **Roles (Funções IAM)** — permissões assumidas temporariamente por serviços ou usuários
- Criação de **políticas personalizadas** para recursos específicos da AWS
- Integração de tudo que foi aprendido: usuários, grupos, políticas e roles funcionando em conjunto

---

## Resumo das Boas Práticas Reforçadas

- ✅ Usar **grupos** para gerenciar permissões em escala
- ✅ **Remover permissões diretas** (inline) após mover o usuário para um grupo
- ✅ Preferir **managed policies** para casos de uso padrão
- ✅ Testar permissões após cada configuração para validar o comportamento esperado
- ✅ Aplicar sempre o **princípio do menor privilégio**

---

*Aula 04 — Curso AWS | Próxima aula: IAM Roles e Políticas Personalizadas*
