---
title: The map
description: The nodes of the map of langlands, with their tier, their status and the Lean declarations that they name.
lead: The map has a node for each definition, theorem and conjecture that the project uses. A tool computes the status of each node from the Lean build. A person does not set the status by hand.
---
## What a node is

The map is a directed graph with no cycles. Its nodes are mathematical statements and definitions. Its edges mean "uses". The map also holds the open conjectures and the routes, so it is the plan of the project too.

A node is one YAML file in `blueprint/nodes/` of [tamnd/langlands](https://github.com/tamnd/langlands). Its tag is `LG` and 8 characters of base 32. A node has a kind, a title, a statement in words, its sources, the nodes that it uses, the names of its Lean statement and its Lean proof, a tier, its routes and its levels. The routes use working names such as `LG-llc-gl2` for the first nodes. When a node gets its tag, it keeps the working name as its slug.

## The status of a node

| Status | Meaning |
|---|---|
| `unstated` | The node has no Lean statement yet. The node lists the vocabulary that is missing. |
| `stated` | The Lean statement exists and builds. |
| `faithful` | The statement passed the fidelity battery for its class. |
| `proved` | A Lean proof exists, it uses only the three standard axioms, and each node that it uses is `proved`. |
| `proved-mod` | A Lean proof exists that takes named nodes as hypotheses. Each hypothesis is a published theorem that is not formalized yet. |
| `open` | The statement is an open conjecture. No proof is claimed. |
| `claimed` | The statement is a fresh claim of route R1. It is never a hypothesis of another node. |
| `refuted` | A Lean proof of the negation exists. |

A proof with `sorry` is never `proved`. A published theorem that is not formalized enters as a named hypothesis, never as an `axiom`.

## The tiers

The tiers follow the corpus of the project. A tier uses only the tiers above it.

| Tier | Content |
|---|---|
| T0 | references |
| T1 | number fields, local fields and adeles |
| T2 | algebraic and reductive groups, root data, L-groups |
| T3 | class field theory and $\mathrm{GL}_1$ |
| T4 | modular and automorphic forms of $\mathrm{GL}_2$ |
| T5 | smooth representations and local Langlands |
| T6 | L-functions, converse theorems and functoriality |
| T7 | trace formula, endoscopy and Arthur's classification |
| T8 | Shimura varieties, Galois representations and modularity |
| T9 | $p$-adic Hodge theory, $p$-adic and mod $p$ Langlands, Fargues-Scholze |
| T10 | function fields and geometric Langlands |

The statements of the program form one more group, S.

## The state of the map

The project is at milestone S0. On 2026-11-25 the map has no nodes. The first nodes are the statements of class field theory and of modularity in `Langlands/Statements/`, and the tiers T1 to T10 as nodes, most of them `unstated` or `stated`. The table below shows the nodes when they exist.
