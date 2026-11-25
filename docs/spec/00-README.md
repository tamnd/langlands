# Spec 2161l: Langlands

The Langlands program in Lean, in public: the statements, the known theory, the open parts as research bets, and a handbook for students.

Written 2026-11-25. This is a research and design spec. It follows spec 2161 (singularity) in its form and its tools. The research behind it is in `research/sources/` (reports A to F, about 350 KB, index in `research/00-index.md`).

## The project in one paragraph

Four repositories:
- `tamnd/langlands`: the map of nodes, the paper and claim records, the lab specs, the trust records and the site sources;
- `tamnd/langlands-lean`: the Lean package `Langlands`;
- `tamnd/langlands-agent`: `lgl`, the toolchain and the model roles;
- `tamnd/langlands-handbook`: a textbook series for students and mathematicians, as PDF and EPUB.

Together they work toward six levels of success (02.3):
- G1: state the program in Lean (44 statements, 06.2);
- G2: prove the abelian case and LLC for $GL_2$;
- G3: formalize the known theory of tiers T1 to T8 (204 sources, 07) and write the handbook (Volumes 0 to 13);
- G4: check fresh claims and find new partial results;
- G5 and G6: the open conjectures themselves.

Everything is published at https://langlands.tamnd.com. The request was to prove all of the open Langlands program. No one can promise that. Functoriality, the general local correspondence and reciprocity over number fields have been open for fifty years. The spec reads the request as three commitments: state all of it, prove what is known in an order that leads to the open parts, and work on the open parts in public with honest status (02.4).

## What changed in 2026

1. **Non-abelian reciprocity is in Lean.**
   - Imperial FLT and `anthropics/fermats-last-theorem` (September 2026) hold quaternionic automorphic forms, Hecke operators, patching, R = T and Wiles' modularity theorem.
   - Both are Apache-2.0. The project ports from them and does not reprove them (05.2).
2. **Class field theory is almost there.**
   - NYLL (Apache-2.0) proves finite abelian local reciprocity.
   - riemann-lean (2026-11-20) contains global CFT with existence, Lubin-Tate theory and Tate's thesis, but it has no licence. The project reads it, cross-checks against it and asks its author for a licence (05.3, Q-07).
3. **The geometric conjecture is a theorem, and the local theory has a centre.**
   - GLC I to V (Gaitsgory, Raskin and coauthors, 947 pages) prove the unramified geometric conjecture in characteristic 0.
   - Fargues-Scholze parameters are now known to match the classical ones in many cases (Cotner-Feng, September 2026).
   - The statements of the field are stable enough to pin (01.3, 01.4).
4. **AI-written mathematics reached this field.**
   - TauCeti (Apache-2.0, Lean FRO) built adic spaces and the Fargues-Fontaine curve, and it has roadmaps for $p$-adic LLC and LLC for $G_2$.
   - Alpöge's Lean proof of the Riemann Hypothesis (found with Claude, certified by the Lean FRO on 2026-11-21) uses theta lifts and a relative trace formula.
   - openai/math holds unrefereed AI-generated claims on geometric Langlands (01.2, 01.12).
5. **Fresh claims arrive faster than people can check them.** Examples are the twisted weighted fundamental lemma (Halleck-Dube, 2611.26750), Arthur-Ramanujan over function fields (GLR, 2603.26925) and new supercuspidal constructions (Fintzen-Kaletha, 2611.31396). Route R1 checks such claims in Lean. This is the most likely first research result (04.2, 04.12).

## The documents

| Doc | Title | Read it for |
|---|---|---|
| [01](01-research-2026.md) | The state of the field, November 2026 | the sourced literature: what is proved and open, fresh claims, each area, ICM 2026, Lean, AI systems, books |
| [02](02-the-goal.md) | The goal | the levels of success G1 to G6, the meaning of "all", non-goals, what would show the plan is wrong |
| [03](03-the-program.md) | The Langlands program, mathematically | the statements: L-groups, LLC, reciprocity, functoriality, Arthur, function fields, geometric, $p$-adic; the dependency picture |
| [04](04-routes.md) | The open targets and the routes | routes R1 to R9, their open targets O-Rk-n, first nodes and weights; Target T |
| [05](05-the-base.md) | The base | Mathlib at the pin, the sources to port, the sources to read only, the porting rule, the first port, the cross-checks |
| [06](06-lean-statements.md) | The Lean statements and how to trust them | the vocabulary, the 44 statements, the fidelity battery F1 to F7, the bridges, the risks, the claim policy |
| [07](07-corpus.md) | The corpus | 204 rows of sources in tiers T0 to T10, the watch list, the paper record, the first ten |
| [08](08-architecture.md) | Architecture | the repositories, the map, the five flows |
| [09](09-langlands-lean.md) | `tamnd/langlands-lean` | layout, Lean rules, toolchain pin, CI, upstreaming |
| [10](10-langlands-agent.md) | `tamnd/langlands-agent` | `lgl`, the roles, the queue, budgets, evaluation |
| [11](11-langlands-handbook.md) | The handbook | Volumes 0 to 13, the chapter format with examples and exercises, `lhb` |
| [12](12-site.md) | The site | pages, doors (with `/teach/` and `/claims/`), rules, the Worker |
| [13](13-computation-lab.md) | The computation lab | tools, specs, experiments E1 to E9, certificates |
| [14](14-trust.md) | Trust | rows Q0 to Q9, the top theorems, threats, disclosure, registration |
| [15](15-milestones.md) | Milestones | S0 (2026-12-15) to S9, exit criteria, risks |
| [16](16-open-questions.md) | Open questions | Q-01 to Q-22, and the questions for experts |
| [research/](research/00-index.md) | The research reports | A geometric, B local, C global, D $p$-adic and arithmetic, E Lean and AI, F books and curriculum |

**Reading order.**
- Mathematicians: 03, 04, 01, 06, 07.
- Engineers: 02, 05, 08, 09, 10, 14, 15.
- Teachers and students: 11, 12, then 03.
- Everyone: 16.

## Decisions made in this spec

1. **Graded levels, not a promise.** The open conjectures are research bets with weights (02, 04). The project reports progress on each level separately.
2. **Statements first, characterized.** Every correspondence is stated with the properties that pin it down (L-factors, ε-factors, Frobenius traces), never as a bare bijection (06.2.3, 06.5).
3. **GL-type statements first (G1a), general groups later (G1b).** Mathlib has no reductive group schemes. The general statements wait for tier T2 and keep a `needs` list until then (06.2.2).
4. **The pin is Lean v4.35.0 with the Mathlib tag v4.35.0 (`56a005855e`),** followed by monthly bumps (09.3).
5. **Port, do not depend.** Single files from Apache-2.0 sources with provenance. riemann-lean, math-yiluo/Langlands-lib and verso-blueprint have no licence and are read only (05.3, 05.4).
6. **Hypotheses, not axioms.** A published theorem that is not yet proved is a named `Prop` with its own fidelity check (09.2).
7. **Fresh claims are never hypotheses.** They have status `claimed` until experts accept the paper. A check is published only after a letter to the authors and 30 days (14.4).
8. **No claim on an open case** is made until the policy of 06.6 is met: two kernels, the fidelity battery, and two outside experts.
9. **The handbook is a textbook.** It has examples, exercises, a parallel textbook for each section, and a `/teach/` door on the site (11, 12).
10. **Style.** Text follows ASD-STE100: short sentences, no "we", no em or en dashes.

## The first four weeks (milestone S0, 2026-12-15)

1. Create the four repositories, after the owner confirms. Copy the skeletons of singularity, singularity-lean, singularity-agent and singularity-handbook, with the names of 08.1.
2. Write `Langlands/Statements/Basic.lean` and `ClassField.lean` (06.1, 06.2.1), and run F1 to F3.
3. Port `finiteAbelianLocalReciprocity` from NYLL to the pin (05.5). Start `lgl port`.
4. Copy the site skeleton from singularity-agent. Deploy `/program/`, `/statements/`, `/map/` and `/trust/` to langlands.tamnd.com.
5. Send the letters:
   - to experts (Q-05);
   - to the author of riemann-lean about a licence (Q-07);
   - to the TauCeti maintainers (Q-20).

   Register in Palomar (Q-13).
6. Start the `reader` role on the [S] and [U] items of 01.15, and on the claim records of 01.2, beginning with Fintzen-Kaletha (Target T, 04.12).
