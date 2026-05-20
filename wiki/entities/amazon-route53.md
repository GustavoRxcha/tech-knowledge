---
title: "Amazon Route 53"
type: entity
tags: [aws, route53, dns, edge-location, dominio, roteamento]
created: 2026-05-20
updated: 2026-05-20
sources: 1
---

# Amazon Route 53

O **Amazon Route 53** é o serviço de **DNS (Domain Name System)** gerenciado da [[entities/aws|AWS]]. Opera nos [[concepts/edge-location|Pontos de Presença]] globalmente para garantir **resolução de nomes de domínio rápida e confiável**.

> O nome "Route 53" faz referência à porta 53, usada pelo protocolo DNS.

---

## O que o DNS faz

O DNS é o "tradutor" da internet: converte nomes de domínio legíveis por humanos em endereços IP que os servidores entendem.

```
Usuário digita: www.meusite.com.br
    ↓ Route 53
Traduz para: 192.0.2.44
    ↓
Redireciona para o servidor mais próximo disponível
```

---

## Por que operar nos Edge Locations

Ao estar presente na borda da rede, o Route 53 consegue:
- Resolver consultas DNS **mais rapidamente** (perto do usuário)
- **Rotear o tráfego** para a região ou servidor mais próximo e saudável
- Implementar **failover automático** — se um endpoint falhar, redireciona para outro

---

## Funcionalidades principais

| Funcionalidade | Descrição |
|---|---|
| Registro de domínios | Comprar e gerenciar domínios diretamente na AWS |
| Roteamento geográfico | Direcionar usuários com base na localização |
| Roteamento por latência | Direcionar para o servidor com menor latência |
| Health checks | Monitorar saúde dos endpoints e fazer failover automático |

---

## Para a prova CLF-C02

- *"Qual serviço da AWS faz tradução de nomes de domínio?"* → **Route 53**
- *"Onde o Route 53 opera para garantir baixa latência?"* → **Edge Locations**

---

## Relações

- [[concepts/edge-location]] — infraestrutura onde o Route 53 opera
- [[entities/amazon-cloudfront]] — frequentemente usado em conjunto (domínio + CDN)
- [[concepts/aws-region]] — as origens para onde o Route 53 roteia o tráfego

## Fontes

- [[sources/clf-c02-aula05-global-infrastructure]]
- [[sources/clf-c02-aula07-edge-cloudfront-route53]]
