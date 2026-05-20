---
title: "AWS Direct Connect"
type: entity
tags: [aws, direct-connect, redes, vpc, fibra-optica, conectividade]
created: 2026-05-20
updated: 2026-05-20
sources: 1
---

# AWS Direct Connect

Serviço de **conexão de fibra óptica dedicada** entre data center corporativo e a AWS. Alternativa à VPN quando velocidade, latência e confiabilidade são críticos.

---

## Características

| Característica | Valor |
|---|---|
| Tipo de conexão | Fibra óptica dedicada (não compartilhada) |
| Velocidade máxima | Até **100 Gbps** |
| Latência | Muito baixa (ponto a ponto) |
| SLA | 99,99% de uptime |
| Custo | Elevado (infraestrutura física dedicada) |
| Tempo de setup | Semanas |
| Tráfego via internet | ❌ Não — conexão ponto a ponto |

## Como funciona

1. AWS possui **Direct Connect locations** (parceiros) em várias regiões
2. Empresa identifica o parceiro Direct Connect mais próximo
3. Conexão de fibra óptica é construída do data center até o local AWS
4. Resultado: link ponto a ponto de alto desempenho sem tráfego pela internet pública

```
[Seu Data Center]
       ↓ fibra óptica dedicada
  [AWS Direct Connect Location]
       ↓
[VPC — qualquer sub-rede]
```

## Quando usar

- ✅ Transferências massivas de dados (terabytes ou mais)
- ✅ Aplicações com requisito de latência muito baixa
- ✅ Conexão permanente e de alto volume entre data center e AWS
- ❌ Trabalho remoto ocasional — use [[concepts/vpn|VPN]]
- ❌ Pequenas transferências — custo não justifica

## Comparativo com VPN

| Aspecto | VPN (VGW) | Direct Connect |
|---|---|---|
| Meio físico | Internet pública (criptografada) | Fibra óptica dedicada |
| Velocidade | Limitada pela internet | Até 100 Gbps |
| Latência | Variável | Muito baixa |
| Custo | Baixo | Alto |
| Setup | Horas | Semanas |
| Caso de uso | Dados sensíveis, trabalho remoto | Grandes volumes, baixíssima latência |

## Relações

- [[entities/amazon-vpc]]
- [[concepts/vpn]]
- [[entities/aws-internet-gateway]]
- [[topics/cloud-fundamentals]]

## Fontes

- [[sources/clf-c02-aula16-connectivity]]
