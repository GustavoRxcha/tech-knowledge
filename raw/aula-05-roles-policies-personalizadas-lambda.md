# IAM na AWS: Roles, Policies Personalizadas e Integração com Lambda

## Visão Geral

Esta é a última aula do módulo de IAM. O conteúdo aborda a criação de **roles (funções IAM)** e **policies personalizadas**, sua atribuição a grupos de usuários, e um exemplo prático de como serviços AWS (como o Lambda) utilizam roles para acessar outros serviços (como o S3).

---

## 1. Recapitulação do Módulo IAM

Até aqui foram abordados:

| Conceito | O que é |
|---|---|
| **Policy** | Objeto JSON que define permissões — o que pode ou não ser feito em quais recursos |
| **Managed Policy** | Política pré-criada e mantida pela AWS (ícone laranja no console) |
| **Inline Policy** | Política criada manualmente e vinculada diretamente a um usuário |
| **Grupo de usuários** | Conjunto de usuários que herdam as mesmas políticas |
| **Role (Função IAM)** | Identidade com um conjunto de políticas, assumida temporariamente por usuários ou serviços |

---

## 2. O que é uma Role (Função IAM)?

Uma **role** é uma identidade IAM que:

- Contém um **conjunto de políticas** de permissão
- **Não pertence** a um usuário específico — pode ser assumida por usuários, serviços ou contas externas
- É usada principalmente para conceder permissões **temporárias** ou para permitir que **serviços AWS acessem outros serviços**

### Casos de uso principais

| Tipo | Descrição |
|---|---|
| **Serviço AWS → Serviço AWS** | Ex: Lambda acessando o S3 ou DynamoDB |
| **Usuário de outra conta** | Acesso cross-account (entre contas AWS diferentes) |
| **Identidade federada** | Login via provedor externo (Google, Active Directory, etc.) |
| **SAM / CloudFormation** | Roles assumidas por ferramentas de infraestrutura como código |

> 📌 Nesta aula o foco é o tipo mais comum para iniciantes: **roles assumidas por serviços AWS** (AWS Service Role).

---

## 3. Criando uma Policy Personalizada para o S3

Antes de criar a role, é necessário criar a **policy** que ela irá conter.

### Passo a passo

1. Acessar o console AWS → **IAM** → **Policies** → **Create policy**
2. Selecionar o serviço: **S3**
3. Definir as **ações permitidas**, por exemplo:
   - `ListBucket` — listar os buckets da conta
   - `GetObject` — ler/baixar objetos de um bucket
   - `PutObject` — fazer upload de objetos
   - `DeleteObject` — excluir objetos
4. Definir o **Resource (ARN)**:
   - Para aplicar a **todos os buckets** da conta:
     ```
     arn:aws:s3:::*
     ```
   - Para aplicar a um bucket específico e todos os seus objetos:
     ```
     arn:aws:s3:::nome-do-bucket
     arn:aws:s3:::nome-do-bucket/*
     ```
5. Adicionar **tags** (opcional, para organização)
6. Dar um nome à policy (ex: `policy-s3-developers`)
7. Clicar em **Create policy**

### Estrutura JSON gerada

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "s3:ListBucket",
        "s3:GetObject",
        "s3:PutObject",
        "s3:DeleteObject"
      ],
      "Resource": [
        "arn:aws:s3:::*",
        "arn:aws:s3:::*/*"
      ]
    }
  ]
}
```

> 📌 O bloco `Statement` é o elemento central de uma policy — ele contém as regras de permissão (`Effect`, `Action`, `Resource`).

---

## 4. Atribuindo a Policy ao Grupo de Desenvolvedores

Após criar a policy personalizada:

1. Acessar **IAM** → **User Groups** → grupo `developers`
2. Na aba **Permissions** → **Add permissions**
3. Localizar a policy recém-criada (`policy-s3-developers`)
4. Confirmar a adição

> ✅ Agora todos os usuários do grupo `developers` herdam a permissão de acesso ao S3 definida na policy.

### Testando o acesso

- Login com o usuário developer
- Antes de atribuir a policy: erro `"You do not have permission to list buckets"`
- Após atribuir a policy: buckets listados com sucesso no console S3

---

## 5. Roles na Prática: Lambda Acessando o S3

### Contexto

O **AWS Lambda** é um serviço **serverless** — permite executar código (funções) sem provisionar servidores. Quando uma função Lambda precisa interagir com outros serviços (como o S3), ela precisa de uma **role de execução** (execution role) com as permissões adequadas.

### Criando uma Role para o Lambda

1. Acessar **IAM** → **Roles** → **Create role**
2. Selecionar o tipo de entidade: **AWS Service**
3. Selecionar o serviço: **Lambda**
4. Anexar a policy desejada (ex: `policy-s3-developers` ou uma managed policy do S3)
5. Dar um nome à role (ex: `role-lambda-s3`)
6. Clicar em **Create role**

### Atribuindo a Role à Função Lambda

Ao criar ou editar uma função Lambda:

1. Na seção **Execution role**, selecionar **Use an existing role**
2. Selecionar a role criada (`role-lambda-s3`)
3. A partir desse momento, a função Lambda pode acessar o S3 com as permissões definidas na role

---

## 6. Teste Prático: Lambda Listando Buckets S3

### Cenário

Uma função Lambda com um script JavaScript que lista todos os buckets da conta AWS.

```javascript
const { S3Client, ListBucketsCommand } = require("@aws-sdk/client-s3");

exports.handler = async () => {
  const client = new S3Client({});
  const response = await client.send(new ListBucketsCommand({}));
  return response.Buckets;
};
```

### Fluxo de teste

| Etapa | Resultado |
|---|---|
| Função sem role ou com role sem permissão S3 | ❌ Erro: acesso negado ao listar buckets |
| Adicionar policy S3 à role da função | ✅ Função executa e retorna a lista de buckets |

> ✅ Após atribuir a role com a policy correta, a função Lambda conseguiu listar os buckets com sucesso — demonstrando na prática como roles conectam serviços AWS entre si.

---

## 7. Diferença entre Policy Direta e Role

| | Policy direta (usuário/grupo) | Role (serviço) |
|---|---|---|
| **Quem usa** | Usuários e grupos IAM | Serviços AWS, contas externas |
| **Vínculo** | Permanente ao usuário/grupo | Assumida temporariamente |
| **Caso de uso** | Pessoas acessando o console/API | Serviços comunicando entre si |

---

## 8. Boas Práticas com Roles

- ✅ Sempre usar roles para **comunicação entre serviços AWS** (nunca hardcodar credenciais no código)
- ✅ Aplicar o **princípio do menor privilégio** nas policies da role
- ✅ Nomear roles de forma descritiva (ex: `role-lambda-s3-readonly`)
- ✅ Revisar as permissões das roles periodicamente

---

## Resumo do Módulo IAM

| Conceito | Finalidade |
|---|---|
| **Usuário IAM** | Identidade para pessoas acessarem a AWS |
| **Grupo** | Agrupa usuários com o mesmo perfil de acesso |
| **Managed Policy** | Política pronta fornecida pela AWS |
| **Inline Policy** | Política customizada vinculada diretamente a uma identidade |
| **Policy personalizada** | Política criada pelo cliente para casos específicos |
| **Role** | Identidade assumida por serviços ou usuários temporariamente |
| **ARN** | Identificador único de cada recurso AWS |
| **MFA** | Camada extra de segurança no login |

---

*Aula 05 (Final do Módulo IAM) — Curso AWS | Próximo módulo: Amazon S3 — Armazenamento de Objetos*
