---
title: The code
description: The Lean package langlands-lean, its pinned toolchain, its layout and the rules for its code.
lead: The Lean code is in tamnd/langlands-lean. It builds with Lean v4.35.0 and Mathlib v4.35.0.
---
## Build

```sh
git clone https://github.com/tamnd/langlands-lean
cd langlands-lean
lake exe cache get
lake build
sh scripts/scan.sh
```

`lake exe cache get` downloads the compiled Mathlib. `lake build` builds the package `Langlands`. `sh scripts/scan.sh` scans the code for the forbidden words of the rules below.

## The toolchain

The project starts on Lean `v4.35.0` with the Mathlib tag `v4.35.0`. The pin is in `lean-toolchain` and `lake-manifest.json`. Imperial FLT and singularity-lean use the same pin, so files from those sources build without change. Other Lean sources use other pins. The project moves the files that it ports to its own pin, file by file. The first toolchain bump, to `v4.36.0`, is planned for milestone S1. After that, a bump runs once a month, and a person merges it.

## Layout

| Directory | Content |
|---|---|
| `Langlands/Statements/` | the pinned statements of the program; they import only Mathlib and `Basic.lean` |
| `Langlands/Ported/` | the ported sources, with their licence headers |
| `Langlands/Foundations/` | tier T1: local fields, adeles, ideles, Haar measure on them |
| `Langlands/Groups/` | tier T2: reductive groups over fields, root data, dual groups, L-groups |
| `Langlands/ClassField/` | tier T3: Weil groups, local and global class field theory, Lubin-Tate, Tate's thesis |
| `Langlands/GL2/` | tier T4: modular forms, Hecke operators, adelic $\mathrm{GL}_2$, newforms |
| `Langlands/Local/` | tier T5: smooth representations, Bernstein-Zelevinsky, the local correspondence |
| `Langlands/LFunctions/` | tier T6: Rankin-Selberg, Godement-Jacquet, converse theorems |
| `Langlands/TraceFormula/` | tier T7: Selberg, orbital integrals, endoscopy |
| `Langlands/Galois/` | tier T8: Galois representations, deformations, patching |
| `Langlands/PAdic/` | tier T9: $(\varphi, \Gamma)$-modules, $p$-adic and mod $p$ |
| `Langlands/FunctionField/` | tier T10: shtukas, Drinfeld, Lafforgue |
| `Langlands/Routes/` | one folder for each route |
| `Langlands/Examples/` | worked examples and certificates from the lab, each a node |
| `Langlands/Bridge/` | the bridges from the statements of the project to Mathlib, formal-conjectures and the ports |
| `Langlands/WIP/` | work with `sorry`; `Langlands.lean` does not import it |
| `manifests/` | `statements.sha256` and `ported.yaml` |

The [statements page](/statements/) lists the statement files and the statements that they will hold. The project is at milestone S0, so most of these directories do not exist yet.

## Rules

1. No `sorry` in the main tree. CI fails on `sorry`, `admit`, a new `axiom`, `opaque`, `native_decide`, `implemented_by` and `@[extern]` outside `WIP/`. A node with a proof that is not finished keeps the proof in `WIP/` and has the status `stated`.
2. Hypotheses, not axioms. A published theorem that is not formalized yet enters as a named `def ... : Prop` in `Statements/`. It is a hypothesis of the theorems that use it. Their status is `proved-mod`, and the site lists the hypotheses.
3. A fresh claim is never a hypothesis of another node. The index fails if one is.
4. Statement files are small and have comments. Other files can be long.
5. The code follows the naming and the style guide of Mathlib, so that parts can go upstream.
6. A ported file keeps its licence header and gets a provenance line, `-- Ported from <repo>@<commit>:<path>`. A change to a ported file is a separate commit with the label `port-change`.

A change to a file in `Langlands/Statements/` must change its hash in `manifests/statements.sha256` in the same pull request. The pull request needs the label `statement-change` and two approvals.

## Contribute

Each pull request refers to a milestone issue of [tamnd/langlands](https://github.com/tamnd/langlands/issues). A proof must use the standard axioms only. An agent proposes a pull request, and a person merges it.
