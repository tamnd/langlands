# 2026-11-26-e2-llc-gl2-small-64a59b93

For p in {3, 5, 7}, does the explicit local Langlands correspondence give the same L-factor and epsilon-factor of pi x chi on the GL2 side and on the Galois side, for the principal series, the twisted Steinberg and the depth-zero supercuspidal representations pi of GL2(Q_p) of conductor exponent at most 4 and the characters chi of conductor exponent at most 2?

Result: agrees: for each of the 45552 pairs (pi, chi) the L-factor and the epsilon-factor of pi x chi on the GL2 side are equal to those on the Galois side, exactly in Q(zeta_N).

## What the run does

F is Q_p and q = p. The additive character is psi(x) = exp(2 pi i {x}_p). It is trivial on Z_p and not on p^-1 Z_p. X is q^-s. The primitive root g is the smallest primitive root mod p^2, and chi_k is the character of Z_p^x with chi_k(g) = exp(2 pi i k / (p(p - 1))). E is the unramified quadratic extension Q_p(sqrt e), with e the smallest non-residue mod p. gamma is the first generator of k_E^x in the order of a + b sqrt e by a + p b, and theta_j is the character of k_E^x with theta_j(gamma) = exp(2 pi i j / (q^2 - 1)).

The values at p of the unramified parts are formal variables: a1 and a2 for the inducing characters of a principal series, a for the character of a twisted Steinberg representation, and c = theta(p) for a supercuspidal representation. Thus each row holds for all the unramified twists of pi. The twists chi are the chi_k of conductor exponent at most 2 with chi(p) = 1. An unramified twist of chi is a shift of s, so these twists cover all the characters of conductor exponent at most 2.

The arithmetic is exact. Each number is an element of Z[zeta_N] with a rational denominator, with N = lcm(4, p^2, p^2 - 1), and the run checks each integer operation for overflow. Two numbers are equal when their difference is 0 modulo the cyclotomic polynomial Phi_N. The square root of q is the quadratic Gauss sum, times -i when p = 3 mod 4. The complex numbers in the tables are for the reader only, and the run does not use them in a comparison.

For each pair (pi, chi), the run computes L(s, pi x chi) and epsilon(s, pi x chi, psi) on the GL2 side from the representation pi tensor chi, and L(s, rec(pi) tensor chi) and epsilon(s, rec(pi) tensor chi, psi) on the Galois side from the Weil-Deligne representation. Then it compares the two L-factors as multisets of roots, and the two epsilon-factors as monomials in X and in the formal variables.

## The families and the formulas

- Principal series pi(chi1, chi2), with chi1 and chi2 of conductor exponent at most 2 each and a(chi1) + a(chi2) at most the bound. The family with formal a1 and a2 is irreducible outside the locus chi1 / chi2 = |.|^(1 or -1). GL2 side: L(s, pi tensor chi) = L(s, chi1 chi) L(s, chi2 chi) and epsilon(s, pi tensor chi, psi) = epsilon(s, chi1 chi, psi) epsilon(s, chi2 chi, psi) (Jacquet-Langlands 1970). Galois side: rec(pi) = chi1 + chi2 with N = 0, and the factors are additive. Both sides come to the same Tate factors, so these rows check the bookkeeping of the run, not an independent identity.
- Twisted Steinberg representations eta St, the irreducible subrepresentation of the normalized induction from eta |.|^(1/2) x eta |.|^(-1/2). (chi St) tensor chi' = (chi chi') St. GL2 side: L(s, eta St) = L(s, mu1) and epsilon(s, eta St, psi) = epsilon(s, mu1, psi) epsilon(s, mu2, psi) L(1 - s, mu1^-1) / L(s, mu2), with mu1 = eta |.|^(1/2) and mu2 = eta |.|^(-1/2) (Jacquet-Langlands 1970). The run cancels the ratio of L-factors and checks that the result is a monomial. Galois side: sp(2) tensor eta, the sum of eta |.|^(-1/2) e1 and eta |.|^(1/2) e2 with N e1 = e2. The run checks Phi N Phi^-1 = q^-1 N for the geometric Frobenius Phi. Then L(s, rho) = det(1 - Phi X | (V^I)^(N = 0))^-1 and epsilon(s, rho, psi) = epsilon(s, rho_ss, psi) det(-Phi X | V^I / (V^I)^(N = 0)) (Deligne 1973; Tate 1979). For eta unramified the two sides are different computations, and both give L = 1/(1 - q^(-1/2) a X) and epsilon = -q^(1/2) a X. For eta ramified both sides come to the same Tate factors.
- Depth-zero supercuspidal representations pi_theta = c-Ind from ZK of Lambda, K = GL2(Z_p), with Lambda on K the inflation of the cuspidal representation sigma_theta of GL2(F_p) of a regular character theta of k_E^x, and Lambda(p) = c. There is one pi_theta for each pair {theta, theta^q}. The character of sigma_theta is (q - 1) theta(a) on a scalar a, -theta(a) on a times a nontrivial unipotent, 0 on a split semisimple class and -(theta(x) + theta(x^q)) on an elliptic class with eigenvalue x (Fulton-Harris, Representation theory, section 5.2).
- GL2 side of the supercuspidal pairs. pi_theta tensor chi is c-Ind of Lambda' = Lambda tensor chi o det, which factors through GL2(Z/p^n) on K with n = max(1, a(chi)). The run uses the functional equation of Godement-Jacquet (Godement-Jacquet 1972) with the matrix coefficient f = tr Lambda' on ZK and the test function Phi = the conjugate of tr Lambda' on K. Then Z(Phi, s, f) = 1 and epsilon(s, pi tensor chi, psi) = Z(Phi^, 1 - s, f^v) = sum over m from -n to 0 of c^-m q^(-4n-3m) X^(-2m) T_m / (q - 1), with T_m the sum over h in GL2(Z/p^n) of the character of the contragredient of Lambda' at h times psi(p^m tr h). The run computes each T_m by a sum over all of GL2(Z/p^n), with the counts of the elements by class mod p, det and trace, and it checks that only m = -n gives a term that is not 0. For a tame chi this is the formula epsilon(s, pi_theta', psi) = -theta'(p) X^2 times the Gauss sum of theta'^-1 over k_E^x with the character psi(Tr x / p), with theta' = theta (chi o N). The tests check this reduction to the Gauss sum of k_E (Kondo 1963). L(s, pi tensor chi) = 1 for a supercuspidal representation.
- Galois side of the supercuspidal pairs. rec(pi_theta) = Ind from W_E to W_F of theta Delta, with Delta the unramified quadratic character of E^x, the rectifier of a level-zero admissible pair (Bushnell-Henniart, The local Langlands conjecture for GL(2), chapter 8, section 34). rec(pi_theta) tensor chi = Ind of xi = theta Delta (chi o N). Then L(s, Ind xi) = L(s, xi) = 1, and epsilon(s, Ind xi, psi) = lambda(E/F, psi) epsilon(s, xi, psi o Tr) by inductivity in degree 0 (Deligne 1973; Tate 1979). The run computes lambda(E/F, psi) = epsilon(1_F) epsilon(eta_E/F) / epsilon(1_E) from Tate's factors, and epsilon(s, xi, psi o Tr) from Tate's Gauss sum over (O_E / p^n)^x. The run also compares the central character theta|F^x chi^2 with det Ind xi = eta_E/F xi|F^x.
- Control. For each supercuspidal pair the run also tests the naive correspondence pi_theta to Ind theta, with no rectifier. A check that cannot fail is not a test, so the control must fail.

The run computes p = 3: lambda(E/F, psi) = 1.

The run computes p = 5: lambda(E/F, psi) = 1.

The run computes p = 7: lambda(E/F, psi) = 1.

## Counts

| p | family | N | representations | twists | pairs | matches |
|---|---|---|---|---|---|---|
| 3 | principal-series | 72 | 21 | 6 | 126 | 126 |
| 3 | steinberg | 72 | 6 | 6 | 36 | 36 |
| 3 | depth-zero-supercuspidal | 72 | 3 | 6 | 18 | 18 |
| 5 | principal-series | 600 | 210 | 20 | 4200 | 4200 |
| 5 | steinberg | 600 | 20 | 20 | 400 | 400 |
| 5 | depth-zero-supercuspidal | 600 | 10 | 20 | 200 | 200 |
| 7 | principal-series | 2352 | 903 | 42 | 37926 | 37926 |
| 7 | steinberg | 2352 | 42 | 42 | 1764 | 1764 |
| 7 | depth-zero-supercuspidal | 2352 | 21 | 42 | 882 | 882 |

## Principal series by conductor

| p | a(pi) | a(pi x chi) | pairs | matches | example | epsilon |
|---|---|---|---|---|---|---|
| 3 | 0 | 0 | 1 | 1 | pi(chi_0 a1, chi_0 a2) x chi_0 | 1 |
| 3 | 0 | 2 | 1 | 1 | pi(chi_0 a1, chi_0 a2) x chi_3 | -3 a1 a2 X^2 |
| 3 | 0 | 4 | 4 | 4 | pi(chi_0 a1, chi_0 a2) x chi_1 | (1.562834+8.863270i) a1^2 a2^2 X^4 |
| 3 | 1 | 1 | 2 | 2 | pi(chi_0 a1, chi_3 a2) x chi_0 | (0.000000+1.732051i) a2 X |
| 3 | 1 | 4 | 4 | 4 | pi(chi_0 a1, chi_3 a2) x chi_1 | (1.562834+8.863270i) a1^2 a2^2 X^4 |
| 3 | 2 | 0 | 1 | 1 | pi(chi_3 a1, chi_3 a2) x chi_3 | 1 |
| 3 | 2 | 2 | 9 | 9 | pi(chi_0 a1, chi_1 a2) x chi_0 | (2.298133+1.928363i) a2^2 X^2 |
| 3 | 2 | 3 | 8 | 8 | pi(chi_0 a1, chi_1 a2) x chi_2 | (3.340022+3.980484i) a1^2 a2 X^3 |
| 3 | 2 | 4 | 12 | 12 | pi(chi_0 a1, chi_1 a2) x chi_1 | 9 a1^2 a2^2 X^4 |
| 3 | 3 | 2 | 8 | 8 | pi(chi_1 a1, chi_3 a2) x chi_3 | (2.298133+1.928363i) a1^2 X^2 |
| 3 | 3 | 3 | 8 | 8 | pi(chi_1 a1, chi_3 a2) x chi_0 | (-3.340022+3.980484i) a1^2 a2 X^3 |
| 3 | 3 | 4 | 8 | 8 | pi(chi_1 a1, chi_3 a2) x chi_1 | 9 a1^2 a2^2 X^4 |
| 3 | 4 | 0 | 4 | 4 | pi(chi_1 a1, chi_1 a2) x chi_5 | 1 |
| 3 | 4 | 1 | 4 | 4 | pi(chi_1 a1, chi_4 a2) x chi_2 | (0.000000+1.732051i) a1 X |
| 3 | 4 | 2 | 12 | 12 | pi(chi_1 a1, chi_1 a2) x chi_2 | -3 a1 a2 X^2 |
| 3 | 4 | 3 | 8 | 8 | pi(chi_1 a1, chi_2 a2) x chi_1 | (3.340022+3.980484i) a1^2 a2 X^3 |
| 3 | 4 | 4 | 32 | 32 | pi(chi_1 a1, chi_1 a2) x chi_0 | (1.562834+8.863270i) a1^2 a2^2 X^4 |
| 5 | 0 | 0 | 1 | 1 | pi(chi_0 a1, chi_0 a2) x chi_0 | 1 |
| 5 | 0 | 2 | 3 | 3 | pi(chi_0 a1, chi_0 a2) x chi_5 | (-2.236068+4.472136i) a1 a2 X^2 |
| 5 | 0 | 4 | 16 | 16 | pi(chi_0 a1, chi_0 a2) x chi_1 | (23.244412+9.203114i) a1^2 a2^2 X^4 |
| 5 | 1 | 1 | 6 | 6 | pi(chi_0 a1, chi_5 a2) x chi_0 | (1.175571+1.902113i) a2 X |
| 5 | 1 | 2 | 6 | 6 | pi(chi_0 a1, chi_5 a2) x chi_5 | (2.628656+4.253254i) a1 a2 X^2 |
| 5 | 1 | 4 | 48 | 48 | pi(chi_0 a1, chi_5 a2) x chi_1 | (9.203114-23.244412i) a1^2 a2^2 X^4 |
| 5 | 2 | 0 | 3 | 3 | pi(chi_5 a1, chi_5 a2) x chi_15 | 1 |
| 5 | 2 | 1 | 6 | 6 | pi(chi_5 a1, chi_10 a2) x chi_10 | (-1.175571+1.902113i) a1 X |
| 5 | 2 | 2 | 47 | 47 | pi(chi_0 a1, chi_1 a2) x chi_0 | (4.911436+0.936907i) a2^2 X^2 |
| 5 | 2 | 3 | 96 | 96 | pi(chi_0 a1, chi_1 a2) x chi_4 | (8.240707-7.555842i) a1^2 a2 X^3 |
| 5 | 2 | 4 | 288 | 288 | pi(chi_0 a1, chi_1 a2) x chi_1 | (24.950668-1.569763i) a1^2 a2^2 X^4 |
| 5 | 3 | 2 | 96 | 96 | pi(chi_1 a1, chi_5 a2) x chi_15 | (-0.936907+4.911436i) a1^2 X^2 |
| 5 | 3 | 3 | 288 | 288 | pi(chi_1 a1, chi_5 a2) x chi_0 | (3.991637+10.443507i) a1^2 a2 X^3 |
| 5 | 3 | 4 | 576 | 576 | pi(chi_1 a1, chi_5 a2) x chi_1 | (-1.569763-24.950668i) a1^2 a2^2 X^4 |
| 5 | 4 | 0 | 16 | 16 | pi(chi_1 a1, chi_1 a2) x chi_19 | 1 |
| 5 | 4 | 1 | 48 | 48 | pi(chi_1 a1, chi_6 a2) x chi_14 | (-1.175571+1.902113i) a1 X |
| 5 | 4 | 2 | 288 | 288 | pi(chi_1 a1, chi_1 a2) x chi_4 | (-2.236068+4.472136i) a1 a2 X^2 |
| 5 | 4 | 3 | 576 | 576 | pi(chi_1 a1, chi_2 a2) x chi_3 | (8.240707-7.555842i) a1^2 a2 X^3 |
| 5 | 4 | 4 | 1792 | 1792 | pi(chi_1 a1, chi_1 a2) x chi_0 | (23.244412+9.203114i) a1^2 a2^2 X^4 |
| 7 | 0 | 0 | 1 | 1 | pi(chi_0 a1, chi_0 a2) x chi_0 | 1 |
| 7 | 0 | 2 | 5 | 5 | pi(chi_0 a1, chi_0 a2) x chi_7 | (4.908502+4.990652i) a1 a2 X^2 |
| 7 | 0 | 4 | 36 | 36 | pi(chi_0 a1, chi_0 a2) x chi_1 | (47.397448-12.429075i) a1^2 a2^2 X^4 |
| 7 | 1 | 1 | 10 | 10 | pi(chi_0 a1, chi_7 a2) x chi_0 | (2.440133+1.022619i) a2 X |
| 7 | 1 | 2 | 20 | 20 | pi(chi_0 a1, chi_7 a2) x chi_7 | (4.582576+5.291503i) a1 a2 X^2 |
| 7 | 1 | 4 | 180 | 180 | pi(chi_0 a1, chi_7 a2) x chi_1 | (-47.397448+12.429075i) a1^2 a2^2 X^4 |
| 7 | 2 | 0 | 5 | 5 | pi(chi_7 a1, chi_7 a2) x chi_35 | 1 |
| 7 | 2 | 1 | 20 | 20 | pi(chi_7 a1, chi_14 a2) x chi_28 | (-2.440133+1.022619i) a1 X |
| 7 | 2 | 2 | 137 | 137 | pi(chi_0 a1, chi_1 a2) x chi_0 | (-6.942530+0.895140i) a2^2 X^2 |
| 7 | 2 | 3 | 360 | 360 | pi(chi_0 a1, chi_1 a2) x chi_6 | (16.025312+9.283823i) a1^2 a2 X^3 |
| 7 | 2 | 4 | 1620 | 1620 | pi(chi_0 a1, chi_1 a2) x chi_1 | (14.942506+46.666064i) a1^2 a2^2 X^4 |
| 7 | 3 | 2 | 360 | 360 | pi(chi_1 a1, chi_7 a2) x chi_35 | (6.942530-0.895140i) a1^2 X^2 |
| 7 | 3 | 3 | 1800 | 1800 | pi(chi_1 a1, chi_7 a2) x chi_0 | (-17.856086-4.915300i) a1^2 a2 X^3 |
| 7 | 3 | 4 | 5400 | 5400 | pi(chi_1 a1, chi_7 a2) x chi_1 | (-14.942506-46.666064i) a1^2 a2^2 X^4 |
| 7 | 4 | 0 | 36 | 36 | pi(chi_1 a1, chi_1 a2) x chi_41 | 1 |
| 7 | 4 | 1 | 180 | 180 | pi(chi_1 a1, chi_8 a2) x chi_34 | (-2.440133+1.022619i) a1 X |
| 7 | 4 | 2 | 1620 | 1620 | pi(chi_1 a1, chi_1 a2) x chi_6 | (4.908502+4.990652i) a1 a2 X^2 |
| 7 | 4 | 3 | 5400 | 5400 | pi(chi_1 a1, chi_2 a2) x chi_5 | (16.025312+9.283823i) a1^2 a2 X^3 |
| 7 | 4 | 4 | 20736 | 20736 | pi(chi_1 a1, chi_1 a2) x chi_0 | (47.397448-12.429075i) a1^2 a2^2 X^4 |

## Twisted Steinberg representations

| p | eta | pairs | matches | L on both sides | epsilon on both sides |
|---|---|---|---|---|---|
| 3 | unramified | 6 | 6 | 1/(1 - q^(-1/2) a X) | -q^(1/2) a X |
| 3 | ramified | 30 | 30 | 1 | eps(eta norm^(1/2)) eps(eta norm^(-1/2)), with norm = the absolute value; for example (1.562834+8.863270i) a^4 X^4 |
| 5 | unramified | 20 | 20 | 1/(1 - q^(-1/2) a X) | -q^(1/2) a X |
| 5 | ramified | 380 | 380 | 1 | eps(eta norm^(1/2)) eps(eta norm^(-1/2)), with norm = the absolute value; for example (23.244412+9.203114i) a^4 X^4 |
| 7 | unramified | 42 | 42 | 1/(1 - q^(-1/2) a X) | -q^(1/2) a X |
| 7 | ramified | 1722 | 1722 | 1 | eps(eta norm^(1/2)) eps(eta norm^(-1/2)), with norm = the absolute value; for example (47.397448-12.429075i) a^4 X^4 |

## Depth-zero supercuspidal representations

| p | a(chi) | pairs | matches | naive epsilon matches | naive central character matches |
|---|---|---|---|---|---|
| 3 | at most 1 | 6 | 6 | 0 | 0 |
| 3 | 2 | 12 | 12 | 12 | 0 |
| 5 | at most 1 | 40 | 40 | 0 | 0 |
| 5 | 2 | 160 | 160 | 160 | 0 |
| 7 | at most 1 | 126 | 126 | 0 | 0 |
| 7 | 2 | 756 | 756 | 756 | 0 |

With no rectifier, the epsilon-factor of a pair with a tame twist has the wrong sign, because Delta(p) = -1 enters to the first power. For a twist of conductor exponent 2, Delta(p) enters to the power 2, so the naive epsilon-factor agrees, and only the central character shows the error: det Ind theta is eta_E/F theta|F^x, not theta|F^x.

Examples:

- p = 3, pi(theta_1), theta(p) = c, twist chi_0: GL2 side epsilon = (2.449490+1.732051i) c X^2; Galois side epsilon = (2.449490+1.732051i) c X^2.
- p = 3, pi(theta_1), theta(p) = c, twist chi_1: GL2 side epsilon = (1.562834+8.863270i) c^2 X^4; Galois side epsilon = (1.562834+8.863270i) c^2 X^4.

## Sources

- Tate's thesis, and J. Tate, Number theoretic background, Corvallis 1979: the factors of a character, and of a Weil-Deligne representation.
- P. Deligne, Les constantes des equations fonctionnelles des fonctions L, 1973: the local constants, and their inductivity in degree 0.
- H. Jacquet and R. P. Langlands, Automorphic forms on GL(2), 1970: the factors of the principal series and of the special representations.
- R. Godement and H. Jacquet, Zeta functions of simple algebras, 1972: the zeta integrals and their functional equation. The run applies it to the test function above; the derivation is in the comments of lab/e2.go.
- W. Fulton and J. Harris, Representation theory, section 5.2: the characters of GL2(F_q).
- T. Kondo, On Gaussian sums attached to the general linear groups over finite fields, 1963: the sum over GL2(F_q) is -q(q - 1) times a Gauss sum over k_E. The tests of lab/e2_test.go check this identity for p = 3, 5 and 7.
- C. J. Bushnell and G. Henniart, The local Langlands conjecture for GL(2), 2006, chapter 8, section 34: the tame correspondence and the rectifier Delta of a level-zero admissible pair, the unramified quadratic character of E^x.

## What the run does not do

- It is a computation, not a proof. An agreement is evidence, and only a certificate that Lean checks makes a theorem (spec 13.4).
- The principal series have inducing characters of conductor exponent at most 2 each. The principal series with an inducing character of conductor exponent 3 or 4 are not in the run.
- The supercuspidal representations of positive depth are not in the run, except as the twists of a depth-zero one by a character of conductor exponent 2. The ramified admissible pairs (conductor exponent 3) and the minimal unramified pairs of level 1 (conductor exponent 4) need the full tame types and a rectifier of positive level, and the run does not have them.
- The case p = 2 of spec 13.3 is not in the run.
- For the principal series and for the Steinberg representations with a ramified eta, both sides come to the same Tate factors. Those rows check the bookkeeping, not an independent identity.
- It does not check the factors of pairs GL2 x GL2 or the converse theorem, so it does not by itself fix rec on the supercuspidal representations.
- It runs in the lgl binary, not in a container with pinned images, and it uses no network and no other tool. It uses no random numbers. The record gives the commit of lgl, so the outputs are reproducible.
