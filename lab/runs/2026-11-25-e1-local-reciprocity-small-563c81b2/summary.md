# 2026-11-25-e1-local-reciprocity-small-563c81b2

For p in {2, 3, 5, 7}, is the norm group of each quadratic extension of Q_p, and of each cyclotomic extension Q_p(zeta_{p^n}) with p^n <= 49, the kernel of the Artin map that Lubin-Tate theory with the uniformizer p predicts?

Result: agrees: in 27 fields each norm that the run computed is in the kernel that Lubin-Tate predicts, and each class of the kernel has a norm.

## What the run does

Local class field theory says that the Artin map of a finite abelian extension L of Q_p has the norm group N(L^x) as its kernel. Lubin-Tate theory with the uniformizer p gives the map: u p^v acts as the Frobenius to the power v on the unramified extensions, and as zeta to zeta^(1/u) on the roots of unity of p-power order. The run computes norms and compares them with the kernel that this formula predicts.

- Quadratic fields: for each Q_p(sqrt d), the run computes the norms a^2 - d b^2 with |a|, |b| <= 40 and finds their classes in Q_p^x modulo squares.
- Cyclotomic fields: for each Q_p(zeta_{p^n}) with p^n <= 49, the run computes the norm of 1 - zeta and of 200 random elements of Z[zeta] with coefficients in [-2, 2] (seed 1). Each norm is an exact determinant. The prediction is that the unit part of each norm is 1 mod p^n. The run also records which classes of (1 + p^n Z_p) / (1 + p^(n+1) Z_p) the norms reach.

## Quadratic fields

| p | d | kind | predicted kernel | classes of the norms | norms | outside |
|---|---|---|---|---|---|---|
| 2 | 5 | unramified | 1, 3, 5, 7 | 1, 3, 5, 7 | 3320 | 0 |
| 2 | -1 | ramified | 1, 5, 2, 10 | 1, 2, 5, 10 | 3320 | 0 |
| 2 | -5 | ramified | 1, 5, 6, 14 | 1, 5, 6, 14 | 3320 | 0 |
| 2 | 2 | ramified | 1, 7, 2, 14 | 1, 2, 7, 14 | 3320 | 0 |
| 2 | -2 | ramified | 1, 3, 2, 6 | 1, 2, 3, 6 | 3320 | 0 |
| 2 | 10 | ramified | 1, 7, 6, 10 | 1, 6, 7, 10 | 3320 | 0 |
| 2 | -10 | ramified | 1, 3, 10, 14 | 1, 3, 10, 14 | 3320 | 0 |
| 3 | 2 | unramified | 1, 2 | 1, 2 | 3320 | 0 |
| 3 | -3 | ramified | 1, 3 | 1, 3 | 3320 | 0 |
| 3 | -6 | ramified | 1, 6 | 1, 6 | 3320 | 0 |
| 5 | 2 | unramified | 1, 2 | 1, 2 | 3320 | 0 |
| 5 | 5 | ramified | 1, 5 | 1, 5 | 3320 | 0 |
| 5 | 10 | ramified | 1, 10 | 1, 10 | 3320 | 0 |
| 7 | 3 | unramified | 1, 3 | 1, 3 | 3320 | 0 |
| 7 | -7 | ramified | 1, 7 | 1, 7 | 3320 | 0 |
| 7 | -21 | ramified | 1, 21 | 1, 21 | 3320 | 0 |

## Cyclotomic fields

| p | n | degree | predicted norm group | norms | outside | classes k of 1 + k p^n | N(1 - zeta) = p |
|---|---|---|---|---|---|---|---|
| 2 | 2 | 2 | <2> x (1 + 4 Z_2) | 190 | 0 | 0, 1 | yes |
| 2 | 3 | 4 | <2> x (1 + 8 Z_2) | 201 | 0 | 0, 1 | yes |
| 2 | 4 | 8 | <2> x (1 + 16 Z_2) | 201 | 0 | 0, 1 | yes |
| 2 | 5 | 16 | <2> x (1 + 32 Z_2) | 201 | 0 | 0, 1 | yes |
| 3 | 1 | 2 | <3> x (1 + 3 Z_3) | 189 | 0 | 0, 1, 2 | yes |
| 3 | 2 | 6 | <3> x (1 + 9 Z_3) | 201 | 0 | 0, 1, 2 | yes |
| 3 | 3 | 18 | <3> x (1 + 27 Z_3) | 201 | 0 | 0, 1, 2 | yes |
| 5 | 1 | 4 | <5> x (1 + 5 Z_5) | 201 | 0 | 0, 1, 2, 3, 4 | yes |
| 5 | 2 | 20 | <5> x (1 + 25 Z_5) | 201 | 0 | 0, 1, 2, 3, 4 | yes |
| 7 | 1 | 6 | <7> x (1 + 7 Z_7) | 201 | 0 | 0, 1, 2, 3, 4, 5, 6 | yes |
| 7 | 2 | 42 | <7> x (1 + 49 Z_7) | 201 | 0 | 0, 1, 2, 3, 4, 5, 6 | yes |

## What the run does not do

- It is a search, not a proof. A norm in the predicted kernel is evidence, and only a certificate that Lean checks makes a theorem (spec 13.4).
- It checks the kernels of the Artin maps, the norm groups. For a quadratic field the kernel fixes the map. For a cyclotomic field of degree more than 2 the run does not check the map element by element.
- It shows that the norm groups are inside the predicted kernels only for the norms that it computed. It does not show that no other norm is outside.
- It covers only the quadratic and the cyclotomic fields of the spec, not every abelian extension.
- It runs in the lgl binary, not in a container with pinned images, and it uses no network and no other tool. The record gives the commit of lgl and the seed, so the outputs are reproducible.
