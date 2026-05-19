---
title: "Postman"
type: entity
tags: [api, testing, http, ferramentas]
created: 2026-05-19
updated: 2026-05-19
sources: 1
---

# Postman

Ferramenta GUI para testar e interagir com APIs HTTP. Permite enviar requisições com qualquer método (GET/POST/PUT/DELETE/PATCH/etc.), configurar headers, body, autenticação, e salvar coleções de requisições.

---

## Uso no curso

Validar manualmente todas as rotas CRUD da [[entities/amazon-api-gateway|API Gateway]] do projeto:

| Operação | Método | Rota | Verificação |
|---|---|---|---|
| Criar | POST | `/items` | Item aparece no console DynamoDB |
| Listar | GET | `/items` | Lista completa |
| Buscar | GET | `/items/{id}` | Objeto correto |
| Atualizar | PUT | `/items/{id}` | Mudança parcial confirmada |
| Deletar | DELETE | `/items/{id}` | Item some |

Ver [[sources/aws-course-apigateway-02-integration-postman]] para detalhes.

## Alternativas

- **Insomnia** — concorrente direto, GUI similar.
- **curl / HTTPie** — CLI, ótimo para CI e automação.
- **Bruno** — open-source, files locais (Git-friendly).
- **Thunder Client** — plugin do VS Code.

## Relações

- [[entities/amazon-api-gateway]] — alvo dos testes
