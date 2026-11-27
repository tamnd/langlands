---
statement: Langlands.LocalLanglandsGLFull
check: F5
date: 2026-11-27
---

## What the statement says

Fix n. For every nonarchimedean local field K and every topological isomorphism art from K^x to W_K^ab that is a local Artin map (uniformizers go to geometric Frobenius, norm groups are the kernels), K gets its Borel sigma-algebra and two things exist together:

1. A function eps(mu, m, rho, psi, s) taking a measure on K, a Weil-Deligne representation of any dimension m, and an additive character psi to a complex number. It must satisfy:
   - (iso) it depends only on the isomorphism class of rho;
   - (monomial) for every mu, rho, psi it equals c q^{-ks} with c nonzero and k an integer;
   - (dimOne) for m = 1, every additive Haar mu, and every psi with some conductor (any nontrivial psi), it is the Tate epsilon of the character det(rho) composed with art: it satisfies Tate's local functional equation for every Schwartz function in the strip where both sides converge;
   - (monodromy) eps(rho) det(-q^{-s} Frob | (ker N)^I) = eps(rho with N set to 0) det(-q^{-s} Frob | V^I). This is Deligne's rule eps(rho) = eps(rho_0) det(-Frob q^{-s} | V^I/(ker N)^I).
2. For each m <= n, a bijection rec_m from iso classes of irreducible admissible smooth representations of GL_m(K) to iso classes of Frobenius-semisimple WD representations of dimension m. These satisfy:
   - rec_1 is class field theory via art;
   - each rec_m matches the central character with det, matches twists by chi∘det with twists by the corresponding character, matches contragredients with duals, and the Godement-Jacquet L-factor of pi with L(s, rec pi) (Frobenius acting on the inertia invariants of ker N);
   - (pairs, L) for 1 <= m' <= m <= n, pi psi-generic, pi' psi^{-1}-generic, psi nontrivial, every additive Haar mu: L(s, rho ⊗ rho') is the Rankin-Selberg L-factor, meaning the normalized generator of the ideal spanned by the JPSS zeta integrals;
   - (pairs, eps) under the same hypotheses, for mu self-dual with respect to psi: eps(mu, mm', rho ⊗ rho', psi) is a monomial satisfying the JPSS functional equation, with the sign omega_{pi'}(-1)^{m-1}.

The tensor product is the usual one (r ⊗ r', N ⊗ 1 + 1 ⊗ N'). The Frobenius is geometric, which agrees with art. The RS integrals use |det|^{s-(m-m')/2}, and the GJ integrals use the standard shift.

## Quantifiers

eps is existential. It is chosen for each K and art, together with rec. It is not tied to the Langlands-Deligne epsilon. The only conditions on it are the four listed. There is no additivity in exact sequences, no inductivity in degree 0, no rule for psi_a or for scaling mu, and no uniqueness. So on irreducible Weil representations of dimension at least 2, eps is constrained only through the pairs condition. In effect the statement says that the RS epsilon of pi × pi' depends only on rec(pi) ⊗ rec(pi'), and that the resulting function is consistent with Tate in dimension 1 and with the monodromy rule. That is a real constraint, but it is weaker than "eps(pi × pi') = eps_Deligne(rho ⊗ rho')". For rho outside the image of tensor products (or for non-self-dual mu, or trivial psi), eps is free apart from being monomial, which is easy to arrange.

## Weaker or stronger than Harris-Taylor / Henniart

- Weaker: only existence (exists rec, not exists!), even though Henniart's theorem includes uniqueness.
- Weaker: the epsilon comparison is with some eps function, not the Langlands-Deligne one (see above).
- Weaker: the pairs conditions apply only to generic pi, pi'. Non-generic representations get only the single GJ L-factor, not epsilon. They still cover the supercuspidals, which is what Henniart's characterization needs.
- eps for a single pi comes in only through m' = 1 (pi' a character). There is no separate GJ epsilon condition.
- Normalization: geometric Frobenius and the self-dual measure (vol(O)^2 q^k = 1 for conductor k) are both standard.
- I found nothing that makes the statement vacuous. The pairs conditions apply to every irreducible m-dimensional class because each rec_m is a bijection. I did not fully check the JPSS integration formulas (Weyl elements, the j range) against the literature, beyond the quotient measure on N\GL_m and the exponents.

## Comparison with the docstring

The translation agrees with the docstring of the statement. The docstring did not say that the ε-factor is chosen with the family and is not fixed in dimension 2 or more, or that the statement does not give uniqueness. PR tamnd/langlands-lean#181 adds these two facts to the docstring.
