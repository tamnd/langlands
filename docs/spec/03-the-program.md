# 03. The Langlands program, mathematically

This document states the main conjectures of the Langlands program in the form that the project uses, and it says what is proved and what is open on 2026-11-25. Documents 04 (routes) and 06 (Lean statements) build on it. The sources are in document 01 and in the research reports A to F (research/sources/). Here a result is named by its authors and year, or by its arXiv number when it is from 2025 or 2026. The tags are those of document 01: [P] primary source read, [S] secondary, [U] unverified. Standard textbook facts carry no tag.

The program is not one statement. It is a network of conjectures that are related by implications, some proved, some expected. The project must state many of them, and the choices in each statement (normalizations, the class of representations, the coefficient field) are part of the work. Section 3.13 lists the consequences for the project.

## 3.1 Global fields, adeles and automorphic representations

Throughout, $F$ is a **global field**: a finite extension of $\mathbb{Q}$, or the function field of a smooth projective geometrically connected curve $X$ over $\mathbb{F}_q$. For a place $v$, $F_v$ is the completion, and for $v$ finite, $\mathcal{O}_v$ is its ring of integers and $q_v$ the size of its residue field. The **adele ring** is the restricted product
$$\mathbb{A}_F = {\prod_v}' (F_v : \mathcal{O}_v),$$
a locally compact ring in which $F$ is discrete and cocompact. The **idele class group** is $C_F = \mathbb{A}_F^\times / F^\times$.

Let $G$ be a connected reductive group over $F$, $Z$ its centre, and $\omega$ a unitary character of $Z(\mathbb{A}_F)$ trivial on $Z(F)$. Then $G(F)$ is a discrete subgroup of $G(\mathbb{A}_F)$, and $G(F) \backslash G(\mathbb{A}_F)^1$ has finite volume (Borel, Harish-Chandra).

**Definition 3.1 (Automorphic form, after Borel-Jacquet 1979).** An *automorphic form* on $G$ is a function $\varphi : G(F) \backslash G(\mathbb{A}_F) \to \mathbb{C}$ that is smooth, right $K$-finite for a maximal compact subgroup $K = \prod_v K_v$, $\mathcal{Z}(\mathfrak{g}_\infty)$-finite, and of moderate growth. It is *cuspidal* if for every proper parabolic $P = MN$ over $F$,
$$\int_{N(F) \backslash N(\mathbb{A}_F)} \varphi(n g)\, dn = 0 \quad \text{for all } g.$$

An **automorphic representation** is an irreducible subquotient of the space of automorphic forms, as a $(\mathfrak{g}_\infty, K_\infty) \times G(\mathbb{A}_F^\infty)$-module. Over a function field there is no archimedean part, and an automorphic form is a locally constant function. By Flath's theorem an irreducible admissible representation factors as a restricted tensor product $\pi = \bigotimes'_v \pi_v$, with $\pi_v$ unramified (that is, $\pi_v^{K_v} \neq 0$ for a hyperspecial $K_v$) for almost all $v$.

**Satake parameters.** For $v$ outside a finite set $S$, $G$ is unramified at $v$, and the Satake isomorphism identifies the spherical Hecke algebra $\mathcal{H}(G(F_v), K_v)$ with $\mathbb{C}[\check{T}]^{W}$ (twisted by Frobenius when $G_v$ is not split). So an unramified $\pi_v$ gives a semisimple conjugacy class $c_v(\pi) \in \check{G} \rtimes \mathrm{Frob}_v$. These classes are the *Hecke* or *Satake parameters*. For a finite dimensional representation $r$ of ${}^L G$ (3.2) the partial L-function is
$$L^S(s, \pi, r) = \prod_{v \notin S} \det\bigl(1 - r(c_v(\pi))\, q_v^{-s}\bigr)^{-1},$$
which converges for $\operatorname{Re} s \gg 0$.

For $G = \mathrm{GL}_2$ over $\mathbb{Q}$, a holomorphic newform $f$ of weight $k$ and level $N$ gives a cuspidal $\pi_f$, and $c_p(\pi_f)$ has eigenvalues $\alpha_p, \beta_p$ with $\alpha_p + \beta_p = a_p(f) p^{-(k-1)/2}$ and $\alpha_p \beta_p = 1$ for $p \nmid N$. This is the dictionary that the handbook (Volumes 4 and 5, document 11) teaches first.

## 3.2 The L-group and Langlands parameters

**Root data duality.** A split reductive group $G$ over a field is determined by its root datum $\Psi = (X^*, \Phi, X_*, \Phi^\vee)$. The **dual group** $\check{G}$ is the complex reductive group with the dual datum $\Psi^\vee = (X_*, \Phi^\vee, X^*, \Phi)$. Examples: $\check{\mathrm{GL}}_n = \mathrm{GL}_n$, $\check{\mathrm{SL}}_n = \mathrm{PGL}_n$, $\check{\mathrm{Sp}}_{2n} = \mathrm{SO}_{2n+1}$, $\check{G}_2 = G_2$. Mathlib has `RootPairing` and `RootDatum` (document 05), but not the reductive group scheme attached to a datum.

**The Weil group.** Let $F$ be a non-archimedean local field with residue field $\mathbb{F}_q$, and $I_F \subset \mathrm{Gal}(\bar{F}/F)$ the inertia group. The **Weil group** $W_F$ is the preimage of $\mathrm{Frob}^{\mathbb{Z}}$ under $\mathrm{Gal}(\bar{F}/F) \to \mathrm{Gal}(\bar{\mathbb{F}}_q/\mathbb{F}_q) \cong \hat{\mathbb{Z}}$, with the topology in which $I_F$ is open with its profinite topology:
$$1 \to I_F \to W_F \to \mathbb{Z} \to 1.$$
It has the norm $|\cdot| : W_F \to q^{\mathbb{Z}}$. For $F = \mathbb{R}$, $W_\mathbb{R} = \mathbb{C}^\times \sqcup j \mathbb{C}^\times$ with $j^2 = -1$. For a number field there is a global Weil group $W_F$, an extension of $\mathrm{Gal}(\bar{F}/F)$ by the connected component of $C_F$ (Artin-Tate, Weil). A **Weil-Deligne representation** is a pair $(r, N)$ of a representation $r : W_F \to \mathrm{GL}(V)$ with open kernel on $I_F$ and a nilpotent $N \in \mathrm{End}(V)$ with $r(w) N r(w)^{-1} = |w| N$. The Weil-Deligne group is $WD_F = W_F \times \mathrm{SL}_2(\mathbb{C})$ in the form that most of the literature uses.

**The L-group.** The Galois group acts on $\Psi^\vee$ through a finite quotient, and so on $\check{G}$ by pinned automorphisms. The **L-group** is ${}^L G = \check{G} \rtimes W_F$. For a local field, a **Langlands parameter** is a continuous homomorphism
$$\varphi : W_F \times \mathrm{SL}_2(\mathbb{C}) \to {}^L G$$
over $W_F$, with $\varphi(W_F)$ consisting of semisimple elements and $\varphi|_{\mathrm{SL}_2}$ algebraic, taken up to $\check{G}$-conjugacy. It is *relevant* for $G$ if every Levi of ${}^L G$ that contains its image is the L-group of a Levi of $G$. $\Phi(G)$ is the set of relevant parameters. The **centralizer group** is $S_\varphi = \pi_0\bigl(Z_{\check{G}}(\varphi)/Z(\check{G})^{\Gamma}\bigr)$, or a central extension of it in the rigid or isocrystal forms (Kaletha).

The choice between arithmetic and geometric Frobenius, and between unitary and Tate normalization, changes every statement by a twist. Document 06 fixes them, and the fidelity battery checks them (risk 1 of 06.5).

## 3.3 Local Langlands

**Conjecture 3.2 (LLC for $\mathrm{GL}_n$).** Let $F$ be a non-archimedean local field. There is a unique family of bijections
$$\mathrm{rec}_F : \mathrm{Irr}(\mathrm{GL}_n(F)) \xrightarrow{\ \sim\ } \{ n\text{-dimensional Frobenius-semisimple WD representations of } W_F \}/\!\cong, \quad n \ge 1,$$
such that:
1. for $n = 1$, $\mathrm{rec}_F$ is the local reciprocity map of class field theory, $F^\times \cong W_F^{\mathrm{ab}}$;
2. $\mathrm{rec}_F(\pi \otimes \chi \circ \det) = \mathrm{rec}_F(\pi) \otimes \mathrm{rec}_F(\chi)$;
3. the central character $\omega_\pi$ corresponds to $\det \mathrm{rec}_F(\pi)$;
4. $\mathrm{rec}_F(\pi^\vee) = \mathrm{rec}_F(\pi)^\vee$;
5. $L(s, \pi \times \pi') = L(s, \mathrm{rec}_F(\pi) \otimes \mathrm{rec}_F(\pi'))$ and $\varepsilon(s, \pi \times \pi', \psi) = \varepsilon(s, \mathrm{rec}_F(\pi) \otimes \mathrm{rec}_F(\pi'), \psi)$.

Henniart proved that 1 to 5 determine $\mathrm{rec}_F$. Supercuspidals correspond to irreducible representations with $N = 0$.

**Status.** Proved: Laumon-Rapoport-Stuhler 1993 for $\mathrm{char}\, F = p$; Harris-Taylor 2001 and Henniart 2000 for $p$-adic $F$; a second proof by Scholze (Invent. Math. 2013, arXiv:1010.1540) [P]. For $n = 2$ the theorem has a purely local proof (Kutzko 1980; Bushnell-Henniart, Grundlehren 335, 2006) [S]. Every known proof for general $n$ uses global input: Shimura varieties or the trace formula. Explicit forms exist for essentially tame representations (Bushnell-Henniart 2005 to 2010) and for middle supercuspidals of $\mathrm{GL}_{2n}$ (Luo-Stevens, arXiv:2608.20225) [P].

**General $G$.** For a connected reductive $G$ over a local field $F$, the conjecture (Taïbi's survey, arXiv:2510.00632 [P]) asks for a finite-to-one surjection
$$\mathrm{LL} : \mathrm{Irr}(G(F)) \to \Phi(G), \qquad \Pi_\varphi := \mathrm{LL}^{-1}(\varphi),$$
with Borel's desiderata: compatibility with central characters, twists, and parabolic induction; $\Pi_\varphi$ consists of essentially discrete series exactly when $\varphi$ is discrete (image in no proper Levi); tempered $\pi$ correspond to bounded $\varphi$. The **refined** form gives, for a quasi-split $G^*$ with a Whittaker datum, a bijection
$$\coprod_{(G', \xi, z)} \mathrm{Irr}(G'(F)) \xrightarrow{\ \sim\ } \{ (\varphi, \rho) : \varphi \in \Phi(G^*),\ \rho \in \mathrm{Irr}(S_\varphi^{\natural}) \},$$
over the rigid inner forms of $G^*$, with the generic member of each tempered packet matched to the trivial $\rho$. These are the **enhanced parameters**. The packets must satisfy **character identities**: for tempered $\varphi$, the distribution $S\Theta_\varphi = \sum_{\pi \in \Pi_\varphi} \dim \rho_\pi \, \Theta_\pi$ is stable, and for each semisimple $s \in S_\varphi$ with endoscopic datum $(H, s, \eta)$ the transfer of $S\Theta_{\varphi_H}$ is $\sum_\pi \mathrm{tr}\, \rho_\pi(s)\, \Theta_\pi$, up to the transfer factor. The **formal degree conjecture** (Hiraga-Ichino-Ikeda) gives $\deg \pi$ from the adjoint $\gamma$-factor of $\varphi$. Henniart's uniqueness has no known analogue for general $G$ without global input (Harris 2022) [P].

**Fargues-Scholze.** For every $G$ and every non-archimedean $F$, Fargues-Scholze (arXiv:2102.13459, Astérisque 466) construct a map
$$\mathrm{Irr}_{\overline{\mathbb{Q}}_\ell}(G(F)) \to \Phi^{\mathrm{ss}}(G), \qquad \pi \mapsto \varphi_\pi^{\mathrm{FS}},$$
to semisimple parameters, through the geometric Satake equivalence on $\mathrm{Bun}_G$ of the Fargues-Fontaine curve [P]. It is compatible with $\mathrm{rec}_F$ for $\mathrm{GL}_n$, with parabolic induction and with central characters. Scholze (arXiv:2501.07944) shows it does not depend on $\ell$ [P]. It agrees with the classical correspondence for $\mathrm{GSp}_4$, odd unitary groups, unramified $\mathrm{SO}$ and $\mathrm{U}$ (Peng, arXiv:2503.04623) and with Genestier-Lafforgue in equal characteristic [P]. Cotner-Feng (arXiv:2609.16381, 2609.16387, September 2026) show that on Yu's supercuspidals the FS parameter restricted to inertia equals Kaletha's, with finite fibres [P]. Fargues-Scholze also state a **categorical** conjecture: $D(\mathrm{Bun}_G) \simeq \mathrm{IndCoh}_{\mathrm{Nilp}}(\mathrm{Par}_{\check{G}})$, open (3.9, 3.10).

## 3.4 Global reciprocity

For $\mathrm{GL}_1$ the statement is class field theory. Artin reciprocity gives a continuous surjection with kernel the connected component $C_F^0$:
$$\mathrm{Art}_F : C_F \twoheadrightarrow \mathrm{Gal}(F^{\mathrm{ab}}/F), \qquad C_F / C_F^0 \cong \mathrm{Gal}(F^{\mathrm{ab}}/F),$$
compatible at each place with the local maps $F_v^\times \to \mathrm{Gal}(F_v^{\mathrm{ab}}/F_v)$. So characters of $C_F$ of finite order are the same as one-dimensional Galois representations, and Hecke L-functions are Artin L-functions.

For $\mathrm{GL}_n$ the conjecture joins Clozel's algebraicity (1990) with Fontaine-Mazur (1995). Fix a prime $\ell$ and an isomorphism $\iota : \overline{\mathbb{Q}}_\ell \cong \mathbb{C}$.

**Conjecture 3.3 (Reciprocity for $\mathrm{GL}_n$, after Clozel and Fontaine-Mazur).** Let $F$ be a number field. There is a bijection between
- cuspidal automorphic representations $\pi$ of $\mathrm{GL}_n(\mathbb{A}_F)$ that are **algebraic** (the infinitesimal character at each archimedean place is integral after the shift by $\frac{n-1}{2}$), and
- irreducible continuous $\rho : \mathrm{Gal}(\bar{F}/F) \to \mathrm{GL}_n(\overline{\mathbb{Q}}_\ell)$ that are unramified at almost all places and de Rham at the places above $\ell$ (**geometric**),

such that $\iota\, \mathrm{WD}(\rho|_{G_{F_v}})^{\mathrm{F\text{-}ss}} \cong \mathrm{rec}_{F_v}(\pi_v \otimes |\det|^{(1-n)/2})$ at every finite $v$ (with the Fontaine functor $\mathrm{WD}$ for $v \mid \ell$), and the Hodge-Tate weights of $\rho$ match the infinitesimal character of $\pi_\infty$.

The Fontaine-Mazur conjecture adds that every geometric $\rho$ is a subquotient of the étale cohomology of a variety, up to Tate twist. So reciprocity is the bridge between motives and automorphic forms (Calegari, arXiv:2109.14145) [P]. For a general $G$ the Galois side needs the C-group of Buzzard-Gee (arXiv:1009.0785) [S], and the full conjecture needs a hypothetical Langlands group $L_F$, which nobody has constructed over a number field.

**Status.** The direction automorphic to Galois is known for **regular** algebraic $\pi$ over totally real and CM fields: Harris-Taylor, Shin, Chenevier-Harris (self-dual), and Harris-Lan-Taylor-Thorne and Scholze (2015, torsion included) without self-duality [S]. Local-global compatibility at $\ell = p$ is partial (Caraiani-Newton, Matsumoto, arXiv:2312.01551) [P]. The direction Galois to automorphic is the modularity problem (3.7, route R3 of document 04). Over fields that are neither totally real nor CM, and for non-regular $\pi$ such as Maass forms, no Galois representation is constructed.

## 3.5 Functoriality

**Conjecture 3.4 (Functoriality, Langlands 1970).** Let $H$ and $G$ be connected reductive over $F$ with $G$ quasi-split, and let $\phi : {}^L H \to {}^L G$ be an L-homomorphism. For every automorphic representation $\pi$ of $H$ there is an automorphic representation $\Pi$ of $G$ with $c_v(\Pi) = \phi(c_v(\pi))$ for almost all $v$.

The case $G = \mathrm{GL}_N$ with $\phi = r$ a representation of ${}^L H$ gives $L^S(s, \pi, r) = L^S(s, \Pi)$, so the analytic properties of the Godement-Jacquet L-function of $\Pi$ pass to $L^S(s, \pi, r)$. Known cases [S]: Jacquet-Langlands; base change and automorphic induction for cyclic extensions (Langlands 1980, Arthur-Clozel 1989); $\mathrm{Sym}^2$ (Gelbart-Jacquet 1978); $\mathrm{GL}_2 \times \mathrm{GL}_2 \to \mathrm{GL}_4$ (Ramakrishnan 2000); $\mathrm{GL}_2 \times \mathrm{GL}_3 \to \mathrm{GL}_6$ and $\mathrm{Sym}^3$ (Kim-Shahidi 2002); $\wedge^2 \mathrm{GL}_4$ and $\mathrm{Sym}^4$ (Kim 2003); classical groups to $\mathrm{GL}_N$ (Cogdell-Kim-Piatetski-Shapiro-Shahidi 2004, then Arthur 2013 and Mok 2015); $\mathrm{Sym}^n$ of non-CM holomorphic eigenforms for all $n$ (Newton-Thorne 2021) and of Hilbert forms of regular weight (arXiv:2212.03595). The methods are converse theorems, the trace formula, and, since 2000 for most new cases, automorphy lifting on the Galois side [S]. $\mathrm{Sym}^5$ of a Maass form and general tensor products $\mathrm{GL}_m \times \mathrm{GL}_n \to \mathrm{GL}_{mn}$ are open.

## 3.6 Arthur's conjectures and the endoscopic classification

The discrete spectrum is not tempered in general (Howe-Piatetski-Shapiro 1979). Arthur's conjectures organize it. A **global A-parameter** for $G$ is, in the substitute form for classical groups, a formal sum
$$\psi = \boxplus_{i} \mu_i \boxtimes \nu_{n_i},$$
with $\mu_i$ cuspidal unitary on $\mathrm{GL}_{m_i}$ and $\nu_n$ the $n$-dimensional representation of the Arthur $\mathrm{SL}_2$, subject to self-duality conditions. Each $\psi$ has local packets $\Pi_{\psi_v}$, a global component group $\mathcal{S}_\psi$, and a sign character $\epsilon_\psi$ built from symplectic root numbers. The **multiplicity formula** says
$$L^2_{\mathrm{disc}}(G(F)\backslash G(\mathbb{A}_F)) \cong \bigoplus_\psi \bigoplus_{\pi \in \Pi_\psi,\ \langle\cdot, \pi\rangle|_{\mathcal{S}_\psi} = \epsilon_\psi} m_\psi\, \pi.$$
Arthur (AMS Colloq. Publ. 61, 2013) proved this for quasi-split symplectic and orthogonal groups, and Mok (2015) for quasi-split unitary groups, assuming the stabilization of the twisted trace formula and some local results [S]. The stabilization (Moeglin-Waldspurger 2016) needs the **fundamental lemma**, proved by Ngô (Publ. IHES 2010, arXiv:0801.0446) through the Hitchin fibration [P], and the **twisted weighted fundamental lemma** (TWFL). Atobe-Gan-Ichino-Kaletha-Mínguez-Shin (arXiv:2410.13504, v3 July 2026) prove the local intertwining relation, so the classification depends only on the TWFL [P]. Halleck-Dube (arXiv:2611.26750, 2026-11-19, 190 pages) claims the TWFL in good characteristic [P]. If it holds, the endoscopic classification of quasi-split classical groups is unconditional. The project records this as `claimed` (06.6) until experts accept it.

## 3.7 Consequences: Ramanujan, Artin, Sato-Tate, Hasse-Weil

- **Ramanujan.** For a cuspidal unitary $\pi$ of $\mathrm{GL}_n(\mathbb{A}_F)$, every $\pi_v$ is tempered; at unramified $v$ the eigenvalues of $c_v(\pi)$ have absolute value 1. Functoriality for all $\mathrm{Sym}^m$ implies it, by Rankin-Selberg and Landau's lemma (Langlands 1970). Known: holomorphic modular forms (Deligne 1974, through the Weil conjectures); regular algebraic essentially self-dual $\pi$ over totally real and CM fields; cohomological $\mathrm{GL}_2$ over CM fields (ACC+ weight 0; BCGNT, arXiv:2309.15880; Matsumoto); $\mathrm{GL}_n$ over function fields (L. Lafforgue 2002) [S]. Best bound for $\mathrm{GL}_2$ over $\mathbb{Q}$: $|\log_p |\alpha_p|| \le 7/64$ (Kim-Sarnak) [U]. Getz-Hahn-Yao (arXiv:2509.14381) derive Ramanujan from expected properties of triple product L-functions [P].
- **Artin.** For an irreducible non-trivial $\rho : \mathrm{Gal}(\bar{F}/F) \to \mathrm{GL}_n(\mathbb{C})$, $L(s, \rho)$ is entire; in the strong form, $\rho$ is automorphic. Known: solvable image in dimension 2 (Langlands-Tunnell), odd 2-dimensional over $\mathbb{Q}$ (Khare-Wintenberger, Kisin). Even icosahedral over $\mathbb{Q}$ is open [S].
- **Sato-Tate.** For a non-CM elliptic curve $E/F$, the angles $\theta_v$ with $a_v = 2\sqrt{q_v} \cos\theta_v$ are equidistributed for $\frac{2}{\pi}\sin^2\theta\, d\theta$. By Serre it follows from automorphy of all $\mathrm{Sym}^n$ with non-vanishing on $\operatorname{Re} s = 1$. Known over totally real fields (Clozel-Harris-Shepherd-Barron-Taylor, Barnet-Lamb-Geraghty-Harris-Taylor 2011) and CM fields (ACC+ 2023) [S].
- **Hasse-Weil.** The zeta function of a smooth projective variety over a number field has meromorphic continuation and a functional equation. Known for curves of genus at most 2 and abelian surfaces over totally real fields (BCGP 2021) and through modularity; open for genus 3 curves over $\mathbb{Q}$ (Gee, arXiv:2510.02756) [P].
- **Modularity of elliptic curves over $\mathbb{Q}$** (Wiles, Taylor-Wiles, BCDT 2001) is the $\mathrm{GL}_2$ case of Conjecture 3.3 for $\rho = H^1_{\mathrm{et}}(E)$. In 2026 it is in Lean, in the semistable case, in anthropics/fermats-last-theorem (document 05) [P].

## 3.8 Function fields

Over a function field the program is much further on, because moduli of shtukas replace Shimura varieties.
- Drinfeld (1974 to 1987): reciprocity for $\mathrm{GL}_2$ [U].
- L. Lafforgue (Invent. Math. 2002): for every $n$, a bijection between cuspidal $\pi$ of $\mathrm{GL}_n(\mathbb{A}_F)$ with central character of finite order and irreducible $\ell$-adic $\rho$ of dimension $n$ with determinant of finite order, with Hecke eigenvalues matched to Frobenius eigenvalues, and Ramanujan as a consequence [S].
- V. Lafforgue (JAMS 2018, arXiv:1209.5352): for every reductive $G$, the space of cuspidal forms decomposes over semisimple global parameters $\sigma : \mathrm{Gal}(\bar{F}/F) \to \check{G}(\overline{\mathbb{Q}}_\ell)$, through excursion operators on the cohomology of stacks of shtukas, without the trace formula [P]. This is the direction automorphic to Galois. It does not say which $\sigma$ occur or with what multiplicity.
- Genestier-Lafforgue (arXiv:1709.00978, v3 2026) give compatible semisimple local parameters [P]. Böckle-Harris-Khare-Thorne (Acta 2019) prove potential automorphy for $\sigma$ with Zariski dense image [S].
- Gaitsgory-Raskin (arXiv:2508.02237) with AGKRRV (arXiv:2102.07906) give, in the unramified case and on a union of components, the arithmetic equivalence $\mathrm{Aut}_{G,c}^{\mathrm{unr}} \simeq \Gamma(\mathrm{LS}^{\mathrm{arthm}}_{\check{G}}, \omega)$ [P]. Gaitsgory-V. Lafforgue-Raskin (arXiv:2603.26925) and Raskin's ICM 2026 text announce Arthur-Ramanujan for unramified cuspidal forms of split $G$: each eigenform has a nilpotent $e \in \check{\mathfrak{g}}$ that controls the absolute values of its Hecke eigenvalues [P]. The full paper is in preparation, so the project records it as `claimed`.

## 3.9 Geometric Langlands

Let $k$ be algebraically closed of characteristic 0, $X$ a smooth complete connected curve over $k$, and $G$ connected reductive. Let $\mathrm{Bun}_G$ be the stack of $G$-bundles on $X$ and $\mathrm{LS}_{\check{G}}$ the derived stack of de Rham $\check{G}$-local systems on $X$.

**Theorem 3.5 (GLC, Gaitsgory, Raskin and coauthors, arXiv:2405.03599, 2405.03648, 2409.07051, 2409.08670, 2409.09856).** The functor
$$\mathbb{L}_G : \mathrm{D\text{-}mod}_{1/2}(\mathrm{Bun}_G) \to \mathrm{IndCoh}_{\mathrm{Nilp}}(\mathrm{LS}_{\check{G}})$$
is an equivalence. It is linear for the spectral action of $\mathrm{QCoh}(\mathrm{LS}_{\check{G}})$ through Hecke functors, it sends the vacuum Poincaré sheaf to the structure sheaf (suitably normalized), and its composite with global sections is the first Whittaker coefficient [P].

The five papers have 947 pages and no journal reference on 2026-11-25 [P]. GLC V reduces the theorem to existence and multiplicity one of Hecke eigensheaves for irreducible local systems, and proves both from the simple connectedness of $\mathrm{LS}^{\mathrm{irred}}_{\check{G}}$ and the scalar endomorphisms of the Poincaré sheaf [P]. The theorem is **global and unramified, in characteristic 0, in the de Rham setting**. It does not cover: Iwahori (tame) or wild ramification, local or global; the quantum version; the $\ell$-adic version over $\bar{\mathbb{F}}_q$ on all components; and the Fargues-Fontaine curve. These six problems are the open list of GLC V §0.4.1, which the authors say they cannot yet solve [P]. Route R8 of document 04 tracks them. The Betti form follows in characteristic 0 by Riemann-Hilbert arguments (GLC I, Thm 3.5.2) [P]. Mathlib has none of the foundations: no D-modules, no IndCoh, no derived stacks, no $\mathrm{Bun}_G$ (document 05).

## 3.10 p-adic and mod p Langlands

For $\mathrm{GL}_2(\mathbb{Q}_p)$ the correspondence is a theorem with $p$-adic coefficients. Colmez's Montreal functor (Astérisque 330, 2010), with Paškūnas (Publ. IHES 2013) and Colmez-Dospinescu-Paškūnas (2014), gives a bijection between absolutely irreducible admissible unitary Banach representations of $\mathrm{GL}_2(\mathbb{Q}_p)$ that are not ordinary and absolutely irreducible $\rho : G_{\mathbb{Q}_p} \to \mathrm{GL}_2(\overline{\mathbb{Q}}_p)$, compatible with $\mathrm{rec}$ on locally algebraic vectors [S]. Emerton (2011) proved local-global compatibility in the completed cohomology of modular curves [S]. Breuil-Mézard for $\mathrm{GL}_2(\mathbb{Q}_p)$ is known (Kisin 2009, Paškūnas 2015, Hu-Tan) [S].

The **categorical** form of Emerton-Gee-Hellmann asks for a fully faithful functor from smooth (or locally analytic) representations to ind-coherent sheaves on the Emerton-Gee stack $\mathcal{X}_n$ of $(\varphi, \Gamma)$-modules. Dotto-Emerton-Gee (arXiv:2603.26887, 279 pages) prove it for smooth $p$-power torsion representations of $\mathrm{GL}_2(\mathbb{Q}_p)$, $p \ge 5$, with fixed central character [P]; Dowd (arXiv:2610.25055) treats the Steinberg block for $p = 3$ [P]. $\mathrm{GL}_2(K)$ for $K \neq \mathbb{Q}_p$ and $\mathrm{GL}_n$ for $n \ge 3$ are open. **Mod p** Langlands beyond $\mathrm{GL}_2(\mathbb{Q}_p)$ is open: $\pi(\bar{\rho})$ is defined only in global cohomology, and its local nature is known in some cases for unramified $\mathrm{GL}_2$ (Breuil-Herzig-Hu-Morra-Schraen) [S]. The Serre weight conjectures are known in generic tame cases [S]. TauCeti has the adic Fargues-Fontaine curve in Lean and a roadmap `PadicLocalLanglandsForGL2Qp` (document 05) [P].

## 3.11 The dependency picture

Arrows go from a result to the results that use it. Square brackets give the tier of document 07.

```
local fields, Haar, adeles [T1] ---> class field theory, Weil group [T3] ---> LLC GL_1 [T3]
        |                                   |                                   |
        v                                   v                                   v
reductive groups, root data,        Hecke characters, Tate's thesis      L-group, parameters [T2]
L-group, Satake [T2]                       [T3,T6]                              |
        |                                                                       v
        +--> smooth reps, types, supercuspidals [T5] -------------> LLC GL_2 (local proof) [T5]
        |                                                                       |
        +--> modular forms, Hecke operators [T4] --> Eichler-Shimura, Deligne [T8]
        |                                                   |
        |      Galois deformations, p-adic Hodge [T8,T9] -->+--> patching, R = T [T8]
        |                                                   |        |
        |                                                   v        v
        |                                    modularity of E/Q   potential automorphy
        |                                    (anthropics FLT)    Sato-Tate, Sym^n [T6,T8]
        v
trace formula [T7] --> Jacquet-Langlands, base change --> Langlands-Tunnell --> Wiles
        |
        +--> stabilization <-- fundamental lemma (Ngo) <-- Hitchin fibration [T10]
        |          ^-- TWFL (Halleck-Dube 2026, claimed)
        v
endoscopic classification (Arthur, Mok; AGIKMS) --> LLC classical groups [T5,T7]
        |
Shimura varieties [T8] --> Galois reps for RACSDC pi --> LLC GL_n (Harris-Taylor) [T5]
        |
        +--> perfectoid methods [T9] --> torsion classes (Scholze), HLTT --> ACC+ over CM
Fargues-Fontaine curve, Bun_G, geometric Satake [T9] --> FS parameters --> Cotner-Feng
shtukas, excursion operators [T10] --> V. Lafforgue --> BHKT; GLC I to V --> Gaitsgory-Raskin --> GLR
```

Two facts stand out. First, the cheapest nodes of high value are definitions and statements, because most top nodes are conjectures. Second, all general results on reciprocity rest on Shimura varieties, $p$-adic Hodge theory or the trace formula, each of which is hundreds of thousands of lines of Lean away (document 05, research E §7).

## 3.12 What is proved and what is open

| Statement | Proved | Open | Lean on 2026-11-25 |
|---|---|---|---|
| Local and global CFT ($\mathrm{GL}_1$) | all global and local fields | nothing classical | NYLL (Apache-2.0), riemann-lean (no licence) [P] |
| LLC $\mathrm{GL}_n$ | all $n$, all non-archimedean $F$ | an explicit form in general; a local proof for $n \ge 3$ | statement fragments only (Langlands-lib, no licence) [P] |
| LLC general $G$ | classical groups (Arthur, Mok, KMSW), $\mathrm{GSp}_4$, $G_2$, many special classes | existence with all desiderata; uniqueness; FS equals classical in general; small $p$; $F_4$ to $E_8$ | nothing; TauCeti PR #2458 plans $G_2$ [P] |
| Reciprocity $\mathrm{GL}_n$ | $n = 1$; $n = 2$ odd over $\mathbb{Q}$; many potential cases | general $n$, non-regular, even, fields neither CM nor totally real | octahedral Langlands-Tunnell in anthropics FLT [P] |
| Functoriality | the cases of 3.5 | general; tensor products; non-endoscopic transfers of Maass forms | nothing |
| Arthur classification | quasi-split classical groups, modulo TWFL (claimed 2026-11-19) | inner forms in general, exceptional groups | nothing |
| Ramanujan | Deligne; regular algebraic cases; function fields | Maass forms; Selberg's $1/4$; general $\mathrm{GL}_n$ | `RamanujanTau` statement in formal-conjectures [P] |
| Artin | solvable 2-dim; odd 2-dim over $\mathbb{Q}$ | even icosahedral; dim $\ge 3$ | nothing |
| Sato-Tate | elliptic curves over totally real and CM fields | genus 2 in general | statement in formal-conjectures [P] |
| Modularity of $E/\mathbb{Q}$ | all $E$ (BCDT) | over general number fields | semistable case in anthropics FLT [P] |
| Function fields | $\mathrm{GL}_n$ (L. Lafforgue); automorphic to Galois for all $G$ | Galois to automorphic for general $G$ with ramification; multiplicities | nothing |
| GLC | char 0, de Rham, unramified | the six problems of GLC V | nothing |
| p-adic LLC | $\mathrm{GL}_2(\mathbb{Q}_p)$, categorical for $p \ge 5$ | $\mathrm{GL}_2(K)$, $\mathrm{GL}_n$, mod $p$ in general | adic FF curve in TauCeti [P] |
| RH, GRH for Dirichlet | claimed by Alpöge 2026-11-20; RH certified by the Lean FRO 2026-11-21 | human understanding; GRH for $\mathrm{GL}_n$, $n \ge 2$ | riemann-lean, read only [P] |

## 3.13 Lessons for the project

1. **Most of the program is statements.** The level G1 of document 02 (every main conjecture stated in Lean, pinned and checked by the fidelity battery) is the most valuable output per line. No public Lean library states LLC, functoriality or Arthur's conjectures with honest definitions (research E §4, §7).
2. **The statements have choices.** Normalizations of Frobenius and of L-functions, the class of representations (algebraic, regular, cohomological), the form of the parameters (enhanced, rigid, isocrystal) and the coefficient field all change the meaning. 06 fixes one choice for each statement and proves equivalences where two choices are in use.
3. **General LLC is not one statement.** For general $G$ the conjecture is a list of desiderata without a known uniqueness theorem. `LocalLanglands` in 06 is a structure of data and properties, not a single proposition, and each property is a separate node.
4. **$\mathrm{GL}_1$ and local $\mathrm{GL}_2$ are the only closed proofs within reach.** CFT is in Lean already under a licence the project can use. The local $\mathrm{GL}_2$ proof is purely local and has a textbook (Bushnell-Henniart). Everything for $n \ge 3$ uses global input. This sets level G2.
5. **Two global routes, both deep.** The Galois route (deformations, patching, $p$-adic Hodge theory) gives most modern reciprocity results and has Lean precedent in two FLT projects. The trace formula route gives the classification and has almost no Lean. The handbook teaches both, and the library starts on the Galois route because the precedent exists.
6. **Fresh claims are frequent.** In November 2026 alone: Halleck-Dube, Fintzen-Kaletha, Atobe-Kaletha-Mínguez-Shin, Dieulefait, and Alpöge's RH. Route R1 of 04 exists to check such claims formally where a part is small enough, and the claim policy of 06.6 keeps them out of the hypotheses until they are checked.
7. **Geometric Langlands is proved but far from Lean.** Its foundations (derived algebraic geometry, ind-coherent sheaves, D-modules on stacks) are years of library work. The project states it last and teaches it in the handbook first.
