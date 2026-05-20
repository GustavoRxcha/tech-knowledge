# Pontos de Presença: Edge Locations, CloudFront e Route 53

> 📋 **Curso:** Infraestrutura Global AWS — Preparatório AWS Cloud Practitioner (CLF-C02)
> 📌 **Aula:** Conceitual — Pontos de Presença e Serviços de Borda

---

## 1. O que são Pontos de Presença?

**Pontos de Presença** são locais físicos distribuídos globalmente — em número muito superior ao de Regiões — que servem para **distribuir conteúdo com baixa latência** e **melhorar a conectividade** para usuários ao redor do mundo.

### Nomes equivalentes — todos se referem à mesma coisa

| Termo | Uso |
|---|---|
| **Pontos de Presença** | Português (tradução oficial) |
| **Edge Locations** | Inglês (mais comum em documentações) |
| **Locais de Borda** | Outra tradução usada em alguns materiais |
| **Rede de Borda** | Referência ao conjunto de Edge Locations |

> ⚠️ Na prova CLF-C02, os três termos podem aparecer. Todos se referem à mesma estrutura.

---

## 2. Por que os Pontos de Presença Existem?

### O problema

As **Regiões** e **Zonas de Disponibilidade** garantem alta disponibilidade e tolerância a falhas, mas estão em locais geográficos fixos. Quando um usuário acessa um serviço em uma região muito distante, a **latência aumenta** e a **experiência degrada**.

### Exemplo prático

```
Usuário em São Paulo
    ↓ acessa serviço hospedado na região da China
    ↓ distância geográfica enorme
    → Alta latência → vídeo travando, site lento
```

Mesmo com conexão de fibra óptica intercontinental, a distância física impõe limites de desempenho.

### A solução: Edge Locations

A AWS instala servidores de borda em pontos estratégicos ao redor do mundo — **muito mais locais do que regiões**. Esses servidores ficam próximos dos usuários e armazenam conteúdo em **cache**, reduzindo drasticamente a latência.

```
Usuário em São Paulo
    ↓ 1º acesso: vai até a região na China (longe)
    ↓ Edge Location em São Paulo armazena o conteúdo em cache
    ↓ 2º acesso: vai apenas até a Edge Location local (perto)
    → Latência muito menor → melhor experiência
```

---

## 3. CloudFront — CDN da AWS

### O que é

O **Amazon CloudFront** é o serviço de **CDN (Content Delivery Network — Rede de Entrega de Conteúdo)** da AWS. Ele utiliza a rede de Edge Locations para entregar conteúdo ao usuário final com **máxima velocidade e mínima latência**.

### Como funciona

1. O conteúdo (vídeos, imagens, páginas, arquivos) está hospedado em uma **origem** (ex: S3, EC2, ou servidor externo) em uma região AWS
2. O CloudFront distribui esse conteúdo para as **Edge Locations** ao redor do mundo
3. Quando um usuário acessa o conteúdo, o CloudFront serve a partir da **Edge Location mais próxima**
4. O conteúdo fica armazenado em **cache** na Edge Location por um período configurável
5. Acessos subsequentes são servidos diretamente do cache local — sem precisar ir até a origem

```
[Origem: S3 em us-east-1]
         ↓ distribuição
[Edge Location SP] [Edge Location Frankfurt] [Edge Location Tóquio]
         ↓
[Usuário em SP acessa] → serve do cache local → muito rápido
```

### Benefícios do CloudFront

| Benefício | Descrição |
|---|---|
| **Baixa latência** | Conteúdo servido do ponto mais próximo do usuário |
| **Alta taxa de transferência** | Otimizado para entrega de grandes volumes |
| **Cache inteligente** | Conteúdo popular fica armazenado nas bordas |
| **Segurança** | Integração com AWS Shield (DDoS) e WAF |
| **Alcance global** | Rede com mais de 400 pontos de presença |

### Casos de uso comuns

- Distribuição de vídeos e streaming
- Entrega de sites e aplicações web estáticas
- Download de arquivos grandes (software, jogos)
- APIs com usuários globais

---

## 4. Route 53 — DNS da AWS

### O que é

O **Amazon Route 53** é o serviço de **DNS (Domain Name System)** gerenciado da AWS. Ele também opera nos Pontos de Presença para garantir **resolução de nomes de domínio rápida e confiável** globalmente.

### O que o DNS faz

O DNS é o "tradutor" da internet: converte nomes de domínio legíveis por humanos em endereços IP que os servidores entendem.

```
Usuário digita: www.meusite.com.br
    ↓ Route 53
Traduz para: 192.0.2.44 (endereço IP do servidor)
    ↓
Redireciona para o servidor mais próximo disponível
```

### Por que usar o Route 53 nos Edge Locations?

Ao estar presente nas bordas da rede, o Route 53 consegue:
- Resolver consultas DNS **mais rapidamente** (perto do usuário)
- **Rotear o tráfego** para a região ou servidor mais próximo e saudável
- Implementar **failover automático** — se um servidor falhar, redireciona para outro

### Funcionalidades principais

| Funcionalidade | Descrição |
|---|---|
| **Registro de domínios** | Comprar e gerenciar domínios diretamente na AWS |
| **Roteamento geográfico** | Direcionar usuários para servidores com base na localização |
| **Roteamento por latência** | Direcionar para o servidor com menor latência |
| **Health checks** | Monitorar saúde dos endpoints e fazer failover automático |

---

## 5. Comparativo: Regiões vs AZs vs Edge Locations

| | Regiões | Zonas de Disponibilidade | Edge Locations |
|---|---|---|---|
| **Quantidade** | ~30+ | ~87+ | ~400+ |
| **Propósito** | Hospedar serviços | Alta disponibilidade | Entregar conteúdo |
| **Serviços** | EC2, S3, RDS, Lambda... | Redundância interna | CloudFront, Route 53 |
| **Latência** | Dependente da distância | Interna à região | Mínima (próxima ao usuário) |
| **Cache** | ❌ | ❌ | ✅ |

---

## 6. Hierarquia Completa da Infraestrutura Global AWS

```
Infraestrutura Global AWS
│
├── Regiões (30+)
│   └── Zonas de Disponibilidade (87+)
│       └── Data Centers físicos
│
└── Edge Locations / Pontos de Presença (400+)
    ├── CloudFront (CDN — cache de conteúdo)
    └── Route 53 (DNS — resolução de domínios)
```

---

> 💡 **Dica para a prova CLF-C02:** Edge Locations, CloudFront e Route 53 são temas frequentes. Questões típicas:
> - *"Qual serviço reduz a latência para usuários globais?"* → **CloudFront**
> - *"O que são Edge Locations?"* → Pontos de presença para entrega de conteúdo em cache
> - *"Qual serviço da AWS faz tradução de nomes de domínio?"* → **Route 53**
> - *"Qual a diferença entre Região e Edge Location?"* → Região hospeda serviços; Edge Location entrega conteúdo em cache próximo ao usuário

---

## Links Úteis

- [Amazon CloudFront](https://aws.amazon.com/pt/cloudfront/)
- [Amazon Route 53](https://aws.amazon.com/pt/route53/)
- [Infraestrutura Global AWS — Mapa](https://infrastructure.aws/)

---

*Aula 02 — Módulo: Infraestrutura Global AWS | Curso Preparatório AWS Cloud Practitioner*
