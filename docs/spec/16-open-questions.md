# 16. Open questions

These are the decisions that the spec does not make. Each one has the options, a recommendation, the milestone by which it must be decided, and who decides.
- "Owner" means the owner of the repositories.
- "Experts" means the outside reviewers of 06.3 (F6) and 14.1 (Q7).

| Id | Question | Options | Recommendation | By | Who |
|---|---|---|---|---|---|
| Q-01 | How to read "prove all of the open Langlands program"? | (a) a promise to prove the open conjectures; (b) the graded levels G1 to G6 of 02.3 | (b). The spec is written for (b). The open conjectures are research bets with weights, not a plan with a date (02.4, 04.13) | S0 | owner |
| Q-02 | Which toolchain pin at the start? | (a) v4.35.0, the pin of Imperial FLT, singularity-lean and AxiomMath; (b) v4.36.0, the pin of NYLL; (c) Mathlib master, as TauCeti | (a), then (b) at the first bump in S1 (09.3) | S0 | owner |
| Q-03 | Port or depend? | (a) Lake dependencies on the large projects; (b) ports of single files with provenance (05.4) | (b). The pins differ, the builds are large, and a port takes only what a node needs | S0 | owner |
| Q-04 | The definition of the Weil group | (a) a subgroup of the absolute Galois group with a finer topology (6.1); (b) an abstract extension of $\mathbb{Z}$ by inertia; (c) the definition of NYLL or of riemann-lean, if one exists | (a), with a proved equivalence to (b), and to (c) where it exists | S0 | owner, one expert |
| Q-05 | How to find expert reviewers? | letters to the groups of 01; a paid review; a workshop | letters first, at S0, with the statements and the trust page; a paid review of the statements (F6) if no one answers in two months; a small online workshop at S5 | S0 and S3 | owner |
| Q-06 | The weights of the routes | the first weights of 04.1 | keep them for the first year; change them only at milestone reports, from proved and refuted nodes (04.13) | S3, then each milestone | owner, with the planner's report |
| Q-07 | riemann-lean has no licence. Ask for one? | (a) write to the author and ask for Apache-2.0 for the CFT, Tate's thesis and adelic $GL_n$ parts; (b) read only, forever | (a) at S0. Until the author answers, (b). The cross-check package is built but not distributed (05.3, 05.6) | S0 | owner |
| Q-08 | How much of the theory of reductive groups to build? | (a) split groups from root data only; (b) quasi-split groups by Galois descent; (c) general reductive group schemes over a base | (a) at S3, (b) by S8; (c) only if Mathlib starts it, then join | S3 | owner, one expert |
| Q-09 | Share code with singularity-agent? | (a) a common Go module for `index`, `trust` and `site`; (b) a copy | (a) for the three shared packages, because the trust needs are the same; (b) for the roles, which differ | S0 | owner |
| Q-10 | Reuse `shb` for the handbook? | (a) fork `shb` as `lhb`; (b) a new builder | (a), with the additions of 11.4 | S0 | owner |
| Q-11 | How much to send upstream to Mathlib? | (a) the Weil group and local CFT only; (b) tiers T1 to T3; (c) nothing until the project is stable | (a) at S2, (b) from S4, coordinated with the open pull requests of 05.1; the authors listed; never block on review (09.5) | S2 | owner |
| Q-12 | Publication and the disclosure of AI | papers on the arXiv with the role and model credits; a statement of what people checked | follow 14.4; a research result (G4) is posted only after an outside expert has read it, with a section on how it was found and checked | S7 | owner, experts |
| Q-13 | Register with Palomar and publish `formalization.yaml`? | yes or no | yes, at S0, in the v0.4 schema (14.5) | S0 | owner |
| Q-14 | Which fresh claims to check first (route R1)? | the list of 01.2 | the finite cores first: Fintzen-Kaletha (Target T, 04.12), then a test case of Halleck-Dube by the lab (E4); never the openai/math families until a human reads them | S0 for the list, S5 for the first check | owner |
| Q-15 | Is Target T (04.12) right? | Target T; the second candidate of 04.12; a target that an expert proposes | Target T, until an expert of the local Langlands group reads 04.12 | S5 | owner, one expert |
| Q-16 | How to treat the FLT ports, which models wrote? | (a) trust the build and the bridges; (b) also a human review of the statements that the project uses | (b) for the top statements that the project uses (`Theorems/` of anthropics FLT); (a) for the rest, with Q0 to Q4 on the whole port | S4 | owner, one expert |
| Q-17 | Budget | 200 dollars a day for the agent at the start (10.6) | raise it only when the cost per proved node is measured (S2) | S2 | owner |
| Q-18 | The name of the toolchain | `lgl`; `lang`; `llc`; `ll` | `lgl`: short, no clash with a common command and no clash with a mathematical term (`llc` is one) [U] | S0 | owner |
| Q-19 | How to review the core volumes of the handbook? | (a) experts only; (b) graduate students for `reviewed` per section, with an expert who signs the volume; (c) a course that uses a draft volume | (b), and (c) when a teacher offers | S2 | owner |
| Q-20 | Coordinate with TauCeti on $p$-adic Langlands and $G_2$? | (a) port from TauCeti; (b) contribute to TauCeti and port back; (c) work alone | (b) for routes R2 ($G_2$) and R9: TauCeti has the roadmaps and the adic spaces; the project brings the classical side and the statements | S3 | owner |
| Q-21 | Geometric Langlands: state it at all in the first two years? | (a) no; (b) the shape with `needs` only (06.2.2); (c) the classical shadows (geometric CFT, the function field case) | (b) and (c); the full statement waits for derived algebraic geometry in Lean | S6 | owner, one expert |
| Q-22 | Send the project's statements to formal-conjectures? | (a) yes, the GL-type statements after F6; (b) no, keep them in the project only | (a): one public home for the open statements helps every project; the bridges of 06.4 keep both copies in agreement | S4 | owner |

## 16.1 Questions for the experts

These are mathematical questions that the project cannot decide alone. They go in the first letters (Q-05).

1. Are the statements of 06.2 the ones you would accept? In particular:
   - Henniart's characterization for `LocalLanglandsGL`;
   - "almost all places" in `ReciprocityGL`;
   - the q-expansion form of `ModularityEllipticQ`.
2. Which normalizations would you fix in the statements, so that they compose without sign errors? The candidates are the geometric Frobenius, the unitary Satake parameters and the additive character of conductor $\mathcal{O}_K$.
3. Which of the routes of 04 do you think has a chance of a new result in two years, and is the key obstruction stated correctly?
4. Is Target T of 04.12 a good first research target? Is the comparison of Fintzen-Kaletha with Bushnell-Kutzko for $GL_2$ and $SL_2$ already in the literature?
5. Which published results in your area have known gaps, or are not accepted? This sets `expert_status` in the paper records (07.13).
6. Which of the fresh claims of 01.2 would you like to see checked, and which part is self-contained enough to check first?
7. For the handbook: which textbook and which chapter order would you use to teach Volumes 5 to 7 in one year?
