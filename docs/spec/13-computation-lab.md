# 13. The computation lab

In the Langlands program, computation has led theory more than once:
- the numerical tables of Birch and Swinnerton-Dyer;
- the first tables of modular forms and elliptic curves (Antwerp IV, Cremona);
- Sato and Tate's distribution;
- the numerical checks of Selberg's eigenvalue conjecture.

The LMFDB now holds millions of L-functions, modular forms, elliptic curves, genus 2 curves and Galois representations. Each object has a label, and each label has a page.

The lab has three uses:
- **Certified examples.** It gives the fidelity battery positive instances (06.3, F2) for the statements.
- **Tests.** It tests the explicit identities of fresh claims (route R1) and of conjectures on the routes, before anyone spends months on a proof.
- **Handbook data.** It gives the handbook its worked examples.

Its results are data, not proofs. A result enters the map only as a node of kind `example`, `counterexample`, `check` or `conjecture`. A result becomes a theorem only when Lean checks a certificate (13.4).

## 13.1 Tools

| Tool | Use | Note |
|---|---|---|
| PARI/GP | number fields, class groups, ray class fields, $L$-function values, elliptic curves, `mf` (modular forms), `lfun` | GPL; the main tool for tiers T1 to T4 |
| SageMath | glue; modular symbols; Hecke operators; $p$-adic computations; `sage.modular` | GPL |
| GAP and CHEVIE | character tables of finite groups of Lie type ($GL_2(\mathbb{F}_q)$, $Sp_4(\mathbb{F}_q)$, $G_2(\mathbb{F}_q)$), Deligne-Lusztig characters | GPL; for depth-zero types (R2) |
| FLINT and Arb | exact and ball arithmetic for certified numerics | LGPL |
| lcalc and the LMFDB `lfunctions` code | zeros and functional equations of $L$-functions | for R4 and R6 tests |
| LMFDB | data: labels, q-expansions, Galois representations, Satake parameters | read through its API; the licence of each data set is recorded in the run [U] |
| Magma | cross-checks only, where the project has a licence; never a required tool | proprietary; a result that only Magma reproduces is marked so |
| `lgl-lab` (Rust) | the inner loops: Hecke eigenvalue tables, point counts over $\mathbb{F}_q$, orbital integrals for small groups, Satake parameter statistics | written by the project, in `langlands-agent/lab/` |
| Lean | checks a certificate (13.4) | |

## 13.2 Specs and runs

A lab job is a spec file in `tamnd/langlands/lab/specs/<name>.yaml`:

```yaml
name: llc-gl2-qp-depth-le-2
question: For p in {3, 5, 7} and every irreducible smooth representation of GL2(Qp) of conductor exponent at most 4, does the explicit correspondence of Bushnell-Henniart match L- and epsilon-factors of pairs with the twists by characters of conductor at most 2?
tool: lgl-lab
inputs:
  p: [3, 5, 7]
  conductor_exponent: [0, 4]
  twist_conductor: [0, 2]
  additive_character: conductor-O
outputs: [table of pairs, factors on both sides, first mismatch if any]
node: LG7Y2N0QBE      # LocalLanglandsGL2, the explicit form
```

`lgl lab run` runs it in a container with pinned images and no network. It writes `lab/runs/<id>/` with these items:
- the spec hash;
- the image digests;
- the seed;
- the wall time;
- the outputs;
- a short summary.

A run is reproducible from its record.

## 13.3 The first experiments

| Id | Question | Route | Why it matters |
|---|---|---|---|
| E1 | Certified small cases of local reciprocity: the Artin map for $\mathbb{Q}_p$ and its ramified quadratic and cyclotomic extensions, for $p \le 7$, against Lubin-Tate | (library, S1) | F2 instances for `LocalReciprocityGL1`; examples for Volume 3 |
| E2 | The explicit LLC for $GL_2(\mathbb{Q}_p)$, $p$ odd, depth $\le 2$, with factors of pairs (the spec above); the same for $p = 2$ as data for the hard case | R2 | the data behind the G2 anchor of 04.12; a test of the normalizations of 06.5 |
| E3 | Depth-zero and regular supercuspidals of $SL_2$, $GSp_4$ and $G_2$ over small $p$, by Deligne-Lusztig; compare the parameters of Kaletha with those of Fintzen-Kaletha (2611.31396) and AKMS (2611.31683) on the cases where both apply | R1, R2 | a cheap test of two fresh claims (01.2) |
| E4 | Orbital integrals and transfer factors for $SL_2$ and $U(2)$, $U(3)$ over $\mathbb{Q}_p$ for small $p$; check the fundamental lemma numerically and compute the test cases of the twisted weighted form of Halleck-Dube (2611.26750) where they are explicit | R1, R5 | numerical evidence for or against a key step of a fresh claim |
| E5 | Modularity of the elliptic curves of LMFDB of conductor $\le 1000$: match $a_p$ with the newform up to the Sturm bound and the Faltings-Serre-Livné bound | R3, F2 | certified instances of `ModularityEllipticQ` (13.4) |
| E6 | Genus 2 curves and paramodular forms (BCGP, 2502.20645): which LMFDB abelian surfaces fall in the proved positive proportion, and why the others do not | R3 | maps the open part of abelian surface modularity |
| E7 | Satake parameter statistics for $\text{Sym}^n$ of newforms of small level, and for Maass forms of level 1 (Booker-Strömbergsson data); the Kim-Sarnak exponent on the data | R4, R6 | the data of the Ramanujan bounds; examples for Volume 7 |
| E8 | Serre weights for $\bar\rho : G_{\mathbb{Q}_{p^f}} \to GL_2(\overline{\mathbb{F}}_p)$ for small $p$ and $f$, against the predictions of Buzzard-Diamond-Jarvis and BHHMS | R9 | data for the mod $p$ route |
| E9 | The explicit identities of each new claim of route R1, where they can be computed | R1 | the cheapest test of a fresh claim |

## 13.4 Certificates: from computation to Lean

A computation that finds a specific object or a specific identity can be checked in Lean when it comes with a certificate. A certificate reduces the claim to a finite check plus a theorem that the project has proved or stated as a named hypothesis:

- **Sturm bound.**
  - Two modular forms of weight $k$ on $\Gamma_0(N)$ are equal when their first $\frac{k}{12}[SL_2(\mathbb{Z}) : \Gamma_0(N)]$ coefficients agree.
  - With the Sturm bound proved (tier T4), equality of forms is a finite check by `decide` or `norm_num` on the coefficients.
- **Faltings-Serre-Livné.**
  - Two 2-dimensional $\ell$-adic Galois representations with the same determinant and residual image of a given type are isomorphic when their traces agree on an explicit finite set of primes.
  - With the theorem stated as a named hypothesis, the check is a finite computation of point counts.
  - This certifies the newform attached to a given elliptic curve, as an instance of `ModularityEllipticQ` for that curve.
- **Point counts.** $\#E(\mathbb{F}_p)$ for a Weierstrass equation is a finite sum, checked by `decide` for small $p$.
- **Local factors.** For an explicit character or type, the L-factor and ε-factor are finite Gauss sums, checked by `norm_num` in a cyclotomic field.
- **Orbital integrals.** For $SL_2(\mathbb{Q}_p)$ and a small $p$, an orbital integral of the unit of the Hecke algebra is a finite sum over a set of lattices, given by the certificate, and checked by counting.

So a counterexample from the lab becomes a Lean theorem (`Langlands.Examples.*`) with status `proved`, and it can refute a node. A positive certificate is an F2 instance. The `refuter` role writes these theorems from the lab outputs.

## 13.5 What the lab does not do

- It does not decide that a statement is true. A conjecture with a million supporting examples has status `open`.
- It does not decide that a fresh claim is false. A numerical mismatch is a question for the authors (14.4). It becomes a Lean counterexample only through a certificate.
- It does not copy LMFDB data into the Lean tree. Data enters Lean only as a certificate for a specific node, with the LMFDB label and the run id.
