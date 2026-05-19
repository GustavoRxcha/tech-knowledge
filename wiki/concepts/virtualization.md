---
title: "Virtualização"
type: concept
tags: [infraestrutura, virtualização, hypervisor, clf-c02]
created: 2026-05-19
updated: 2026-05-19
sources: 1
---

# Virtualização

Tecnologia que permite **um único hardware físico rodar múltiplas instâncias virtuais** (VMs) simultaneamente, cada uma com seu próprio SO. Base técnica sobre a qual a cloud foi construída.

---

## Como funciona

Um **hypervisor** (software de virtualização) abstrai o hardware físico e cria múltiplas VMs isoladas em cima dele:

```
[Servidor Físico]
       ↓
   [Hypervisor]
       ↓
├── VM 1 (Linux)
├── VM 2 (Windows)
└── VM 3 (Linux)
```

## Tipos de hypervisor

| Tipo | Onde roda | Exemplos |
|---|---|---|
| **Type 1 (bare-metal)** | Direto no hardware | VMware ESXi, Hyper-V, Xen, KVM |
| **Type 2 (hosted)** | Sobre um SO host | VirtualBox, VMware Workstation |

Cloud pública usa quase sempre Type 1 — performance mais próxima do hardware.

## Por que importa para a cloud

- **Aproveitamento de hardware**: um servidor caro hospeda dezenas de cargas.
- **Isolamento**: VMs do cliente A não interferem nas do cliente B (multi-tenancy).
- **Provisionamento rápido**: criar uma nova VM é minutos, não dias.
- **Migração**: mover VMs entre hosts físicos sem downtime.

Sem virtualização, a economia de escala da [[concepts/cloud-computing|cloud]] não seria viável.

## Containers como evolução

Containers (Docker, Kubernetes) vão um passo além: virtualizam **só o SO**, não o hardware, com overhead muito menor. Não cobertos pelas fontes atuais.

> [!question] Quando ingerir aulas sobre containers, criar `concepts/containers.md` e relacionar.

## Para a prova CLF-C02

Aparece em contexto histórico ("o que tornou a cloud possível"). Não costuma ser muito profundo — basta saber:
- Virtualização = múltiplas VMs em um hardware via hypervisor
- É a base da elasticidade e da multi-tenancy
- Cloud surge **depois** da maturidade da virtualização

## Fontes

- [[sources/clf-c02-aula01-cloud-computing]]

## Relações

- [[concepts/cloud-computing]]
- [[concepts/on-premises]]
- [[concepts/iaas]]
- [[topics/cloud-fundamentals]]
