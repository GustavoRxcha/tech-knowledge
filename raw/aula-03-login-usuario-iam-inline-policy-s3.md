# IAM na AWS: Login com Novo Usuário e Criação de Inline Policies

## Visão Geral

Esta aula demonstra o acesso ao console AWS com as credenciais do novo usuário IAM criado anteriormente, e aprofunda a criação de **inline policies** — políticas de permissão criadas manualmente e atribuídas diretamente a um usuário, usando o serviço **S3** como exemplo prático.

---

## 1. Acessando o Console com o Novo Usuário

### Passo a passo

1. Fazer **logout** do usuário root
2. Abrir o arquivo **CSV** de credenciais gerado na criação do usuário
3. O CSV contém os campos:
   - **Console login link** — URL de acesso específica da conta AWS
   - **Username** — nome do usuário IAM
   - **Password** — senha inicial gerada
4. Acessar o link de login — ele já preenche automaticamente o **número da conta AWS**
5. Inserir o **username** e a **password** do CSV
6. No primeiro acesso, a AWS solicita a **redefinição de senha**
7. Após redefinir, o login é concluído com o novo usuário

> ✅ A partir desse momento, você está operando com um usuário IAM com credenciais independentes do root.

---

## 2. Introdução ao Amazon S3

Antes de criar a política de exemplo, a aula apresenta brevemente o **S3 (Simple Storage Service)**:

- É o serviço de **armazenamento de arquivos** da AWS
- Funciona de forma similar ao **Dropbox** — você armazena arquivos e os acessa remotamente
- Os arquivos são organizados dentro de **buckets** (equivalente a diretórios/pastas)
- Cada arquivo armazenado tem uma URL de acesso única

> 📌 O S3 será estudado em profundidade em um módulo dedicado do curso. Nesta aula, é usado apenas como recurso de exemplo para demonstrar a atribuição de permissões.

---

## 3. Inline Policy — Permissão Direta e Customizada

### O que é uma Inline Policy?

Uma **inline policy** é uma política de permissão criada manualmente pelo administrador e **vinculada diretamente** a um usuário específico (não reutilizável como as managed policies).

### Diferença entre tipos de políticas

| Tipo | Criação | Reutilizável | Gerenciada por |
|---|---|---|---|
| **Managed Policy** | AWS ou cliente | ✅ Sim | AWS ou conta |
| **Inline Policy** | Administrador | ❌ Não | Conta (exclusiva do usuário) |

---

## 4. Criando uma Inline Policy para o S3

### Cenário do exemplo

Criar uma política que permite ao usuário:
1. **Inserir objetos** (`PutObject`) em um bucket S3 específico
2. **Buscar/ler objetos** (`GetObject`) desse mesmo bucket

### Passo a passo no console

1. Acessar o serviço **IAM** → **Users** → selecionar o usuário desejado
2. Na aba **Permissions**, clicar em **Add permissions** → **Create inline policy**
3. Selecionar o serviço: **S3**
4. Escolher as **ações permitidas**, por exemplo:
   - `PutObject` — permite inserir/fazer upload de objetos no bucket
   - `GetObject` — permite ler/baixar objetos do bucket
5. Definir o **Resource (ARN)**

---

## 5. ARN — Amazon Resource Name

### O que é?

O **ARN (Amazon Resource Name)** é o identificador único de cada recurso dentro da AWS. Todo recurso possui um ARN.

### Formato geral

```
arn:aws:<serviço>:<região>:<conta>:<tipo-recurso>/<nome-recurso>
```

### Exemplo para um bucket S3

```
arn:aws:s3:::nome-do-bucket
```

Para especificar **todos os objetos dentro do bucket**:

```
arn:aws:s3:::nome-do-bucket/*
```

> 📌 O `/*` no final indica que a permissão se aplica a **todos os objetos** dentro daquele bucket.

### Como obter o ARN

No console AWS, ao selecionar um recurso (ex: um bucket S3), o ARN é exibido nos detalhes do recurso.

---

## 6. Revisando e Salvando a Inline Policy

Após configurar as ações e o ARN:

1. Clicar em **Review policy**
2. Dar um **nome** à política (ex: `policy-s3-curso`)
3. Clicar em **Create policy**

### Resultado

O usuário passa a ter as seguintes permissões no bucket S3 especificado:
- ✅ `PutObject` — pode **inserir** objetos
- ✅ `GetObject` — pode **ler/baixar** objetos

---

## 7. Editando uma Inline Policy Existente

Após criar a política, é possível **editá-la** para adicionar ou remover permissões:

1. Acessar o usuário no IAM
2. Localizar a inline policy
3. Clicar em **Edit policy**
4. Adicionar novas ações ou recursos conforme necessário
5. Salvar as alterações

---

## 8. Contexto de Permissões para Gerenciar o IAM

> ⚠️ **Importante:** Para criar, editar ou remover permissões de outros usuários no IAM, é necessário estar logado com um usuário que possua **permissões de administrador** (ou permissão específica sobre o IAM).

Neste exemplo, as configurações foram feitas enquanto logado com o **usuário administrador**, que tem poder de gerenciar permissões de todos os outros usuários.

---

## Resumo das Etapas Concluídas

| Etapa | Status |
|---|---|
| Ativação de MFA no root | ✅ Concluído (Aula 01) |
| Criação de usuário IAM | ✅ Concluído (Aula 01) |
| Login com novo usuário | ✅ Concluído (Aula 03) |
| Criação de inline policy (S3) | ✅ Concluído (Aula 03) |
| Criação de grupos de usuários | 🔜 Próxima aula |

---

*Aula 03 — Curso AWS | Continuação na próxima aula: Grupos de Usuários IAM e Atribuição de Permissões por Grupo*
