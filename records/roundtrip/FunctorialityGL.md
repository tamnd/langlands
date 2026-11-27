---
statement: Langlands.FunctorialityGL
check: F5
date: 2026-11-27
---

## What the statement says

Fix n, m and a group homomorphism r from GL_n(C) to GL_m(C). Suppose r is algebraic: each matrix entry of r(g) is a polynomial in the entries of g and in det(g)^{-1}. So r is a rational representation of GL_n(C). Then for every number field K, every nonzero element N of O_K, and every function phi on GL_n(A_K) that satisfies these conditions:
- phi is a cusp form of level N (IsCuspForm: continuous, left invariant under GL_n(K), right invariant under the principal congruence subgroup of level N, with a central character, of moderate growth, with vanishing constant terms along the standard maximal parabolics);
- phi is not 0;
- phi is a Hecke eigenform at almost all places: outside a finite set of finite places, phi is spherical at v and an eigenvector of all T_{v,i},

there exist a finite family of cusp forms phi_1, ..., phi_k on GL_{n_1}, ..., GL_{n_k} over K, each nonzero and of some level, with n_1 + ... + n_k = m, and a finite set S of finite places, with this property. For each finite place v outside S, each eigensystem ev of phi at v, and each ordering alpha_1, ..., alpha_n of the Satake parameters of phi at v, there are eigensystems mu_j of the phi_j at v such that the union with multiplicity of the Satake parameters of the phi_j at v is the multiset of eigenvalues of r(diag(alpha_1, ..., alpha_n)).

The Satake parameters are the unitary normalisation, e_i(alpha) = q_v^{-i(n-i)/2} lambda(T_{v,i}), on both sides. The Satake parameters of phi at v are nonzero, because T_{v,n} is translation by a central element and its eigenvalue is omega_v(varpi_v), so an ordering alpha with values in C^x always exists. The choice of ordering does not matter, because the eigenvalues of r(diag(alpha)) do not change under a permutation of alpha. The family (phi_j) stands for the isobaric sum Pi_1 ⊞ ... ⊞ Pi_k of the cuspidal representations they generate. IsCuspForm does not ask for a unitary central character, so the Pi_j may be cuspidal representations twisted by |det|^{s_j}. This is what the Langlands classification needs.

## Quantifiers

The hypothesis IsAlgebraicRep r comes first. Then K, N and phi are universal. The data (phi_j) and the set S are existential, and they depend on phi but not on v. After that, v outside S, the eigensystem ev and the ordering alpha are universal, and the eigensystems mu_j of the phi_j at v are existential. The phi_j need not be Hecke eigenforms in the global sense, but the conclusion asks them to be eigenvectors at every v outside S, so in effect they are. For r = id the statement is proved (functorialityGL_id), with k = 1, phi_1 = phi and S empty. Without the finiteness of S the statement would be trivially true (Langlands/Fidelity/GlobalGL.lean), and the finiteness is present.

The same remark about the cuspidal condition as in RamanujanGL applies. The condition uses invariant probability measures on (A_K/K)^{n x n}. These exist because A_K/K is compact, so the condition is the usual one. Mathlib does not yet prove this, and the conclusion uses IsCuspForm for the phi_j too.

## Weaker or stronger than Langlands (Problems in the theory of automorphic forms)

- Weaker: this is weak functoriality. The match is only at the finite places outside a finite set, through Satake parameters. There is no claim at the ramified places or at the infinite places, so no compatibility with the local Langlands correspondence there. By strong multiplicity one for isobaric representations (Jacquet and Shalika), the weak transfer still determines Pi.
- Weaker: r is a representation of GL_n(C) only. A general L-homomorphism from ^L GL_n to ^L GL_m is a representation of GL_n(C) x W_K. It is a sum of products r_i ⊗ sigma_i, with r_i a rational representation of GL_n(C) and sigma_i an irreducible representation of W_K. When each sigma_i has dimension 1, the transfer is a sum of twists of transfers in this statement by Hecke characters. When some sigma_i has dimension 2 or more, this statement does not cover it. That case contains the strong Artin conjecture (take n = 1 and r_i trivial).
- The source is cuspidal phi only. That is the usual case, because the transfer of an isobaric sum is the isobaric sum of the transfers.
- The target is an isobaric sum of cuspidal representations, possibly with non-unitary twists. This is the right target on GL_m.
- Normalisation: unitary Satake parameters on both sides, which is the standard normalisation for functoriality through the dual group.
- I found nothing that makes the statement stronger than the conjecture or vacuous.

## Comparison with the docstring

The translation agrees with the docstring, except for one sentence. The docstring says that the L-homomorphisms that are not trivial on W_K "are twists of these by Hecke characters on the image". This is true only when the W_K part acts through characters. A product r ⊗ sigma with sigma an irreducible representation of W_K of dimension at least 2 is not a twist by a Hecke character, and its transfer contains the strong Artin conjecture. I recommend this text in place of that sentence: "A general L-homomorphism is a sum of products r_i ⊗ sigma_i with sigma_i an irreducible representation of W_K. When each sigma_i is a character, its transfer is a twist of the transfer for r_i by the corresponding Hecke character. When some sigma_i has dimension at least 2, the statement does not cover it; this case contains the strong Artin conjecture." The docstring also does not say that the summands of Pi may be non-unitary twists of cuspidal representations. This is correct behaviour, but a reader can expect unitary summands. I recommend adding: "The summands are cusp forms with any central character, so they can be twists of unitary cuspidal representations by |det|^s."
