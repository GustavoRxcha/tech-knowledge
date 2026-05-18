---
title: "Curso AWS 01 — Configuração de MFA e Criação de Usuário IAM"
type: source
tags: [aws, iam, mfa, segurança, curso]
created: 2026-05-18
updated: 2026-05-18
sources: 1
---

# Curso AWS 01 — Configuração de MFA e Criação de Usuário IAM

Arquivo fonte: `raw/aula-01-mfa-e-iam-aws.md` (PT-BR)

Primeira aula de um curso AWS. Cobre o setup inicial de segurança em uma conta nova: ativar MFA no usuário root e criar os primeiros usuários [[aws-iam|IAM]] com permissões adequadas.

---

## Pontos-chave

- O **usuário root** tem acesso irrestrito; o [[mfa]] deve ser ativado nele imediatamente após a criação da conta.
- A AWS exibe um aviso explícito recomendando **desativar a access key do root** — opere o dia a dia com usuários [[aws-iam|IAM]].
- Usuários [[aws-iam|IAM]] podem receber **acesso programático** ([[access-keys]]), **acesso ao console** (login + senha), ou ambos.
- Permissões podem ser atribuídas de três formas: via **grupos**, **copiadas de outro usuário**, ou **políticas anexadas diretamente**.
- [[iam-policy|Policies]] são documentos JSON com `Effect`, `Action`, `Resource` — gerenciadas pela AWS ou pelo cliente.
- `AdministratorAccess` é a managed policy mais ampla — acesso total a todos os serviços.

## Procedimentos abordados

### Ativando MFA no usuário root
1. Abrir as configurações de segurança do usuário root no console AWS.
2. Escolher um dispositivo virtual de MFA (app autenticador, ex.: [[google-authenticator]]).
3. Escanear o QR Code e inserir dois códigos TOTP sequenciais para confirmar o pareamento.
4. Logins subsequentes passam a exigir o código do autenticador.

### Criando um usuário IAM
1. Navegar até **IAM → Users → Create user**.
2. Definir o username (exemplo da aula: `curso`).
3. Selecionar o tipo de acesso — programático, console ou ambos.
4. Definir senha (autogerada ou manual; opcionalmente forçar troca no primeiro login).
5. Anexar permissões: grupo / clonagem / policy direta.

## Boas práticas declaradas

- Ativar MFA no usuário root imediatamente.
- Não usar o root para operações do dia a dia.
- Desativar a access key do root.
- Aplicar o [[principle-of-least-privilege|princípio do menor privilégio]] aos usuários IAM.
- Organizar usuários em grupos com policies bem definidas.

---

## Entidades e conceitos tocados

- Entidades: [[aws]], [[aws-iam]], [[google-authenticator]]
- Conceitos: [[mfa]], [[iam-policy]], [[access-keys]], [[principle-of-least-privilege]]
- Tópicos: [[aws-security]]
