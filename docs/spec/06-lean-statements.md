# 06. The Lean statements and how to trust them

A Lean proof is worth only as much as its statement. In the Langlands program this risk is large, for two reasons:
- The main statements are correspondences. A bare bijection between two sets of the same cardinality is easy to prove and says nothing. The content is in the properties that pin down the bijection: L-factors, ε-factors, Frobenius traces, local-global compatibility.
- The vocabulary is deep. An automorphic representation, a Weil-Deligne representation or an L-packet has several standard definitions. These definitions agree only after a theorem.

This document fixes the Lean form of the main statements and the checks that each statement passes before any proof of it counts.

The statements live in one file per family, `Langlands/Statements/*.lean`. Each file imports only Mathlib and `Langlands/Statements/Basic.lean`.
- The files are small and have comments. They are the files that a referee reads.
- Each statement is a `def ... : Prop`. A proof is a separate `theorem` in another file.
- The statement files are pinned in `manifests/statements.sha256` and compared with `lake comparator` (09.6).

The Mathlib names in this document are those of the pin of 09.3, as reported in document 05 [S]. The `stater` role checks each name at S0, and a renamed declaration changes only the code, not the decision.

## 6.1 The vocabulary

All names are in the namespace `Langlands`. Where Mathlib or a ported source (05) has the notion, the statement uses it and does not define it again. The vocabulary below is the part that the GL-type statements need. It is written at S0.

```lean
import Mathlib

universe u

namespace Langlands

section Local

variable (K : Type u) [Field K] [ValuativeRel K] [TopologicalSpace K]
  [IsNonarchimedeanLocalField K]

/-- The Weil group `W_K`: the elements of the absolute Galois group that act on the
    residue field of the separable closure as an integer power of the Frobenius,
    with the topology in which the inertia subgroup is open and has its profinite
    topology. -/
def WeilGroup : Type u := sorry -- written at S0; no `sorry` remains in the pinned file

instance : Group (WeilGroup K) := sorry
instance : TopologicalSpace (WeilGroup K) := sorry
instance : IsTopologicalGroup (WeilGroup K) := sorry

/-- The map to the absolute Galois group: continuous, injective, with dense image. -/
def WeilGroup.toGalois : WeilGroup K →* Field.absoluteGaloisGroup K := sorry

/-- The degree: `w` acts on the residue field as `Frob ^ degree w`, where `Frob` is
    the arithmetic Frobenius `x ↦ x ^ q`. -/
def WeilGroup.degree : WeilGroup K →* Multiplicative ℤ := sorry

/-- The topological abelianization: the quotient by the closure of the commutator subgroup. -/
def WeilGroup.Ab : Type u := WeilGroup K ⧸ (commutator (WeilGroup K)).topologicalClosure

/-- A Frobenius-semisimple Weil-Deligne representation of dimension `n` over `ℂ`. -/
structure WeilDeligneRep (n : ℕ) where
  r : WeilGroup K →* Matrix.GeneralLinearGroup (Fin n) ℂ
  r_smooth : ∃ U : Subgroup (WeilGroup K), IsOpen (U : Set (WeilGroup K)) ∧ U ≤ r.ker
  N : Matrix (Fin n) (Fin n) ℂ
  N_nilpotent : IsNilpotent N
  N_conj : ∀ w, (r w : Matrix _ _ ℂ) * N * (r w)⁻¹ =
    (Nat.card (IsLocalRing.ResidueField 𝒪[K]) : ℂ) ^ (-(Multiplicative.toAdd (WeilGroup.degree K w))) • N
  frobSS : ∀ w, IsSemisimple (r w : Matrix _ _ ℂ)

end Local

/-- A smooth representation of a topological group on a complex vector space: the
    stabilizer of each vector is open. -/
def IsSmooth {G V : Type*} [Group G] [TopologicalSpace G] [AddCommGroup V] [Module ℂ V]
    (ρ : Representation ℂ G V) : Prop :=
  ∀ v : V, IsOpen {g : G | ρ g v = v}

/-- Isomorphism classes of irreducible smooth representations of `G`. -/
def IrrSmooth (G : Type u) [Group G] [TopologicalSpace G] : Type (u + 1) := sorry
```

The `sorry` above marks the bodies that the S0 milestone writes. The pinned file has none. CI rejects a statement file that contains `sorry`, `axiom` or `opaque` (09.2).

Three decisions in the vocabulary:
- **The Weil group is a subgroup of the Galois group with a finer topology.** The project does not take the Weil group as an abstract extension. The definition as a subgroup is the one of Tate's "Number theoretic background" (Corvallis 1979). It makes `toGalois` injective by construction.
- **The normalization is geometric.** The local reciprocity map sends a uniformizer to a geometric Frobenius (degree $-1$), as in Deligne and Harris-Taylor. The other normalization is a theorem: compose with inversion.
- **Representations are complex.** The statements over $\overline{\mathbb{Q}}_\ell$ are proved equivalent by a choice of field isomorphism $\iota : \overline{\mathbb{Q}}_\ell \cong \mathbb{C}$. This is a check of F2, and every statement that uses $\iota$ says so.

## 6.2 The main statements

Each statement has a class: **theorem** (a published proof accepted by experts), **open** (a conjecture), or **claimed** (a fresh claim, 01.2). Each statement also has a vocabulary status:
- **ready**: the statement can be written at the pin with the vocabulary of 6.1;
- **partial**: it needs a definition that the project writes in tiers T1 to T4;
- **missing**: it needs a theory that does not exist in Lean, for example reductive group schemes, D-modules on stacks or diamonds.

### 6.2.1 Abelian and local statements

```lean
/-- Local class field theory as the local Langlands correspondence for GL(1). -/
def LocalReciprocityGL1 : Prop :=
  ∀ (K : Type u) [Field K] [ValuativeRel K] [TopologicalSpace K] [IsNonarchimedeanLocalField K],
    ∃ rec : Kˣ ≃ₜ* WeilGroup.Ab K,
      -- normalization: a uniformizer maps to a geometric Frobenius
      (∀ ϖ : Kˣ, IsUniformizer (ϖ : K) → WeilGroup.Ab.degree K (rec ϖ) = Multiplicative.ofAdd (-1)) ∧
      -- the finite quotients: for every finite abelian `L / K`, the composite to
      -- `Gal(L/K)` is surjective with kernel the norm group
      (∀ (L : Type u) [Field L] [Algebra K L] [FiniteDimensional K L] [IsAbelianGalois K L],
        Function.Surjective (WeilGroup.Ab.restrict K L ∘ rec) ∧
        ∀ x, WeilGroup.Ab.restrict K L (rec x) = 1 ↔ IsFieldNorm K L x)

/-- The local Langlands correspondence for GL(n), characterized as in Henniart. -/
def LocalLanglandsGL (n : ℕ) : Prop :=
  ∀ (K : Type u) [Field K] [ValuativeRel K] [TopologicalSpace K] [IsNonarchimedeanLocalField K],
    ∃ rec : ∀ m ≤ n, IrrSmooth (GL (Fin m) K) ≃ WDIso K m,
      IsLanglandsFamily K n rec
```

`IsLanglandsFamily` is a structure with six fields. Together they characterize the family uniquely (Henniart 1993) [S]:
1. for $m = 1$, `rec` is composition with `LocalReciprocityGL1`;
2. `rec` takes the central character to the determinant;
3. `rec` commutes with twists by characters;
4. `rec` takes the contragredient to the dual;
5. `rec` preserves the L-factors of pairs, $L(s, \pi \times \pi') = L(s, \text{rec}\,\pi \otimes \text{rec}\,\pi')$;
6. `rec` preserves the ε-factors of pairs, with respect to a fixed additive character.

The L-factors and ε-factors of pairs on the automorphic side are those of Jacquet, Piatetski-Shapiro and Shalika. On the Galois side they are those of Deligne and Langlands. Both are definitions of tier T5. So `LocalLanglandsGL` is `partial` at S0. It becomes `ready` at S3.

### 6.2.2 The list

| Statement | Informal meaning | Class | Vocabulary | Planned |
|---|---|---|---|---|
| `LocalReciprocityGL1` | local CFT as above (Lubin-Tate, Serre) | theorem | ready | S0 |
| `LocalExistence` | each open subgroup of finite index in $K^\times$ is a norm group | theorem | ready | S0 |
| `GlobalReciprocity` | the Artin map $\mathbb{A}_K^\times / \overline{K^\times (K_\infty^\times)^\circ} \cong \text{Gal}(K^{ab}/K)$, compatible with `LocalReciprocityGL1` at each finite place | theorem | ready (Mathlib adeles) | S0 |
| `GlobalExistence` | each open subgroup of finite index in the idele class group is a norm group | theorem | ready | S0 |
| `KroneckerWeber` | $\mathbb{Q}^{ab} = \bigcup_n \mathbb{Q}(\zeta_n)$; a check of `GlobalReciprocity` | theorem | ready | S0 |
| `LocalLanglandsTorus` | $\text{Hom}_{cts}(T(K), \mathbb{C}^\times) \cong H^1(W_K, \hat T)$ for a torus given by its character lattice (Langlands) | theorem | ready | S1 |
| `HeckeFunctionalEquation` | the completed Hecke L-function of a Hecke character has meromorphic continuation and $\Lambda(s, \chi) = \varepsilon(s, \chi)\Lambda(1 - s, \bar\chi)$ (Tate's thesis) | theorem | partial (Mathlib `HeckeCharacter`) | S1 |
| `LocalLanglandsGL n` | 6.2.1 | theorem (Harris-Taylor, Henniart, Scholze) | partial | S0 shape, S3 full |
| `LocalLanglandsGL2` | the case $n = 2$, with the explicit form of Bushnell-Henniart | theorem (Kutzko) | partial | S3 |
| `LocalLanglandsSL2` | L-packets of $SL_2$ from restriction of $GL_2$ (Labesse-Langlands, Gelbart-Knapp) | theorem | partial | S5 |
| `LocalLanglandsGSp4` | Gan-Takeda | theorem | partial | S6 |
| `LocalLanglandsG2` | Gan-Savin, with the TauCeti roadmap PR #2458 as a bridge | theorem | missing ($G_2$ as a group scheme) | S6 |
| `LocalLanglands G` | the general conjecture: a finite-to-one map from $\text{Irr}(G(K))$ to L-parameters, with the desiderata of Borel, the internal structure of packets and the character identities | open | missing (reductive groups over $K$) | S3 shape |
| `FormalDegree` | the formal degree conjecture of Hiraga-Ichino-Ikeda | open (theorem for some groups) | missing | S8 |
| `LocalGGP` | the local Gan-Gross-Prasad conjecture | theorem in many cases | missing | S8 |
| `FarguesScholzeCompatible` | the Fargues-Scholze parameter equals the classical one for $GL_n$ | theorem | missing (diamonds) | R9 |
| `ModularityEllipticQ` | each elliptic curve over $\mathbb{Q}$ has a weight 2 newform with the same L-series (BCDT) | theorem | ready (q-expansions) | S0 |
| `ModularitySemistableQ` | the semistable case (Wiles, Taylor-Wiles); bridge to anthropics FLT | theorem | ready | S0 |
| `EichlerShimuraDeligne` | each newform of weight $k \ge 2$ has a compatible system of $\ell$-adic Galois representations with $\text{tr}\,\rho(\text{Frob}_p) = a_p$ | theorem | partial | S4 |
| `RamanujanPeterssonHolomorphic` | $\lvert a_p \rvert \le 2 p^{(k-1)/2}$ for a newform of weight $k$ (Deligne) | theorem | ready | S0 |
| `SerreModularity` | each odd irreducible $\bar\rho : G_\mathbb{Q} \to GL_2(\overline{\mathbb{F}}_p)$ is modular (Khare-Wintenberger) | theorem | ready | S4 |
| `FontaineMazurGL2Q` | each odd irreducible 2-dimensional $\ell$-adic representation that is de Rham at $\ell$ with distinct Hodge-Tate weights comes from a newform (Kisin, Emerton, Pan) | theorem with conditions [S] | partial ($p$-adic Hodge theory) | S8 |
| `ArtinOdd2Q` | Artin's conjecture for odd 2-dimensional representations of $G_\mathbb{Q}$ | theorem | partial (Artin L-functions) | S4 |
| `ArtinConjecture` | each non-trivial irreducible Artin L-function is entire | open | partial | S2 |
| `SatoTate` | Sato-Tate for non-CM elliptic curves over $\mathbb{Q}$ (Barnet-Lamb, Geraghty, Harris, Taylor); bridge to formal-conjectures | theorem | ready | S0 |
| `HasseWeilEllipticQ` | $L(E, s)$ is entire with a functional equation; corollary of modularity | theorem | ready | S0 |
| `HasseWeil` | the general Hasse-Weil conjecture for smooth projective varieties over number fields | open | partial | S8 |
| `JacquetLanglandsGL2` | the Jacquet-Langlands correspondence between $GL_2$ and the units of a quaternion algebra | theorem | partial | S6 |
| `SelbergEigenvalue` | $\lambda_1 \ge 1/4$ for congruence subgroups | open | ready (Laplacian on $\Gamma \backslash \mathbb{H}$) | S2 |
| `RamanujanMaass` | Ramanujan for Maass forms for $GL_2$ over $\mathbb{Q}$ | open | partial | S4 |
| `RamanujanGL n K` | each cuspidal automorphic representation of $GL_n(\mathbb{A}_K)$ has tempered local components | open | partial (automorphic forms of $GL_n$) | S4 |
| `AutomorphicToGalois n K` | regular algebraic cuspidal $\pi$ of $GL_n(\mathbb{A}_K)$, $K$ CM, gives a compatible system with local-global compatibility at unramified places (HLTT, Scholze) | theorem | partial | S8 |
| `ReciprocityGL n K` | the bijection of Clozel and Fontaine-Mazur: cuspidal algebraic $\pi$ and irreducible geometric $\rho$ with equal Satake and Frobenius polynomials at almost all places | open | partial | S4 |
| `FunctorialityGL n m r` | for an algebraic representation $r : GL_n(\mathbb{C}) \to GL_m(\mathbb{C})$, each cuspidal $\pi$ of $GL_n(\mathbb{A}_K)$ has an isobaric transfer $\Pi$ with $\text{Sat}(\Pi_v) = r(\text{Sat}(\pi_v))$ at almost all $v$ | open | partial | S4 |
| `SymPowerFunctoriality` | the case $r = \text{Sym}^n$ for holomorphic newforms (Newton-Thorne) | theorem | partial | S8 |
| `BaseChangeCyclic` | cyclic base change for $GL_n$ (Arthur-Clozel) | theorem | partial | S8 |
| `Functoriality G H r` | the general principle for an L-homomorphism ${}^L H \to {}^L G$ | open | missing | S3 shape |
| `FundamentalLemma` | Ngô's theorem, first in the Lie algebra form for unitary groups (Laumon-Ngô) | theorem | partial (orbital integrals) | S8 |
| `ArthurClassification` | the endoscopic classification of the discrete spectrum of quasi-split symplectic and orthogonal groups | theorem, `proved-mod` the twisted weighted fundamental lemma | missing | S8 shape |
| `ReciprocityFunctionFieldGL n` | L. Lafforgue: cuspidal automorphic representations of $GL_n(\mathbb{A}_F)$, $F$ a global function field, match irreducible $\ell$-adic representations, with equal Hecke and Frobenius data at every place | theorem | partial | S6 |
| `VLafforgueParametrization` | the automorphic to Galois direction for every reductive $G$ over a function field | theorem | missing | R7 |
| `GeometricLanglands` | GLC I to V: $\mathbb{L}_G : \text{D-mod}_{1/2}(\text{Bun}_G) \simeq \text{IndCoh}_{\text{Nilp}}(\text{LS}_{\check G})$ | theorem | missing (derived stacks, D-modules, IndCoh) | R8 |
| `PadicLanglandsGL2Qp` | Colmez-Paskunas: the $p$-adic correspondence for $GL_2(\mathbb{Q}_p)$, through the Montreal functor | theorem | missing ($(\varphi, \Gamma)$-modules) | R9 |
| `BreuilMezardGL2Qp` | the Breuil-Mézard conjecture for $GL_2(\mathbb{Q}_p)$ (Kisin, Paskunas) | theorem | partial | R9 |

The table has 44 rows. G1 (02.3) has two parts:
- **G1a: the GL-type statements.** These are the rows with vocabulary `ready` or `partial`. They need only $GL_n$, modular forms, adeles and the Weil group. Target: all of them stated and through F5 by S4.
- **G1b: the statements for a general reductive group.** These are the rows with vocabulary `missing`. They wait for reductive groups over local and global fields (tier T2), or for theories outside the first two years (tier T10). Until then, each has a node with status `unstated`. The node lists the missing definitions as `needs` edges.

The project writes the shape of each G1b statement early, with the missing definitions as named parameters of a structure. An example is `LocalLanglands (G : ReductiveGroupData K)` with a `ReductiveGroupData` that is only an interface. This lets the handbook and the map refer to it. Such a shape is not a statement and does not count for G1.

### 6.2.3 The decisions in these statements

| Decision | Choice | Why |
|---|---|---|
| A bijection or a characterized bijection | always characterized | a bare bijection between $\text{Irr}(GL_n(K))$ and $n$-dimensional Weil-Deligne representations exists for reasons of cardinality; the content is the list of 6.2.1 |
| $\mathbb{C}$ or $\overline{\mathbb{Q}}_\ell$ | $\mathbb{C}$ for local and automorphic statements; $\overline{\mathbb{Q}}_\ell$ with an explicit $\iota$ for Galois statements | the standard choice; the check of F2 proves independence of $\iota$ where it is known |
| Global reciprocity: all places or almost all places | almost all places in `ReciprocityGL`, with the full local-global compatibility as a separate statement `LocalGlobalCompatibility` | by strong multiplicity one and Chebotarev, almost all places determine both sides; full compatibility is a stronger theorem (Taylor-Yoshida, Caraiani) |
| Modularity: q-expansions or automorphic representations | q-expansions for statements over $\mathbb{Q}$ | Mathlib has modular forms and q-expansions; the automorphic form is a theorem of tier T4 |
| Reductive groups | split groups and concrete matrix groups first ($GL_n$, $SL_2$, $Sp_{2n}$, $GSp_4$); the general case waits for tier T2 | Mathlib has root data but no reductive group schemes (05.1) |
| Universe | one universe `u` for fields | as in the bases; a check theorem moves the statements between universes |
| Hypotheses for deep inputs | a published but unformalized theorem is a named `def ... : Prop`, never an `axiom` | the proof of a downstream theorem shows its hypotheses in its type, and `#print axioms` stays clean (09.2) |

## 6.3 The fidelity battery

A statement is *trusted* only after it passes every check below. The results are rows of `records/fidelity.json`. The site shows them (12, page Trust).

| Check | What it does | Who does it |
|---|---|---|
| F1. Elaboration | the file builds with the pinned toolchain; it has no `sorry`, `axiom` or `opaque`; `#print axioms` of each statement shows at most the three standard axioms | CI |
| F2. Positive instances | proofs of known special cases from the statement or of the statement in a known case: `LocalLanglandsGL 1` from `LocalReciprocityGL1`; `KroneckerWeber` from `GlobalReciprocity`; the unramified characters; `ModularityEllipticQ` for $X_0(11)$ by a certified computation (13.4); `RamanujanPeterssonHolomorphic` for $\Delta$ against `RamanujanTau` of formal-conjectures | agent `stater` and people |
| F3. Negative instances | proofs that wrong variants are false or trivial: drop the ε-factor condition and show a second family that satisfies the rest (twisting by an unramified sign character of the determinant for $n = 2$ gives an example) [U]; use the arithmetic normalization and show that the twisted variant fails F2; state reciprocity at "some" places and show it is satisfied by a wrong match | agent `refuter` |
| F4. Triviality attack | a strong prover gets a budget to prove the statement in a trivial way: by cardinality, with an empty type of representations, through a universe quirk, or with a topology that makes everything open; a success is a failed check | agent `refuter`, budget in 10.6 |
| F5. Round trip | an independent model translates the Lean statement to English without the docstring; a person compares the result with the docstring and with the source paper | agent `explainer` and people |
| F6. Human review | two number theorists sign that the Lean statement means the docstring; the names and dates go into `records/fidelity.json` | people |
| F7. Pinning | the statement file hash is in `manifests/statements.sha256`; `lake comparator` matches each proof to the pinned statement | CI |

A statement of class `theorem` counts for G1 after F1 to F5. A statement that a top theorem of 14.2 proves needs F6 too.

A statement of class `open` needs all seven before any proof of it is announced. F6 must have reviewers from two different groups of document 01. The groups include:
- a local Langlands group, such as the Kaletha, Fintzen or Gan circles;
- an automorphy lifting group, such as the Taylor, Calegari, Gee, Newton or Thorne circles;
- a trace formula group, such as the Arthur or Shin circles;
- a geometric group, such as the Gaitsgory, Raskin or Ben-Zvi circles.

A statement is frozen after F6. A change after F6 starts the battery again.

## 6.4 The bridges to other statements

In 2026 there are several public Lean statements that overlap the project's. Each is a test of the project's statements, because different people wrote them for different purposes.

| External statement | Where | Bridge to prove |
|---|---|---|
| `finiteAbelianLocalReciprocity` | NYLL (05.5) | the finite part of `LocalReciprocityGL1` is equivalent to it; the project ports the proof |
| `reciprocityMap`, `ker_reciprocityMap` | riemann-lean (read only) | in the cross-check package only (05.6): `GlobalReciprocity` from them, built but not distributed while the licence is open |
| `completedLFunction_eq_rootNumber_mul` | riemann-lean | the same, for `HeckeFunctionalEquation` |
| `ModularityConjecture` | formal-conjectures | equivalent to `ModularityEllipticQ` |
| `SatoTate` | formal-conjectures | equivalent to `SatoTate` |
| `RamanujanTau` | formal-conjectures | follows from `RamanujanPeterssonHolomorphic` |
| `HasseWeil` | formal-conjectures | the elliptic case is `HasseWeilEllipticQ` |
| `IsAutomorphicForm` for $GL_n$ over $\mathbb{Q}$ (Borel-Jacquet) | formal-conjectures | the project's automorphic forms of $GL_n(\mathbb{A}_\mathbb{Q})$ agree with it on $K$-finite vectors |
| semistable modularity, Langlands-Tunnell (octahedral) | anthropics/fermats-last-theorem (`Theorems/`) | `ModularitySemistableQ` is equivalent to their top statement; their Langlands-Tunnell statement against the project's `ArtinOdd2Q` restricted to octahedral image |
| quaternionic automorphic forms, Hecke operators | Imperial FLT | the project's `JacquetLanglandsGL2` uses their definitions, with an equivalence where the definitions differ |
| `PadicLocalLanglandsForGL2Qp`, `LanglandsParameterStacks`, `LLC for G2` roadmaps | TauCeti | when a TauCeti statement exists, the project proves it equivalent to `PadicLanglandsGL2Qp` or `LocalLanglandsG2` |

The bridges are proved in `Langlands/Bridge/`, one file per external statement. Each external statement is copied word for word into the bridge file with its source commit. A change upstream then shows as a failed comparison, not as a silent change of meaning. For riemann-lean, the copy stays in the cross-check package, which is not distributed (05.3).

## 6.5 Misformalization risks, ranked

1. **Bijection by cardinality.** A correspondence statement that loses one of its characterizing properties becomes trivial. Check: F4, and for each correspondence a Lean proof that the remaining properties do not determine the bijection (F3).
2. **The Weil group and its topology.** With the subspace topology from the Galois group, the Weil group is not locally compact, and its abelianization is not $K^\times$. Check: `WeilGroup.Ab K ≃ₜ* Kˣ` fails with the wrong topology (F3), and the inertia subgroup is open and compact (F2).
3. **The normalization.** Arithmetic and geometric Frobenius differ by an inverse. A statement with the wrong sign is still a theorem, but its compositions with other statements fail. Check: one normalization lemma, used by every statement, and the F2 instance of unramified characters.
4. **Smooth, admissible and irreducible.** Irreducible smooth representations of $GL_n(K)$ are admissible (Jacquet, Bernstein). A definition that asks for admissibility is equivalent only after that theorem. Check: state both and prove the equivalence in tier T5. Until then, the statements use smooth irreducible and say so.
5. **Automorphic forms.** Classical, adelic, $L^2$ and $K$-finite definitions differ. Check: the bridge to `IsAutomorphicForm` of formal-conjectures, and the classical to adelic dictionary for $GL_2$ (tier T4) as a theorem.
6. **L-factors and ε-factors.** The ε-factor depends on an additive character and a Haar measure. Check: the dependence is proved, and the statement fixes the character of conductor $\mathcal{O}_K$ where a choice is needed.
7. **Hecke eigenvalues and Satake parameters.** Unitary and arithmetic normalizations differ by $q^{(n-1)/2}$. Check: the $GL_2$ case against the q-expansion of $\Delta$ and of the newform of level 11.
8. **The choice of $\iota$.** A statement that uses $\iota : \overline{\mathbb{Q}}_\ell \cong \mathbb{C}$ without saying so can depend on it. Check: `#print axioms` shows `Classical.choice` anyway, so the check is structural: $\iota$ is an explicit parameter.
9. **Universe and size.** A statement over `Type u` that is proved only for `u = 0`. Check: `#check @theorem.{1}` works.

## 6.6 Claims

The project never states in its README, on the site or in a release note that it has proved an open case unless all of these hold:
- the proof builds;
- the axioms are the three standard ones;
- two kernels accept it (the Lean kernel and nanoda, 14.1);
- the statement passed F1 to F7;
- at least two experts who are not paid by the project have read the written proof in the handbook.

Before that, the status is "a Lean proof that has passed the checks C1 to Cn". The site says which checks (14).

For a fresh claim of route R1 the rule is the same in the other direction. The project says only "a Lean check of section X of the preprint found Y". It names the statement, the hypotheses and the checks passed. It writes to the authors before any page goes public (14.4). A fresh claim is never a hypothesis of another node. It enters as a hypothesis only after its paper is accepted by experts, and then as a named `Prop` with its paper record (07.13).
