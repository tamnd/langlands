# langlands

The Langlands program in Lean 4, in public.

The Langlands program connects automorphic forms, Galois representations and the representations of reductive groups over local fields. Its main conjectures are reciprocity, functoriality and the local Langlands correspondence. Some cases are theorems: class field theory, the local correspondence for $GL_n$, the modularity of elliptic curves over $\mathbb{Q}$ and the geometric conjecture in characteristic 0. The general conjectures are open. This project states the program in Lean, proves the known parts in an order that leads to the open parts, and works on the open parts in the open.

The site is https://langlands.tamnd.com.

## The repositories

| Repository | Content |
|---|---|
| langlands (this repository) | the map of the program, the paper records, the claim records, the lab specs, the trust records, the spec and the pages of the site |
| [langlands-lean](https://github.com/tamnd/langlands-lean) | the Lean package `Langlands`: the statements, the fidelity checks, the library and the proofs |
| [langlands-agent](https://github.com/tamnd/langlands-agent) | `lgl`, the toolchain: it checks the map and the records, and it builds and checks the site |
| [langlands-handbook](https://github.com/tamnd/langlands-handbook) | The Langlands Handbook, a textbook for students and mathematicians, as PDF and EPUB |

## Status

No open case of the program is proved here, in Lean or on paper. The site shows the status of each statement. A tool computes each status from the Lean build and the records. No status is written by hand.

The work goes in milestones. Each milestone has a tracking issue with the label `milestone`. The plan is in `docs/spec/15-milestones.md`.

| Milestone | Goal | Release |
|---|---|---|
| S0 | the repositories, the first statements and the site | v0.1.0 |
| S1 | local $GL_1$: the Weil group and local class field theory | v0.2.0 |
| S2 | global class field theory and Tate's thesis | v0.3.0 |
| S3 | reductive groups and smooth representations | v0.4.0 |
| S4 | $GL_2$: modular forms and automorphic representations | v0.5.0 |
| S5 | the local Langlands correspondence for $GL_2$, $p$ odd | v0.6.0 |
| S6 | $p = 2$, Jacquet-Langlands and the first frontier check | v0.7.0 |
| S7 | the first research result | v0.8.0 |
| S8 | the library to $GL_n$ | v0.9.0 |
| S9 | an open case | v1.0.0 |

A patch release v0.x.y marks a set of merged pull requests inside a milestone. A minor release v0.x.0 closes a milestone.

## Layout

| Path | Content |
|---|---|
| `docs/spec/` | the spec: the research of 2026, the goal, the program, the routes, the statements, the corpus, the architecture and the milestones |
| `blueprint/nodes/` | the map: one YAML file for each statement or definition, with its sources, its uses and its Lean names |
| `blueprint/routes.yaml` | the research routes R1 to R9 of spec 04, with their weights |
| `papers/` | one record for each paper or book of the corpus (spec 07) |
| `claims/` | one record for each fresh claim of route R1 (spec 01.2) |
| `records/` | the records that tools write: the Lean build, the trust report and the fidelity checks |
| `lab/` | the specs and the runs of the computation lab (spec 13) |
| `site/` | the pages of the site |
| `reports/` | the milestone and weekly reports |

## Build the site

```sh
git clone https://github.com/tamnd/langlands-agent ../langlands-agent
(cd ../langlands-agent && go build -o bin/lgl ./cmd/lgl)
../langlands-agent/bin/lgl check -content .
../langlands-agent/bin/lgl site build -content . -out public
../langlands-agent/bin/lgl site serve -dir public
```

## Licence

The prose is licensed under CC BY-SA 4.0 and the data under Apache-2.0. See `LICENSES/`.
