# 14. Trust

The project will produce a large amount of Lean code. Much of it is written by models or ported from projects that models wrote: anthropics FLT, TauCeti, NYLL with Codex. The claims of the project must survive a hostile referee.

This document is the trust report that the site shows (`/trust/`), in the form of singularity's. It is a list of questions, how each one is checked, and the current answer. The answer of each row is one of these:
- **yes**;
- **no**;
- **open**: a person must decide;
- **not run**.

## 14.1 The questions

| Row | Question | Check | Where |
|---|---|---|---|
| Q0 | Is the source the one that the site describes? | the site build records the commit of `tamnd/langlands-lean` and the commit of each port; `lgl site check` refuses a mismatch | CI |
| Q1 | Does it build? | `lake build` of `Langlands` at the pinned toolchain, from a clean cache, on a machine of the project | `trust` workflow |
| Q2 | Which axioms do the top theorems use? | `#print axioms` and the constant walk of `lgl trust`, for each `proved` node; each must be `propext`, `Classical.choice`, `Quot.sound` only | `trust` workflow |
| Q3 | Does a second kernel accept it? | `lean4checker --fresh` on the modules of the top theorems, and `lake comparator --paranoid`, which replays the export in the independent checkers (lean4lean, nanoda) | `trust` workflow, weekly |
| Q4 | Do the proved theorems have the pinned statements? | `lake comparator` against `Langlands/Statements/`, with `lake check` for the package | `trust` workflow |
| Q5 | Do the statements mean what the docstrings say? | the fidelity battery of 06.3 | `records/fidelity.json` |
| Q6 | Which published theorems are still hypotheses? | the list of `proved-mod` hypotheses (09.2) used by each top theorem, each with its paper record and its expert status (07.13) | `records/status.json` |
| Q7 | Has a person read the proof? | the handbook sections of the top theorems at status `reviewed`, with names | handbook |
| Q8 | Has someone outside the project reproduced Q1 to Q4? | a link to an independent run | by hand |

Q0 to Q4 are mechanical and run on every release. Q5 to Q8 need people. The site shows all nine rows, for each top theorem separately. The home page shows the rows of the statements of 06.2.

For a check of a fresh claim (route R1) the report has one more row:
- **Q9.** Have the authors seen the result, and what did they answer?

The page of the claim shows it (12.2, `/claims/`).

## 14.2 The top theorems

The trust report covers these theorems. More are added as the map grows.

| Theorem | Meaning | Milestone |
|---|---|---|
| `Langlands.localReciprocityGL1` | local class field theory as LLC for $GL_1$ (from the NYLL port) | S1 |
| `Langlands.localLanglandsTorus` | Langlands' correspondence for tori | S1 |
| `Langlands.globalReciprocity`, `Langlands.globalExistence` | global class field theory | S2 |
| `Langlands.heckeFunctionalEquation` | Tate's thesis for Hecke characters | S2 |
| `Langlands.kroneckerWeber` | the check of `GlobalReciprocity` | S2 |
| `Langlands.modularitySemistableQ` | Wiles and Taylor-Wiles, through the anthropics FLT port and the bridge of 06.4 | S4 |
| `Langlands.eichlerShimura` | Galois representations of weight 2 newforms, `proved-mod` the hypotheses that tier T8 names | S4 |
| `Langlands.localLanglandsGL2_odd` | LLC for $GL_2$ over a $p$-adic field, $p$ odd (04.12) | S5 |
| `Langlands.localLanglandsGL2` | the same for all $p$ | S6 |
| `Langlands.jacquetLanglandsGL2` | the Jacquet-Langlands correspondence | S6 |
| `Langlands.localLanglandsGL` | LLC for $GL_n$, `proved-mod` the cohomology of the Lubin-Tate tower | S8 |
| the nodes of the open statements of 06.2 | the open conjectures | S9 |
| the claim checks of route R1 | each check separately, with Q9 | from S6 |

## 14.3 Threats and answers

| Threat | Answer |
|---|---|
| A wrong statement that is easy to prove, in particular a correspondence that has lost a characterizing property (06.5, risk 1) | the fidelity battery, F3 and F4 in particular, and the freeze of 06.3 |
| A kernel bug used by a generated proof (the soundness bugs reported in July and August 2026, document 01) | Q3 with two independent kernels; a pinned toolchain that has the fixes; the scan of 09.2 for escape hatches; a weekly replay |
| A hidden axiom in a dependency or a port | the constant walk of Q2 covers the ports and Mathlib, not only the project |
| A ported file that changed meaning in the port | the bridge of 06.4 against the source statement; the provenance line and the `port-change` label of 09.2 |
| A port from a source without a licence | `lgl port check` refuses a source that is not in the allow list of `manifests/ported.yaml`; riemann-lean and Langlands-lib are read only (05.3) |
| A change to a statement in a large pull request | the hash manifest of 09.6 and the `statement-change` label |
| A hypothesis that is never discharged and is false | each `proved-mod` hypothesis is a named statement with its own fidelity check and a source; each hypothesis lists the expert status of its source |
| A fresh claim used as if it were a theorem | `lgl index` fails when a `claimed` node is the hypothesis of another node (09.2) |
| A public statement that harms an author | the claim policy of 06.6; the 30-day rule of 14.4; neutral words (12.3) |
| A generated proof that nobody understands | Q7; the handbook is part of the trust, not decoration |
| Prompt injection from a paper or from external Lean code | 10.7 |
| A model that reports success it did not reach | `lgl` runs the role checks of 10.3, not the model; the run record has the build log |

## 14.4 Disclosure

- **Pull requests.** Every merged pull request that a role wrote has the role, the model and the run id in its body and as a commit trailer.
- **Handbook sections.** Every handbook section names its drafter and its reviewers.
- **Public statement.** The README and the site say plainly three things:
  - much of the code and the text is written by models;
  - it is checked by Lean and by people;
  - which checks a given result has passed.

  This follows the norms that the field wrote down in 2025 and 2026 (01): disclose how a result was made, keep it independently checkable, keep people responsible.

For route R1 there is a second rule:
1. Before a page about a check of a fresh claim goes public, the project writes to the authors. The letter has the Lean statement, the checks passed, and the gap or the confirmation.
2. The page waits 30 days or until they answer, whichever comes first.
3. A confirmation is published only with the authors' consent to be named.
4. A gap is published only as a neutral statement of what Lean found (12.3).

## 14.5 Registration

The project publishes a `formalization.yaml` at the root of `tamnd/langlands`. It uses the schema of the Mathlib Initiative that hironaka uses (version `v0.4`). The file lists each source with its relationship (`formalizes`, `uses`, `states`, `ports`) and its author endorsement state.

The project registers the main statements in the Palomar registry, and the trust rows of each registered statement link to the site. The file also lists these sources with their commit and licence:
- the statements that the project takes from other projects (06.4);
- the ported files (05.4).
