# 00. Index of the research notes

## What this note is for

This note is the entry point to the research notes for the Langlands project. The project goal is to state the Langlands program in Lean, prove its known parts, attack chosen open cases, and write a handbook for human students (document 02). This note gives the tags, a summary of each source report, the main findings, a map of the files and the notes still to write.

## Status line

As of 2026-11-25, the six source reports A to F exist in `sources/`. Six research agents wrote them on 2026-11-24 and 2026-11-25. The agents shared one web search budget, and it ran out near the end of each report. So some items that a full check would confirm are tagged [S] or [U], and each report ends with a list of items to recheck. Document 01, section 1.15, collects these lists for the `reader` role (document 10). The numbered research notes 01 to 05 below are planned and not yet written. No note proves a new result.

## Tags

- [P]: the report read the primary source (arXiv abstract page or PDF, journal page, author page, official schedule, repository through `gh` or a local copy).
- [S]: the fact comes from a secondary source (a search snippet, a citation, a news item, a catalogue).
- [U]: the fact is unverified, often from memory. Treat it as a lead.
- [R]: a claim that a repository makes about itself (README, notes), not checked.
- [P via report X]: the spec cites a fact that report X read in the primary source.

## The source reports

| Report | Title | Size | Scope |
|---|---|---|---|
| [A](sources/A-geometric-langlands.md) | Geometric Langlands, November 2026 | 666 lines, 47 KB | GLC I to V, follow-ups, the 18 open problems, expositions, Lean prerequisites, openai/math |
| [B](sources/B-local-langlands.md) | The local Langlands correspondence, November 2026 | 595 lines, 55 KB | statements, known cases, Fargues-Scholze compatibility, supercuspidals, 2025 to 2026 list, 17 open problems, Lean ingredients for $GL_1$ and $GL_2$ |
| [C](sources/C-global-langlands.md) | Global Langlands: reciprocity and functoriality | 617 lines, 60 KB | statements, function fields, number fields, modularity, automorphy lifting, functoriality, trace formula and endoscopy, 20 open problems, the dependency picture |
| [D](sources/D-p-adic-arithmetic.md) | p-adic, mod p and arithmetic-geometric Langlands | 714 lines, 65 KB | $p$-adic LLC for $GL_2(\mathbb{Q}_p)$, mod $p$, the categorical $p$-adic program, Fargues-Scholze, analytic stacks, Shimura varieties, patching, 13 open problems, TauCeti |
| [E](sources/E-lean-ai-infrastructure.md) | Lean, Mathlib and AI systems for the Langlands program | 674 lines, 50 KB | Mathlib inventory and gaps, open PRs, FLT projects, CFT projects, Langlands-lib, riemann-lean, formal-conjectures, AI systems, trust tools, pins, per-layer assessment, first milestones |
| [F](sources/F-books-courses-curriculum.md) | Books, courses and a curriculum for the handbook | 601 lines, 71 KB | books, schools, courses, surveys, what students find hard, the sister handbook format, a 14-volume curriculum (Volumes 0 to 13) |

### A. Geometric Langlands

GLC in char 0, global and unramified, for every reductive $G$, is proved in GLC I to V (arXiv:2405.03599, 2405.03648, 2409.07051, 2409.08670, 2409.09856; 947 pages; no journal reference yet) [P]. The report states the theorem exactly (GLC I, Conjecture 1.6.7) and outlines the construction of the functor and the structure of the proof. It covers the follow-ups: Gaitsgory-Raskin in char $p$ (2508.02237), the GLR filtration (2603.26925), Betti, quantum, Dolbeault (Toda 2602.09359), ramified (Nam 2608.04207), local, and relative duality (BZSV 2409.04677; Chen-Wang 2610.36377). Its table of 18 open problems includes the six that GLC V names as unsolved. It lists the 2026 expositions (Scholze's Bourbaki exposé 1252, Ben-Zvi 2605.23167, Raskin's Yale notes) and records that no Lean exists for any part, because Mathlib lacks D-modules, IndCoh, derived algebraic geometry and $\mathrm{Bun}_G$. It records the unrefereed AI claims of openai/math families 014 and 069.

### B. Local Langlands

The LLC for general $G$ is still a conjecture (Taïbi 2510.00632) [P]. The report gives the statements (Borel's desiderata, refined LLC, enhanced parameters, character identities, the formal degree conjecture, local GGP) and a table of about 40 known cases. It follows the compatibility of Fargues-Scholze with classical constructions up to Cotner-Feng (2609.16381, 2609.16387), the supercuspidal constructions up to Fintzen-Kaletha (2611.31396, 23 Nov 2026), and the classification work up to AKMS (2611.31683). It dates about 40 preprints of 2025 and 2026, lists 17 open problems, gives a 19-item Lean ingredient list for LLC for $GL_1$ and $GL_2$, and proposes a five-part layering for the handbook. It notes the TauCeti roadmap PR #2458 for $G_2$.

### C. Global Langlands

The report states reciprocity, functoriality, Arthur's conjectures, Ramanujan, Artin, Hasse-Weil, Sato-Tate and Beyond Endoscopy. It gives a function field timeline from Drinfeld to the GLR announcement of Arthur-Ramanujan. For number fields it covers CFT, modularity of elliptic curves over many fields (Caraiani-Newton 2301.10509 v4 accepted), abelian surfaces (BCGP 2502.20645), Galois representations, automorphy lifting, Ramanujan over CM fields, the known cases of functoriality and the endoscopic classification. Its main fresh finding is Halleck-Dube (2611.26750), which claims the twisted weighted fundamental lemma and so, with AGIKMS, an unconditional endoscopic classification. It records the Alpöge RH release and its certification. It ends with 20 open problems rated 1 to 5, a dependency graph and a table of priorities for formalization.

### D. $p$-adic, mod $p$ and arithmetic geometry

The report covers the $p$-adic LLC for $GL_2(\mathbb{Q}_p)$ (Colmez, Paškūnas, CDP, Emerton), mod $p$ Langlands (BHHMS, Hu-Wang, Serre weights, Breuil-Mézard), the categorical $p$-adic program (EGH notes v5, JNWE, DEG 2603.26887, Dowd 2610.25055), Fargues-Scholze and the $\ell$-adic categorical progress of 2026, real local Langlands and analytic stacks, Shimura varieties (Caraiani-Scholze, Igusa stacks of DvHKZ, torsion vanishing of Yang-Zhu, CHZ), and patching. Its Lean section records the TauCeti adic spaces and adic Fargues-Fontaine curve (completed 2026-10-28) and the open roadmaps `PadicLocalLanglandsForGL2Qp` and `LanglandsParameterStacks`, and the open Mathlib PRs on Huber rings (#42312) and perfectoid fields (#26389).

### E. Lean, Mathlib and AI systems

The report is the inventory for documents 05, 06 and 09. It lists what Mathlib master b5aed57ecb has (adeles, local fields, Hecke characters and L-functions, the abstract Hecke ring, about 40 files of modular forms, root data, Lie algebras, cohomology, condensed and derived categories) and what it lacks (Weil group, L-group, reductive group schemes, smooth representations, Tate's thesis, CFT, Lubin-Tate, Hecke operators on forms, Galois representations, Shimura varieties, $\mathrm{Bun}_G$), with the open PRs. It reads Imperial FLT and anthropics FLT, the CFT projects (NYLL, lana-agents, kbuzzard), Langlands-lib, riemann-lean and formal-conjectures, with licences and pins. It lists AI systems, trust tools, blueprint tools and the pin landscape. It recommends the pin v4.35.0 and five first milestones, starting with the Weil group and the LLC for $GL_1$ as a comparator Challenge.

### F. Books, courses and curriculum

The report lists the books (Getz-Hahn GTM 300 as the spine of the automorphic side, Diamond-Shurman, Bump, Bushnell-Henniart, Milne), the schools (Arizona Winter School, IHES 2022 and PSPUM 112), courses and personal notes, and the main surveys. It records what students find hard and what experts recommend. It studies the format of the sister handbooks and proposes changes: Examples, Exercises, and Notes and history sections; the front matter keys `level` and `reads_with`; the node prefix LG; the builder `lhb`. It proposes a curriculum of 14 volumes (Volumes 0 to 13, about 5,800 pages) with prerequisites, theorems, sources and a style for each, and a dependency chart. It finds no new general Langlands textbook in 2025 or 2026.

## Main findings

1. GLC in char 0 (global, unramified) is a theorem (A). The LLC for general $G$, reciprocity for $GL_n$ over number fields, functoriality in general and Ramanujan for Maass forms are open (B, C).
2. Many 2026 results are fresh and unrefereed: Halleck-Dube, GLR, Cotner-Feng, Fintzen-Kaletha, AKMS, DEG, Dowd, Dieulefait, Takanashi (01, 1.2). They are claims, not hypotheses.
3. On 2026-11-20 a Lean proof of RH appeared, found with Claude, and the Lean FRO certified it on 2026-11-21 (C 4.4). Its method passes through theta lifts, periods and a relative trace formula. Its library holds CFT, Tate's thesis and adelic $GL_n$, but it has no licence (E 3.5).
4. Mathlib has the base layer of an adelic $GL_1$ and $GL_2$ programme and stops short of every object that names Langlands (E 1.5).
5. Licensed Lean sources for the first layers exist: NYLL and kbuzzard for CFT, Imperial FLT and anthropics FLT for $GL_2$ and patching, TauCeti for adeles, ramification and adic spaces, epsilon_FML and epsilon_SML for epsilon factors (E 3).
6. No Lean statement of any Langlands conjecture exists in Mathlib or formal-conjectures (E 4). A faithful set of statements is a new product.
7. No new general textbook on the Langlands program appeared in 2025 or 2026 (F 1). The handbook fills a real gap.

## File map

| File | Title | Content | Status |
|---|---|---|---|
| `sources/A` to `sources/F` | the six source reports | see above | written 2026-11-24 to 2026-11-25 |
| 01-gl1-cft-plan | the $GL_1$ plan | the Weil group, LLC for $GL_1$ and tori, local and global CFT, Tate's thesis: the files to port from NYLL and TauCeti, the statements, the nodes, the order | planned, for S0 and S1 |
| 02-llc-gl2-plan | the LLC for $GL_2$ | smooth representations, types, Bushnell-Henniart chapter by chapter, the 19 ingredients of B 5.4, the comparison with Mathlib PRs #41520 and #41525 | planned, for S2 |
| 03-fresh-claims-audit | the audit of fresh claims | for each claim of 01 (1.2): the key lemmas, what Lean needs, a cost estimate, a contact with the authors; the input to route R1 | planned, for S0 |
| 04-statements-draft | the statements | the Lean drafts of 06.2, the definitions they need, the fidelity notes, the bridges to formal-conjectures, NYLL and anthropics FLT | planned, for S0 |
| 05-handbook-curriculum | the curriculum | Volumes 0 to 13 of report F 7 fixed as chapters, with the notation table and the mapping from chapters to nodes | planned, for S0 and S1 |
| 06-dependency-graph | the dependency graph | the arrows of C 6 and the tiers of 07 as a graph of nodes, the input to `lgl index` | planned, for S1 |
| 07-riemann-lean-reading | what riemann-lean uses | a reading of the Langlands content of riemann-lean (CFT, Tate's thesis, theta lifts, periods), for citation only, and a letter to the author about a licence | planned, for S1 |

## Notes and references

- The spec documents 00 to 16 are in the parent directory. Document 01 is the synthesis of A to F.
- Each report has its own list of sources with URLs at its end.
- The numbered notes follow the convention of spec 2161: one note per topic, tags on every claim, and a "proved here" mark only for complete proofs.
