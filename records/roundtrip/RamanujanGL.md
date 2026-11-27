---
statement: Langlands.RamanujanGL
check: F5
date: 2026-11-27
---

## What the statement says

Fix n and a number field K. Let N be a nonzero element of O_K and let phi be a function on GL_n(A_K) with values in C. Suppose phi is a cusp form of level N in the sense of IsCuspForm:
- phi is continuous;
- phi(gamma g) = phi(g) for gamma in GL_n(K);
- phi(g k) = phi(g) for each k in the principal congruence subgroup of level N, that is, k is 1 at the infinite places and k and k^{-1} are congruent to 1 modulo N at each finite place;
- phi has a central character: there is a function omega on the ideles with phi(g z) = omega(z) phi(g) for each scalar z;
- phi has moderate growth: |phi(g)| <= C |det g|^s for some real C and s;
- for each r with 0 < r < n and each g, the integral of x -> phi(u_r(x) g) over (A_K/K)^{n x n} is 0, for every translation-invariant probability measure on the Borel sets of (A_K/K)^{n x n}. Here u_r(x) is the unipotent matrix 1 + x in the upper right block of size r x (n - r). The integrand is well defined because phi is left invariant under the K-points of this unipotent group.

Suppose also that phi is not 0 and that phi is bounded. Let v be a finite place and let ev be a sequence of complex numbers. Suppose phi is invariant under GL_n(O_v) and that T_{v,i} phi = ev(i) phi for 1 <= i <= n. Here T_{v,i} is the Hecke operator of the double coset of diag(varpi_v, ..., varpi_v, 1, ..., 1) with i entries varpi_v. It is the sum over the usual upper triangular coset representatives: diagonal entries varpi_v or 1, and an entry in O/varpi_v at the place (j, k) with j < k when d_j = varpi_v and d_k = 1. The conclusion is that each root alpha of X^n + sum_{i=1}^n (-1)^i q_v^{-i(n-i)/2} ev(i) X^{n-i} has |alpha| = 1.

The Satake parameters are the unitary normalisation: e_i(alpha) = q_v^{-i(n-i)/2} lambda(T_{v,i}). With this normalisation the trivial representation of GL_2 has parameters q_v^{1/2} and q_v^{-1/2}, which the F3 check in Langlands/Fidelity/GlobalGL.lean confirms. Boundedness of a nonzero phi with a central character forces |omega| = 1, so the hypothesis is the normalisation to a unitary central character. Every unitary cuspidal automorphic representation pi has bounded nonzero vectors, and for each finite place v where pi_v is unramified it has such a vector that is spherical at v. The function phi need not lie in one irreducible pi. It lies in the unitary cuspidal spectrum, and ev is then the Hecke eigensystem of each irreducible constituent in which phi has a nonzero component. So the statement is equivalent to this: for each unitary cuspidal automorphic representation pi of GL_n(A_K) and each finite place v where pi_v is unramified, the Satake parameters of pi_v have absolute value 1.

## Quantifiers

All quantifiers are universal: over N, phi, the finite place v and the eigensystem ev, and over the roots alpha. Nothing is existential. The place v is any finite place where phi is spherical, so v may divide N. The level structure is the full principal congruence subgroup at all finite places, and there is no condition at the infinite places. There is no K_infinity-finiteness and no Z(g)-finiteness, so phi ranges over continuous vectors, not only smooth vectors. This does not change the set of eigensystems that occur. For n = 0 the polynomial is 1 and the statement is empty. For n = 1 it is proved as ramanujanGL_one.

The cuspidal condition is universal over invariant probability measures. Mathematically such a measure exists and is unique, because A_K/K is a compact metrizable group, so the condition is the usual vanishing of the constant terms along the standard maximal parabolics. Mathlib does not yet prove the compactness. If no such measure existed, every function would be cuspidal and the statement would be false for n >= 2 (Langlands/Fidelity/GlobalGL.lean). So the statement is not vacuous, and its truth for n >= 2 depends on the compactness of A_K/K.

## Weaker or stronger than Sarnak (generalized Ramanujan conjecture)

- Weaker: only the finite places where pi_v is unramified. The textbook form also says that pi_v is tempered at the ramified finite places and at the infinite places. The archimedean part contains the Selberg eigenvalue conjecture, which this statement does not contain.
- Same: all unitary cuspidal pi, of any infinity type, are covered. This includes Maass forms on GL_2 over Q, where the statement is open.
- Same: the normalisation is the unitary Satake normalisation, so |alpha| = 1 is the right condition.
- I found nothing that makes the statement stronger than the conjecture or vacuous, given the remark above about the invariant measure.

## Comparison with the docstring

The translation agrees with the docstring. The docstring says that a cusp form is bounded exactly when its central character is unitary. For IsCuspForm, which asks only for continuity and moderate growth, only one direction is clear: boundedness implies a unitary central character. A continuous but not smooth cuspidal function with a unitary central character need not be bounded. The statement does not need the other direction, because each unitary cuspidal pi has bounded smooth vectors. The docstring also says that phi is a vector in a unitary cuspidal representation pi. phi is a Hecke eigenvector only at v, so it can be a sum of vectors from several pi with the same eigensystem at v. The conclusion is the same. The docstring does not say that the statement depends on the compactness of A_K/K through the cuspidal condition. I recommend this text in place of the second and third sentences: "A nonzero bounded cusp form has a unitary central character, and each unitary cuspidal automorphic representation has bounded vectors, so these phi give all the unitary cuspidal automorphic representations pi. The eigensystem of phi at v is the eigensystem of pi_v for each pi in which phi has a nonzero component." I also recommend this sentence at the end of the first paragraph: "The cuspidal condition uses the invariant probability measure on (A_K/K)^{n x n}, which exists because A_K/K is compact; Mathlib does not yet have this fact."
