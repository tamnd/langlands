# 07. The corpus: the theories and papers to formalize

This is the list that "all the theory of the Langlands program" means in document 02. Each row is a paper or a book that some node of the map needs, with the reason it is needed. The tiers are in dependency order. A tier uses only the tiers above it, except where a row says otherwise. This is the first version of the list. It grows when a node needs a new source, and each addition names the node that asked for it.

The sources are the reports A to F in `research/sources/`. The tags [P], [S], [U] are those of document 01. They apply to the bibliographic facts of the row, not to the truth of the theorem. Every [S] and [U] row is a task for the `reader` role (document 10) before a node depends on it.

The column **Lean** says what exists in Lean on 2026-11-25. **ML**: in Mathlib (5.1). **PR**: in an open Mathlib pull request. **NY**: NYLL. **IF**: Imperial FLT. **AF**: anthropics/fermats-last-theorem. **TC**: TauCeti. **eps**: epsilon_FML or epsilon_SML. **PM**: PadicModForms. These sources are portable (5.2). **rl**: riemann-lean. **LL**: math-yiluo/Langlands-lib. These two are read only (5.3). **fc**: a statement in formal-conjectures. **none**: nothing found.

The column **Use** is the plan of the project. **reuse**: use the Mathlib result as it is. **prove**: a full formal proof. **port**: a proof ported from a source of 5.2, then checked. **state**: a Lean statement, used as a `proved-mod` hypothesis until it is proved (09.2.2). **ex**: certified examples (document 13). **read**: a source of ideas, definitions and handbook text, with no theorem in the map.

The column **Pri** is the priority. **A**: needed before milestone S5 (document 15). **B**: needed by the routes of document 04 in the first two years. **C**: later, or only for the handbook.

## 7.1 Tier T0: references

The standard texts that define the language. They enter the map through definitions and through the handbook (document 11), not through theorems.

| Id | Work | What it gives | Lean | Use | Pri | Tag |
|---|---|---|---|---|---|---|
| T0-01 | Langlands, letter to Weil (January 1967), IAS archive publications.ias.edu/rpl | the origin of the L-group and of functoriality | none | read | C | [P] |
| T0-02 | Langlands, "Problems in the theory of automorphic forms", LNM 170 (1970) | the first published statement of the conjectures | none | read | B | [P] |
| T0-03 | Borel and Casselman (eds.), Corvallis, PSPUM 33.1 and 33.2 (1979) | Borel's "Automorphic L-functions", Tate's "Number theoretic background", Borel-Jacquet; the reference definitions of 06.1 | fc (Borel-Jacquet form) | read | A | [P] |
| T0-04 | Cassels and Fröhlich (eds.), *Algebraic Number Theory*, 2nd ed. LMS (2010) | Serre and Tate on CFT, Tate's thesis, the exercises | none | read | A | [S] |
| T0-05 | Neukirch, *Algebraic Number Theory*, Grundlehren 322 (1999) | valuations, CFT, zeta and L-functions | partly ML | read | A | [P] |
| T0-06 | Serre, *Local Fields*, GTM 67 (1979) | ramification, group cohomology, local CFT | partly ML | read | A | [U] |
| T0-07 | Milne, *Class Field Theory*, course notes v4.03 (2020) | Lubin-Tate, cohomological local and global CFT; the base text of Vol. 3 | none | read | A | [P] |
| T0-08 | Bump, *Automorphic Forms and Representations*, CSAM 55 (1997) | GL(1), GL(2) local and global, Rankin-Selberg | none | read | A | [P] |
| T0-09 | Getz and Hahn, *An Introduction to Automorphic Representations*, GTM 300 (2024) | algebraic groups, adeles, automorphic representations, trace formulae; the main textbook of Vols. 5 and 8 | none | read | A | [P] |
| T0-10 | Bushnell and Henniart, *The Local Langlands Conjecture for GL(2)*, Grundlehren 335 (2006) | the full local proof for $GL_2$; the plan of S5 | none | read | A | [P] |
| T0-11 | Diamond and Shurman, *A First Course in Modular Forms*, GTM 228 (2005) | Hecke theory, Eichler-Shimura, the modularity statement | partly ML | read | A | [P] |
| T0-12 | Arthur, Ellwood, Kottwitz (eds.), Clay Math. Proc. 4 (2005) | Arthur's introduction to the trace formula, Milne on Shimura varieties | none | read | B | [P] |
| T0-13 | Chaudouard, Gan, Kaletha, Sakellaridis (eds.), *The Langlands Program*, PSPUM 112.1 to 112.3 (2025), the IHES 2022 school | the current surveys of every part | none | read | B | [P] |
| T0-14 | Milne, *Algebraic Groups*, CSAM 170 (2017); Conrad, "Reductive group schemes", Panoramas et Synthèses 42-43 | algebraic and reductive groups over a field and over a base | none (rl, LL) | read | A | [P] |
| T0-15 | Kaletha and Prasad, *Bruhat-Tits Theory: A New Approach*, CUP (2023) | buildings and parahoric subgroups | none (LL) | read | B | [P] |
| T0-16 | Buzzard and Gee, "The conjectural connections between automorphic representations and Galois representations", arXiv:1009.0785 | C-algebraic and L-algebraic; the precise form of `ReciprocityGL` | none | read | A | [U] |

## 7.2 Tier T1: number fields, local fields and adeles

| Id | Work | What it gives | Lean | Use | Pri | Tag |
|---|---|---|---|---|---|---|
| T1-01 | valuations, completions, places (Neukirch, Chapter II) | the completions $K_v$ | ML | reuse | A | [P] |
| T1-02 | nonarchimedean local fields: structure, unit filtrations $U^{(n)}$ (Serre, *Local Fields*, Chapters I to IV) | `IsNonarchimedeanLocalField` and its API | ML, partly | prove | A | [P] |
| T1-03 | ramification groups, upper numbering, Herbrand's functions (Serre, Chapter IV) | the conductors of T5 | ML (`RamificationGroup`, lower numbering only) | prove | A | [P] |
| T1-04 | Hasse-Arf theorem (Serre, Chapter V) | integrality of the upper jumps for abelian extensions; local conductors of characters | none (rl `ArtinConductor`) | prove | A | [U] |
| T1-05 | adeles and ideles of a number field | `NumberField.AdeleRing`, `IdeleClassGroup` | ML | reuse | A | [P] |
| T1-06 | local compactness of the adeles, strong approximation | Haar measure on $\mathbb{A}_K$, the compactness of $\mathbb{A}_K^1/K^\times$ | none (smmercuri, licence not checked) | prove | A | [U] |
| T1-07 | finiteness of the class group, Dirichlet's unit theorem | the compactness of the norm one idele class group | ML | reuse | A | [P] |
| T1-08 | self-dual Haar measures and Pontryagin duality of $K_v$ and $\mathbb{A}_K$ (Tate 1950) | Fourier analysis for Tate's thesis | partly ML | prove | A | [U] |
| T1-09 | adeles of a global function field | the correct construction (the Mathlib docstring warns) | none | prove | B | [P] |
| T1-10 | infinite Galois theory, Krull topology | $\mathrm{Gal}(K^{sep}/K)$ as a profinite group | ML | reuse | A | [P] |
| T1-11 | unramified extensions, Witt vectors, the maximal unramified extension $K^{ur}$ | Frobenius, the Weil group of T3 | ML (Witt vectors), none for $K^{ur}$ | prove | A | [P] |
| T1-12 | Krasner's lemma; finitely many extensions of a given degree | the local Galois group is topologically finitely generated | none | prove | B | [U] |
| T1-13 | Dedekind zeta, the class number formula | the analytic base of T3 | ML | reuse | A | [P] |
| T1-14 | Riemann-Roch for curves over $\mathbb{F}_q$, the zeta function of a curve | the base of T10 and of route R7 | none | prove | B | [U] |
| T1-15 | Chebotarev density | the density theorems used by strong multiplicity one and by `SatoTate` | TC (roadmap complete) | port | A | [P] |

## 7.3 Tier T2: algebraic and reductive groups, root data, L-groups

| Id | Work | What it gives | Lean | Use | Pri | Tag |
|---|---|---|---|---|---|---|
| T2-01 | root data and root systems (Bourbaki, *Lie* IV to VI; Springer) | `RootDatum`, the dual root datum | ML | reuse | A | [P] |
| T2-02 | classification of reduced root systems, including $G_2$ | the Dynkin types | ML (`Finite/G2`) | reuse | A | [P] |
| T2-03 | linear algebraic groups over a field (Milne 2017) | Borel subgroups, maximal tori, the structure theorem | none | prove | A | [P] |
| T2-04 | reductive group schemes over a base (SGA3; Conrad) | the groups of the global statements | none (rl, LL) | state | B | [P] |
| T2-05 | Chevalley's existence and isomorphism theorems | a split reductive group from a root datum | none | state | A | [P] |
| T2-06 | tori, character and cocharacter groups; duality of tori | the L-group of a torus | none | prove | A | [P] |
| T2-07 | quasi-split forms, inner forms, $H^1(F, G)$, Kottwitz's map | the parametrization of inner forms in `LocalLanglands` | none | state | B | [S] |
| T2-08 | the dual group $\hat G$ and the L-group ${}^L G = \hat G \rtimes W_F$ (Borel, Corvallis) | the target of every parameter; defined from based root data in 06.1 | none | prove | A | [P] |
| T2-09 | Bruhat-Tits buildings (Kaletha-Prasad) | parahoric subgroups, depth | none (LL `Geometry/Building`) | state | B | [P] |
| T2-10 | Moy-Prasad filtrations and depth | depth preservation (Mishra, arXiv:2509.04997) | none | state | B | [P] |
| T2-11 | the Satake isomorphism (Satake 1963; Gross, "On the Satake isomorphism") | unramified parameters from spherical Hecke algebras; the unramified part of `LocalLanglands` | none (rl `SatakeDualWeyl`) | prove | A | [U] |
| T2-12 | Cartan, Iwasawa and Bruhat decompositions of $GL_n(K)$ | the structure of spherical and Iwahori Hecke algebras | none | prove | A | [U] |
| T2-13 | semisimple Lie algebras, Killing form, $\mathfrak{sl}_2$ | the Lie side of T2 | ML | reuse | A | [P] |
| T2-14 | real reductive groups and $(\mathfrak g, K)$-modules (Knapp 1986) | the archimedean places of `ReciprocityGL` | none | state | B | [P] |
| T2-15 | Kottwitz, "Isocrystals with additional structure", Compositio 56 (1985); $B(G)$ | the strata of $\mathrm{Bun}_G$ in T9 | none | read | C | [U] |

## 7.4 Tier T3: class field theory and GL(1)

| Id | Work | What it gives | Lean | Use | Pri | Tag |
|---|---|---|---|---|---|---|
| T3-01 | finite abelian local reciprocity (Serre; Milne, Chapter I to III) | `finiteAbelianLocalReciprocity` | NY [P] | port | A | [P] |
| T3-02 | the local existence theorem | norm subgroups correspond to finite abelian extensions | NY [R], rl | port | A | [R] |
| T3-03 | Lubin-Tate, "Formal complex multiplication in local fields", Ann. of Math. 81 (1965) | the explicit reciprocity map, $K^{ab} = K^{ur} K_\pi$ | none (rl) | prove | A | [U] |
| T3-04 | the Weil group of a local field (Tate, "Number theoretic background", Corvallis) | `WeilGroup` (06.1) | none (rl, 3 files) | prove | A | [P] |
| T3-05 | local Langlands for $GL_1$ | `LocalReciprocityGL1`, the case $n = 1$ of `LocalLanglandsGL` | none | prove | A | [P] |
| T3-06 | class formations (Artin-Tate) | the abstract reciprocity law | PR #42687 | port | B | [P] |
| T3-07 | the Brauer group of a local field and the invariant map | the cohomological proof of local reciprocity | ML, partly | prove | B | [U] |
| T3-08 | global reciprocity in idelic form (Artin) | `GlobalReciprocity` | NY [R], rl | port | A | [R] |
| T3-09 | the global existence theorem | ray class fields | NY [R], rl | port | A | [R] |
| T3-10 | the global Weil group (Weil 1951; Tate, Corvallis) | the global parameters of `ReciprocityGL` | none | state | B | [U] |
| T3-11 | Tate's thesis: local zeta integrals and local functional equations (Tate 1950; Cassels-Fröhlich XV) | local $L$ and $\varepsilon$ factors of $GL_1$ | none (rl) | prove | A | [S] |
| T3-12 | the global functional equation of Hecke L-functions | `HeckeFunctionalEquation`; continuation of Mathlib's `HeckeCharacter.LFunction` | ML (definition only), rl | prove | A | [P] |
| T3-13 | Hecke characters of type $A_0$ and their $\ell$-adic characters (Weil; Serre, *Abelian ℓ-adic Representations*) | the GL(1) case of `ReciprocityGL` | none | prove | B | [U] |
| T3-14 | class field theory of global function fields | the GL(1) case of route R7 | NY [R] | port | B | [R] |
| T3-15 | Langlands for tori (Langlands, "Representations of abelian algebraic groups", 1968; Yu) | `LocalLanglands` for tori | none (kckennylau, Lean 3) | prove | B | [U] |
| T3-16 | local Tate duality, Poitou-Tate | Selmer groups of T8; Galois cohomology of deformations | none (rl) | state | B | [P] |
| T3-17 | geometric class field theory (Serre, *Algebraic Groups and Class Fields*; Deligne) | the GL(1) case of `GeometricLanglands` | none | prove | B | [U] |

## 7.5 Tier T4: modular and automorphic forms of GL(2)

| Id | Work | What it gives | Lean | Use | Pri | Tag |
|---|---|---|---|---|---|---|
| T4-01 | modular forms of level $N$, q-expansions, cusp forms | the space $S_k(\Gamma_0(N))$ | ML | reuse | A | [P] |
| T4-02 | Hecke operators $T_n$ at level $N$, commutativity (Diamond-Shurman, Chapter 5) | eigenforms; replaces the q-expansion form of formal-conjectures | PR #40934 | prove | A | [P] |
| T4-03 | newforms, Atkin-Lehner theory, multiplicity one (Atkin-Lehner 1970) | the normalized newform of `ModularityEllipticQ` | none | prove | A | [U] |
| T4-04 | Petersson inner product, self-adjointness of $T_n$ | the eigenbasis | ML (Petersson) | prove | A | [P] |
| T4-05 | the L-function of a modular form, its functional equation | the analytic side of modularity | ML | reuse | A | [P] |
| T4-06 | Weil's converse theorem (Math. Ann. 168, 1967) | modularity from functional equations of twists | AF (a converse theorem with Rankin-Selberg) [R] | port | B | [U] |
| T4-07 | the modular curve $X_0(N)$ as a scheme, its Jacobian | the geometric side of Eichler-Shimura | AF [R], rl (8 files) | port | B | [R] |
| T4-08 | Eichler-Shimura relation and Galois representations of weight 2 (Shimura 1971) | $\rho_f$ for $k = 2$ | none | state | A | [P] |
| T4-09 | Deligne, "Formes modulaires et représentations ℓ-adiques", Sém. Bourbaki 355 (1969) | $\rho_f$ for $k \ge 2$ | none | state | A | [U] |
| T4-10 | Deligne, "La conjecture de Weil I", Publ. IHES 43 (1974) | Ramanujan-Petersson for holomorphic forms | fc (for τ) | state | A | [S] |
| T4-11 | Deligne-Serre, "Formes modulaires de poids 1", Ann. ENS 7 (1974) | weight 1 forms give odd Artin representations | none | state | B | [U] |
| T4-12 | adelization: modular forms as automorphic forms on $GL_2(\mathbb{A}_\mathbb{Q})$ (Gelbart, Annals Studies 83, 1975) | the bridge from T4-01 to `IsAutomorphicForm` | fc (Borel-Jacquet) | prove | A | [P] |
| T4-13 | Jacquet-Langlands, *Automorphic Forms on GL(2)*, LNM 114 (1970) | automorphic representations of $GL_2$, the global correspondence with quaternion algebras | none (Langlandscape-Mathathon, read) | state | B | [U] |
| T4-14 | strong multiplicity one (Jacquet-Shalika 1981; Piatetski-Shapiro 1979) | uniqueness in `ReciprocityGL` | none | state | A | [U] |
| T4-15 | automorphic forms on totally definite quaternion algebras, concrete Hecke algebras | the finite-dimensional model of Hecke theory | IF [P] | port | A | [P] |
| T4-16 | Eisenstein series and the continuous spectrum of $GL_2$ (Gelbart; Garrett, CSAM 173-174) | the spectral decomposition | ML (classical Eisenstein series) | state | B | [S] |
| T4-17 | Maass forms; bounds toward Ramanujan (Selberg 3/16; Kim-Sarnak 7/64) | the open case of `RamanujanGL` for $n = 2$ (route R4) | none | state | B | [U] |
| T4-18 | Rankin-Selberg for $GL_2 \times GL_2$ | the analytic input of the converse theorem | AF [R] | port | B | [R] |
| T4-19 | Serre's p-adic modular forms | the base of T9 | PM [P] | port | C | [P] |

## 7.6 Tier T5: smooth representations and local Langlands

| Id | Work | What it gives | Lean | Use | Pri | Tag |
|---|---|---|---|---|---|---|
| T5-01 | smooth and admissible representations, Jacquet modules (Bernstein-Zelevinsky 1976, 1977; Bernstein's Harvard notes 1992) | the automorphic side of `LocalLanglandsGL` | PR #41520, #41525, #45067 | prove | A | [P] |
| T5-02 | the Bernstein decomposition and the Bernstein centre (Bernstein 1984) | blocks; the target of Fargues-Scholze's map of centres | none | state | B | [U] |
| T5-03 | supercuspidals of $GL_2(F)$ by types (Bushnell-Henniart, Chapters 4 to 6) | the explicit side of S5 | none | prove | A | [P] |
| T5-04 | Bushnell-Kutzko types for $GL_n$, Annals Studies 129 (1993) | the classification of supercuspidals of $GL_n$ | none | state | B | [U] |
| T5-05 | Zelevinsky's classification, Ann. ENS 13 (1980) | reduction to supercuspidals | none | prove | B | [U] |
| T5-06 | Godement-Jacquet, LNM 260 (1972) | standard $L$ and $\varepsilon$ factors of $GL_n$ | none | prove | B | [U] |
| T5-07 | Jacquet, Piatetski-Shapiro, Shalika, "Rankin-Selberg convolutions", Amer. J. Math. 105 (1983) | factors of pairs; the characterization of LLC | none | state | B | [U] |
| T5-08 | Weil-Deligne representations, Frobenius-semisimplicity (Deligne 1973; Tate, Corvallis) | the Galois side of `LocalLanglandsGL` | none | prove | A | [P] |
| T5-09 | Deligne-Langlands local constants; Langlands's First and Second Main Lemmas | $\varepsilon(\rho, \psi)$ on the Galois side | eps [P] | port | A | [P] |
| T5-10 | Kutzko, LLC for $GL_2$ (Invent. Math. 1980); Bushnell-Henniart's proof | `LocalLanglandsGL 2` | none | prove | A | [S] |
| T5-11 | Henniart, numerical correspondence and characterization (1993; Invent. Math. 139, 2000) | uniqueness of LLC from factors of pairs | none | state | A | [S] |
| T5-12 | Harris-Taylor, Annals Studies 151 (2001) | LLC for $GL_n$, p-adic | none | state | A | [S] |
| T5-13 | Scholze, arXiv:1010.1540, Invent. Math. 192 (2013) | a second proof of LLC for $GL_n$ | none | state | B | [P] |
| T5-14 | Laumon-Rapoport-Stuhler, Invent. Math. 113 (1993); Li-Huerta, arXiv:2106.05381 | LLC for $GL_n$ in char $p$ | none | state | B | [S] |
| T5-15 | local Jacquet-Langlands (Deligne-Kazhdan-Vignéras; Rogawski; Badulescu) | inner forms of $GL_n$ | none | state | B | [S] |
| T5-16 | Langlands classification for real groups (1973; Math. Surveys Monogr. 31, 1989) | `LocalLanglands` over $\mathbb{R}$ | none | state | B | [P] |
| T5-17 | Kaletha, regular supercuspidal L-packets, JAMS 32 (2019), arXiv:1602.03144 | explicit LLC, tame, good $p$ (route R2) | none | state | B | [P] |
| T5-18 | Kaletha, "Supercuspidal L-packets", arXiv:1912.03274 | non-singular supercuspidals, $p \nmid \lvert W \rvert$ | none | state | B | [P] |
| T5-19 | Yu (2001); Fintzen, Ann. of Math. 193 (2021); Fintzen-Kaletha-Spice, Duke 172 (2023); Fintzen-Schwein, arXiv:2501.18553 | construction and exhaustion of tame supercuspidals | none | state | B | [S] |
| T5-20 | Gan-Takeda, Ann. of Math. 173 (2011) | LLC for $GSp_4$ | none | state | B | [S] |
| T5-21 | Gan-Savin, arXiv:2209.07346; Takanashi, arXiv:2609.19439, 2609.19430, 2611.06742 | LLC for $G_2$, character identities, formal degrees, Arthur packets | none (TauCeti roadmap PR #2458 [S]) | state | B | [P] |
| T5-22 | Aubert-Moussaoui-Solleveld, arXiv:1511.05335; Solleveld, Amer. J. Math. 145 (2023); Solleveld-Xu, arXiv:2411.19846 | the Hecke algebra method; LLC for unipotent and depth zero | none | read | B | [P] |
| T5-23 | local Gan-Gross-Prasad (Astérisque 346, 2012); Beuzart-Plessis | branching laws, a test of packets | none | read | C | [S] |
| T5-24 | Beuzart-Plessis, arXiv:2508.08470 | the formal degree conjecture for symplectic and even orthogonal groups | none | read | C | [P] |
| T5-25 | Cotner-Feng, arXiv:2609.16381 and 2609.16387 | Fargues-Scholze on inertia equals Kaletha for Yu's supercuspidals; finite fibres | none | read (route R1) | B | [P] |
| T5-26 | Taïbi, "The local Langlands conjecture", arXiv:2510.00632 | the precise general statement; the base of `LocalLanglands` in 06.2 | none | read | A | [P] |

## 7.7 Tier T6: L-functions, converse theorems and functoriality

| Id | Work | What it gives | Lean | Use | Pri | Tag |
|---|---|---|---|---|---|---|
| T6-01 | Cogdell and Piatetski-Shapiro, converse theorems for $GL_n$, Publ. IHES 79 (1994), J. reine angew. Math. 507 (1999) | the tool of most cases of `Functoriality` to $GL_N$ | none | state | B | [U] |
| T6-02 | Shahidi, the Langlands-Shahidi method (Ann. of Math. 132, 1990; AMS Colloq. 58, 2010) | L-functions from Eisenstein series | none | read | C | [U] |
| T6-03 | global Rankin-Selberg for $GL_n \times GL_m$ (JPSS 1983) | analytic properties of $L(s, \pi \times \pi')$ | none | state | B | [U] |
| T6-04 | Gelbart-Jacquet, Ann. ENS 11 (1978) | $\mathrm{Sym}^2: GL_2 \to GL_3$ | none | state | B | [U] |
| T6-05 | Langlands, *Base Change for GL(2)*, Annals Studies 96 (1980); Tunnell, Bull. AMS 5 (1981) | cyclic base change; Langlands-Tunnell | AF (octahedral case) [R] | port | B | [U] |
| T6-06 | Arthur-Clozel, Annals Studies 120 (1989) | base change and automorphic induction for $GL_n$ | none | state | B | [U] |
| T6-07 | Ramakrishnan, Ann. of Math. 152 (2000) | $GL_2 \times GL_2 \to GL_4$ | none | state | C | [S] |
| T6-08 | Kim-Shahidi, Ann. of Math. 155 (2002); Kim, JAMS 16 (2003) | $\mathrm{Sym}^3$, $\mathrm{Sym}^4$, $\wedge^2$ | none | state | C | [U] |
| T6-09 | Cogdell, Kim, Piatetski-Shapiro, Shahidi, Publ. IHES 99 (2004) | generic classical groups to $GL_N$ | none | state | C | [U] |
| T6-10 | Newton-Thorne, arXiv:1912.11261 and 2009.07180, Publ. IHES 134 (2021); arXiv:2212.03595 | $\mathrm{Sym}^n$ of holomorphic eigenforms for all $n$; Hilbert forms | none | state | B | [P] |
| T6-11 | Getz-Hahn-Yao, arXiv:2509.14381 | triple product L-functions imply Ramanujan (route R4) | none | read | B | [P] |
| T6-12 | known cases of Artin's conjecture: Langlands-Tunnell; Khare-Wintenberger with Kisin | `ArtinConjecture` for odd 2-dimensional over $\mathbb{Q}$ | AF (octahedral) [R] | state | B | [U] |
| T6-13 | Luo-Rudnick-Sarnak (1995, 1999); Kim-Sarnak (2003) | bounds toward `RamanujanGL` | none | state | B | [U] |
| T6-14 | Arthur, "The principle of functoriality", Bull. AMS 40 (2003) | the general statement; the source of `Functoriality` in 06.2 | none | read | A | [P] |

## 7.8 Tier T7: trace formula, endoscopy and Arthur's classification

| Id | Work | What it gives | Lean | Use | Pri | Tag |
|---|---|---|---|---|---|---|
| T7-01 | the trace formula for a finite group acting on functions | the teaching model of route R5 | none | prove | A | [U] |
| T7-02 | Selberg, the trace formula for a cocompact discrete subgroup (1956) | the first real trace formula in Lean (route R5) | none | prove | B | [U] |
| T7-03 | Arthur, "An introduction to the trace formula", Clay Proc. 4 (2005) | the Arthur-Selberg trace formula in general | none | read | B | [P] |
| T7-04 | Gelbart, *Lectures on the Arthur-Selberg Trace Formula*, AMS ULS 9 (1996), arXiv:math/9505206 | the $GL_2$ case in detail | none | read | B | [S] |
| T7-05 | orbital integrals, Shalika germs, the Harish-Chandra descent | the local terms | none (rl, 493 lines) | prove | B | [U] |
| T7-06 | Labesse-Langlands, "L-indistinguishability for SL(2)", Canad. J. Math. 31 (1979) | the first endoscopy; the test case of `FundamentalLemma` | none | prove | B | [U] |
| T7-07 | Langlands-Shelstad, transfer factors, Math. Ann. 278 (1987) | the definition needed by `FundamentalLemma` | none | state | B | [U] |
| T7-08 | Ngô, "Le lemme fondamental pour les algèbres de Lie", arXiv:0801.0446, Publ. IHES 111 (2010) | the fundamental lemma | none | state | B | [P] |
| T7-09 | Waldspurger, transfer and change of characteristic; Cluckers-Hales-Loeser | from Lie algebras to groups, from char $p$ to char 0 | none | state | B | [U] |
| T7-10 | Chaudouard-Laumon, the weighted fundamental lemma | the input to stabilization | none | state | C | [S] |
| T7-11 | Moeglin-Waldspurger, *Stabilisation de la formule des traces tordue*, Progr. Math. 316, 317 (2016) | the stable twisted trace formula | none | state | C | [U] |
| T7-12 | Arthur, *The Endoscopic Classification of Representations*, AMS Colloq. 61 (2013) | `ArthurClassification` for quasi-split $Sp_{2n}$ and $SO_n$ | none | state | B | [P] |
| T7-13 | Mok, Mem. AMS 235 (2015), arXiv:1206.0882; Kaletha-Minguez-Shin-White, arXiv:1409.3731 | quasi-split unitary groups; pure inner forms | none | state | C | [S] |
| T7-14 | Atobe, Gan, Ichino, Kaletha, Minguez, Shin, arXiv:2410.13504 (v3 2026-07-24) | the local intertwining relation; the classification is conditional only on the twisted weighted fundamental lemma | none | read (route R1) | B | [P] |
| T7-15 | Gee-Taïbi, arXiv:1807.03988 | Arthur's multiplicity formula for $GSp_4$ | none | state | C | [U] |
| T7-16 | Kottwitz, "Stable trace formula: elliptic singular terms", Math. Ann. 275 (1986) | stabilization of the elliptic part | none | read | C | [U] |
| T7-17 | Beyond Endoscopy: Langlands (2004); Altuğ (Compositio, 2015); Y. Cheng, arXiv:2505.18967 to 2608.15553; Deng-Espinosa, arXiv:2603.21506 | the trace formula approach to functoriality without endoscopy (route R5) | none | read | B | [S] |

## 7.9 Tier T8: Shimura varieties, Galois representations and modularity

| Id | Work | What it gives | Lean | Use | Pri | Tag |
|---|---|---|---|---|---|---|
| T8-01 | Deligne, "Variétés de Shimura", Corvallis (1979); Milne, Clay Proc. 4 | Shimura data, canonical models | none | state | B | [S] |
| T8-02 | Kottwitz, "Points on some Shimura varieties over finite fields", JAMS 5 (1992) | point counting, the Kottwitz conjecture | none | read | C | [U] |
| T8-03 | Mazur, "Deforming Galois representations" (1989) | deformation rings | IF `Deformations` | port | A | [U] |
| T8-04 | Taylor-Wiles and Wiles, Ann. of Math. 141 (1995) | patching; semistable modularity | IF `Patching`, AF [R] | port | A | [U] |
| T8-05 | Ribet, Invent. Math. 100 (1990); Mazur, Publ. IHES 47 (1977) | level lowering; the Eisenstein ideal | AF [R] | port | B | [U] |
| T8-06 | Breuil, Conrad, Diamond, Taylor, JAMS 14 (2001) | `ModularityEllipticQ` for every $E/\mathbb{Q}$ | none (AF has the semistable case) | state | A | [U] |
| T8-07 | Khare-Wintenberger, Invent. Math. 178 (2009) | Serre's modularity conjecture | none | state | B | [U] |
| T8-08 | Kisin, JAMS 22 (2009) and Ann. of Math. 170 (2009); Pan, JAMS (2022) | Fontaine-Mazur for $GL_2/\mathbb{Q}$ in most cases | none | state | C | [U] |
| T8-09 | Clozel-Harris-Taylor and Taylor, Publ. IHES 108 (2008) | automorphy lifting for conjugate self-dual representations | none | state | C | [U] |
| T8-10 | HSBT, Ann. of Math. 171 (2010); BLGHT, PRIMS 47 (2011) | `SatoTate` for non-CM elliptic curves over totally real fields | fc (statement) | state | B | [S] |
| T8-11 | Barnet-Lamb, Gee, Geraghty, Taylor, arXiv:1010.2561 | potential automorphy and change of weight | none | state | C | [S] |
| T8-12 | Harris, Lan, Taylor, Thorne, arXiv:1411.6717 | Galois representations without self-duality | none | state | C | [P] |
| T8-13 | Scholze, arXiv:1306.2070, Ann. of Math. 182 (2015) | torsion classes; perfectoid Shimura varieties | none | state | C | [P] |
| T8-14 | Calegari-Geraghty, Invent. Math. 211 (2018) | patching when $\ell_0 > 0$ | none | read (route R3) | C | [S] |
| T8-15 | Allen, Calegari, Caraiani, Gee, Helm, Le Hung, Newton, Scholze, Taylor, Thorne, arXiv:1812.09999, Ann. of Math. 197 (2023) | automorphy lifting over CM fields | none | state | C | [P] |
| T8-16 | Boxer, Calegari, Gee, Newton, Thorne, arXiv:2309.15880 | Ramanujan and Sato-Tate for Bianchi forms (route R4) | none | state | C | [P] |
| T8-17 | Freitas-Le Hung-Siksek, Invent. Math. (2015); Derickx-Najman-Siksek; Box | modularity over real quadratic, cubic and quartic fields | none | state | C | [S] |
| T8-18 | Caraiani-Newton, arXiv:2301.10509 (v4 accepted 2026-10-20) | modularity over imaginary quadratic fields | none | state | C | [P] |
| T8-19 | Boxer, Calegari, Gee, Pilloni, Publ. IHES (2021); arXiv:2502.20645 | potential modularity of abelian surfaces; modularity of a positive proportion over $\mathbb{Q}$ | none | read (route R3) | C | [P] |
| T8-20 | Caraiani-Scholze, Ann. of Math. 186 (2017); Hamann-Lee, arXiv:2309.08705; Yang-Zhu, arXiv:2505.04329 | torsion vanishing | none | read | C | [S] |
| T8-21 | Daniels, van Hoften, Kim, Zhang, arXiv:2408.01348, 2603.24921 | Igusa stacks for Hodge and abelian type | none | read | C | [P] |
| T8-22 | Kisin, JAMS 23 (2010); Kisin-Pappas, Publ. IHES 128 (2018) | integral models | none | read | C | [S] |
| T8-23 | Calegari, "Reciprocity in the Langlands program since FLT", arXiv:2109.14145; Caraiani-Shin, arXiv:2311.13382 | the surveys of reciprocity; the introductions of Vols. 10 and 11 | none | read | A | [P] |

## 7.10 Tier T9: p-adic Hodge theory, p-adic and mod p Langlands, Fargues-Scholze

| Id | Work | What it gives | Lean | Use | Pri | Tag |
|---|---|---|---|---|---|---|
| T9-01 | Fontaine, étale $(\varphi, \Gamma)$-modules (Grothendieck Festschrift II, 1990) | the equivalence with $\mathbb{Z}_p$-representations of $G_{\mathbb{Q}_p}$ | none | prove (route R9) | B | [U] |
| T9-02 | Fontaine's period rings $B_{dR}$, $B_{cris}$; Brinon-Conrad, CMI notes (2009) | p-adic Hodge theory | ML (seeds: `BDeRham`, `FontaineTheta`) | prove | C | [U] |
| T9-03 | Huber, adic spaces (Math. Z. 1994; Aspects of Math. 1996) | the geometry of T9 | TC (complete, 2026-10-28) [P], PR #42312 | port | C | [P] |
| T9-04 | Scholze, "Perfectoid spaces", Publ. IHES 116 (2012) | tilting | PR #26389 (draft), TC roadmap | state | C | [P] |
| T9-05 | Fargues-Fontaine, *Courbes et fibrés vectoriels*, Astérisque 406 (2018) | the curve | TC (adic curve) [P] | port | C | [U] |
| T9-06 | Scholze-Weinstein, *Berkeley Lectures on p-adic Geometry*, Annals Studies 207 (2020) | diamonds, mixed characteristic shtukas | none | read | C | [P] |
| T9-07 | Fargues-Scholze, arXiv:2102.13459, Astérisque 466 (2026) | semisimple L-parameters for every $G$; the categorical conjecture | none (TC roadmap `LanglandsParameterStacks`) | state | B | [P] |
| T9-08 | Scholze, arXiv:2501.07944 (to appear in Crelle) | independence of $\ell$ of the FS parameters | none | read | C | [P] |
| T9-09 | Colmez, Astérisque 330 (2010) | the Montreal functor | none (TC roadmap `PadicLocalLanglandsForGL2Qp`) | state | C | [S] |
| T9-10 | Paskūnas, Publ. IHES 118 (2013), arXiv:1005.2008 | the image of the Montreal functor, $p \ge 5$ | none | state | C | [P] |
| T9-11 | Colmez-Dospinescu-Paskūnas, Cambridge J. Math. 2 (2014), arXiv:1310.2235 | the p-adic LLC for $GL_2(\mathbb{Q}_p)$ | none | state | C | [S] |
| T9-12 | Barthel-Livné, Duke (1994); Breuil, Compositio 138 (2003) | mod $p$ representations of $GL_2(\mathbb{Q}_p)$; the mod $p$ correspondence | none | prove (route R9) | B | [U] |
| T9-13 | Buzzard-Diamond-Jarvis, Duke 155 (2010); Herzig's recipe | Serre weight conjectures; a combinatorial statement | none | ex, prove | B | [U] |
| T9-14 | Breuil, Herzig, Hu, Morra, Schraen; Hu-Wang (report D, 2.3 to 2.4) | mod $p$ Langlands for $GL_2(\mathbb{Q}_{p^f})$ | none | read | C | [S] |
| T9-15 | Emerton-Gee, *Moduli Stacks of Étale $(\varphi,\Gamma)$-Modules*, Annals Studies 215 (2023) | the Emerton-Gee stack | none | read | C | [S] |
| T9-16 | Emerton-Gee-Hellmann, arXiv:2210.01404 (v5 2025) | the categorical p-adic program | none | read | C | [P] |
| T9-17 | Johansson, Newton, Wang-Erickson, arXiv:2403.19565, Compositio 162 (2026) | the locally admissible categorical case | none | read | C | [S] |
| T9-18 | Dotto-Emerton-Gee, arXiv:2603.26887; Dowd, arXiv:2610.25055 | categorical p-adic LLC for $GL_2(\mathbb{Q}_p)$, $p \ge 5$; $p = 3$ Steinberg | none | read (route R1) | C | [P] |
| T9-19 | Pan, arXiv:2008.07099, 2209.06366 (Ann. of Math. 203, 2026) | locally analytic vectors; Fontaine-Mazur cases | none | read | C | [S] |
| T9-20 | Breuil-Mézard; Kisin; Feng-Le Hung, arXiv:2310.07006 | multiplicities of deformation rings | none | read | C | [S] |
| T9-21 | Zhu, arXiv:2008.02998 and 2504.07482; Hansen-Mann, arXiv:2606.00983; Helm-Solleveld-Xu, arXiv:2606.10149 | the categorical local Langlands conjecture and its known cases | none | read | C | [P] |
| T9-22 | Clausen-Scholze, condensed and analytic stacks (arXiv:2605.03658 and the 2023 to 2024 course); Anschütz-Le Bras-Mann, arXiv:2412.20968 | the foundations of the p-adic geometric side | ML (`Condensed/*`) | read | C | [S] |

## 7.11 Tier T10: function fields and geometric Langlands

| Id | Work | What it gives | Lean | Use | Pri | Tag |
|---|---|---|---|---|---|---|
| T10-01 | Drinfeld, $GL_2$ over function fields by shtukas (1974 to 1987) | the first global case of `ReciprocityGL` over a function field | none | read | C | [U] |
| T10-02 | L. Lafforgue, Invent. Math. 147 (2002) | `ReciprocityGL` and `RamanujanGL` for $GL_n$ over function fields | none | state | B | [U] |
| T10-03 | V. Lafforgue, arXiv:1209.5352, JAMS 31 (2018) | automorphic to Galois for every $G$, by excursion operators | none | state | B | [P] |
| T10-04 | Genestier-Lafforgue, arXiv:1709.00978 (v3 2026-07-30) | semisimple local parameters in equal characteristic | none | state | C | [P] |
| T10-05 | Böckle, Harris, Khare, Thorne, Acta Math. 223 (2019) | potential automorphy of Zariski-dense local systems | none | read | C | [S] |
| T10-06 | Sawin-Templier, JAMS 34 (2021); Ciubotaru-Harris, arXiv:2311.15300 | Ramanujan over function fields | none | read | C | [P] |
| T10-07 | the Picard scheme of a curve, the Abel-Jacobi map | the GL(1) case of `GeometricLanglands` (with T3-17) | none | prove | B | [U] |
| T10-08 | Mirković-Vilonen, geometric Satake, Ann. of Math. 166 (2007) | the Hecke action on the geometric side | none | state | C | [U] |
| T10-09 | Beilinson-Drinfeld, quantization of the Hitchin system (preprint); Frenkel, CSAM 103 (2007) | opers; the local geometric picture | none | read | C | [P] |
| T10-10 | Gaitsgory-Rozenblyum, *A Study in Derived Algebraic Geometry*, AMS SURV 221 (2017) | prestacks, IndCoh; the language of GLC | none | read | C | [P] |
| T10-11 | Arinkin-Gaitsgory, "Singular support of coherent sheaves" (Selecta 2015) | $\mathrm{IndCoh}_{\mathrm{Nilp}}$ | none | read | C | [U] |
| T10-12 | AGKRRV, arXiv:2010.01906, 2012.07665, 2102.07906 | restricted local systems; automorphic functions as the trace of Frobenius | none | read | C | [P] |
| T10-13 | GLC I to V: arXiv:2405.03599, 2405.03648, 2409.07051, 2409.08670, 2409.09856 (947 pages) | `GeometricLanglands` in char 0, unramified, every reductive $G$ | none | state (route R8) | C | [P] |
| T10-14 | Gaitsgory-Raskin, arXiv:2508.02237 | part of the $\ell$-adic GLC in char $p$ | none | read | C | [P] |
| T10-15 | Gaitsgory, V. Lafforgue, Raskin, arXiv:2603.26925 | tempered and generic automorphic functions | none | read | C | [P] |
| T10-16 | Ben-Zvi-Nadler, arXiv:1606.08523; Dhillon-Taylor, arXiv:2501.14157 | Betti GLC; the tame local Betti case | none | read | C | [P] |
| T10-17 | Ben-Zvi, Sakellaridis, Venkatesh, arXiv:2409.04677 | relative Langlands duality | none | read | C | [P] |
| T10-18 | Toda, arXiv:2602.09359; Donagi-Pantev, Invent. Math. 189 (2012) | Dolbeault GLC for $GL_2$ with reduced spectral curves | none | read | C | [P] |
| T10-19 | Lomelí, arXiv:2610.23985 | base change for unitary groups in char $p$; Ramanujan for Langlands-Shahidi L-functions | none | read | C | [P] |
| T10-20 | Gaitsgory, arXiv:2509.24902 (ICM 2026); Ben-Zvi, arXiv:2605.23167; Scholze, Bourbaki exposé 1252 | the expositions of the proof and of the open conjectures | none | read | B | [P] |

## 7.12 Watch list: fresh claims that are not in the corpus

These are recorded with the kind `claim` and the status `claimed` (06.6). They are never used as hypotheses until the `reader` role and an outside expert have checked them, and the paper record has `expert_status: accepted`. Each one has a page on the site with its date and status. Route R1 of document 04 is the project's work on them.

| Claim | Source | Date | What it claims | Why it matters |
|---|---|---|---|---|
| Twisted weighted fundamental lemma | Halleck-Dube, arXiv:2611.26750, 190 pages [P] | 2026-11-19 | the weighted fundamental lemma for quasi-split unramified groups, the twisted form in good characteristic | with AGIKMS (T7-14), Arthur's classification becomes unconditional |
| Arthur-Ramanujan over function fields, unramified | Gaitsgory, V. Lafforgue, Raskin; Raskin's ICM text (dated 2025-10-12, updated 2026-03-10) [P] | announced | Theorems A to C of report C, 2.5 | the full paper is "in preparation" [S] |
| Restricted GLC in char $p$ with full support; quantum GLC at irrational level | openai/math, families 014 and 069 [P] | 2026-09-24, 2026-10-04 | two open problems of report A, section 3 | not reviewed; no Lean; retraction labels in family 014 [S] |
| The Riemann hypothesis, and GRH for Dirichlet L-functions | Alpöge, riemann-lean and "Remark" [P] | 2026-11-20 | RH in Lean; the Lean FRO and the Mathlib Initiative certified the statement and the proof on 2026-11-21 [P, report C] | the method uses theta lifts between unitary groups, GGP periods and a relative trace formula; its library may hold Langlands content (5.3). The proof is checked by kernels, but no written human account exists yet |
| A human-only GRH manuscript | Masullo, posted 2026-11-20 [S] | 2026-11-20 | GRH | issues reported within hours [S] |
| From potential modularity to modularity lifting | Dieulefait, arXiv:2611.32569 [P] | 2026-11-24 | modularity lifting over totally real fields, $p \ge 7$ | one day old at the time of writing |
| Supercuspidals by double covers; LIR for inner forms of $GL_N$ | Fintzen-Kaletha, arXiv:2611.31396; Atobe-Kaletha-Minguez-Shin, arXiv:2611.31683 [P] | 2026-11-23 | report B, 2.2 and 2.3 | by experts of the area, but two days old; they move to T5 and T7 after a reading |
| "Proved" statements of Langlands-lib | math-yiluo/Langlands-lib notes [R] | 2026 | for example `globalFundamentalClassStatement` | AI-written, no licence, not built by the project |
| Hamann, compatibility for $GSp_4$, v4 "after A.I. review" | arXiv:2109.01210 v4 [P] | 2026-10-07 | a corrected version | a reminder that published results also change; the reader role rechecks the version |

## 7.13 The paper record

Each paper has a file `papers/<id>.yaml` in `tamnd/langlands`:

```yaml
id: T5-10
key: Kut80
title: The Langlands conjecture for Gl2 of a local field
authors: [Philip Kutzko]
where: Ann. of Math. 112 (1980) 381-412      # the reader role checks it
doi: null
arxiv: null
also: [T0-10]                                # Bushnell-Henniart, the proof the project follows
read: { version: journal, by: reader, date: 2026-12-01, tag: S }
tier: T5
why: the first proof of LLC for GL(2); the target of milestone S5
expert_status: accepted                      # accepted | claimed | announced | withdrawn | disputed
uses: [T5-01, T5-03, T5-08, T5-09, T3-05]
results:
  - id: "Main theorem"
    statement: LocalLanglandsGL 2            # the name in Langlands/Statements/ (06.2)
    node: LG5LLC2001
    kind: theorem                            # theorem | definition | conjecture | claim | example
    status: stated                           # computed from the map: unstated | stated | proved-mod | proved | refuted | claimed
lean_elsewhere:                              # other formalizations, with commit and licence
  - { repo: math-yiluo/Langlands-lib, commit: null, licence: none, what: statement only, use: read }
lean_status: none                            # none | stated | port-available | proved
code_licence: null                           # the licence of the code the project ports for this paper
handbook: { volume: 6, chapter: null }       # document 11
notes: Follow Bushnell-Henniart, not the 1980 paper; plan the node graph with the planner role first.
```

- `expert_status` is set by a person. It is shown with every `proved-mod` hypothesis that comes from the paper (14.3).
- `announced` is for a result that its authors state in a talk or a survey without a full paper (for example the GLR theorem of 7.12).
- `lean_status` and `code_licence` let `lgl` find the cheapest source for a node: a ported proof beats a new proof (5.4).

## 7.14 Counts and order

The tiers have 204 rows: 16 in T0, 15 in T1, 15 in T2, 17 in T3, 19 in T4, 26 in T5, 14 in T6, 17 in T7, 23 in T8, 22 in T9 and 20 in T10. A row with several papers counts as one. The watch list has 9 more rows.

By use, about 30 rows are `prove`, about 15 `port`, about 65 `state` and the rest `read`, `reuse` or `ex`. This ratio is deliberate. G1 (document 02) needs the statements, not the proofs. The project writes only the proofs on the path to G2.

The first ten to formalize, in order:

1. **T3-04**, the Weil group of a local field.
2. **T3-01**, finite abelian local reciprocity, ported from NYLL (5.5).
3. **T3-05**, `LocalReciprocityGL1`, from 1 and 2 with the infinite extension.
4. **T3-11**, Tate's local functional equation.
5. **T3-08 with T3-09**, global reciprocity and existence, ported from NYLL.
6. **T3-12**, the global functional equation of Hecke L-functions.
7. **T2-08**, the L-group from based root data.
8. **T5-01**, smooth and admissible representations, after the open PRs.
9. **T5-08**, Weil-Deligne representations, then the statement `LocalLanglandsGL`.
10. **T4-02**, Hecke operators at level $N$, then the bridge of `ModularityEllipticQ` to formal-conjectures (5.6).

These items give GL(1) complete, which is half of G2. They give the statements of the main local conjecture and of modularity, which are the core of G1. They also give the base of the GL(2) work. They are the work of milestones S1 to S3 (document 15). The next five are T5-03, T5-09, T5-10, T4-15 and T4-12, for the LLC for $GL_2$ at S5.
