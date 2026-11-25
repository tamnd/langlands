# 05. The base: what the project starts from

The project does not start from zero. Mathlib has the base layer for an adelic theory of GL(1) and GL(2). Several Lean projects of 2025 and 2026 have proved large parts of the next layers: class field theory (CFT), Hecke algebras, patching and the GL(2) modularity steps of Fermat's Last Theorem (FLT). This document records what each source has, what the project takes from it, and the rules for the use of the code. The main source is report E (`research/sources/E-lean-ai-infrastructure.md`). The facts were measured on 2026-11-25 with `gh api` and local file counts, unless a row says otherwise. The tags [P], [S], [U] and [R] are those of document 01. [R] marks a claim that a README makes and that nobody checked.

**Decision (settles Q-03 of document 16 in principle).**
- Mathlib at the tag `v4.35.0` is the only Lake dependency of `Langlands`.
- Every other source is either ported (copied with its licence and provenance, 5.4) or read only (5.3).
- No large project is a `require`.

## 5.1 Mathlib at the pin

The pin is Lean `v4.35.0` with the Mathlib tag `v4.35.0` (commit `56a005855e`, Lean released 2026-10-12) [P]. Document 09.3 explains the choice. The fallback is `v4.36.0` (`fc4f59e577`), the pin of NYLL. The inventory below is from Mathlib master `b5aed57ecb` (2026-11-25). Master is two tags ahead of the pin. Each item must be checked again at the pin before a node uses it. That check is the first task of the `reader` role at S0.

**Present** (paths under `Mathlib/`) [P]:

| Topic | Path | Key declarations |
|---|---|---|
| Adeles and ideles of a number field | `NumberTheory/NumberField/AdeleRing.lean`, `FiniteAdeleRing.lean`, `InfiniteAdeleRing.lean` | `NumberField.AdeleRing`, `principalSubgroup`, the product formula `norm_algebraMap_eq_one_of_ne_zero` |
| Finite adeles of a Dedekind domain | `RingTheory/DedekindDomain/FiniteAdeleRing.lean` | the restricted product over height one primes |
| Completions at places | `NumberTheory/NumberField/Completion/{FinitePlace, InfinitePlace, Ramification}` | completions, ramification of places |
| Nonarchimedean local fields | `NumberTheory/LocalField/Basic.lean:44` | `class IsNonarchimedeanLocalField`, on `ValuativeRel`; compact ring of integers, finite residue field |
| Hecke characters and their L-functions | `NumberTheory/NumberField/HeckeLFunction.lean` | `HeckeCharacter := IdeleClassGroup R K →ₜ* ℂ`, `IsUnramifiedAt`, `localValue`, `LFunction` |
| Dedekind zeta | `NumberTheory/NumberField/DedekindZeta.lean` | the residue and the class number formula |
| Abstract Hecke rings | `NumberTheory/HeckeRing/Defs.lean` | `IsHeckeTriple`, `HeckeCoset`, `HeckeRing` (Shimura, Chapter 3) |
| Modular forms | `NumberTheory/ModularForms/` (about 40 files) | q-expansions, Eisenstein series, level one dimension formula, Petersson product, `Discriminant`, `DedekindEta`, the L-function with its functional equation (`LFunction.lean`) |
| L-series | `NumberTheory/LSeries/*` | Riemann and Dirichlet L-functions, continuation, non-vanishing on Re(s) = 1, primes in progressions |
| Root data | `LinearAlgebra/RootSystem/` (24 files) | `RootPairing` (`Defs.lean:80`), `RootDatum` (`Defs.lean:110`), `WeylGroup`, `CartanMatrix`, `Finite/G2` |
| Lie algebras | `Algebra/Lie/` (60 files) | Killing form, Cartan subalgebras, semisimple Lie algebras, `Sl2` |
| Representations and group cohomology | `RepresentationTheory/*`, `.../Homological/GroupCohomology/*`, `TateCohomology/Basic` | `Rep`, `FDRep`, induction, Hilbert 90, Shapiro's lemma, Tate cohomology |
| Infinite Galois theory, profinite groups | `FieldTheory/Galois/{Infinite, Profinite, Abelian}`, `Topology/Algebra/Category/ProfiniteGrp` | Krull topology, the fundamental theorem, `IsAbelianGalois` |
| Haar measure | `MeasureTheory/Measure/Haar/*` | |
| Group schemes and étale sites | `AlgebraicGeometry/Group/*`, `AlgebraicGeometry/Sites/{Etale, Proetale}` | |
| Condensed, triangulated, derived | `Condensed/*`, `CategoryTheory/Triangulated/*`, `Algebra/Homology/DerivedCategory/*`, `AlgebraicTopology/Quasicategory/*` | `CondensedMod.IsSolid`, Ext |
| Seeds of p-adic Hodge theory | `RingTheory/Perfectoid/{BDeRham, FontaineTheta, Untilt}`, `RingTheory/WittVector/*` | |

One warning [P]: the docstring of `AdeleRing` says that the construction does not give the correct answer for function fields. The function field routes (R7, R8 of document 04) need their own adeles.

**Absent.** A search by path and name found nothing for these topics [U]:
- the Weil group $W_K$ and Weil-Deligne representations;
- the dual group and the L-group;
- reductive group schemes over a base;
- smooth and admissible representations of p-adic groups;
- Tate's thesis;
- local and global CFT and Lubin-Tate theory;
- Hecke operators acting on modular forms;
- the Galois representations of modular forms;
- Shimura varieties and $\mathrm{Bun}_G$.

Each statement of document 06 needs at least one of these. The project defines them in `Langlands/Basic/` and offers them upstream (09.5).

**Open Mathlib PRs to watch** [P]:

| PR | Topic | Opened | Project use |
|---|---|---|---|
| #40934 | Hecke operators at level one | 2026-06-26 | T4 of document 07; replace the project's own definition when it merges |
| #41277 | convolution on abstract Hecke rings | 2026-07-08 | T4 |
| #43087 | `RepresentationTheory/Hecke/Basic` | 2026-11-06 | T5 |
| #41520, #41525, #45067 | smooth representations | 2026-09-18 | T5, the automorphic side of `LocalLanglandsGL` |
| #42687 | class formations | 2026-10-24 | T3 |
| #42312 | Huber rings (status `awaiting-author`) | 2026-07-31 | T9 |
| #26389 | perfectoid fields (draft, 13 `sorry` on a fork) | 2025-06-25 | T9 |

The rule for an open PR: do not wait for it. Write the project's own definition in a file that has the PR number in its header. When the PR merges, prove the two definitions equal, then delete the project's file at the next bump (09.3).

## 5.2 The sources to port

All rows have a licence that allows a copy. "Cost" is a guess by this spec of the work to bring the files to the pin and to the rules of 09.2 [U].

| Source | Licence | Pin | Size | What to take | Cost |
|---|---|---|---|---|---|
| n-yamaguchi-0729/ClassFieldTheory, in the umbrella NYLL | Apache-2.0 [P] | v4.36.0 | 4,293 files, 47 MB [P] | local reciprocity for every nonarchimedean local field (`finiteAbelianLocalReciprocity`) [P]; local existence, global reciprocity with existence, and function field CFT [R] | medium: one minor version down, AI-written code to prune; the first port (5.5) |
| ImperialCollegeLondon/FLT | Apache-2.0 [P] | v4.35.0 | 271 files, 2.79 MB, 25 files with `sorry` [P] | `AutomorphicForm/QuaternionAlgebra/*`, concrete Hecke operators `HeckeOperator.T`, `HeckeOperator.U`, `HeckeAlgebra` [P]; `Patching/*` with `REqualsT`; `Deformations/*`; `HaarMeasure/HaarChar` | low: same pin, written by people; never port a file that has a `sorry` or an `axiom` from `FLT/Assumptions/` |
| anthropics/fermats-last-theorem | Apache-2.0 [P] | v4.33.1 | at least 45,938 files, about 1.05M declarations, nanoda-checked [R] | octahedral Langlands-Tunnell, R = T at p = 3, 5, `WeierstrassCurve.modularity_of_semistableModel`, Ribet for the Frey curve, Mazur's Eisenstein quotient, $X_0(N)$ and Néron models [R] | high: two minor versions down; results are stated in the strength that FLT needs. Port the statements first, then proofs by need |
| lana-agents/local-class-field-theory | Apache-2.0 [P] | v4.32.0 | 122 files, 1.5 MB [P] | p-adic local CFT: the Artin map to $\mathrm{Gal}(K^{ab}/K)$, existence, the profinite completion [R] | medium; only a cross-check of NYLL in the p-adic case |
| kbuzzard/ClassFieldTheory | Apache-2.0 [P] | v4.36.0-rc2 | 110 files, 0.53 MB [P] | the human-written CFT of the 2025 Clay summer school; the model for names and API | low; partial |
| TauCetiProject/TauCeti | Apache-2.0 [P] | not checked [U] | 30 roadmaps declared complete [P] | adic spaces (Huber rings, Spa, Tate acyclicity, sheafiness) and the adic Fargues-Fontaine curve (2026-10-28) [P]; roadmaps `PadicLocalLanglandsForGL2Qp`, `LanglandsParameterStacks`, `PerfectoidSpaces`, `ShimuraData` [P] | high for the code; zero for the roadmaps. Align with the roadmaps, do not duplicate them (route R9) |
| fukubillueda-web/epsilon_FML and epsilon_SML | Apache-2.0 [P] | v4.32.2 | 141 and 211 files [P] | Langlands's First and Second Main Lemmas on epsilon factors | medium; input to the local constants of T5 |
| ANR-FALSE/PadicModForms | Apache-2.0 [P] | v4.36.0 | 66 files [P] | Serre p-adic modular forms; a Verso site to copy | low |
| CBirkbeck/LeanModularForms | Apache-2.0 [P] | v4.31.0-rc2 | 234 files [P] | staging for Mathlib modular forms | check what Mathlib already took first |
| dagurtomas/LeanCondensed | Apache-2.0 [P] | v4.34.0-rc2 | 43 files [P] | condensed and solid staging | low; only for T9 and T10 |
| emilyriehl/infinity-cosmos | Apache-2.0 [P] | v4.34.0-rc1 | 32 files [P] | ∞-categories | only for T10; no first-year use |
| Rogerhu12/hecke-seven-eighths | Apache-2.0 [P] | v4.35.0-rc3 | 8,736 files, 92 MB [P] | a zero-free region for Hecke L-functions [R] | read first; port only lemmas that T3 needs |

## 5.3 Sources to read but not copy

These sources have no licence. The project may read them, cite them and compare names with them. It does not copy a line into a repository of the project.

- **riemann-lean** (`tamnd/riemann-lean`, the release of 2026-11-20 by Levent Alpöge) [P].
  - Size: 175,187 files, 17,374,215 lines, about 1.06M declarations.
  - Pin: v4.33.1, Mathlib `0df444a3`. Not built on a machine of the project yet. `NOTICE.md` says that the copyright stays with the author.
  - The files are the first two layers of a Langlands library, written once already:
    - `GroundTheory/GlobalFields/` (384 files, 72,305 lines): `reciprocityMap : IdeleClassGroup K →* (L ≃ₐ[K] L)` with `ker_reciprocityMap`, the existence theorem `exists_isAbelianGalois_range_ideleClassNorm_eq_of_finiteIndex`, Tate's thesis (77 files) with `completedLFunction_eq_rootNumber_mul`, and three Weil group files;
    - `GroundTheory/LocalFields/` (159 files, 40,767 lines): Lubin-Tate reciprocity, conductors, and the local existence theorem `exists_isAbelianGalois_range_normUnits_eq` (`NormCorrespondence.lean:41`);
    - `GroundTheory/AutomorphicForms/` (542 files, 150,005 lines): `AdelicGLn`, `Whittaker`, `AdmissibleInduction`;
    - `ReciprocityTheory/ReductiveGroups/` (2,799 files, 409,976 lines);
    - `PositivityTheory/.../JacquetLanglands` (114 files).
  - Action at S0: write to the author and ask for a licence, preferably Apache-2.0, for `GroundTheory/` and `ReciprocityTheory/`. A licence would save the project most of the work of milestones S1 and S2 (document 15). Until an answer comes, riemann-lean is used only in the cross-check package of 5.6.
- **math-yiluo/Langlands-lib** [P].
  - Size: 28,764 files, 212 MB. Pin: v4.34.0. No licence on GitHub. It vendors code of anthropics FLT, Imperial FLT, NYLL and TauCeti under their own licences.
  - Its own notes say that most targets are `Prop`-valued `...Statement` definitions marked "Unproved", and that the local correspondence for $GL_n$ is not constructed [R].
  - Use: a map of names and dependencies for the stater role. Its errata for Borel-Tits, Milne and Springer go to the `reader` role.
- **leanprover/verso-blueprint** [P]: no licence on GitHub. The site of the project (document 12) does not depend on it until it has one. Verso itself is Apache-2.0 and can be used.

Also read, with a short or no licence: Langlandsproject/Langlands (a knowledge base), larsbx/langlands-lab, kckennylau/local-langlands-abelian (Lean 3, 2018, a statement of LLC for tori), and drjanosch42/Langlandscape-Mathathon (CC-BY-4.0 header; a Jacquet-Langlands event output). The headers of the last one must be checked before any use [U].

## 5.4 The porting rule

1. **Port files, never `require` a large project.** Each ported file goes to `Langlands/Ported/<Source>/<path>.lean`, with the same relative path as in the source.
2. **Keep the licence and the provenance.** Each file keeps its copyright header. It adds two lines:
   - `Ported from <repo> at <commit>, path <path>.`
   - `Modified by tamnd/langlands-lean.`
   The repository has a `NOTICE` file that lists each source and its licence.
3. **Record the source.** `manifests/ported.yaml` has one entry per source: the repository, the commit, the licence, the list of files, and the SHA-256 of each file at the source commit. `lgl port check` (document 10) recomputes them and fails CI on a difference.
4. **Bring the file to the rules of 09.2.** That means: no `sorry`, no `axiom`, no `native_decide`, `autoImplicit` off, and names in the Mathlib style. A file that cannot meet the rules stays out.
5. **Prefer the statement, then the proof.** A ported theorem first enters as a statement in `Statements/` with status `stated`. Its ported proof then makes it `proved`. If the proof is too costly to port, the statement stays `proved-mod`, with the source named as the reference (09.2.2).
6. **Upstream when general.** A ported file that is general (for example the Weil group, or class formations) is offered to Mathlib with the original authors listed first.

The reasons for the rule:
- **The pin.** The sources are on five different pins (v4.32 to v4.36). A Lake dependency forces one pin on all of them.
- **The build cost.** anthropics FLT took 5 h 32 min on 96 jobs and 153 GB of memory [R]. riemann-lean has 17 million lines. A dependency on either makes CI impossible on a normal runner.
- **Trust.** A ported file is in the repository and is checked by the trust run (document 14) with the rest of `Langlands`. A dependency is checked only if its own checks are repeated.

## 5.5 The first port: local reciprocity from NYLL

The first port is the work of milestone S1. NYLL states finite abelian local reciprocity over Mathlib's `IsNonarchimedeanLocalField`, so it covers $\mathbb{Q}_p$, its finite extensions and $\mathbb{F}_q((t))$. The file is `Nyll/ClassFieldTheory/Theorems/LocalClassFieldTheory/FiniteAbelianLocalReciprocity.lean` [P]:

```lean
theorem finiteAbelianLocalReciprocity (K : Type u) (L : Type v) [Field K] [Field L]
    [Algebra K L] [FiniteDimensional K L] [IsAbelianGalois K L]
    [ValuativeRel K] [TopologicalSpace K] [IsNonarchimedeanLocalField K] :
    ∃ artin : Kˣ →ₜ* (L ≃ₐ[K] L), Function.Surjective artin ∧
      ∀ x : Kˣ, artin x = 1 ↔ IsFieldNorm K L x
```

A copy in the Palomar Archive, on v4.35.0-rc2, has a comparator Challenge for the quotient form `Kˣ / N(Lˣ) ≃ₜ* Gal(L/K)` [P]. It is the template for the project's challenge file.

The steps from the theorem to `LocalReciprocityGL1` of document 06:

1. **Port and pin.** Port the theorem and its imports from v4.36.0 to v4.35.0. Measure the import closure first, with `lgl port add -plan` (document 10). The target is under 400 files.
2. **Uniqueness and normalization.** The theorem gives an `∃`. The statement of 06 needs the map. Add the normalization: a uniformizer goes to a geometric Frobenius on the maximal unramified extension, the convention of 06.1. With the normalization fixed, prove that the map is unique, then define `artinMap K L` from it.
3. **Compatibility.** Prove that `artinMap` commutes with the restriction maps for $K \subset L \subset L'$, and that it is functorial for a finite extension $K'/K$ through the norm.
4. **The infinite extension.** Pass to the limit over finite abelian $L$, and get $K^\times \to \mathrm{Gal}(K^{ab}/K)$, continuous, injective with dense image, and its profinite completion an isomorphism. The existence theorem of NYLL (its order isomorphism of norm subgroups [R]) gives the image.
5. **The Weil group.** Define `WeilGroup K` as the preimage of $\mathbb{Z}$ (the powers of Frobenius) in $\mathrm{Gal}(K^{sep}/K)$, with the topology in which the inertia group is open. Prove that its abelianization is $W_K^{ab} \cong$ the preimage of $\mathbb{Z}$ in $\mathrm{Gal}(K^{ab}/K)$.
6. **The statement.** `LocalReciprocityGL1 K` is the statement `Kˣ ≃ₜ* (WeilGroup K)ᵃᵇ`, with the normalization of step 2. The proof follows from steps 4 and 5.
7. **Characters.** Corollary: continuous characters of $K^\times$ match continuous characters of $W_K$. This is `LocalLanglandsGL 1 K`. It is the first case of the main local statement, and the first `proved` node of the map of kind `theorem` on a statement of 06.

The cross-checks of the port:
- prove the same theorem for p-adic $K$ from lana-agents in the cross-check package;
- compare the normalization with riemann-lean's Lubin-Tate reciprocity (read only, 5.6).

## 5.6 The cross-checks

Each statement of document 06 that has a counterpart in another Lean project gets a bridge: a proof that the two statements are equivalent, or that one implies the other, in the cases where both apply. A bridge that fails shows a difference of meaning, and the fidelity battery records it (F2 of 06.3).

| Project statement | Counterpart | Where it lives | Bridge |
|---|---|---|---|
| `ModularityEllipticQ` | `modularityConjecture E` in `FormalConjectures/Wikipedia/ModularityConjecture.lean` [P]; it uses a q-expansion form of an eigenform because Mathlib has no Hecke operators | `Langlands/Bridges/FormalConjectures.lean` | equivalence, after the Hecke operators of T4 are defined |
| `ModularityEllipticQ`, semistable case | `WeierstrassCurve.modularity_of_semistableModel` of anthropics FLT [R] | `Langlands/Bridges/AnthropicFLT.lean`, after the port | the semistable case of the project's statement follows |
| `SatoTate` | `satoTate_conjecture` in `FormalConjectures/Wikipedia/SatoTateConjecture.lean` [P] | `Langlands/Bridges/FormalConjectures.lean` | equivalence |
| `RamanujanGL` for $n = 2$, level 1, weight 12 | `ramanujan_petersson` (for τ) in `RamanujanTau.lean` [P] | same | the project's statement implies it |
| the automorphic forms of `ReciprocityGL` over $\mathbb{Q}$ | `IsAutomorphicForm` for $GL_n$ over $\mathbb{Q}$ in `FormalConjecturesForMathlib/NumberTheory/AutomorphicForm/BorelJacquet.lean` [P] | same | the two definitions of automorphic form are equal |
| `GlobalReciprocity` | `reciprocityMap` and `ker_reciprocityMap` of riemann-lean [P] | the package `langlands-crosscheck` | the riemann-lean theorem implies the project's statement |
| `LocalReciprocityGL1` | `exists_isAbelianGalois_range_normUnits_eq` and Lubin-Tate reciprocity of riemann-lean [P] | `langlands-crosscheck` | same normalization, same map |
| Tate's thesis (`HeckeFunctionalEquation`, T3) | `completedLFunction_eq_rootNumber_mul` of riemann-lean [P] | `langlands-crosscheck` | the two root numbers are equal |

Rules for the cross-check package:
- `langlands-crosscheck` is a separate Lake package that `Langlands` does not import.
- It fetches riemann-lean at a pinned commit, on its own pin v4.33.1, and redistributes nothing.
- It is built only in the weekly trust run. A build of riemann-lean is a large job (document 14).
- formal-conjectures (`9097e2f90e`, v4.33.1) is on the same old pin. Its bridges therefore also live in a separate package until it bumps. The project may send its own statements to formal-conjectures (Q-22 of document 16). formal-conjectures has no file that contains the string "Langlands" [P].

## 5.7 What the base does not give

- **No reductive groups over a base.** Mathlib has root data and `GL (Fin n) R`, but no reductive group schemes, no Borel subgroups as schemes and no L-groups. The project starts T2 from root data and makes the L-group a combinatorial object first (06.1). riemann-lean has 410,000 lines on reductive groups, which the project cannot copy.
- **No smooth representation theory.** Three PRs are open (5.1). The local side of every statement after GL(1) waits for this. It is the work of milestone S3.
- **No Galois representations of automorphic forms.** Eichler-Shimura and Deligne are absent everywhere. anthropics FLT has the weight 2 case only in the strength that FLT needs. These enter as `proved-mod` hypotheses with named sources (09.2.2).
- **No trace formula.** riemann-lean has 493 lines under `TraceFormulas`. No licensed source has any. Route R5 starts from zero.
- **No Shimura varieties, no $\mathrm{Bun}_G$, no D-modules, no IndCoh.** The geometric and p-adic layers (T9, T10) have only the TauCeti adic spaces and the Mathlib condensed seeds. A Lean statement of `GeometricLanglands` is years away. Document 06 states it as a goal, not as a near-term target.
- **No checked statement of any Langlands conjecture.** Nothing found in Lean states functoriality, the LLC for $GL_n$ with both sides defined, or the Ramanujan conjecture for $GL_n$, with a fidelity check [U]. That is the work of G1 (document 02). The base gives the parts. It does not give the statements.
