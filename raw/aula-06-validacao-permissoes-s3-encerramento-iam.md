# IAM na AWS: Validação de Permissões no S3 e Encerramento do Módulo

## Visão Geral

Esta é a aula de encerramento do módulo de IAM. O conteúdo é prático: atualização de políticas de acesso existentes, adição de novas permissões ao S3 e validação completa do comportamento de cada permissão configurada com um usuário developer logado no console.

---

## 1. Atualizando a Policy de Acesso ao S3

Com o usuário **admin** logado no console:

1. Acessar **IAM** → **Policies**
2. Localizar a policy personalizada criada anteriormente (`policy-s3-developers`)
3. Clicar em **Edit policy**
4. Adicionar a ação **`s3:ListAllMyBuckets`** — permite listar todos os buckets da conta
5. Confirmar o **ARN** do resource (pode ser `arn:aws:s3:::*` para todos os buckets)
6. Salvar as alterações

> 📌 O documento **JSON** da policy é atualizado automaticamente ao editar pela interface visual, refletindo todas as permissões configuradas.

---

## 2. Validação Prática com o Usuário Developer

Login realizado com o usuário **developer (G1)** para testar cada permissão configurada na policy.

### Testes realizados no S3

| Ação | Permissão | Resultado |
|---|---|---|
| **Listar buckets** da conta | `s3:ListAllMyBuckets` | ✅ Buckets exibidos no console |
| **Acessar um bucket** específico | `s3:ListBucket` | ✅ Conteúdo do bucket listado |
| **Upload de arquivo** (ex: imagem) | `s3:PutObject` | ✅ Upload realizado com sucesso |
| **Download de objeto** | `s3:GetObject` | ✅ Objeto baixado com sucesso |
| **Versionamento** de objetos | `s3:PutObjectVersioning` | ❌ Sem permissão configurada |
| **Deletar objeto** | `s3:DeleteObject` | ✅ Deleção realizada (permissão presente) |

> ✅ As permissões configuradas funcionaram exatamente como esperado — o usuário consegue realizar apenas as operações explicitamente permitidas na policy.

---

## 3. Observação: Block Public Access

Durante os testes foi identificado que o bucket não tinha o **Block Public Access** habilitado, o que significa que ele ficaria **exposto publicamente** na internet.

> ⚠️ **Boas práticas de segurança no S3:**
> - Sempre habilitar o **Block Public Access** em buckets que não precisam ser acessíveis publicamente
> - Configurações de acesso público devem ser deliberadas e documentadas
> - O controle de acesso deve ser feito pelas **bucket policies** e **ACLs**, nunca deixando o bucket aberto sem necessidade

---

## 4. Encerramento do Módulo IAM

### O que foi aprendido neste módulo

| Aula | Conteúdo |
|---|---|
| **01** | Console AWS, MFA no root, criação de usuário IAM |
| **02** | Policies, Tags, tipos de acesso e download do CSV de credenciais |
| **03** | Login com novo usuário, inline policies, ARN e permissões no S3 |
| **04** | Grupos de usuários, managed policies, testes de acesso com EC2 e Lambda |
| **05** | Roles (funções IAM), policies personalizadas, Lambda acessando S3 |
| **06** | Atualização de policies, validação prática de permissões no S3 |

---

## 5. Por que o IAM é Fundamental?

O IAM é o serviço **mais elementar** da AWS porque:

- Todo serviço AWS depende de **identidades e permissões** para funcionar
- Sem IAM configurado corretamente, nenhum outro serviço pode ser usado com segurança
- Nos próximos módulos do curso, o IAM será revisitado constantemente — cada novo serviço exigirá configuração de políticas e roles

> 📌 Sempre que um novo serviço AWS for estudado, haverá uma etapa de configuração de permissões via IAM. O domínio desse serviço é o alicerce para trabalhar com toda a plataforma AWS.

---

## 6. Próximos Passos

Nos próximos módulos do curso serão abordados outros serviços AWS, e o IAM continuará presente como camada de segurança e acesso em todos eles. Para fixar o conteúdo deste módulo, é recomendado:

- ✅ Criar novos usuários e grupos com diferentes combinações de permissões
- ✅ Testar roles com outros serviços AWS (além do Lambda e S3)
- ✅ Explorar as managed policies disponíveis no console IAM
- ✅ Praticar a leitura e edição de documentos JSON de policies
- ✅ Habilitar o **Block Public Access** em todos os buckets S3 de teste

---

## Resumo Geral de Boas Práticas IAM

- 🔐 Ativar **MFA** no usuário root imediatamente
- 🚫 **Nunca usar** o usuário root para operações do dia a dia
- 👥 Organizar usuários em **grupos** com políticas bem definidas
- 🔑 Aplicar sempre o **princípio do menor privilégio**
- 🤖 Usar **roles** para comunicação entre serviços (nunca hardcodar credenciais)
- 🏷️ Usar **tags** para organizar e classificar recursos
- 💾 Fazer o **download do CSV** de credenciais imediatamente após criar usuários
- 🔒 Manter buckets S3 com **Block Public Access** ativado por padrão

---

*Aula 06 — Encerramento do Módulo IAM | Curso AWS*
