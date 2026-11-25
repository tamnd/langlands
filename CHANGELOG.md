# Changelog

Each release has a section. The newest release is first.

## Unreleased

### Added

- The node LG01JZBNVC for Hecke's theorem over Q. It is proved by `Langlands.heckeFunctionalEquationAt_rat`.

### Changed

- The node LG06WS8A1Y for the theorem of Kronecker and Weber is proved, by `Langlands.Bridge.kroneckerWeber` and the port of global class field theory.
- `records/lean.json` is at langlands-lean 8e3e859, with 702 declarations.

- Six nodes with the status stated: the Galois representations of modular forms (LGG3ZW59RX), the weak form of Serre's conjecture (LGKH3WKEVV), Artin's conjecture (LGEHB4MGJK), Artin's conjecture for odd representations of dimension 2 over Q (LGX6BXWH0J), Selberg's eigenvalue conjecture (LG0S1WN9ND) and the Ramanujan conjecture for Maass forms (LG75ERTV5K). Three of them are open conjectures.
- The paper records Del69 (Deligne), KW09 (Khare and Wintenberger), Kis09 (Kisin), DS74 (Deligne and Serre), Sel65 (Selberg) and Kim03 (Kim and Sarnak).

## v0.1.2 (2026-11-25)

### Added

- The node LG4S7A4G1F for the local Langlands correspondence for induced tori. It is proved.
- The node LG6NN4B43V for the functional equation of Hecke L-functions, with the status stated, and the paper records CF67 (Cassels and Frohlich, with Tate's thesis in Chapter XV) and Neu99 (Neukirch).
- `blueprint/milestones.yaml`: the default weights of the milestones for `lgl queue`.
- `records/lean.json`: the declarations of langlands-lean at commit 54b0386, with 483 declarations.
- The nodes LG3VDFDBW0 (the Weil group is dense in the absolute Galois group), LGDEPE7CM9 (the abelianized Weil group embeds in the abelianized Galois group) and LG5YHMSJZM (the local Langlands correspondence for split tori). All three are proved.
- `records/lean.json`: the declarations of langlands-lean at commit 835c3bf.

## v0.1.1 (2026-11-25)

### Added

- The first run of lab experiment E1 in `lab/runs/`, with its spec in `lab/specs/e1-local-reciprocity-small.yaml`. In 27 quadratic and cyclotomic extensions of Q_p for p <= 7, each computed norm is in the kernel that Lubin-Tate theory predicts, and each class of the kernel has a norm.

### Changed

- The node LG875TDM3B, the local existence theorem, is proved. Its proof is `Langlands.Bridge.localExistence` of langlands-lean, from the NYLL port.
- `records/lean.json`: the declarations of langlands-lean at commit 61d225c.

## v0.1.0 (2026-11-25)

### Changed

- This release closes milestone S0. It has the same content as v0.0.2. The statements, the map, the records and the site of S0 are complete.

## v0.0.2 (2026-11-25)

### Added

- The first 15 nodes of the map in `blueprint/nodes/`: the Weil group, its geometric Frobenius elements and its abelianization, finite abelian local reciprocity, the statements of class field theory, the statements of modularity, Hasse-Weil, Ramanujan-Petersson and Sato-Tate, and the false modularity statement of formal-conjectures.
- The paper records BCDT01, Wil95, Del74 and BLGHT11 for the rows T8-06, T8-04, T4-10 and T8-10 of the corpus.
- `records/lean.json`: the declarations of langlands-lean at commit 3668a96, from `lgl index`.
- The nodes LG6W8W7GE6 and LG1DP2ZDPA for the bridges of spec 06.4 to the Sato-Tate and Ramanujan statements of formal-conjectures. Both are proved.
- `records/fidelity.json`: the checks F1, F2 and F3 of spec 06.3 pass for `LocalReciprocityGL1`, `GlobalReciprocity`, `ModularityEllipticQ` and `SatoTate`. The checks F4 and F5 are not done, so no statement is `faithful` yet.

### Changed

- The paper records Ser67, Mil20 and Tat79 link their results to the nodes. Ser67 has the result for the finite abelian case, which the NYLL port proves.

## v0.0.1 (2026-11-25)

### Added

- The spec of the project in `docs/spec/`, from the research of November 2026.
- The writing rules check `scripts/style.py`, the lint workflow, the deploy workflow and the scorecard workflow.
- The first pages of the site at https://langlands.tamnd.com: the program, the map, the routes, the papers, the statements, the trust page, the code, the handbook and the about page.
- The routes R1 to R9 in `blueprint/routes.yaml`.
- The paper records Ser67, Ser79, Tat79 and Mil20.
