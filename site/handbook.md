---
title: The handbook
description: The Langlands Handbook, a textbook of the Langlands program in fourteen volumes, from number fields to geometric Langlands.
lead: The handbook teaches the Langlands program as a set of textbooks, in PDF and EPUB volumes. Each result on the map links to its section. All volumes are drafts, and none is released yet.
---
The handbook is in [tamnd/langlands-handbook](https://github.com/tamnd/langlands-handbook). It is for students who know algebra and analysis at the level of a first graduate year, and for mathematicians who do not read Lean. Each chapter defines its objects, states its results in standard notation and proves them. It ends with exercises and notes. Each chapter names a standard textbook to read with it.

The handbook covers far more than the project formalizes. Most of Volumes 10 to 13 will have no Lean proof for years. There the text gives the published proof or its plan, and each `Node:` line gives the Lean status of the result as it is.

## The volumes

| Volume | Title | Level | Tiers | State |
|---|---|---|---|---|
| 0 | Guide: how to read, the program in one chapter, notation and normalizations, the map, the status | all | all | draft |
| 1 | Number fields, local fields and adeles | background | T1 | draft |
| 2 | Lie groups, algebraic groups and their representations: root data, reductive groups, the dual group | background | T2 | draft |
| 3 | Class field theory and $\mathrm{GL}_1$: Weil groups, Lubin-Tate, Tate's thesis, Hecke and Artin L-functions | core | T3 | draft |
| 4 | Modular forms and elliptic curves | core | T4 | draft |
| 5 | Automorphic representations of $\mathrm{GL}_2$ | core | T4 | draft |
| 6 | Representations of $p$-adic groups and the local Langlands correspondence | core | T5 | draft |
| 7 | L-functions, converse theorems and functoriality for $\mathrm{GL}_n$ | core | T6 | draft |
| 8 | The trace formula | advanced | T7 | draft |
| 9 | Endoscopy and Arthur's classification | advanced | T7 | draft |
| 10 | Shimura varieties and automorphic Galois representations | advanced | T8 | draft |
| 11 | Galois deformations and modularity | advanced | T8 | draft |
| 12 | $p$-adic Hodge theory, $p$-adic Langlands and the geometrization of local Langlands | research | T9 | draft |
| 13 | Function fields and geometric Langlands; the program in 2026 and its open problems | research | T10, routes | draft |

No volume has a release yet, so the page has no files to download.

## The order of writing

The volumes follow the order of the milestones. Volumes 0, 1 and 3 come first (S1, S2). Volumes 2, 4 and 5 come next (S3, S4). Volume 6 follows (S5). The research part of Volume 13 comes out at each milestone as a research report.

## The state of a section

A section is drafted when the writer has written it. It is checked when a second model pass and the script checks find no problem. It is reviewed when a person with the right background has read it and signed it. Only reviewed chapters go into a numbered release. A volume gets a release when all its chapters are reviewed. Until then, the drafts are in the development builds, with a banner.

The handbook does not prove an open conjecture. The volumes state the open conjectures, and the map gives them the status open.
