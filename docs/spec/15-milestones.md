# 15. Milestones

Each milestone has a goal, exit criteria and a release. A tool can check each exit criterion, or a named person signs it. The dates are targets set on 2026-11-25. Each milestone closes with a minor release v0.x.0 of each repository, and the work inside a milestone gets patch releases v0.x.y. The levels G1 to G6 are those of document 02, the tiers T0 to T10 are those of 07, and the routes R1 to R9 are those of 04.

| Milestone | Target | Goal | Exit criteria | Release |
|---|---|---|---|---|
| S0 | 2026-12-15 | the four repositories, the first statements, the site | `Langlands/Statements/Basic.lean` and `ClassField.lean` build at the pin, with no `sorry`; F1 to F3 of 06.3 pass for `LocalReciprocityGL1`, `GlobalReciprocity`, `ModularityEllipticQ` and `SatoTate`; the bridges to formal-conjectures (`ModularityConjecture`, `SatoTate`, `RamanujanTau`) are stated; `lgl index`, `lgl status`, `lgl port check` and `lgl site build` work; langlands.tamnd.com shows `/program/`, `/statements/`, `/map/` (tiers T1 to T10 as nodes, most `unstated` or `stated`) and `/trust/`; the NYLL port of `finiteAbelianLocalReciprocity` builds at the pin; the letters of Q-05 and Q-07 are sent | v0.1.0 of each repository |
| S1 | 2027-01-31 | local GL(1) | `WeilGroup` with its topology and the F2 and F3 checks of 06.5 (risk 2); `localReciprocityGL1` proved (Q0 to Q4 **yes**); `LocalExistence` proved; `localLanglandsTorus` proved for split and induced tori; the first toolchain bump to `v4.36.0`; lab E1 run | v0.2.0; handbook Vol. 0 draft, Vol. 3 chapters 1 to 4 drafted |
| S2 | 2027-03-31 | global CFT and Tate's thesis | `globalReciprocity`, `globalExistence` and `kroneckerWeber` proved; `heckeFunctionalEquation` proved; in the cross-check package, the same statements from riemann-lean (05.6), or a written reason why not; every GL-type statement of 06.2.2 at least `stated`; the first measurement of cost per proved node; the eval sets of 10.9 in use | v0.3.0; Vol. 1 drafted; Vol. 3 checked |
| S3 | 2027-05-31 | groups and smooth representations | tier T2: split reductive groups over a field from root data, dual groups, L-groups for split and quasi-split groups; tier T5 start: smooth and admissible representations, Jacquet modules, parabolic induction, the Bernstein-Zelevinsky classification for $GL_2$; `LocalLanglandsGL` with full vocabulary (`IsLanglandsFamily`), F1 to F5 done; the shapes of the G1b statements written; lab E2 run | v0.4.0; Vol. 2 drafted; Vol. 6 chapters 1 to 3 drafted |
| S4 | 2027-08-31 | GL(2): modular and automorphic | tier T4: Hecke operators on $S_k(\Gamma_0(N))$, newforms, the Sturm bound, the adelic dictionary for $GL_2$; `modularitySemistableQ` from the anthropics FLT port with its bridge; `eichlerShimura` `proved-mod`; `RamanujanGL`, `ReciprocityGL` and `FunctorialityGL` stated and F1 to F5 done (G1a complete); lab E5 run, with certified instances of `ModularityEllipticQ` | v0.5.0; Vol. 4 checked, Vol. 5 drafted |
| S5 | 2027-11-30 | LLC for GL(2), $p$ odd | `localLanglandsGL2_odd` proved (Target T step 1, 04.12), with Q0 to Q5 **yes**; Target T step 2 stated; F6 for `LocalLanglandsGL` (two reviewers); the decision of 04.12 on Target T, with the reasons | v0.6.0; Vol. 6 checked |
| S6 | 2028-03-31 | $p = 2$, Jacquet-Langlands and the first frontier check | `localLanglandsGL2` for all $p$; `jacquetLanglandsGL2` proved or `proved-mod` with at most five named hypotheses; the Selberg trace formula for compact quotients (tier T7 start); the first R1 report: one self-contained part of a 2026 claim checked, with Q9 (14.1) | v0.7.0; Vols. 1, 3, 4 released; Vol. 8 drafted |
| S7 | 2028-06-30 | the first research result (G4) | Target T step 3, or another node on a route of 04 of the size of a paper lemma, proved in Lean, with a preprint that an outside expert has read | v0.8.0; Vol. 13 first research report |
| S8 | 2028-12-31 | the library to GL(n) (G3, first part) | `localLanglandsGL` `proved-mod` the cohomology of the Lubin-Tate tower; tiers T1 to T6 at least 90% `proved` or `proved-mod`; the G1b statements for split groups stated; Vols. 0 to 7 released | v0.9.0 |
| S9 | open | an open case (G5) | a named open target of 04 proved and all nine trust rows **yes** | v1.0.0 |

The research routes (04) run from S3 on, in parallel with the library.
- From S3 on they take about a third of the agent budget, and more as the library is finished.
- Route R1 starts earlier, at S0, with reading only. The `reader` role builds the claim records of 01.2 and 07.12, and the lab tests their explicit identities (E3, E4, E9).
- Each milestone report says what each route found, including the negative results.

## 15.1 What can slip and what cannot

- **The statements and the trust tooling (S0) cannot slip.** Every later result depends on them.
- **The order of the library can change.** If smooth representations arrive in Mathlib early (the pull requests of 05.1), S3 is shorter. If the anthropics FLT port is cheaper than expected, S4 moves before S3.
- **S3 is the largest risk of the library.** Mathlib has no reductive group schemes, and the project must decide how much of the general theory to build (Q-08). The plan budgets four months and allows split groups only at the milestone.
- **S5 is the largest risk of G2.** The tame parametrization of Bushnell-Henniart is delicate (04.12). The plan budgets three months and allows `proved-mod` with named hypotheses for the ε-factor computations at the milestone. The release is v0.6.0 in both cases, and the milestone report names the hypotheses.
- **S7 is a research milestone.** If no route gives a new result by then, the milestone report says so. The project then re-plans with the experts (02.6).

## 15.2 The budget

- **Agent budget.** It starts at 200 dollars a day (10.6). The owner raises it when the measured cost per proved node shows that it pays.
- **Machines.** The trust workflow, the full builds and the port builds need a rented machine for a few hours each week. The anthropics FLT build is large, at about 1.05 million declarations (05.2).
- **First measurement.** The first measurement of cost per node is an exit criterion of S2.
