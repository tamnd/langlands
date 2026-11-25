---
title: Trust
description: The checks that each Lean result of langlands must pass before the project calls it proved, and the state of each check.
lead: A Lean proof is only as good as its statement and its build. These checks say what a reader can trust. A hostile referee must be able to repeat each one.
---
## The rows

Each row has one of four answers: yes, no, open (a person must decide), or not run. A row is "not run" until the trust workflow runs it on a machine of the project. The rows come from `records/trust.json`, which a tool writes. A person does not edit it. At milestone S0 no top theorem exists yet, so no row has run.

| Row | Question | Check |
|---|---|---|
| Q0 | Is the source the one that the site describes? | The site build records the commit of langlands-lean and the commit of each port. The site check refuses a mismatch. |
| Q1 | Does it build? | `lake build` of `Langlands` at the pinned toolchain, from a clean cache, on a machine of the project. |
| Q2 | Which axioms do the top theorems use? | `#print axioms` and a walk over the constants of each `proved` node. Each proof must use only `propext`, `Classical.choice` and `Quot.sound`. |
| Q3 | Does a second kernel accept it? | `lean4checker --fresh` on the modules of the top theorems, and `lake comparator --paranoid`, which replays the export in the independent checkers lean4lean and nanoda. |
| Q4 | Do the proved theorems have the pinned statements? | `lake comparator` against `Langlands/Statements/`, with `lake check` for the package. |
| Q5 | Do the statements mean what the docstrings say? | The fidelity battery F1 to F7. |
| Q6 | Which published theorems are still hypotheses? | The list of the hypotheses of each `proved-mod` top theorem, each with its paper record and the state of its acceptance by experts. |
| Q7 | Has a person read the proof? | The handbook sections of the top theorems at status reviewed, with the names of the reviewers. |
| Q8 | Has someone outside the project reproduced Q1 to Q4? | A link to an independent run. |

Q0 to Q4 are mechanical and run at each release. Q5 to Q8 need people. The site shows the nine rows for each top theorem separately. A check of a fresh claim of route R1 has one more row, Q9: have the authors seen the result, and what did they answer?

## The fidelity battery

A statement is trusted only after it passes each check below. The results go to `records/fidelity.json`.

| Check | What it does |
|---|---|
| F1. Elaboration | The file builds with the pinned toolchain. It has no `sorry`, `axiom` or `opaque`. `#print axioms` of each statement shows at most the three standard axioms. |
| F2. Positive instances | Known special cases follow from the statement, or the statement holds in a known case. An example: `LocalLanglandsGL 1` follows from `LocalReciprocityGL1`. |
| F3. Negative instances | Wrong variants of the statement are proved false or trivial. An example: drop the condition on $\varepsilon$-factors and show a second family that satisfies the other conditions. |
| F4. Triviality attack | A strong prover gets a budget to prove the statement in a trivial way: by cardinality, with an empty type of representations, through a quirk of universes, or with a topology that makes all sets open. A success is a failed check. |
| F5. Round trip | An independent model translates the Lean statement to English without the docstring. A person compares the result with the docstring and with the source paper. |
| F6. Human review | Two number theorists sign that the Lean statement means what the docstring says. Their names and the dates go into the record. |
| F7. Pinning | The hash of the statement file is in `manifests/statements.sha256`, and `lake comparator` matches each proof to the pinned statement. |

A statement of class theorem counts for the level G1 after F1 to F5. A statement of class open needs all seven checks before any proof of it is announced. For F6 the two reviewers of an open statement must come from two different research groups. A statement is frozen after F6. A change after F6 starts the battery again.

## The claim rule

The project does not say that it has proved an open case unless all of these hold: the proof builds; it uses only the three standard axioms; two kernels accept it; the statement passed F1 to F7; and at least two experts who are not paid by the project have read the written proof in the handbook. Before that, the site says which checks the result has passed.

For a fresh claim of route R1 the project says only what a Lean check of a given part found. It writes to the authors before any page about the check goes public. The page waits 30 days or until the authors answer, whichever comes first. The page uses neutral words. It never says that a paper is wrong.

## Disclosure

Much of the code and the text of the project is written by AI models. Lean and people check it. Each merged pull request that an agent role wrote names the role, the model and the run. Each handbook section names its drafter and its reviewers.
