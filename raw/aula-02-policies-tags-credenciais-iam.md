# IAM na AWS: Políticas, Tags e Credenciais de Usuário

## Visão Geral

Esta aula aprofunda o entendimento sobre **políticas IAM (Policies)**, introduz o conceito de **tags** para organização de recursos e demonstra o processo final de criação de um usuário, incluindo o gerenciamento das credenciais geradas.

---

## 1. Estrutura de uma Política IAM (Policy)

Uma política IAM é definida em formato **JSON** e determina o que um usuário ou grupo pode ou não fazer dentro da AWS.

### Exemplo: AdministratorAccess

A política `AdministratorAccess` é uma das mais amplas disponíveis:

- Concede permissão para **todas as ações** em **todos os recursos**
- Abrange aproximadamente **300 serviços** da AWS
- Exemplo de permissão inclusa: `s3:GetObject` (leitura de objetos no S3) — e equivalentes para todos os demais serviços

> ⚠️ **Atenção:** O acesso administrador é extremamente poderoso. É **fortemente recomendado** que esse tipo de política seja atribuído **somente** a usuários que realmente exercem a função de administrador da conta. Use com muito cuidado.

### Formato JSON da Policy

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": "*",
      "Resource": "*"
    }
  ]
}
```

> 📌 O `"Action": "*"` e `"Resource": "*"` indicam permissão total — característica da `AdministratorAccess`.

---

## 2. Tags (Etiquetas de Recursos)

### O que são?

**Tags** são pares de chave-valor utilizados para **classificar e organizar** recursos dentro da AWS.

### Analogia

Funcionam como **etiquetas de bagagem**: você as usa para identificar e separar seus recursos por qualquer critério que faça sentido para o seu contexto.

### Casos de uso comuns

| Critério | Exemplo de Tag |
|---|---|
| Ambiente | `Env: Production` / `Env: Development` |
| Departamento | `Team: Backend` / `Team: Data` |
| Centro de custo | `CostCenter: 1042` |
| Projeto | `Project: Curso-AWS` |

### Por que usar?

- Facilita a **visualização e organização** de recursos no console
- Permite **filtrar cobranças** por tag no AWS Cost Explorer
- Essencial para **governança** em contas com muitos recursos

> 📌 Nesta aula, as tags são introduzidas conceitualmente. A configuração prática será explorada em conjunto com outros recursos ao longo do curso.

---

## 3. Finalização da Criação do Usuário IAM

### Revisão do processo

Ao concluir a criação de um usuário IAM, o console apresenta um **resumo** com:

- **Link de acesso ao console** — URL específica da conta para login
- **Nome de usuário**
- **Senha** (gerada automaticamente ou definida manualmente)
- **Access Key ID** — identificador da chave de acesso programático
- **Secret Access Key** — chave secreta para uso via CLI/API/SDK

### Tipos de credenciais e seus usos

| Credencial | Uso |
|---|---|
| **Login + Senha** | Acesso ao console web da AWS |
| **Access Key ID + Secret Access Key** | Acesso via terminal (CLI), SDKs e APIs |

---

## 4. Download do Arquivo CSV de Credenciais

> ⚠️ **Passo crítico — não pule esta etapa!**

Ao criar um usuário com acesso programático, a AWS exibe as credenciais **uma única vez**. Após fechar a tela, a **Secret Access Key não pode ser recuperada**.

### O que fazer

1. Clicar em **"Download .csv"** antes de fechar a tela de criação
2. O arquivo `.csv` pode ser aberto no Excel ou qualquer editor de texto
3. Armazene o arquivo em local seguro

### Caso perca as credenciais

- Não é possível recuperar a Secret Access Key
- A solução é **deletar a chave existente** e **gerar um novo par** de credenciais para o usuário

---

## Boas Práticas Resumidas

- ✅ Atribuir a política `AdministratorAccess` **somente** a quem realmente é administrador
- ✅ Preferir políticas com **menor privilégio possível** para cada usuário
- ✅ Usar **tags** desde o início para manter os recursos organizados
- ✅ **Baixar o CSV** de credenciais imediatamente após criar o usuário
- ✅ Guardar as credenciais em local seguro (ex: gerenciador de senhas)

---

*Aula 02 — Curso AWS | Continuação na próxima aula*
