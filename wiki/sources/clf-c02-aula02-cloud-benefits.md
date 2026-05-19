---
title: "CLF-C02 Aula 02 — Benefícios do Cloud Computing"
type: source
tags: [aws, clf-c02, cloud, benefícios, certificação]
created: 2026-05-19
updated: 2026-05-19
sources: 1
---

# CLF-C02 Aula 02 — Benefícios do Cloud Computing

Arquivo fonte: `raw/clf-c02-aula02-beneficios-cloud-computing.md` (PT-BR)

Apresenta os **5 benefícios oficiais documentados pela AWS** para Cloud Computing — tema recorrente no exame **CLF-C02**, geralmente em forma de cenário ("identifique qual benefício se aplica").

---

## Os 5 benefícios oficiais

| # | Benefício | Conceito-chave | Palavras-gatilho da prova |
|---|---|---|---|
| 1 | **Troque despesas iniciais por variáveis** | CapEx → OpEx | "custo inicial", "investimento", "hardware" |
| 2 | **Pare de adivinhar capacidade** | [[concepts/elasticity\|Elasticidade]] | "pico", "Black Friday", "escalar automaticamente" |
| 3 | **Beneficie-se de economias de escala** | Preço por unidade cai com escala agregada | "redução de custo", "escala" |
| 4 | **Aumente velocidade e agilidade** | Infra em minutos, MVP rápido | "lançar rápido", "MVP", "agilidade" |
| 5 | **Alcance global em minutos** | Regiões AWS distribuídas | "latência", "usuários globais", "expansão" |

## Detalhes resumidos

### 1. CapEx → OpEx
- **CapEx** (Capital Expenditure): comprar hardware antes de usar — risco de super/subdimensionar.
- **OpEx** (Operational Expenditure): pagar conforme o uso — alinhado ao consumo real.
- Cloud transforma investimento em despesa proporcional.

### 2. [[concepts/elasticity|Elasticidade]]
- Recursos sobem e descem **automaticamente** conforme métricas (CPU, memória, requisições).
- Você paga só pelo tempo ativo.
- Resolve o dilema "comprar para o pico" do on-premises.

### 3. Economias de escala
- AWS agrega demanda de milhões de clientes → custo unitário cai → preços repassados.
- Impossível replicar com infra própria.

### 4. Velocidade e agilidade
- Em on-prem, provisionar leva semanas/meses; na cloud, minutos/segundos.
- Times focam no **produto**, não na infra.
- Habilita ciclos ágeis e MVPs.

### 5. Alcance global
- AWS tem **regiões** distribuídas pelo mundo.
- Hospedar próximo ao usuário reduz latência.
- Expansão global sem montar infra física em cada país.

> 💡 Regra: trate cada benefício como uma resposta a um **problema específico de on-premises**. A prova testa esse mapeamento.

---

## Entidades e conceitos tocados

- Entidades: [[entities/aws]]
- Conceitos: [[concepts/cloud-benefits]] (novo), [[concepts/elasticity]] (novo), [[concepts/cloud-computing]], [[concepts/on-premises]]
- Tópicos: [[topics/cloud-fundamentals]]
