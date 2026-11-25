# 01. The state of the field, November 2026

This document records what is known on 2026-11-25, with sources. It is a synthesis of the six research reports A to F in `research/sources/` (index: `research/00-index.md`). The tags are:
- **[P]**: the primary source was read (arXiv abstract page, paper, journal page, repository, official schedule);
- **[S]**: secondary, from citations, search results or memory, and partly confirmed;
- **[U]**: unverified;
- **[R]**: a claim that a repository makes about itself in its README or notes, not checked by the project.

A tag after a row or a sentence is the tag that the report gives. A judgment of difficulty or of value is the project's own and is [U]. Every [S] and [U] item becomes a task for the `reader` role (document 10) before a node of the map depends on it. Links to arXiv have the form `https://arxiv.org/abs/<id>`.

## 1.1 What is proved and what is open

The Langlands program is not one conjecture. It is a family of conjectures that relate automorphic forms and representations of reductive groups to Galois representations and motives. Some parts are theorems, some parts are open with a clear strategy, and some parts have no known strategy. The table gives the state by area. Sections 1.3 to 1.8 have the details and the sources.

| Area | Proved (selected) | Open (selected) | Source |
|---|---|---|---|
| $GL_1$ (class field theory) | local and global CFT, Hecke L-functions, Tate's thesis, Langlands for tori | nothing central | C 3.1, B 2.1 [U, standard] |
| Local Langlands, $GL_n$ | $p$-adic (Harris-Taylor, Henniart, Scholze), char $p$ (Laumon-Rapoport-Stuhler, Li-Huerta) | explicit forms for wild cases | B 2.1 [S]/[P] |
| Local Langlands, other $G$ | quasi-split classical groups (Arthur, Mok), $GSp_4$, $G_2$ (Gan-Savin), real groups, regular and non-singular supercuspidals (Kaletha), unipotent (Solleveld); semisimple parameters for all $G$ (Fargues-Scholze, Genestier-Lafforgue) | the full LLC for general $G$ with all desiderata; exceptional groups beyond $G_2$; small $p$ | B 0, B 4 [P] |
| Global, function fields | $GL_n$ both directions (L. Lafforgue); automorphic to Galois for all $G$ (V. Lafforgue); unramified arithmetic equivalence on some components (Gaitsgory-Raskin with AGKRRV) | ramified Galois to automorphic for general $G$; Arthur multiplicity (announced, unramified) | C 2 [P] |
| Global, number fields, reciprocity | elliptic curves over $\mathbb{Q}$, real quadratic, cubic, many imaginary quadratic fields; Serre's conjecture; potential automorphy over totally real and CM fields; a positive proportion of abelian surfaces over $\mathbb{Q}$ | reciprocity for $GL_n$, $n \ge 3$, in general; even and irregular cases; abelian varieties of dimension $\ge 3$ | C 3, C 5 [P]/[U] |
| Functoriality | base change, Jacquet-Langlands, $\mathrm{Sym}^2,\mathrm{Sym}^3,\mathrm{Sym}^4$, $GL_2 \times GL_3$, $\wedge^2 GL_4$, classical groups to $GL_N$, all $\mathrm{Sym}^n$ of holomorphic eigenforms (Newton-Thorne) | functoriality in general, $\mathrm{Sym}^5$ of Maass forms, non-endoscopic transfers | C 3.8 [P]/[S]/[U] |
| Trace formula, endoscopy | Arthur-Selberg trace formula; fundamental lemma (Ngô); endoscopic classification of quasi-split classical groups, conditional on the twisted weighted fundamental lemma (AGIKMS) | the twisted weighted fundamental lemma is claimed (1.2); exceptional and non-quasi-split groups | C 3.9 [P] |
| Ramanujan | holomorphic forms (Deligne); $GL_n$ over function fields (L. Lafforgue); regular algebraic self-dual cases; cohomological $GL_2$ over CM fields in large part | Maass forms on $GL_2/\mathbb{Q}$ (bound $7/64$); Selberg's $\lambda_1 \ge 1/4$ | C 5 [P]/[U] |
| Geometric Langlands | GLC in char 0, global, unramified, every reductive $G$ (GLC I to V) | ramified, quantum, $\ell$-adic in char $p$ in full, Fargues-Fontaine curve | A 0, A 3 [P] |
| $p$-adic and mod $p$ | $p$-adic LLC for $GL_2(\mathbb{Q}_p)$ (Colmez, Paškūnas, CDP); categorical form for $p \ge 5$ (DEG 2026) | $GL_2(K)$, $K \ne \mathbb{Q}_p$; $GL_n$, $n \ge 3$; mod $p$ beyond $GL_2(\mathbb{Q}_p)$ | D 7, D 9 [P] |
| Shimura varieties | Galois representations for regular algebraic $\pi$ over CM and totally real fields (HLTT, Scholze); Igusa stacks for Hodge and abelian type; torsion vanishing for abelian type | Langlands-Rapoport in general; Kottwitz conjecture in general; non-abelian type | D 5, D 7 [P]/[S] |

## 1.2 Fresh claims of 2026, not yet checked

These results appeared in 2026, most of them in the last three months. None is refereed. The project treats each one as a claim with a date and a status. It never uses one as a hypothesis (06.6, 14.3) until the `reader` role and one expert have checked it. Route R1 (document 04) is the formal check of some of them in Lean.

| Claim | Source | What it claims | Status on 2026-11-25 |
|---|---|---|---|
| Halleck-Dube | arXiv:2611.26750 (19 Nov 2026, 190 pages) [P] | the weighted fundamental lemma for Lie algebras of quasi-split unramified groups, by $\xi$-stable Higgs bundles for group schemes over a curve; from this the twisted weighted fundamental lemma in good characteristic, and so, with AGIKMS (arXiv:2410.13504 v3), an unconditional endoscopic classification of quasi-split classical groups | six days old, unrefereed; the last input of Arthur's classification if correct |
| Gaitsgory-V. Lafforgue-Raskin (GLR) | Raskin's ICM 2026 text (samraskin.net/icm.pdf) [P]; companion arXiv:2603.26925 (27 Mar 2026, v2 14 Apr 2026) [P] | the Arthur-Ramanujan conjecture for everywhere unramified cusp forms on split $G$ over function fields, through geometric Langlands | announced; the main paper is "in preparation" [S] |
| Alpöge, RH in Lean | release of 2026-11-20 (alpo.ge, note remark.pdf) [P]; Lean FRO and Mathlib Initiative joint statement of 2026-11-21 [P] | a Lean proof of the Riemann hypothesis, found with Claude; the note also claims GRH for Dirichlet L-functions; the method uses chains of theta lifts between definite unitary groups, GGP periods, Rallis seesaw and a relative trace formula | the formal statement and proof are certified by the FRO statement [P]; human understanding of the proof is pending; the local copy (riemann-lean) is not built by the project and has no licence (05) |
| openai/math family 014 | github.com/openai/math, created 6 Oct 2026 [P] | the full-support restricted GLC in char $p$ under four hypotheses on $p$ (dated 24 Sep 2026); also a GLR rationality conjecture and Ramanujan for generic exceptional groups | AI-generated, unrefereed, no Lean entry for this family; "Retracted 6 October 2026" labels inside the family in a Pitt catalogue [S]; no community check listed [P] |
| openai/math family 069 | same [P] | global quantum GLC at irrational level $c \in \mathbb{C} \setminus \mathbb{Q}$ for all simple $G$ (4 Oct 2026) | AI-generated, unrefereed, no Lean entry, no community check [P] |
| Fintzen-Kaletha | arXiv:2611.31396 (23 Nov 2026) [P] | supercuspidal representations and types from double covers of twisted Levi subgroups and the Fourier-Weil representation, with a direct link to the Galois side | two days old |
| Atobe-Kaletha-Minguez-Shin (AKMS) | arXiv:2611.31683 (23 Nov 2026) [P] | the local intertwining relation for inner forms of $GL_N$ in char 0; an input to the endoscopic classification of non-quasi-split unitary groups (KMSW) | two days old |
| Cotner-Feng | arXiv:2609.16381 and 2609.16387 (14 Sep 2026) [P] | the Fargues-Scholze parameter on inertia of Yu's supercuspidals equals Kaletha's parametrization; Fargues-Scholze has finite fibres and is surjective onto inertial parameters; v2 is unconditional | two months old |
| Dotto-Emerton-Gee (DEG) | arXiv:2603.26887 (27 Mar 2026, 279 pages) [P] | a categorical $p$-adic LLC for $GL_2(\mathbb{Q}_p)$, $p \ge 5$, for torsion coefficients | unrefereed |
| Dowd | arXiv:2610.25055 (Oct 2026, v2 Nov 2026) [P] | the $3$-adic Steinberg block and a categorical LLC for $GL_2(\mathbb{Q}_3)$ | unrefereed |
| Dieulefait | arXiv:2611.32569 (24 Nov 2026) [P] | from potential modularity to modularity lifting over totally real $F$, $p \ge 7$ unramified | one day old |
| Matsumoto | arXiv:2312.01551 v3 (29 Nov 2025) [P, abstract only] | Ramanujan for all cohomological cuspidal $GL_2$ over CM fields | unrefereed |
| Lomelí | arXiv:2610.23985 (14 Oct 2026) [P] | stable base change for unitary groups over function fields; Ramanujan and RH for Langlands-Shahidi L-functions | unrefereed |
| Takanashi, $G_2$ | arXiv:2609.19430, 2609.19439 (16 Sep 2026), 2611.06742 (4 Nov 2026) [P] | the formal degree conjecture for $G_2$; endoscopic character identities for Gan-Savin packets; Arthur packets for $G_2$ | unrefereed |
| Masullo, GRH | posted by Ravi Vakil, 20 Nov 2026 [S] | a human proof of GRH | issues reported within hours [S]; the project ignores it |

[U] The fresh claims are the best test bed that the project has for G4 (document 02). A Lean formalization of a recent preprint, or of one of its key lemmas, gives a result that is new, checkable and useful to its authors. The project writes to the authors before it publishes any result about their work (14.4).

## 1.3 Geometric Langlands

**The proof.** The geometric Langlands conjecture (GLC) in char 0, global and unramified, for every connected reductive $G$, is proved in five papers by Gaitsgory, Raskin and coauthors: arXiv:2405.03599, 2405.03648, 2409.07051, 2409.08670 and 2409.09856, 947 PDF pages in total [P]. The theorem is that the functor
$$\mathbb{L}_G : \text{D-mod}_{1/2}(\mathrm{Bun}_G) \to \mathrm{IndCoh}_{\mathrm{Nilp}}(\mathrm{LS}_{\check G})$$
is an equivalence. This is Conjecture 1.6.7 of GLC I, the Arinkin-Gaitsgory form (arXiv:1201.6343) [P]. GLC I is at v3 (30 Sep 2025) and GLC V at v3 (16 Jan 2026). None of the five has a journal reference [P].

**Follow-ups.**
- Gaitsgory-Raskin, arXiv:2508.02237 (4 Aug 2025): the restricted $\ell$-adic GLC in char $p$ on a union of components [P].
- Gaitsgory's ICM write-up, arXiv:2509.24902: the local and global conjectures over function fields, by the categorical trace of Frobenius [P].
- GLR, arXiv:2603.26925: a canonical filtration of automorphic functions that separates the tempered and generic parts [P].
- Toda, arXiv:2602.09359: Dolbeault GLC for $GL_2$ with reduced spectral curves [P].
- Nam, arXiv:2608.04207: the Iwahori fundamental local equivalence [P]. Faergeman 2405.18268 and Nam 2411.03057 are earlier steps toward tame GLC [P].
- Dhillon-Taylor: tame local Betti GLC, v2 with integer coefficients (5 Oct 2026) [P].
- Zhu, arXiv:2504.07482: tame categorical local Langlands for unramified quasi-split groups [P].
- Chen-Wang, arXiv:2610.36377 (26 Oct 2026): the Gross-Prasad case of relative duality for $SO(n) \times SO(n-1)$ [P].
- Ben-Zvi-Sakellaridis-Venkatesh (BZSV), arXiv:2409.04677: relative Langlands duality [P].

**The six open problems of GLC V.** GLC V Section 0.4.1 lists six problems that the authors write they do not yet know how to solve: Iwahori (tame) ramification, quantum GLC, wild local, wild global, the restricted $\ell$-adic GLC in char $p$ for all components, and GLC for the Fargues-Fontaine curve [P]. Report A Section 3 lists 18 open problems in all, with ratings [U].

**Expositions of 2026.** Scholze, Séminaire Bourbaki exposé 1252 (March 2026, 56 pages), the best short guide to the proof [P]. Ben-Zvi, "What is the Geometric Langlands Correspondence about?", arXiv:2605.23167 (22 May 2026) [P]. Raskin, "Introduction to Geometric Langlands", Yale course notes, Fall 2025, 74 pages [P].

**Lean.** No Lean formalization of any part of GLC exists [P]. Mathlib has quasicategories, model categories, triangulated and derived categories, schemes and sites. It has no D-modules, no IndCoh, no derived algebraic geometry and no $\mathrm{Bun}_G$ [P]. A faithful statement of GLC is several years of infrastructure away [U]. Realistic targets are the classical shadows: the dual root datum, the affine Grassmannian as an ind-scheme, the Satake isomorphism, the unramified Hecke algebra over a function field, and the abelian case (geometric class field theory) [U].

## 1.4 Local Langlands

**The general conjecture is open.** Taïbi's survey (arXiv:2510.00632, IHES 2022 school) states the LLC for all connected reductive $G$ as Conjecture 6.1 [P]. No paper claims a full proof for all groups [S].

**Fargues-Scholze.** arXiv:2102.13459 (v4, accepted version; published as Astérisque 466) attaches a semisimple L-parameter to every irreducible smooth representation of every $G(E)$, $E$ a local field [P]. Scholze's motivic sequel, arXiv:2501.07944 (to appear in Crelle), proves that the parameters do not depend on $\ell$ [P]. The parameters agree with the classical LLC for $GL_n$ and inner forms, $GSp_4$ (Hamann), odd unramified unitary groups (Bertoloni Meli-Hamann-Nguyen), unramified $SO$ and $U$ for odd $p$ (Peng, arXiv:2503.04623, v4 9 Jul 2026), local function fields through Genestier-Lafforgue (Li-Huerta), and depth zero (Fu, arXiv:2610.16445, conditional) [P]. Cotner-Feng (1.2) add Yu's supercuspidals on inertia.

**Supercuspidals.** Kaletha's explicit LLC for regular supercuspidals (JAMS 32, 2019, arXiv:1602.03144) and non-singular supercuspidals (arXiv:1912.03274) covers almost all supercuspidals in large residue characteristic [P]. Fintzen (Annals 2021) proved Yu's construction exhaustive when $p \nmid |W|$ [P]. Fintzen-Schwein, arXiv:2501.18553, extend it to $p = 2$ [P]. Fam, arXiv:2602.14121, treats exceptional groups at $p = 2, 3$ [P]. Luo-Stevens, arXiv:2608.20225, give an explicit LLC for middle supercuspidals of $GL_{2n}$ [P].

**Classification and character identities.** AGIKMS (arXiv:2410.13504) prove the local intertwining relation for quasi-split classical groups [P]. Beuzart-Plessis, arXiv:2508.08470, proves the Hiraga-Ichino-Ikeda formal degree conjecture for symplectic and even orthogonal groups [P]. Kaletha-Mezo, arXiv:2605.06922, give the refined LLC for discrete parameters of disconnected real groups [P]. Solleveld-Xu, arXiv:2411.19846, treat non-singular depth zero [P].

**Categorical LLC.** Hansen-Mann, arXiv:2606.00983 (266 pages): a programme in which one hypothesis implies the full categorical LLC for $GL_n$ [P]. Helm-Solleveld-Xu, arXiv:2606.10149: the generic categorical LLC for many quasi-split groups [P]. Gleason-Hamann-Ivanov-Lourenço-Zou, arXiv:2606.02799: Zhu's category equals the Fargues-Scholze category for torsion coefficients [P]. Dillery-Eteve, arXiv:2608.02708: an extended spectral action for non-quasi-split groups [P]. The full conjecture is open [P].

**Open in the local theory.** Report B Section 4 lists 17 problems. The main ones: the LLC with all desiderata for general $G$; a characterization without global input; Fargues-Scholze equals the classical LLC in general; small $p$ and wild ramification; exceptional groups beyond $G_2$; converse theorems beyond $GL_n$ (Matringe, arXiv:2409.20240, shows failure for $SO_{2n}$, $n \ge 3$, over some fields) [P]/[S].

**$G_2$ in Lean.** A TauCeti roadmap PR (TauCetiProject/TauCetiRoadmap #2458, opened 16 Nov 2026) plans a Lean formalization of LLC for $G_2$ [P].

## 1.5 Global Langlands over function fields

- L. Lafforgue (Invent. Math. 147, 2002): the Langlands correspondence for $GL_n$ in both directions, with Ramanujan [U]; content confirmed in Raskin's ICM text [P].
- V. Lafforgue (JAMS 31, 2018, arXiv:1209.5352): automorphic to Galois for every reductive $G$, by excursion operators, without the trace formula [P].
- Genestier-Lafforgue, arXiv:1709.00978 (v3 30 Jul 2026): semisimple local parameters in equal characteristic, compatible with the global ones [P].
- Böckle-Harris-Khare-Thorne (Acta Math. 223, 2019): Zariski dense $\check G$-local systems are potentially automorphic [S].
- AGKRRV, arXiv:2010.01906, 2012.07665, 2102.07906: restricted local systems, nilpotent singular support, automorphic functions as the trace of Frobenius [P].
- Gaitsgory-Raskin with AGKRRV give an unramified arithmetic equivalence $\mathrm{Aut}^{\mathrm{unr}}_{G,c} \simeq \Gamma(\mathrm{LS}^{\mathrm{arthm},\prime}_{\check G}, \omega)$ on some components, and on all components for $GL_n$ [P, as stated in Raskin's ICM text].
- GLR announce Arthur-Ramanujan for unramified cusp forms on split $G$ (1.2).
- Lomelí, arXiv:2610.23985 (1.2).

Open over function fields: Galois to automorphic for general $G$ with ramification; the Arthur multiplicity formula beyond the unramified case (C 5, problems 16 and 17) [P].

## 1.6 Global Langlands over number fields

**Modularity and reciprocity.**
- All elliptic curves over $\mathbb{Q}$ are modular (Wiles, Taylor-Wiles, BCDT) [U]. Serre's modularity conjecture (Khare-Wintenberger, with Kisin), and with it the odd 2-dimensional Artin conjecture over $\mathbb{Q}$ [U].
- Elliptic curves are modular over real quadratic (Freitas-Le Hung-Siksek), totally real cubic (Derickx-Najman-Siksek) and quartic fields without $\sqrt5$ (Box) [S].
- Caraiani-Newton, arXiv:2301.10509 v4 (accepted, 20 Oct 2026): all elliptic curves over infinitely many imaginary quadratic fields, among them $\mathbb{Q}(\sqrt{-d})$, $d = 1, 2, 3, 5$ [P].
- Boxer-Calegari-Gee-Pilloni (BCGP), arXiv:2502.20645 (28 Feb 2025, 230 pages): a positive proportion of abelian surfaces over $\mathbb{Q}$ are modular [P]. Gee's ICM survey (arXiv:2510.02756) gives a density of $5551/46656 \approx 0.119$ in a natural genus 2 sample [P].

**Galois representations and automorphy lifting.**
- Harris-Lan-Taylor-Thorne (arXiv:1411.6717) and Scholze (arXiv:1306.2070): Galois representations for regular algebraic cuspidal $\pi$ of $GL_n$ over CM or totally real fields [P].
- ACC+ (10 authors, Annals 197, 2023, arXiv:1812.09999): automorphy lifting over CM fields without self-duality; potential modularity of elliptic curves over CM fields; Ramanujan for weight 0 $GL_2$ over CM fields [P abstract].
- BCGNT, arXiv:2309.15880 (v3 Mar 2025): Ramanujan and Sato-Tate for Bianchi forms of weight $\ge 2$, and parallel weight over CM fields [P].
- Survey: Caraiani-Shin, arXiv:2311.13382 [P].

**Functoriality.** The known cases are in 1.1. Newton-Thorne prove all symmetric powers of non-CM holomorphic eigenforms over $\mathbb{Q}$ (Publ. IHES 134, 2021) and of Hilbert forms of regular weight (arXiv:2212.03595 v2) [P]/[S]. Almost all cases after 2000 come from Galois methods, not from the trace formula or converse theorems [S].

**Trace formula and endoscopy.** Ngô proved the fundamental lemma (arXiv:0801.0446) [P]. Chaudouard-Laumon proved the split weighted fundamental lemma [S]. Moeglin-Waldspurger stabilized the twisted trace formula assuming the twisted weighted fundamental lemma [U]. AGIKMS make the endoscopic classification conditional only on that lemma [P], and Halleck-Dube claims it (1.2). Gee-Taïbi give Arthur's multiplicity formula for $GSp_4$ (arXiv:1807.03988) [U].

**Beyond Endoscopy.** Yuhao Cheng's five-part series on ramified $GL_2/\mathbb{Q}$ (arXiv:2505.18967 to 2608.15553) [S]/[P]; Deng-Espinosa on $GL_3/\mathbb{Q}$, arXiv:2603.21506 [P]; Getz-Hahn-Yao, arXiv:2509.14381, triple product L-functions imply Ramanujan [P]. No new case of functoriality has come from Beyond Endoscopy [P].

**Open.** Report C Section 5 lists 20 open problems with ratings 1 to 5 [U for the ratings]. The main ones: reciprocity for $GL_n$ over $\mathbb{Q}$; full local-global compatibility; modularity of all elliptic curves over all number fields; the paramodular conjecture; Fontaine-Mazur; Artin's conjecture (even icosahedral over $\mathbb{Q}$, dimension $\ge 3$); Ramanujan for Maass forms; functoriality in general; the Langlands group $L_F$.

## 1.7 $p$-adic and mod $p$ Langlands

- $GL_2(\mathbb{Q}_p)$: Colmez (Astérisque 330, 2010), Paškūnas (Publ. IHES 2013), Colmez-Dospinescu-Paškūnas (Cambridge J. Math. 2014), Emerton's local-global compatibility [S].
- Emerton-Gee-Hellmann, "An introduction to the categorical p-adic Langlands program", arXiv:2210.01404, v5 (19 Sep 2025, final, 252 pages) [P].
- Johansson-Newton-Wang-Erickson (JNWE), arXiv:2403.19565, Compositio 162 (2026): a categorical form for locally admissible representations [S].
- DEG (arXiv:2603.26887) for $p \ge 5$ and Dowd (arXiv:2610.25055) for $p = 3$, Steinberg block (1.2) [P].
- Mod $p$ $GL_2$: Breuil-Herzig-Hu-Morra-Schraen (BHHMS) on finite length; Bertoletti beyond multiplicity one; Dotto-Le Hung and Zhao-Hu on Gelfand-Kirillov dimension (2026); Chan on Breuil's lattice conjecture [P].
- Analytic foundations: the Clausen-Scholze analytic stacks course, analytic de Rham stacks of Fargues-Fontaine curves, a 6-functor formalism on the curve, rational analytic prismatization (2026) [P]/[S]. Clausen-Scholze, "Lectures on Condensed Mathematics", arXiv:2605.03658 [S].
- Open (report D Section 7, 13 rows): $p$-adic LLC for $GL_2(K)$, $K \ne \mathbb{Q}_p$; any $p$-adic LLC for $GL_n$, $n \ge 3$; mod $p$ beyond $GL_2(\mathbb{Q}_p)$; Serre weights for general $GL_n$; Breuil-Mézard in general; real geometrization [P]/[S].

## 1.8 Shimura varieties

- Caraiani-Scholze (Annals 186, 2017 and 199, 2024): the generic part of the cohomology of unitary Shimura varieties, an input to ACC+ [S].
- Igusa stacks: Daniels-van Hoften-Kim-Zhang (DvHKZ I, arXiv:2408.01348, v3 Nov 2026) for Hodge type [S]; DvHKZ II, arXiv:2603.24921 (26 Mar 2026), for abelian type, with Fargues-Scholze LLC equal to the semisimplified Arthur and Mok LLC for classical groups of types A, B, D [P].
- Torsion vanishing: Yang-Zhu, arXiv:2505.04329, prove the Hamann-Lee conjecture for abelian type with a mild restriction on $\ell$ [P]. Caraiani-Hamann-Zhang (CHZ), arXiv:2607.25889, treat intersection cohomology [S].
- Langlands-Rapoport: abelian type at hyperspecial level is essentially done (Kisin, Kisin-Shin-Zhu); parahoric level in part (van Hoften) [S].

## 1.9 ICM 2026 and prizes

ICM 2026 was in Philadelphia, 23 to 30 July 2026. The rows come from an unofficial mirror of the full schedule [P].

| Speaker | Title | Type |
|---|---|---|
| Dennis Gaitsgory | Local and Global Langlands Conjecture(s) Over Function Fields | plenary, 24 Jul |
| Sam Raskin | Unramified Automorphic Forms | section |
| Toby Gee | Modularity Theorems for Abelian Surfaces | section |
| Jessica Fintzen | Reduction from Representations of p-adic Groups to Representations of Finite Groups | section, 27 Jul |
| David Ben-Zvi, David Nadler | Potent Categorical Representations | joint section |
| Valentin Blomer; Paul Nelson; Srikanth Iyengar; Yongchang Zhu; Raf Cluckers | density theorems; the orbit method and L-functions; congruence ideals; loop groups; motivic integration | section |

Prizes [P]/[S]: the 2025 Breakthrough Prize to Gaitsgory and a 2025 New Horizons Prize to Raskin, both for GLC [P]. The 2026 Fields Medals (Deng, Pardon, Tsimerman, Wang) are not for Langlands work [S]. The Abel Prize 2026 went to Faltings [S]. The 2026 Breakthrough Prize went to Merle, unrelated [P].

## 1.10 Lean and Mathlib

Mathlib master is b5aed57ecb (2026-11-25) on Lean v4.37.0-rc1. The tag v4.35.0 is 56a005855e, and the tag v4.36.0 is fc4f59e577 [P].

**Present** [P]: `NumberField.AdeleRing`, the finite adele ring of a Dedekind domain, completions at places; `IsNonarchimedeanLocalField` (`NumberTheory/LocalField/Basic.lean:44`); `HeckeCharacter` and `LFunction` (`NumberTheory/NumberField/HeckeLFunction.lean`); the abstract `HeckeRing` (Shimura ch. 3); about 40 files of modular forms with q-expansions, Eisenstein series, the Petersson product and L-functions; `RootPairing` and `RootDatum` (`LinearAlgebra/RootSystem/Defs.lean:80,110`); Lie algebras; group cohomology with Hilbert 90 and Shapiro; infinite Galois theory; profinite groups; Haar measure; étale and pro-étale sites; condensed mathematics; triangulated and derived categories; quasicategories; seeds of $B_{\mathrm{dR}}$ and Fontaine's $\theta$. The `AdeleRing` docstring says the construction is wrong for function fields [P].

**Absent** [U, name search]: the Weil group and Weil-Deligne representations; the L-group; reductive group schemes over a base; smooth and admissible representations; Tate's thesis; local and global CFT; Lubin-Tate theory; Hecke operators on modular forms; Galois representations of modular forms; Shimura varieties; $\mathrm{Bun}_G$.

**Open PRs** [P]: #40934, #41277, #43087 (Hecke operators and Hecke rings); #41520, #41525, #45067 (smooth representations); #42687 (class formations); #42312 (Huber rings, `awaiting-author`); #26389 (perfectoid fields, draft, 13 `sorry`s in a fork commit). No open PR matched "Weil group", "Tate thesis", "Lubin-Tate" or "Galois representation" [P].

**formal-conjectures** (9097e2f90e, v4.33.1) has no string "Langlands" [P]. It has `ModularityConjecture`, `SatoTateConjecture`, `RamanujanTau`, `HasseWeil`, and a Borel-Jacquet `IsAutomorphicForm` for $GL_n$ over $\mathbb{Q}$ without cusp forms [P]. These are the first bridges of 06.

**Trust tools** [P]: comparator, nanoda, lean4export, `formalization.yaml` (Mathlib Initiative), the Palomar Archive (1,110 repositories with a comparator Challenge/Solution layout). All are Apache-2.0 except where the repositories differ.

## 1.11 Other Lean projects

| Project | Content | Licence | Pin | Use (05) |
|---|---|---|---|---|
| ImperialCollegeLondon/FLT | quaternionic automorphic forms, concrete Hecke operators `HeckeOperator.T`, `U`, deformations, patching with `REqualsT`, a Verso blueprint; human, funded to 2029; 25 files with `sorry` | Apache-2.0 | v4.35.0 | port [P] |
| anthropics/fermats-last-theorem | FLT end to end by AI agents; about 1.05M declarations checked by nanoda; octahedral Langlands-Tunnell, R = T, Wiles semistable, Ribet for the Frey curve, Mazur; layout `Theorems/Thm_X_y.lean` and `P2M/Sol/S_X_y.lean` | Apache-2.0 | v4.33.1 | port [P]/[R] |
| n-yamaguchi-0729/NYLL and ClassFieldTheory | local, global and function field CFT, Codex-assisted; `finiteAbelianLocalReciprocity` over `IsNonarchimedeanLocalField` | Apache-2.0 | v4.36.0 | port [P]/[R] |
| kbuzzard/ClassFieldTheory | human, Clay summer school 2025, ongoing | Apache-2.0 | v4.36.0-rc2 | read, align [P] |
| lana-agents/local-class-field-theory | $p$-adic local CFT by agents | Apache-2.0 | v4.32.0 | read [P] |
| TauCetiProject/TauCeti | AI-written library downstream of Mathlib, incubated by the Lean FRO; 30 completed roadmaps, among them adic spaces and the adic Fargues-Fontaine curve (2026-10-28), local Galois groups, ramification, adeles and Hecke characters, Chebotarev; open roadmaps `PadicLocalLanglandsForGL2Qp`, `LanglandsParameterStacks`, `PerfectoidSpaces`, `ShimuraData`, `GeometricSatakeAndFusion`, `BunGAndNewtonStrata` | Apache-2.0 | not recorded | port, align roadmaps [P] |
| fukubillueda-web/epsilon_FML, epsilon_SML | Langlands's first and second main lemmas on epsilon factors | Apache-2.0 | v4.32.2 | port [P] |
| Rogerhu12/hecke-seven-eighths | Hecke L-functions zero-free for $\mathrm{Re}(s) > 7/8$ | Apache-2.0 | v4.35.0-rc3 | read [P]/[R] |
| ANR-FALSE/PadicModForms | Serre $p$-adic modular forms, Verso site | Apache-2.0 | v4.36.0 | read [P] |
| CBirkbeck/LeanModularForms | Mathlib staging for modular forms | Apache-2.0 | v4.31.0-rc2 | read [P] |
| emilyriehl/infinity-cosmos; dagurtomas/LeanCondensed | $\infty$-categories; condensed staging | Apache-2.0 | v4.34.0-rc1; v4.34.0-rc2 | later layers [P] |
| AxiomMath/Stacks, AxiomMath/CFSG | Stacks Project and CFSG, model-written | Apache-2.0 | v4.35.0 | read [P] |
| math-yiluo/Langlands-lib | 28,764 files, mostly `Prop`-valued `...Statement` definitions, most marked "Unproved"; errata in Borel-Tits, Milne, Springer | none on GitHub | v4.34.0 | read only, a map of names [P]/[R] |
| riemann-lean (local copy) | 17.4M lines; global CFT with existence (`reciprocityMap`, `ker_reciprocityMap`), Lubin-Tate, Tate's thesis (`completedLFunction_eq_rootNumber_mul`), Weil groups, adelic $GL_n$ with Whittaker models, 410K lines of reductive groups | none, copyright with the author | v4.33.1 | read and cite only; not built [P] |
| drjanosch42/Langlandscape-Mathathon | Jacquet-Langlands, event output | NOASSERTION (CC-BY-4.0 header) | none | read [P] |

## 1.12 AI systems

- AI systems wrote verified Lean at the scale of a million declarations in arithmetic geometry in 2026: anthropics FLT (September), the riemann-lean release (November), AxiomMath/Stacks and CFSG [P]/[S].
- CFT libraries were written by agents in a few months (NYLL with Codex; lana-agents) [P]/[R].
- Systems with public Lean output: Gauss (Math Inc, strong PNT, sphere packing), Aristotle (Harmonic), AxiomProver (AxiomMath), Anthropic agents, OpenAI Codex, DeepSeek-Prover-V2, Seed-Prover, Kimina-Prover, Goedel-Prover-V2 [P]/[S]. AlphaProof and AlphaEvolve were not rechecked [U].
- openai/math: about 730 manuscripts in 375 families, about 42% of top-line results with Lean; families 014 and 069 touch geometric Langlands (1.2) [P].
- Critiques: arXiv:2603.03684 on "drive-by proving" [S]; arXiv:2610.16323 on Aristotle-style claims [S]. Johan de Jong asked on 2026-10-21 that AI-generated PRs not be sent to the Stacks Project [S].
- A reviewer of Mathlib PR #42312 asked for disclosure of AI use [P]. The project discloses its use of models on every page (14.4).

## 1.13 Books and teaching

- The best modern textbook for the automorphic side is Getz-Hahn, "An Introduction to Automorphic Representations", GTM 300 (2024) [P].
- The classical spine: Diamond-Shurman (GTM 228) for modular forms, Bump (CSAM 55) for $GL(2)$, Bushnell-Henniart (Grundlehren 335) for the local Langlands of $GL(2)$, Milne's CFT notes [P].
- The new reference layer: "The Langlands Program", PSPUM 112.1 to 112.3 (AMS 2025), from the IHES 2022 summer school, with chapters by Taïbi, Kaletha-Taïbi, Caraiani-Shin, Fargues-Scholze, Emerton-Gee-Hellmann, Yun, Gan and Fintzen [P]/[S].
- No new general textbook on the Langlands program appeared in 2025 or 2026 [S]. No single text goes from Tate's thesis to modularity lifting to geometric Langlands with one notation. The handbook (document 11) fills this gap.
- Geometric Langlands has no textbook. The path is Frenkel's lectures, Gaitsgory-Rozenblyum, Raskin's Yale notes, Scholze's Bourbaki exposé and Ben-Zvi's 2026 survey [P].
- What students find hard (report F 5.1): the breadth of prerequisites; the step from modular forms to adelic representations; Weil-Deligne representations; L-groups; the analysis of the trace formula; stable conjugacy; Shimura varieties; R = T; higher categories; no common notation [S]/[U].

## 1.14 What this means for the project

1. **The statements are the first product.** No Lean statement of the local or global Langlands conjectures exists in Mathlib or formal-conjectures. The atlas of Langlands-lib has no licence and mostly unproved statements. A small set of faithful, pinned and fidelity-checked statements (06) is new and useful by itself (G1).
2. **$GL_1$ is within reach now.** NYLL, TauCeti, kbuzzard/ClassFieldTheory and riemann-lean all have CFT. Mathlib has adeles, Hecke characters and local fields. The Weil group and LLC for $GL_1$ and tori are the first proofs (G2, milestone S1).
3. **$GL_2$ has a Lean base.** Imperial FLT and anthropics FLT have Hecke operators, quaternionic forms, patching and an octahedral Langlands-Tunnell. The local Langlands of $GL_2$ (Bushnell-Henniart) has no Lean yet and is the second large target.
4. **The fresh claims are the research front.** Halleck-Dube, GLR, Cotner-Feng, Fintzen-Kaletha, AKMS and DEG are recent and unrefereed. Formal checks of their key lemmas (route R1) are the most direct way to a G4 result. Each claim stays a claim until it is checked (06.6).
5. **The deep layers wait for foundations.** The trace formula, Shimura varieties, the categorical forms and geometric Langlands need years of library. The project states them early and works on them through statements, shadows and small cases (routes R5, R7, R8, R9).
6. **The checking tools exist and are public.** comparator, nanoda, lean4export and `#print axioms` are the trust rows of 14. The project uses the Palomar layout and `formalization.yaml`.
7. **Verification of meaning is the bottleneck, not of proofs.** The riemann-lean release shows that a very large proof can be certified while human understanding is pending. The handbook (11) and the fidelity battery (06.3) address the gap between "checked" and "understood".
8. **Port, do not depend, and check licences.** The sources sit on pins from v4.31 to v4.37. The project pins v4.35.0 and ports Apache-2.0 files with attribution (05, 09). It reads but does not copy riemann-lean and Langlands-lib.

## 1.15 Items to recheck

These items are [S] or [U] in the reports, or the reports could not finish them because the shared search budget ran out. Each is a first task for the `reader` role (10).

1. Journal status of GLC I to V; the contents of ICM 2026 proceedings Vol. 2 (the SIAM page returned 403) [S] (A 8).
2. Which manuscripts of openai/math family 014 were retracted [S] (A 6).
3. The arXiv identifier of Hemo-Zhu and the authors of the quantum FLE paper [GH25] [S]/[U] (A 8).
4. Summer schools and workshops on Langlands in 2025 and 2026 [U] (A 8, F 9).
5. The classical references tagged [U] in B 2.1 and C 3: Kutzko 1980, Gelbart-Knapp, Aubert-Baum-Plymen-Solleveld, Langlands-Tunnell, Wiles, BCDT, Khare-Wintenberger, Kisin, Arthur-Clozel, Kim-Shahidi, Kim, the volumes of Moeglin-Waldspurger.
6. The Selberg eigenvalue bound $975/4096$ [U] (C 5).
7. Sato-Tate for genus 2 curves in general [U] (C 3.5).
8. The authors of arXiv:2607.03830, 2607.25383 and 2611.06742 as listed in C 4.1 (B lists Takanashi for 2611.06742) [S].
9. The Lean names in anthropics FLT `PROOF-PATH.md` were not opened [U] (E 2.4).
10. The scope of the Mathlib PRs #44964, #45067 and #27437 (titles only) [U] (E 1.4).
11. The absence list of 1.10 is a name search; a helper elsewhere in Mathlib cannot be ruled out [U] (E 1.3).
12. DeepMind and OpenAI formal results of late 2026 [U] (E 5.1).
13. The URL of the riemann-hypothesis repository under leanprover-community [S] (C 4.4).
14. The licence of leanprover/verso-blueprint (none on GitHub) before any use [P] (E 6.2).
15. The publication data and contents of PSPUM 112.1 to 112.3, the Notices issue of Ben-Zvi's article, and the MathOverflow threads on learning the Langlands program (F 9).
16. Fresh claims of 1.2: check for v2, errata, or expert comments every month.
