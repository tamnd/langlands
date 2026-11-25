# 02. The goal

## 2.1 In one sentence

State the Langlands program in Lean. Prove in Lean the parts that are known, from class field theory to the local Langlands correspondence for $GL_2$ and beyond. Attack the open parts as research bets. Explain each result for students, with its paper, its proof in words and its Lean proof, in public at langlands.tamnd.com.

## 2.2 Why now

Five facts of 2026 make this a project and not a wish. Document 01 has the sources.

1. **The modularity machine is in Lean.**
   - Two FLT projects exist: Imperial FLT (Apache-2.0, Lean v4.35.0) and `anthropics/fermats-last-theorem` (Apache-2.0, September 2026, about 1.05 million declarations, checked by nanoda).
   - Together they hold:
     - quaternionic automorphic forms;
     - concrete Hecke operators;
     - patching;
     - R = T;
     - octahedral Langlands-Tunnell;
     - Wiles' semistable modularity theorem.
   - This is the first non-abelian reciprocity in a proof assistant.
2. **Class field theory is close.**
   - NYLL (n-yamaguchi ClassFieldTheory, Apache-2.0, Lean v4.36.0) proves finite abelian local reciprocity.
   - The riemann-lean release of 2026-11-20 contains global class field theory with the existence theorem, Lubin-Tate theory, Tate's thesis and adelic $GL_n$. That release has no licence, so the project reads it and does not copy it (05.3).
   - Mathlib has the adele ring, Hecke L-functions of characters and root data.
3. **The geometric conjecture is a theorem.**
   - Gaitsgory, Raskin and coauthors proved the unramified geometric Langlands conjecture in characteristic 0, for every reductive $G$, in five papers (2024 to 2026, 947 pages).
   - The local theory has a new centre: Fargues-Scholze parameters. Their compatibility with the classical correspondences was proved case by case in 2025 and 2026 (Cotner-Feng, September 2026).
   - The statements of the field are more stable than ever, and they are ready to be written down.
4. **TauCeti showed that models can build p-adic geometry.**
   - TauCeti is Apache-2.0, AI-written and incubated by the Lean FRO.
   - It finished adic spaces and the adic Fargues-Fontaine curve in October 2026.
   - It has open roadmaps for p-adic local Langlands of $GL_2(\mathbb{Q}_p)$ and for the local Langlands correspondence of $G_2$.
5. **Fresh claims arrive faster than people can check them.**
   - In November 2026 alone:
     - a claimed proof of the twisted weighted fundamental lemma (Halleck-Dube, 2611.26750), which would make Arthur's classification unconditional;
     - new supercuspidal results (Fintzen-Kaletha, 2611.31396; Atobe-Kaletha-Minguez-Shin, 2611.31683);
     - a Lean proof of the Riemann Hypothesis by Alpöge, found with Claude, whose method uses theta lifts and relative trace formulas.
   - The openai/math repository has unrefereed AI-generated claims on geometric Langlands.
   - A Lean check is the strongest test that such a claim can get.

This does not make the open program tractable. Functoriality, the general local correspondence and global reciprocity for $GL_n$ over number fields have been open for fifty years. The strongest mathematicians of each generation have worked on them. The plan treats the open parts as research bets. It makes every other part worth doing if the bets fail.

## 2.3 The levels of success

| Level | Name | What it means | Measured by |
|---|---|---|---|
| G1 | The statements | the main conjectures and theorems of the program are stated in Lean (44 statements, list in 06.2.2), pinned in `manifests/statements.sha256`; F1 to F5 of 06.3 pass; they are bridged to formal-conjectures, anthropics FLT and NYLL where these overlap | `Langlands/Statements/` builds; the fidelity record of each statement |
| G2 | The first formal proofs | GL(1) complete: local and global class field theory, the Weil group, LLC for $GL_1$ and for tori, Tate's thesis, Hecke L-functions. Then LLC for $GL_2$ over a $p$-adic field, first for $p$ odd, then for all $p$ | the trust rows Q0 to Q5 of the top theorems of 14.2 |
| G3 | The library and the handbook | tiers T1 to T8 of document 07 are `proved`, or `proved-mod` with named hypotheses that are published theorems; Volumes 0 to 13 of the handbook are released, each chapter `reviewed` | node counts by tier in `records/status.json`; handbook releases |
| G4 | Frontier checks and new partial results | at least one 2026 preprint (route R1) is checked in Lean, or refuted with a Lean certificate; or a new result of the size of a paper lemma on a route of 04 is proved and read by an outside expert | a node of kind `theorem`, `check` or `counterexample` on a route, with a report or preprint |
| G5 | An open case | one named open target of 04 is proved in Lean: for example a new case of functoriality, LLC for a new family of groups, or modularity of a new class of varieties. All nine trust rows are **yes** | 06.6 and 14 |
| G6 | The program | the general conjectures: `LocalLanglands` for all $G$, `ReciprocityGL` and `Functoriality` over number fields, the ramified and arithmetic geometric conjectures | the same |

G1 to G3 are engineering of known difficulty. G1 and the GL(1) part of G2 are the work of the first six months. G4 is research with a fair chance in two years, because route R1 checks claims that experts already believe. G5 is a research result of paper size. G6 is the program itself and has no date. The milestones (15) are set so that each one finishes a part of G1 to G4. Each milestone report gives the progress on each level separately.

## 2.4 What "all of the open Langlands program" means

The request is to prove all of the open Langlands program. The spec does not promise this. It reads the request as three commitments:

1. **State all of it.** Each open conjecture of documents 03 and 04 has a Lean statement or a written reason why it cannot be stated yet. The reason is usually a missing vocabulary, for example D-modules on $\text{Bun}_G$, or analytic stacks. The missing vocabulary becomes library work in the map.
2. **Prove what is known, in an order that leads to the open parts.** The corpus (07) is the set of papers and books on a path from Mathlib to a theorem of 14.2 or to a node of a route of 04. It is not all of number theory. A paper enters the corpus when a node needs it, and the corpus says why each paper is there. The first list has 204 rows in eleven tiers, T0 to T10.
3. **Work on the open parts in public, with honest status.** Each open target has a node with status `stated`. Each attempt is logged, including the negative results. A claim of an open case follows the policy of 06.6.

## 2.5 Non-goals

- **Not a replacement for Mathlib.** The project sends general parts upstream (09.5). It does not wait for review and does not shape its code to the Mathlib review queue.
- **Not geometric Langlands first.** The proof of GLC needs derived algebraic geometry, ind-coherent sheaves and D-modules on stacks. None of these exists in Lean. Tier T10 is in the corpus and route R8 states the statements, but the formal proof of GLC is not a target of the first two years.
- **Not a claim engine.** The project does not announce the proof of an open case on the strength of a Lean build. 06.6 has the rule.
- **Not a judge of other people's claims.** Route R1 publishes what a Lean check found. If it finds a gap, it writes to the authors first (14.4).
- **Not a copy of unlicensed code.** riemann-lean and math-yiluo/Langlands-lib have no licence. The project reads them and cites them. It does not copy them (05.3).

## 2.6 What would show the plan is wrong

- **The port fails.** If the NYLL port does not build at the pin, or if `LocalReciprocityGL1` needs more than two months after the port, the cost estimates of tiers T1 to T3 are wrong by a factor of two or more. Measured in S1.
- **The statements are not faithful.** If the fidelity battery or the experts find that a statement of 06.2 is wrong in a way that changes its meaning, every node below it must be checked again. Measured in S0 to S2, then at each statement freeze.
- **The infrastructure does not exist.** If smooth representations of $p$-adic groups are not available (from Mathlib or from the project) by S3, the local Langlands layer slips by at least six months.
- **The frontier checks are too expensive.** If route R1 cannot check one self-contained part of a 2026 preprint by S7, the G4 plan is wrong. The project then re-plans with the experts it has met by then.
- **No new result.** If, after LLC for $GL_2$ (S5) and the first frontier check, no route has a new and true node of the size of a paper lemma, the G5 plan is wrong for now. The project keeps the library and the handbook, and reports the result.
