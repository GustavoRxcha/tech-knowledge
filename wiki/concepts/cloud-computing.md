---
title: "Cloud Computing"
type: concept
tags: [cloud, conceito-fundamental, clf-c02]
created: 2026-05-19
updated: 2026-05-19
sources: 2
---

# Cloud Computing

Entrega de recursos de TI **sob demanda, pela internet, com pagamento conforme o uso**. Conceito raiz dos serviços de nuvem.

---

## Definição formal (AWS)

> *"Entrega de recursos de TI sob demanda, por meio da internet, com precificação baseada em pagamento conforme o uso."*

| Termo | Significado |
|---|---|
| **Recursos de TI** | Servidores, storage, banco de dados, rede, software |
| **Sob demanda** | Disponíveis imediatamente, sem compra prévia |
| **Pela internet** | Acessíveis de qualquer lugar |
| **Pagamento pelo uso** | Paga só pelo que consome (pay-as-you-go) |

## Pay-as-you-go — o modelo de cobrança

Princípio econômico central da cloud. Substitui custo fixo de infra (CapEx) por custo proporcional ao consumo (OpEx). Ver [[concepts/cloud-benefits|cloud-benefits]] para os impactos.

## Como surgiu

1. **Cliente-servidor** — pequenos ambientes locais.
2. **[[concepts/on-premises|On-Premises]]** — data centers próprios, alto custo e complexidade.
3. **[[concepts/virtualization|Virtualização]]** — hypervisor permite múltiplas VMs num só hardware; base técnica para a cloud.
4. **Cloud** — provedores como AWS oferecem infra elástica via internet; clientes consomem sob demanda.

A massificação de internet, mobile e IoT tornou data centers locais inviáveis para escala global — e a cloud preencheu a lacuna.

## Modelos relacionados

- **Modelos de serviço** (quanto gerencio): [[concepts/iaas|IaaS]] / [[concepts/paas|PaaS]] / [[concepts/saas|SaaS]]
- **Modelos de implantação** (onde roda): [[concepts/on-premises|On-Premises]] / [[concepts/hybrid-cloud|Híbrido]] / Cloud / [[concepts/private-cloud|Privada]]

## Para a prova CLF-C02

A definição formal da AWS é cobrada literalmente. Saber recitar "sob demanda, pela internet, pagamento conforme o uso" já vale pontos.

## Fontes

- [[sources/clf-c02-aula01-cloud-computing]]
- [[sources/clf-c02-aula04-deployment-models]]

## Relações

- [[concepts/cloud-benefits]]
- [[concepts/virtualization]]
- [[entities/aws]]
- [[topics/cloud-fundamentals]]
