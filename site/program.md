---
title: The program
description: The main conjectures of the Langlands program, the parts that are theorems, the parts that are open, and the levels of success of the project.
lead: The Langlands program is a network of conjectures that relate Galois representations, automorphic representations and their L-functions. Some parts are theorems. The general conjectures are open. This project does not prove an open conjecture.
---
## The program in short

Let $F$ be a global field: a finite extension of $\mathbb{Q}$, or the function field of a curve over $\mathbb{F}_q$. Let $G$ be a connected reductive group over $F$. The program predicts three things. Reciprocity matches automorphic representations of $G$ with Galois representations into the L-group ${}^L G$. Functoriality transfers automorphic representations from one group to another along a map of L-groups. The local correspondence matches irreducible representations of $G(F_v)$ at each place $v$ with local Langlands parameters. The three predictions agree with each other through L-functions and Satake parameters.

The program is not one statement. Each conjecture has choices: the normalization of Frobenius and of L-functions, the class of representations, the form of the parameters and the field of coefficients. These choices change the meaning of a statement. The project fixes one choice for each statement in its Lean form. The [statements page](/statements/) lists the Lean statements.

## The main conjectures

**The local Langlands correspondence for $\mathrm{GL}_n$.** Let $F$ be a nonarchimedean local field. There is a unique family of bijections $\mathrm{rec}_F$ from the irreducible smooth representations of $\mathrm{GL}_n(F)$ to the $n$ dimensional Frobenius semisimple Weil-Deligne representations of $W_F$, for $n \ge 1$. For $n = 1$ it is the reciprocity map of local class field theory. The family is compatible with twists, central characters, duals, and the L-factors and $\varepsilon$-factors of pairs. Henniart proved that these properties determine the family. This is a theorem: Laumon, Rapoport and Stuhler (1993) for $\mathrm{char}\, F = p$, Harris-Taylor (2001) and Henniart (2000) for $p$-adic $F$, and a second proof by Scholze (2013). For $n = 2$ a purely local proof exists (Kutzko 1980, Bushnell-Henniart 2006). Every known proof for general $n$ uses global input.

**The local Langlands correspondence for a general $G$.** The conjecture asks for a map from $\mathrm{Irr}(G(F))$ to the set $\Phi(G)$ of Langlands parameters, with finite fibres, the L-packets. It must satisfy the desiderata of Borel, the internal structure of the packets and the character identities. This is open. It is known for classical groups (Arthur, Mok and others), for $\mathrm{GSp}_4$ (Gan-Takeda), for $G_2$ (Gan-Savin) and for many special classes. Fargues and Scholze construct a semisimple parameter for every $G$. Its agreement with the classical correspondence is known only case by case.

**Global reciprocity for $\mathrm{GL}_1$.** This is class field theory. The Artin map is a continuous surjection $C_F \to \mathrm{Gal}(F^{\mathrm{ab}}/F)$ from the idele class group $C_F = \mathbb{A}_F^\times / F^\times$, and it is compatible with the local maps at each place. It is a theorem.

**Global reciprocity for $\mathrm{GL}_n$.** Let $F$ be a number field. The conjecture of Clozel and Fontaine-Mazur asks for a bijection between the cuspidal algebraic automorphic representations $\pi$ of $\mathrm{GL}_n(\mathbb{A}_F)$ and the irreducible geometric $\ell$-adic representations $\rho$ of $\mathrm{Gal}(\bar F / F)$ of dimension $n$, with equal Satake and Frobenius data at almost all places. It is open. The direction from automorphic to Galois is known for regular algebraic $\pi$ over totally real and CM fields. The direction from Galois to automorphic is the modularity problem. It is known for elliptic curves over $\mathbb{Q}$ (Breuil, Conrad, Diamond and Taylor) and in many other cases.

**Functoriality.** Let $H$ and $G$ be connected reductive groups over $F$, with $G$ quasi split, and let $\phi : {}^L H \to {}^L G$ be an L-homomorphism. For each automorphic representation $\pi$ of $H$ there is an automorphic representation $\Pi$ of $G$ with $c_v(\Pi) = \phi(c_v(\pi))$ for almost all places $v$. This is open in general. Known cases include Jacquet-Langlands, cyclic base change, $\mathrm{Sym}^2$, $\mathrm{Sym}^3$, $\mathrm{Sym}^4$, the transfer from classical groups to $\mathrm{GL}_N$, and $\mathrm{Sym}^n$ of holomorphic eigenforms without CM for all $n$ (Newton-Thorne 2021).

**Arthur's conjectures.** They describe the discrete spectrum with A-parameters and a multiplicity formula. Arthur (2013) and Mok (2015) proved the classification for quasi split symplectic, orthogonal and unitary groups, on the condition of the twisted weighted fundamental lemma. Halleck and Dube claimed a proof of that lemma on 2026-11-19. The project records this as a claim until experts accept it.

**The consequences.** The Ramanujan conjecture, the Artin conjecture, the Sato-Tate conjecture and the Hasse-Weil conjecture follow from cases of reciprocity and functoriality. Each is known in some cases and open in general.

**Function fields.** Over a function field the program is much further on. L. Lafforgue (2002) proved reciprocity for $\mathrm{GL}_n$. V. Lafforgue (2018) proved the direction from automorphic to Galois for every reductive $G$.

**Geometric Langlands.** Gaitsgory, Raskin and coauthors proved the unramified geometric conjecture in characteristic 0, in the de Rham setting, for every reductive $G$, in five papers (2024 to 2026). The ramified, quantum and $\ell$-adic forms are open.

## What is proved and what is open

The table gives the state of the mathematics on 2026-11-25. It does not give the state of the Lean code. The [map](/map/) gives the Lean status of each node.

| Statement | Proved | Open |
|---|---|---|
| Local and global class field theory ($\mathrm{GL}_1$) | all global and local fields | nothing classical |
| Local Langlands for $\mathrm{GL}_n$ | all $n$, all nonarchimedean $F$ | an explicit form in general; a local proof for $n \ge 3$ |
| Local Langlands for a general $G$ | classical groups, $\mathrm{GSp}_4$, $G_2$, many special classes | existence with all desiderata; uniqueness; small $p$; $F_4$ to $E_8$ |
| Reciprocity for $\mathrm{GL}_n$ | $n = 1$; $n = 2$, odd, over $\mathbb{Q}$; many potential cases | general $n$; non regular and even cases; fields that are not CM or totally real |
| Functoriality | the known cases above | the general case; tensor products |
| Arthur's classification | quasi split classical groups, on the condition of the twisted weighted fundamental lemma | inner forms in general; exceptional groups |
| Ramanujan | Deligne; regular algebraic cases; function fields | Maass forms; Selberg's $1/4$; general $\mathrm{GL}_n$ |
| Artin | solvable image in dimension 2; odd dimension 2 over $\mathbb{Q}$ | even icosahedral; dimension $\ge 3$ |
| Sato-Tate | elliptic curves over totally real and CM fields | genus 2 in general |
| Modularity of elliptic curves | all $E$ over $\mathbb{Q}$ | general number fields |
| Function fields | $\mathrm{GL}_n$; automorphic to Galois for all $G$ | Galois to automorphic for general $G$ with ramification |
| Geometric Langlands | characteristic 0, de Rham, unramified | the six open problems of GLC V |
| $p$-adic Langlands | $\mathrm{GL}_2(\mathbb{Q}_p)$ | $\mathrm{GL}_2(K)$ for $K \neq \mathbb{Q}_p$; $\mathrm{GL}_n$; mod $p$ in general |

## The levels of success

The project measures its progress on six levels. G1 to G3 are engineering of known difficulty. G4 is research. G5 is a research result of the size of a paper. G6 is the program itself and has no date.

| Level | Name | What it means |
|---|---|---|
| G1 | The statements | The main conjectures and theorems are stated in Lean (44 statements), pinned by hash, checked by the fidelity battery F1 to F5, and joined to other public Lean statements where they overlap. |
| G2 | The first formal proofs | $\mathrm{GL}_1$ complete: local and global class field theory, the Weil group, the local correspondence for $\mathrm{GL}_1$ and for tori, Tate's thesis, Hecke L-functions. Then the local correspondence for $\mathrm{GL}_2$ over a $p$-adic field, first for odd $p$, then for all $p$. |
| G3 | The library and the handbook | The tiers T1 to T8 are `proved`, or `proved-mod` with named hypotheses that are published theorems. Volumes 0 to 13 of the handbook are released and reviewed. |
| G4 | Frontier checks and new partial results | A 2026 preprint is checked in Lean or refuted with a Lean certificate, or a new result of the size of a paper lemma is proved and read by an outside expert. |
| G5 | An open case | One named open target of the routes is proved in Lean, and all nine trust rows are yes. |
| G6 | The program | The general conjectures: the local correspondence for all $G$, reciprocity and functoriality over number fields, and the ramified and arithmetic geometric conjectures. |

## What the project claims

No open conjecture of the program is proved here. The project is at milestone S0. The map has no nodes yet, and no statement of the program is proved in Lean yet.

The project calls an open case proved only when all of these hold: the Lean proof builds; it uses only the three standard axioms; two kernels accept it; the statement passed the fidelity checks F1 to F7; and at least two experts who are not paid by the project have read the written proof. Until then, the site says which checks a result has passed. The [trust page](/trust/) lists the checks.

## What the project does not do

- It does not replace Mathlib. It sends general parts upstream when they are stable.
- It does not put geometric Langlands first. The formal proof of the geometric conjecture needs derived algebraic geometry, ind coherent sheaves and D-modules on stacks, and none of these exists in Lean.
- It does not announce the proof of an open case on the strength of a Lean build alone.
- It does not judge the work of other people. A check of a fresh claim reports what Lean found, and the authors see the result first.
- It does not copy code without a licence. It reads riemann-lean and math-yiluo/Langlands-lib and cites them, but it does not copy them.

The [routes](/routes/) say how the project works on the open parts.
