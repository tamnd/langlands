# 11. tamnd/langlands-handbook: The Langlands Handbook

The handbook is the Langlands program written as a set of textbooks.
- **Voice.** It is written in the voice and to the standard of an expert. Each chapter defines its objects, states its results in standard notation with numbers and proves them as a mathematician proves them. It ends with exercises and notes.
- **Readers.** Its readers are students who know algebra and analysis at the level of a first graduate year, and working mathematicians who do not read Lean.
- **Formats.** It comes as PDF and EPUB volumes. The site has the same text in HTML.

It differs from the sister handbooks in two ways:
- **It is a textbook first.**
  - The riemann handbook explains one finished Lean proof. The singularity handbook explains one problem and its theory.
  - This handbook teaches a whole field to students. So each chapter has examples and exercises, and it has a parallel reading in a standard textbook (`reads_with`).
- **It covers far more than the project formalizes.**
  - Most of Volumes 10 to 13 will have no Lean proof for years.
  - The text then gives the published proof or its architecture, and the `Node:` lines say honestly that the Lean status is `stated` or `unstated`.

The curriculum is the result of research report F (research/sources/F-books-courses-curriculum.md, sections 6 and 7).

## 11.1 The volumes

| | Volume | Level | Pages (estimate) | Best textbook to follow | Tiers |
|---|---|---|---|---|---|
| 0 | Guide: how to read, the program in one chapter, notation and normalizations, the map, the status | all | 120 | Gelbart 1984; Arthur 2003; Calegari 2021 | all |
| 1 | Number fields, local fields and adeles | background | 350 | Neukirch; Serre, *Local Fields* | T1 |
| 2 | Lie groups, algebraic groups and their representations: root data, reductive groups, the dual group | background | 450 | Milne 2017; Springer; Knapp | T2 |
| 3 | Class field theory and GL(1): Weil groups, Lubin-Tate, Tate's thesis, Hecke and Artin L-functions | core | 350 | Milne, CFT notes; Cassels-Fröhlich | T3 |
| 4 | Modular forms and elliptic curves | core | 400 | Diamond-Shurman; Shimura | T4 |
| 5 | Automorphic representations of GL(2) | core | 450 | Bump; Gelbart 1975; Getz-Hahn | T4 |
| 6 | Representations of $p$-adic groups and the local Langlands correspondence | core | 500 | Bernstein's notes; Bushnell-Henniart; Kaletha-Taïbi | T5 |
| 7 | L-functions, converse theorems and functoriality for GL(n) | core | 400 | Goldfeld-Hundley II; Getz-Hahn; Cogdell's notes [U] | T6 |
| 8 | The trace formula | advanced | 450 | Getz-Hahn Part III; Arthur (Clay 2005); Gelbart 1996 | T7 |
| 9 | Endoscopy and Arthur's classification | advanced | 400 | Kaletha's $SL_2$ lectures; Arthur 2013 | T7 |
| 10 | Shimura varieties and automorphic Galois representations | advanced | 500 | Milne (Clay 2005); Harris-Taylor; Caraiani-Shin | T8 |
| 11 | Galois deformations and modularity | advanced | 500 | Darmon-Diamond-Taylor; Cornell-Silverman-Stevens; Gee 2022 | T8 |
| 12 | $p$-adic Hodge theory, $p$-adic Langlands and the geometrization of local Langlands | research | 500 | Scholze-Weinstein; Emerton-Gee-Hellmann; Fargues-Scholze | T9 |
| 13 | Function fields and geometric Langlands; the program in 2026 and its open problems | research | 500 | Frenkel 2007; Yun's IHES lectures; Gaitsgory-Rozenblyum; GLC I to V | T10, routes |

The total is about 5,800 pages. This is the size of a long series, not of one book. The volumes are written in the order of the milestones:
- 0, 1 and 3 first (S1, S2);
- then 2, 4 and 5 (S3, S4);
- then 6 (S5).

The research part of Volume 13 is released at each milestone, as a research report, like Volume 9 of the singularity handbook. Each other volume has a release when all its chapters are at status `reviewed` (11.3).

Dependencies between volumes (from F, 7.1):

| Volume | Needs |
|---|---|
| 3 | 1, 2 (compact groups only) |
| 4 | 1 |
| 5 | 2, 3, 4 |
| 6 | 2, 3 |
| 7 | 5, 6 |
| 8 | 5, 6 (7 helps) |
| 9 | 6, 8 |
| 10 | 4, 5, 6, 8 |
| 11 | 4, 5, 10 (12 Part I for $p$-adic Hodge theory) |
| 12 | 6, 11 for Part II; 1, 2 and rigid geometry for Part I |
| 13 | 2, 3, 6; 12 Part III for the Fargues-Scholze bridge |

No new general textbook on the Langlands program appeared in 2025 or 2026 [S]. The best recent text is Getz-Hahn (GTM 300, 2024). This is a gap that the handbook can fill, in particular for Volumes 6 to 9, where the literature is mostly papers and lecture notes.

## 11.2 A chapter

The folder layout, the front matter, the numbering, the `Node:` lines and the status rules are those of the singularity handbook. So `lhb` can start as a copy of `shb`.

A chapter is a folder `content/<NN-volume>/<NN-chapter>/` with an `intro.md` and one file per section. The last two sections of every chapter are `Exercises` and `Notes and history`. Most chapters also have an `Examples` section. A section opens with front matter:

```markdown
---
title: Tate's local functional equation
nodes: [LG0000012A]
sources: [tate1950thesis, getzhahn2024]
reads_with: [getzhahn2024:ch5, cassels-frohlich:ch15]
level: core            # background | core | advanced | research
status: drafted        # drafted | checked | reviewed
drafted_by: writer@claude-opus-5-5
reviewed_by: []
---
## Tate's local functional equation

<One paragraph: what this section proves, why the program needs it, and the example to keep in mind.>

**Theorem (Tate).** Let $K$ be a nonarchimedean local field, $\chi$ a quasi-character of $K^\times$ ...

Node: LG0000012A · Lean: `Langlands.ClassField.tate_local_functional_equation` (status: stated)

*Proof.* ... $\square$

**Example.** For $K = \mathbb{Q}_p$ and $\chi$ unramified ...
```

Rules:
- Each theorem on the map has a `Node:` line with its tag and its Lean name. The builder writes the current status from `records/status.json` of `tamnd/langlands` at build time.
- A statement that has no Lean proof says so in that line. The text never claims more than the status.
- A classical result that is not on the map may have no `Node:` line. The check gives a warning, not an error.
- Volume 0 has a table of notations and normalizations. Examples are the geometric Frobenius, the unitary or arithmetic Satake parameters, and the choice of additive character. Every later volume follows that table and cites it at the first use.

Style by band (from F, 7.3):

| Band | Volumes | Style |
|---|---|---|
| Background | 1, 2 | complete proofs; many small examples; standard exercises; short history notes; follow the best textbook closely and say so |
| Core | 3 to 7 | complete proofs of the GL(1) and GL(2) theory; explicit computations; each chapter opens with a motivating example and ends with exercises and notes; the target is the standard of Bump or Diamond-Shurman |
| Advanced | 8 to 11 | full proofs for the smallest cases ($GL_2$, $SL_2$, $U(1)$); precise statements with references for the general case; reader's guides to the long sources (Arthur 2013, Harris-Taylor) |
| Research | 12, 13 | statements, the architecture of the proofs, the key examples worked out and a status table; proofs only where they are short or where the Lean map covers them |

## 11.3 Who writes and who checks

The `writer` role drafts from the papers, the map and the Lean code.
- **`checked`.** A draft becomes `checked` when a second model pass and the script checks find no problem. The checks are these:
  - every cited result exists in the source at the given place;
  - every `Node:` line resolves;
  - the numbers are consistent;
  - each exercise has a solution in the private solutions file;
  - the style rules hold.
- **`reviewed`.** A section becomes `reviewed` when a person with the right background has read it and signed it in `reviewed_by`.

Only `reviewed` chapters go into a numbered release. Drafts are in the `-dev` builds and on the site with a banner.

The core volumes (3 to 7) are the heart of the handbook and its main use for students. The project looks for reviewers for them first. Graduate students who have taken a course from the parallel textbook are good reviewers, with an expert who signs the volume (Q-19).

Some proofs in the literature are long and, in places, hard to follow. Examples are Harris-Taylor, Arthur 2013 and Cossart-Piltant in the sister project. The handbook may give a different proof than the paper when the Lean proof does. It then says so and gives both references.

Solutions to exercises are in a separate file, `solutions/<NN-volume>.md`. It is released to teachers on request, so that the exercises stay useful for courses.

## 11.4 The builder

`lhb` is the builder. It is written in Python, as `shb` of the singularity handbook and `rhb` of the riemann handbook. It does these steps:
1. It reads the Markdown.
2. It numbers the statements (`lhb number --write`).
3. It checks the links, the `Node:` lines and the `reads_with` keys.
4. It writes LaTeX with `tex/handbook.sty` and runs LuaLaTeX.
5. It writes the EPUB.

It starts as a copy of `shb`, with the singularity-specific parts removed and these additions:
- the `level` and `reads_with` keys;
- the exercise and solution split;
- a per-volume index of the Lean names.

The output goes to `build/langlands-handbook-<NN-volume>-<version>.{pdf,epub}`. Each release is a GitHub release. `EDITION` records the commits of `tamnd/langlands` and `tamnd/langlands-lean` that the edition describes.
