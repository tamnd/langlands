# 04. The open targets and the routes

Spec 2161 has one open problem and many routes to it. This program is the reverse: it has many open problems, and they share their formal infrastructure. Here a **route** is a cluster of open targets that use the same definitions, the same library tiers of document 07, and the same kind of proof. Work on a route builds that infrastructure, and the infrastructure makes the next target of the route cheaper. The sources are in documents 01 and 03 and in the research reports A to F. Claims marked [U] are the project's own guesses.

**The honest view.** Nobody can prove "all of the open Langlands program" on a schedule. Most targets below are rated 4 or 5, which means that experts have no strategy or only a partial one. The project does not promise a date for any of them. The weights of 4.1 buy information: which infrastructure is cheap, which claims survive a formal check, and where a small new result is within reach. Level G5 of document 02 is one named open target of this document proved in Lean. Level G6 is the program, and it is not a plan.

**Each route section gives:** the idea; what is known; the open targets, named `O-Rk-n`, with a difficulty from 1 (within reach of current methods) to 5 (no plausible strategy); the first nodes that the project can state now (map nodes `LG-...` in `blueprint/nodes/`, document 08); the key obstruction, for the formalization and for the mathematics; the first weight.

The difficulties come from the research reports:
- C §5 uses the scale 1 to 5;
- A §3 uses E, M and H, and this document maps them to 2, 3 to 4, and 5;
- B §4 and D §7 have no rating, so the ratings for those targets are the project's own and are tagged [U].

For targets in R1 a second number gives the cost of the formal check. That cost is a different question from the difficulty of the mathematics.

## 4.1 Summary

| Route | Cluster | Known up to (2026-11-25) | Key obstruction | First weight |
|---|---|---|---|---|
| R1 | formal checks of fresh 2026 claims | the claims exist as preprints; none has a Lean proof | the claims rest on foundations that are not in Lean; a check must find a self-contained part | 0.20 |
| R2 | explicit LLC for small groups and low depth | $\mathrm{GL}_2$ (local proof), $\mathrm{SL}_2$, $\mathrm{GSp}_4$, $G_2$, regular and non-singular supercuspidals, depth zero | smooth representation theory of $p$-adic groups is absent from Mathlib; small $p$ is open | 0.15 |
| R3 | modularity and automorphy lifting | $E/\mathbb{Q}$; real quadratic to quartic fields; imaginary quadratic in many cases; 11.9% of abelian surfaces over $\mathbb{Q}$ | Galois representations of automorphic forms need Shimura varieties; non-regular weight | 0.15 |
| R4 | Ramanujan bounds | Deligne; regular algebraic cases; $7/64$ for $\mathrm{GL}_2/\mathbb{Q}$ | no method for Maass forms | 0.05 |
| R5 | trace formula and Beyond Endoscopy | Selberg, Arthur, Ngô; Beyond Endoscopy for $\mathrm{GL}_2/\mathbb{Q}$ | the trace formula has no Lean; Beyond Endoscopy has given no new transfer | 0.10 |
| R6 | functoriality cases and converse theorems | the transfers of 03.5 | non-endoscopic transfers without Galois input | 0.10 |
| R7 | function fields | $\mathrm{GL}_n$ (L. Lafforgue); automorphic to Galois for all $G$ | shtukas and étale cohomology of stacks | 0.05 |
| R8 | geometric Langlands | GLC in char 0, unramified, de Rham | derived algebraic geometry is absent from Lean; six open problems of GLC V | 0.05 |
| R9 | $p$-adic and mod $p$ | $\mathrm{GL}_2(\mathbb{Q}_p)$, categorical for $p \ge 5$ | $(\varphi,\Gamma)$-modules and the Emerton-Gee stack are absent from Lean | 0.10 |
| Lab | computation lab (4.11, document 13) | LMFDB, Sage, PARI, Magma | data is not proof | 0.05 |

The weights set the share of the research budget of the agent (10.6) for the first year. Library work for levels G1 to G3 is outside this budget. The weights change at each milestone report (document 15), from proved, refuted and stalled nodes. The weights are higher where a route has a cheap first node that also serves G2 or G3 (R2, R3), or where the information value is high and the check is cheap (R1).

## 4.2 R1: formal checks of fresh 2026 claims

**Idea.** In 2026 strong results appear faster than referees read them, and some come from AI systems with no human author. A formal check of a self-contained part is new evidence that no referee can give. The route does not try to formalize a whole 190-page paper. For each claim it does four things:
1. it writes a claim record (07.11) with the date and the status;
2. it states the main theorem in Lean as a `def ... : Prop` with status `claimed`;
3. it maps the dependencies;
4. it picks the smallest part that is new, self-contained and checkable. That part can be a finite computation, a combinatorial lemma, a statement about finite groups, or an implication between named hypotheses.

**What is known.** The claims and their state, from reports A, B, C and D [P]:

| Id | Claim | What it says | Math | Formal check |
|---|---|---|---|---|
| O-R1-1 | Halleck-Dube, arXiv:2611.26750 (2026-11-19) | twisted weighted fundamental lemma in good characteristic, so Arthur's classification is unconditional | 5 (if open) | 5: Hitchin fibration, perverse sheaves |
| O-R1-2 | Gaitsgory-V. Lafforgue-Raskin, arXiv:2603.26925 and the ICM 2026 announcement | Arthur-Ramanujan for unramified forms over function fields | 3 | 5: GLC foundations |
| O-R1-3 | Cotner-Feng, arXiv:2609.16381 and 2609.16387 | FS parameters on Yu's supercuspidals equal Kaletha's on inertia; finite fibres | 4 | 5 for the whole; 3 for the Kaletha side (part I) |
| O-R1-4 | Fintzen-Kaletha, arXiv:2611.31396 (2026-11-23) | supercuspidals and types through double covers and the Fourier-Weil representation | 3 | 3: finite Heisenberg groups and Weil representations, Moy-Prasad quotients |
| O-R1-5 | Atobe-Kaletha-Mínguez-Shin, arXiv:2611.31683 | local intertwining relation for inner forms of $\mathrm{GL}_N$ | 4 | 5: trace formula input |
| O-R1-6 | Dowd, arXiv:2610.25055 | categorical $p$-adic LLC on the 3-adic Steinberg block of $\mathrm{GL}_2(\mathbb{Q}_3)$ | 4 | 5: $\infty$-categories of ind-coherent sheaves |
| O-R1-7 | openai/math families 014 and 069 (October 2026) | restricted GLC in char $p$ on all components; global quantum GLC at irrational level | 4 | 2 for the statements; 5 for the proofs; no Lean in `lean/formalization.yaml` |
| O-R1-8 | Alpöge, riemann-lean (2026-11-20) | RH (certified 2026-11-21) and GRH for Dirichlet L-functions; the proof uses theta lifts between unitary groups, GGP periods and a relative trace formula | solved if correct | 2 to 3 for the cross-check of the Langlands statements it proves |

Other new preprints go to the watch list of 07.10 with a claim record but no node. These are Luo-Stevens 2608.20225, Takanashi 2609.19439, 2609.19430 and 2611.06742, Dieulefait 2611.32569, and Lomelí 2610.23985.

**First nodes.** `LG-claim-twfl`, `LG-claim-glr-ar`, `LG-claim-cf`: the three statements with status `claimed`, stated over the library vocabulary of 06. The parts that need missing foundations are stated as named hypotheses; `LG-claim-fk-weil`: the finite group core of Fintzen-Kaletha: the twisted Heisenberg-Weil representation and its character, over a finite field of odd characteristic; `LG-cross-rl-cft`, `LG-cross-rl-tate`: the global reciprocity map and Hecke's functional equation from riemann-lean (03.12), restated in the project's vocabulary. The project then proves them from its own library (route of G2) and compares. riemann-lean has no licence, so the project reads it and does not copy it (05).

**Key obstruction.** For the formalization: most claims sit on top of foundations that Lean does not have, so the check reaches only an edge of the claim. For the mathematics: a check of a part is not a check of the claim. The record must say exactly which part was checked (14.3).

**First weight: 0.20.** It is the highest weight because the information per dollar is high. A refuted lemma is news, and a checked lemma is a strong signal to the experts. Most of the cost is the reader and stater roles (10.3), not the prover.

## 4.3 R2: explicit LLC for small groups and low depth

**Idea.** Build the local theory from the bottom up: smooth representations, types, supercuspidals, and the explicit correspondence. The route ends at classes of groups and representations where an explicit LLC is known or nearly known, and it pushes at the edges: small $p$, wild ramification, non-split groups, exceptional groups.

**What is known.** $\mathrm{GL}_2$ has a purely local proof (Kutzko; Bushnell-Henniart 2006) [S]; $\mathrm{SL}_2$ and the inner forms follow by restriction (Labesse-Langlands, Gelbart-Knapp) [S]; $\mathrm{U}(1,1)$ and other small unitary groups follow by theta and base change [U]; $\mathrm{GSp}_4$ is due to Gan-Takeda (Annals 2011) [S], and $G_2$ to Gan-Savin (arXiv:2209.07346) with Takanashi's 2026 work [P]; Kaletha's regular (JAMS 2019) and non-singular supercuspidals give an explicit LLC for tame groups with $p \nmid |W|$ [P]; for depth zero there are DeBacker-Reeder (2009) and Solleveld-Xu (arXiv:2411.19846) [S] [P]; Fintzen proved exhaustion of Yu's construction for $p \nmid |W|$. Fintzen-Schwein (arXiv:2501.18553) treat $p = 2$ [P].

**Open targets.**

| Id | Target | Difficulty |
|---|---|---|
| O-R2-1 | Kaletha's explicit LLC equals the classical LLC wherever both exist (B §4 row 5) | 4 [U] |
| O-R2-2 | exhaustion and parametrization of supercuspidals for small $p$, including $p = 2, 3$ for $G_2$ (B §4 row 6) | 4 [U] |
| O-R2-3 | an LLC for $F_4$, $E_6$, $E_7$, $E_8$ beyond special classes (B §4 row 14) | 5 [U] |
| O-R2-4 | a characterization of LLC for general $G$ without global input (B §4 row 2) | 5 [U] |
| O-R2-5 | the formal degree conjecture for all $G$ (B §4 row 11) | 4 [U] |
| O-R2-6 | the first machine-checked LLC for $\mathrm{GL}_2(F)$, $p$ odd (known mathematics; a G2 milestone, not research) | 2 formal |

**First nodes** (from the ingredient list of research B §5.4): `LG-smooth-rep`: smooth and admissible representations, after Mathlib PRs #41520, #41525 and #45067; `LG-ind-jacquet`: parabolic induction and Jacquet modules, with Frobenius reciprocity; `LG-gl2-nonsc`: the classification of the non-cuspidal irreducibles of $\mathrm{GL}_2(F)$; `LG-gl2-types`: strata, simple characters and types for $\mathrm{GL}_2$; `LG-admissible-pairs`: admissible pairs $(E/F, \xi)$ and the tame parametrization for $p \neq 2$; `LG-llc-gl2`: `LocalLanglandsGL 2` (06); `LG-g2-roadmap`: the statement of LLC for $G_2$, aligned with TauCeti roadmap PR #2458 (opened 2026-11-16).

**Key obstruction.** For the formalization: $\varepsilon$-factors of Weil group representations (Deligne-Langlands) are the expensive item. Bushnell-Henniart avoid the general theory for $n = 2$, and the project follows them. Moy-Prasad filtrations need Bruhat-Tits buildings, which no Lean library has. For the mathematics: the edges (small $p$, exceptional groups, uniqueness) are open because the explicit methods need tame hypotheses.

**First weight: 0.15.** The route shares almost all its nodes with G2, so its first research steps are nearly free once LLC for $\mathrm{GL}_2$ is done.

## 4.4 R3: modularity and automorphy lifting

**Idea.** Prove Galois to automorphic by deformation theory: show $R = \mathbb{T}$ by Taylor-Wiles-Kisin patching, then switch primes or use potential automorphy. Two Lean FLT projects (Imperial FLT, anthropics FLT) have done this route in part, with Apache-2.0 code (document 05).

**What is known.** Elliptic curves over $\mathbb{Q}$ (BCDT), and over real quadratic, totally real cubic and totally real quartic fields without $\sqrt5$ [S]; over imaginary quadratic fields with $X_0(15)(F)$ finite (Caraiani-Newton, arXiv:2301.10509 v4, accepted 2026-10-20) [P]; potential modularity over totally real and CM fields (ACC+, Annals 2023) [S]; a positive proportion of abelian surfaces over $\mathbb{Q}$ (BCGP, arXiv:2502.20645) [P]; Dieulefait (arXiv:2611.32569) passes from potential modularity to modularity lifting over totally real fields [P].

**Open targets.**

| Id | Target | Difficulty |
|---|---|---|
| O-R3-1 | modularity of all elliptic curves over all number fields (C §5 row 3) | 3 to 4 |
| O-R3-2 | modularity of all abelian surfaces over $\mathbb{Q}$, the paramodular conjecture (C §5 row 4) | 3 |
| O-R3-3 | modularity lifting for small or highly ramified $p$ and non-regular weight (C §5 row 19) | 3 |
| O-R3-4 | reciprocity for $\mathrm{GL}_n$ over $\mathbb{Q}$, Galois to automorphic, in general (C §5 row 1) | 4 |
| O-R3-5 | Fontaine-Mazur beyond $\mathrm{GL}_2/\mathbb{Q}$ (C §5 row 7) | 4 to 5 |
| O-R3-6 | Artin for even icosahedral $\rho$ over $\mathbb{Q}$ (C §5 row 8) | 4 |

**First nodes.** `LG-patching`: the abstract patching theorem as pure commutative algebra, ported from Imperial FLT; `LG-wiles-criterion`: Wiles's numerical criterion and congruence modules (after Iyengar-Khare-Manning, ICM 2026); `LG-galrep`: continuous Galois representations and "the Galois representation attached to an eigenform" as a predicate; `LG-mod-ell-q`: `ModularityEllipticQ` (06), bridged to `modularity_of_semistableModel` in anthropics FLT and to `ModularityConjecture` in formal-conjectures.

**Key obstruction.** For the formalization:
- Deligne's construction of Galois representations is far more than 500,000 lines with a full proof (research E §7.2) [U];
- the general case needs Shimura varieties and perfectoid methods.

The route therefore states those inputs as `proved-mod` hypotheses (Eichler-Shimura, Deligne, Carayol) and proves the algebra around them.

For the mathematics: no Galois representation is known for fields with a complex place that are not CM, and patching fails outside regular weight without new ideas.

**First weight: 0.15.**

## 4.5 R4: Ramanujan bounds

**Idea.** Ramanujan follows from functoriality of all symmetric powers (03.7). Partial functoriality gives partial bounds. Kim-Sarnak used $\mathrm{Sym}^4$ to get $7/64$ for $\mathrm{GL}_2/\mathbb{Q}$.

**What is known.** Deligne for holomorphic forms. The regular algebraic self-dual cases over totally real and CM fields. Cohomological $\mathrm{GL}_2$ over CM fields (BCGNT 2309.15880; Matsumoto 2312.01551). $\mathrm{GL}_n$ over function fields. Getz-Hahn-Yao (2509.14381) reduce Ramanujan to the analytic properties of triple product L-functions [P].

**Open targets.**

| Id | Target | Difficulty |
|---|---|---|
| O-R4-1 | Ramanujan for Maass forms on $\mathrm{GL}_2/\mathbb{Q}$ (C §5 row 9) | 5 |
| O-R4-2 | Selberg's eigenvalue conjecture $\lambda_1 \ge 1/4$ (C §5 row 10) | 5 |
| O-R4-3 | Ramanujan for regular algebraic $\pi$ beyond the self-dual and $\mathrm{GL}_2$ cases (C §5 row 9) | 3 |
| O-R4-4 | an improvement of $7/64$ | 5 [U] |

**First nodes.** `LG-ramanujan`: `RamanujanGL` (06); `LG-ramanujan-tau`: the bridge to `RamanujanTau` in formal-conjectures; `LG-symn-to-ram`: the theorem "automorphy of $\mathrm{Sym}^m \pi$ for all $m$ implies Ramanujan at unramified places", by Rankin-Selberg and Landau's lemma. It is a clean implication with named analytic hypotheses, and it is provable early [U].

**Key obstruction.** Every known bound for Maass forms comes from functoriality of small symmetric powers, and the next one ($\mathrm{Sym}^5$, $\mathrm{Sym}^6$) is open. The weight is low for this reason.

**First weight: 0.05.**

## 4.6 R5: the trace formula and Beyond Endoscopy

**Idea.** The trace formula compares spectral and geometric data. It gives Jacquet-Langlands, base change, Langlands-Tunnell and the endoscopic classification. Beyond Endoscopy (Langlands 2004) tries to detect poles of $L(s, \pi, r)$ in a limit of the stable trace formula, and so to reach functoriality in general.

**What is known.** Selberg's formula for cocompact lattices; Arthur's invariant and stable formulas, and Ngô's fundamental lemma (arXiv:0801.0446) [P]; Beyond Endoscopy for the standard representation of $\mathrm{GL}_2/\mathbb{Q}$: Altuğ in the unramified case, and the five-part series of Cheng in the ramified case (2505.18967 to 2608.15553) [S] [P]; first steps for $\mathrm{GL}_3/\mathbb{Q}$ (Deng-Espinosa, arXiv:2603.21506) [P].

**Open targets.**

| Id | Target | Difficulty |
|---|---|---|
| O-R5-1 | a new case of functoriality from Beyond Endoscopy (C §5 row 14) | 5 |
| O-R5-2 | Beyond Endoscopy for $\mathrm{Sym}^2$ through the simple trace formula (arXiv:2607.25383) | 4 [U] |
| O-R5-3 | an independent check of the TWFL (with O-R1-1) | 5 |

**First nodes.** `LG-tf-finite`: the trace formula for a finite group acting on functions on a finite set, as a teaching statement; `LG-tf-selberg`: the Selberg trace formula for a cocompact discrete subgroup of a unimodular group, with trace class as a hypothesis; `LG-orbital-gl2`: orbital integrals for $\mathrm{GL}_2(F)$; `LG-fl`: `FundamentalLemma` (06), as a statement and then as a `proved-mod` node.

**Key obstruction.** For the formalization: nothing exists. riemann-lean has 493 lines (research E §3.5). Arthur's formula for $\mathrm{GL}_2$ alone is 100,000 lines or more [U]. For the mathematics: in Beyond Endoscopy the main terms are controlled, but the error terms in the limit are not, beyond $\mathrm{GL}_2$.

**First weight: 0.10.** It is low compared with its importance, because the first nodes are library work (G3) and are paid from the library budget.

## 4.7 R6: functoriality cases and converse theorems

**Idea.** Prove a transfer $\pi \mapsto \Pi$ by showing that the candidate $\Pi$ has the right twisted L-functions (converse theorems of Hecke, Weil, Jacquet-Piatetski-Shapiro-Shalika and Cogdell-Piatetski-Shapiro), or by Galois methods (Newton-Thorne).

**What is known.** The transfers of 03.5. Matringe (arXiv:2409.20240) proves a local converse theorem for split $G$ with acceptable dual, and shows that it fails for $\mathrm{SO}_{2n}$, $n \ge 3$ [P].

**Open targets.**

| Id | Target | Difficulty |
|---|---|---|
| O-R6-1 | functoriality in general (C §5 row 11) | 5 |
| O-R6-2 | $\mathrm{GL}_m \times \mathrm{GL}_n \to \mathrm{GL}_{mn}$ beyond the known cases | 5 [U] |
| O-R6-3 | $\mathrm{Sym}^5$ of a Maass form | 5 |
| O-R6-4 | converse theorems beyond $\mathrm{GL}_n$ (B §4 row 16) | 4 [U] |
| O-R6-5 | symmetric power functoriality over CM fields | 4 [U] |

**First nodes.** `LG-functoriality`: `Functoriality` (06), with L-homomorphisms; `LG-hecke-converse`: Hecke's converse theorem for level 1, from Mathlib's L-function of a modular form and its functional equation. It is within reach now [U]; `LG-weil-converse`: Weil's converse theorem for $\Gamma_0(N)$; `LG-rankin-selberg`: Rankin-Selberg for $\mathrm{GL}_2 \times \mathrm{GL}_2$.

**Key obstruction.** Converse theorems need the analytic control of all twisted L-functions of the candidate. That is known only when the candidate comes from a construction (Langlands-Shahidi or Galois). New transfers need new constructions.

**First weight: 0.10.**

## 4.8 R7: function fields

**Idea.** Over a function field the program is close to complete for $\mathrm{GL}_n$, and it is open with ramification for general $G$. Shtukas replace Shimura varieties.

**What is known.** 03.8.

**Open targets.**

| Id | Target | Difficulty |
|---|---|---|
| O-R7-1 | Galois to automorphic for general $G$ with ramification (C §5 row 16) | 3 |
| O-R7-2 | the Arthur multiplicity formula over function fields (C §5 row 17; A §3 row 18) | 3 |
| O-R7-3 | the remaining components of $\mathrm{LS}^{\mathrm{restr}}$ in Gaitsgory-Raskin (with O-R1-7) | 3 to 4 |

**First nodes.** `LG-ff-statements`: L. Lafforgue's bijection and V. Lafforgue's decomposition, as statements; `LG-ff-cft`: class field theory for global function fields, from NYLL; `LG-ff-drinfeld-gl2`: Drinfeld's $\mathrm{GL}_2$ theorem, as a statement.

**Key obstruction.** Étale cohomology of stacks of shtukas and geometric Satake are far from Lean.

**First weight: 0.05.**

## 4.9 R8: geometric Langlands

**Idea.** State GLC (Theorem 3.5) and the six problems of GLC V. Prove the abelian case: geometric class field theory.

**Open targets** (A §3; the letters E, M and H are mapped to numbers as in the introduction):

| Id | Target | Difficulty |
|---|---|---|
| O-R8-1 | restricted $\ell$-adic GLC in char $p$, all components (A row 3; claimed in O-R1-7) | 3 to 4 |
| O-R8-2 | tame (Iwahori) global GLC (A row 5) | 3 to 4 |
| O-R8-3 | wild ramification, local (A row 6) | 5 |
| O-R8-4 | wild ramification, global (A row 7) | 5 |
| O-R8-5 | quantum GLC, global (A row 12; claimed at irrational level in O-R1-7) | 3 to 4 |
| O-R8-6 | GLC for the Fargues-Fontaine curve (A row 15) | 5 |
| O-R8-7 | Dolbeault GLC beyond $\mathrm{GL}_2$ with reduced spectral curves (Toda, arXiv:2602.09359) (A row 14) | 3 to 4 |

**First nodes.** `LG-gcft`: geometric class field theory for $\mathrm{GL}_1$: the Abel-Jacobi map, and the descent of a rank one local system to $\mathrm{Pic}$. It needs only schemes and Picard groups; `LG-gl1-eigensheaf`: the Hecke eigensheaf property for $\mathrm{GL}_1$; `LG-glc`: `GeometricLanglands` (06), as a placeholder statement until the foundations exist.

**Key obstruction.** D-modules, IndCoh, derived stacks and $\mathrm{Bun}_G$ are absent from Lean. They are several hundred thousand lines of foundations (research E §7.6) [U].

**First weight: 0.05.** The handbook (Volume 13, document 11) covers this area much more than the Lean work does.

## 4.10 R9: $p$-adic and mod $p$

**Idea.** Build the objects of the $\mathrm{GL}_2(\mathbb{Q}_p)$ theory: étale $(\varphi,\Gamma)$-modules, Colmez's functor, the mod $p$ classification, Serre weights and Galois deformation rings. Align with TauCeti's roadmap `PadicLocalLanglandsForGL2Qp` (a plan of 2,629 lines) rather than duplicate it.

**What is known.** 03.10 and research D §7.

**Open targets.**

| Id | Target | Difficulty |
|---|---|---|
| O-R9-1 | $p$-adic LLC for $\mathrm{GL}_2(K)$, $K \neq \mathbb{Q}_p$ (D row 1) | 5 [U] |
| O-R9-2 | categorical $p$-adic LLC beyond $\mathrm{GL}_2(\mathbb{Q}_p)$, and for $p = 2, 3$ in full (D row 3) | 4 to 5 [U] |
| O-R9-3 | mod $p$ Langlands: the local nature of $\pi(\bar\rho)$ (D row 4) | 4 [U] |
| O-R9-4 | Serre weights for $\mathrm{GL}_n$, non-generic and ramified cases (D row 5) | 4 [U] |
| O-R9-5 | Breuil-Mézard: large weight, ramified $K$, non-generic (D row 6) | 4 [U] |

**First nodes.** `LG-phigamma`: étale $(\varphi,\Gamma)$-modules over $\mathbb{Q}_p$ and Fontaine's equivalence; `LG-modp-gl2`: the classification of irreducible smooth mod $p$ representations of $\mathrm{GL}_2(\mathbb{Q}_p)$ (Barthel-Livné, Breuil); `LG-serre-weights`: Serre weights as representations of $\mathrm{GL}_2(\mathbb{F}_q)$, and Herzig's recipe as a combinatorial statement; `LG-def-functor`: Galois deformation functors and their representability.

**Key obstruction.** For the formalization:
- the categorical statements need $\infty$-categories of ind-coherent sheaves on formal algebraic stacks;
- perfectoid fields are still a draft Mathlib PR (#26389, 13 sorries).

For the mathematics: no construction of $\Pi(\rho)$ is known for $K \neq \mathbb{Q}_p$.

**First weight: 0.10.**

## 4.11 The computation lab as a method, not a route

The lab (document 13) serves all routes:
- it pulls examples from LMFDB and checks them with Sage, PARI/GP and Magma: Hecke eigenvalues, Satake parameters, conductors, root numbers and Sato-Tate histograms;
- it builds tables of explicit supercuspidals of $\mathrm{GL}_2(\mathbb{Q}_p)$ for small $p$ and their parameters;
- it tests the Lean statements of 06 on certified examples (fidelity check F4 of 06.3).

A misformalized statement often fails on the first example. The lab gives data, not proofs. A computation enters the map only as a Lean-checked certificate (13.4). For example, the first eigenvalues of $\Delta$ checked against the Lean definition of $T_n$, or a congruence between two forms checked by Sturm's bound.

**Weight: 0.05.**

## 4.12 A candidate first research target [U]

This section is a guess by the project. No expert has read it yet (16.1).

**Target T: the Fintzen-Kaletha construction for $\mathrm{GL}_2$ and $\mathrm{SL}_2$, checked against the tame LLC of Bushnell-Henniart, in Lean.** The target has three steps.
1. **G2 anchor (R2, O-R2-6).** Prove `LocalLanglandsGL 2` in Lean for $p$-adic $F$ with $p$ odd, end to end. The proof follows Bushnell-Henniart: the non-cuspidal classification, types, admissible pairs, the tame parametrization with the character $\Delta_\theta$, and the converse theorem for $\mathrm{GL}_2$ for uniqueness. The $\varepsilon$-factors of the Weil group side are restricted to dimension at most 2, where Bushnell-Henniart give a local treatment.
2. **The finite core of a 2026 claim (R1, O-R1-4).** State the construction of supercuspidal types of Fintzen-Kaletha (arXiv:2611.31396, 2026-11-23) for tame $G$. Prove its finite group core in Lean, the twisted Heisenberg-Weil representation of the double cover, over $\mathbb{F}_q$ with $q$ odd.
3. **The comparison (G4).** Prove in Lean that for $G = \mathrm{GL}_2$ the Fintzen-Kaletha supercuspidals are the Bushnell-Kutzko ones. Then prove that Kaletha's regular LLC, with the Fintzen-Kaletha-Spice twist, gives the same parameters as the Bushnell-Henniart rectifier. Then prove the same for $\mathrm{SL}_2$ and its L-packets.

**Why this target.**
- It is mostly finite and algebraic. Depth and Moy-Prasad filtrations for $\mathrm{GL}_2$ need only lattice chains, not general buildings. No step needs Shimura varieties, $p$-adic Hodge theory or the trace formula.
- Step 1 is G2 work, so step 3 costs little extra.
- Step 3 is a first machine check of a construction published two days before this spec. For $\mathrm{GL}_n$ the comparison is known on paper (Oi-Tokimoto, arXiv:1912.07851), so the target tests the claim against a known answer and has a clear success criterion.
- If a sign or a character does not match, the project has found a correction. The double cover and its sign are where such errors live. Either result is worth a short note.
- The route continues: $\mathrm{U}(1,1)$, then depth zero for general $G$, then the edge of O-R2-1.

**What would make it fail.**
- Step 1 can be far larger than estimated. The tame parametrization uses Gauss sums and $\lambda$-factors in a delicate way.
- Fintzen-Kaletha can use structure that has no simple form for $\mathrm{GL}_2$.
- The comparison is perhaps already in the paper for $\mathrm{GL}_n$, and then step 3 is a check, not a new result. It is still a G4 frontier check, but not a new theorem.

The milestone report of S5 (document 15) decides whether T stays.

**Second candidate.** If T fails, `LG-symn-to-ram` (R4) and `LG-hecke-converse` (R6) are small theorems that the project can prove early. They are not new mathematics. They are the first steps of the analytic side.

## 4.13 What the weights buy

In the first year the project measures, for each route:
- the cost per proved node;
- the number of nodes that reach `proved` against the number that stall at `proved-mod`;
- the number of claims checked or corrected.

A route with no progress for two milestones loses half its weight to the route with the best cost per node. The milestone report says so in plain terms. A route with a new result of the size of a paper lemma, read by an outside expert, gets the first call on a raised budget (16, Q on budget). The project reports a negative result (a stalled route, a claim that a check could not reach) with the same care as a positive one.
