---
title: "Benefícios do Cloud Computing (5 oficiais AWS)"
type: concept
tags: [cloud, benefícios, clf-c02, capex, opex]
created: 2026-05-19
updated: 2026-05-19
sources: 1
---

# Benefícios do Cloud Computing — os 5 oficiais (AWS)

Lista canônica que a AWS publica e que cai recorrentemente no exame **CLF-C02**, geralmente em forma de cenário ("identifique o benefício aplicável").

---

## Tabela-resumo

| # | Benefício | Conceito | Palavras-gatilho |
|---|---|---|---|
| 1 | **Troque CapEx por OpEx** | Despesa variável em vez de investimento inicial | "custo inicial", "investimento", "hardware" |
| 2 | **Pare de adivinhar capacidade** | [[concepts/elasticity\|Elasticidade]] | "pico", "Black Friday", "auto scaling" |
| 3 | **Economias de escala** | Preço por unidade cai com escala agregada | "redução de custo", "escala" |
| 4 | **Velocidade e agilidade** | Infra em minutos | "MVP", "lançar rápido", "agilidade" |
| 5 | **Alcance global em minutos** | Regiões AWS pelo mundo | "latência", "usuários globais", "expansão" |

## 1. CapEx → OpEx

- **CapEx** (Capital Expenditure): investimento em ativos (servidores, refrigeração) antes do uso.
- **OpEx** (Operational Expenditure): despesa proporcional ao consumo.
- Risco eliminado: **superdimensionar** (paga por idle) ou **subdimensionar** (precisa trocar).
- Cenário: startup começa pagando R$ 50/mês de infra; cresce e pagamento acompanha receita.

## 2. [[concepts/elasticity|Elasticidade]]

- Recursos sobem/descem automaticamente conforme métricas (CPU, memória, requisições).
- Você paga só pelo tempo em que estiveram ativos.
- Resolve o dilema "comprar para o pico vs aguentar a Black Friday".

## 3. Economias de escala

- AWS atende milhões de clientes → custo unitário cai → preços baixam continuamente.
- Algo impossível de replicar com infra própria — você não tem demanda agregada suficiente.

## 4. Velocidade e agilidade

- On-prem: provisionar leva semanas/meses (cotação, compra, instalação).
- Cloud: minutos/segundos (cliques no console, IaC).
- Habilita ciclos ágeis, MVPs, experimentação barata.

## 5. Alcance global

- AWS tem **regiões** em vários continentes.
- Hospedar próximo ao usuário reduz latência.
- Expandir para Europa/EUA/Ásia em minutos, sem montar data center físico.

## Para a prova

A prova testa o mapeamento **cenário → benefício**. Treine identificar a palavra-gatilho na descrição:

| Cenário | Benefício |
|---|---|
| "Empresa não quer investir em hardware" | 1 (CapEx → OpEx) |
| "Site precisa aguentar Black Friday" | 2 (Elasticidade) |
| "Empresa quer crescer pagando menos com volume" | 3 (Economias de escala) |
| "Startup precisa testar uma ideia em dias" | 4 (Agilidade) |
| "Empresa quer atender clientes no Japão sem latência" | 5 (Alcance global) |

## Fontes

- [[sources/clf-c02-aula02-cloud-benefits]]

## Relações

- [[concepts/cloud-computing]]
- [[concepts/elasticity]]
- [[concepts/on-premises]]
- [[entities/aws]]
- [[topics/cloud-fundamentals]]
