---
title: "Customer-Managed Policy"
type: concept
tags: [aws, iam, policies, permissões]
created: 2026-05-18
updated: 2026-05-18
sources: 1
---

# Customer-Managed Policy

[[concepts/iam-policy|Policy]] IAM criada e mantida pelo próprio usuário da conta AWS. Contrasta com **Managed Policy** (criada e mantida pela AWS) e com [[concepts/inline-policy|Inline Policy]] (embutida diretamente em uma identidade).

---

## Comparação dos três tipos

| | Managed Policy (AWS) | Customer-Managed Policy | Inline Policy |
|---|---|---|---|
| **Criada por** | AWS | Você | Você |
| **Reutilizável** | Sim | Sim | Não (1:1 com a identidade) |
| **Mantida por** | AWS (atualizada automaticamente) | Você | Você |
| **Visível em** | IAM → Policies (ícone laranja) | IAM → Policies | Diretamente no usuário/grupo/role |
| **Quando usar** | Casos padrão de serviços AWS | Permissões específicas do negócio | Exceções pontuais e únicas |

---

## Criando uma customer-managed policy

1. **IAM → Policies → Create policy**
2. Selecionar o serviço (ex: S3)
3. Marcar as ações permitidas
4. Definir o **Resource** via [[concepts/arn|ARN]]
5. Adicionar [[concepts/resource-tags|tags]] (opcional)
6. Nomear a policy (ex: `policy-s3-developers`)
7. **Create policy**

---

## Exemplo: policy-s3-developers

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "s3:ListAllMyBuckets",
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

> A interface visual do console gera o JSON automaticamente — edições visuais refletem no JSON em tempo real.

---

## Boas práticas

- Preferir **managed policies da AWS** para casos padrão (menos manutenção)
- Criar customer-managed policies quando as managed da AWS são muito permissivas
- Aplicar [[concepts/principle-of-least-privilege|menor privilégio]]: só as ações e resources necessários
- Nomear de forma descritiva: `policy-[serviço]-[grupo/função]`

---

## Relações

- [[concepts/iam-policy]] — estrutura JSON base de qualquer policy
- [[concepts/inline-policy]] — alternativa embutida diretamente na identidade
- [[concepts/arn]] — identifica os resources na policy
- [[concepts/principle-of-least-privilege]] — guia o escopo das actions e resources
- [[entities/aws-iam]] — serviço onde as policies são gerenciadas
