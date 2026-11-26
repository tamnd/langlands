# Changelog

Each release has a section. The newest release is first.

## Unreleased

## v0.1.9 (2026-11-27)

### Added

- The first measurement of the cost per proved node, in reports/2026-11-27-cost-per-node.md, with the data of each agent run.

## v0.1.8 (2026-11-27)

### Added

- The spec `lab/specs/e2-llc-gl2-small.yaml` and the run `lab/runs/2026-11-26-e2-llc-gl2-small-64a59b93/` of lab experiment E2. The run compares the L-factors and the ε-factors of 45552 pairs for $GL_2(\mathbb{Q}_p)$ with $p$ in 3, 5 and 7, and it finds no mismatch.

## v0.1.7 (2026-11-26)

### Changed

- `records/lean.json` is at langlands-lean 6531e9e, with 2252 declarations, 0 with `sorry`.
- `records/replay.json` has the result of the kernel replay of langlands-lean 6531e9e. leanchecker --fresh, lean4lean, nanoda and `lake comparator --paranoid` accept the commit. Rows Q0 to Q4 of the trust report are yes.

## v0.1.6 (2026-11-26)

### Added

- The paper records GT11 (Gan and Takeda), HLTT16 (Harris, Lan, Taylor and Thorne) and Sch15 (Scholze), from the bibliographic data only, with the read tag U.

### Changed

- Four nodes have a Lean statement now. The local Langlands correspondence for GSp(4) (LGQCVGBMVA), the Galois representations of regular algebraic cuspidal representations (LGV2KZTSNS) and the global Jacquet-Langlands correspondence (LGZWX81F9A) are stated. The reciprocity conjecture for GL(n) (LGRYCDD49K) is open, with a weak form in Lean. The notes of each node say what the Lean statement leaves out.
- The Breuil-Mezard conjecture (LGRMD7S8EV) stays unstated. Its notes say why a special form is not stated.
- `records/lean.json` is at langlands-lean 9a88d56, with 1537 declarations.
- `records/replay.json` is new. It has the result of the kernel replay of langlands-lean 9a88d56 by leanchecker, lean4lean and nanoda. Row Q3 of the trust report is yes. Row Q4 is no, because the statement manifest of that commit was old. tamnd/langlands-lean#56 corrects it.

## v0.1.5 (2026-11-26)

### Added

- Eleven nodes for the new statements of langlands-lean about GL(n). Eight have the status stated: the local Langlands correspondence for GL(n) (LG2E74SP8W) and for GL(2) (LG453577KN), the L-packets of SL(2) (LG75V240RB), the local Jacquet-Langlands correspondence for GL(2) (LG7NVV7NSF), symmetric power functoriality (LGC3KP178Q), cyclic base change (LGCH6QCV3P), the fundamental lemma for unitary Lie algebras (LGH8C75DFX) and Kisin's theorem on the Fontaine-Mazur conjecture for GL(2) over Q (LGNT1M1N6Z). Three are open conjectures: the Ramanujan conjecture for GL(n) (LGAGRC05KF), functoriality from GL(n) to GL(m) (LGANNYN8R0) and the Hasse-Weil conjecture (LGFQ0HXS3H).
- Six nodes with the status unstated, for the rows of section 6.2.2 that have no Lean statement yet: the local Langlands correspondence for GSp(4) (LGQCVGBMVA), the Breuil-Mezard conjecture for GL(2) over Q_p (LGRMD7S8EV), the reciprocity conjecture for GL(n) (LGRYCDD49K), the Galois representations of regular algebraic cuspidal representations (LGV2KZTSNS), the Langlands correspondence for GL(n) over function fields (LGZJQ4K11G) and the global Jacquet-Langlands correspondence (LGZWX81F9A). The notes of each node say which vocabulary is missing.
- The paper records HT01 (Harris and Taylor), Hen00 (Henniart), Kut80 (Kutzko), BH06 (Bushnell and Henniart), LL79 (Labesse and Langlands), JL70 (Jacquet and Langlands), NT21 (Newton and Thorne), AC89 (Arthur and Clozel), Ngo10 (Ngo), Kis09b (Kisin) and Lan70 (Langlands). They are made from the bibliographic data only, and their read tag is U.
- The paper record Laf02 (L. Lafforgue, Invent. Math. 147, 2002), from the bibliographic data only, with the read tag U.

### Changed

- `records/lean.json` is at langlands-lean 3c0391a, with 1337 declarations.
- The node LGZJQ4K11G for the Langlands correspondence over function fields has the status stated. Its Lean statement is `Langlands.ReciprocityFunctionFieldGL`, and its source is Laf02.

## v0.1.4 (2026-11-26)

### Changed

- The nodes LGVAKJJD8Y for global reciprocity and LGX8K4ZEGW for the global existence theorem are proved, by `Langlands.Bridge.globalReciprocity` and `Langlands.Bridge.globalExistence` and the port of global class field theory.
- The node LG06WS8A1Y for the theorem of Kronecker and Weber is proved and not proved-mod, because the node for global reciprocity that it uses is proved.
- `records/lean.json` is at langlands-lean b6f61f2, with 707 declarations.

## v0.1.3 (2026-11-26)

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
