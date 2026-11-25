---
title: The papers
description: The corpus of papers and books on the Langlands program that langlands reads, states, ports or proves, sorted by tier.
lead: Each paper record says why a node of the map needs the paper, what exists in Lean, and how the project uses it.
---
## The corpus

The corpus is the set of papers and books on a path from Mathlib to a top theorem of the project or to a node of a route. It is not all of number theory. A paper enters the corpus when a node needs it, and the record says which node asked for it. The first list in spec 07 of the project has 204 rows in eleven tiers, T0 to T10, and a watch list of fresh claims. Each record is a YAML file in `papers/` of [tamnd/langlands](https://github.com/tamnd/langlands), and the record pins the version that the project read.

The tiers go from the references (T0) and the local fields and adeles (T1) to the function fields and geometric Langlands (T10). The [map](/map/) lists the tiers.

## The fields of a record

The tag says how well the project knows the bibliographic facts of the record. It does not say whether the theorem is true. P marks a primary source that the project read. S marks a secondary source. U marks a fact that is not verified yet.

The use is the plan of the project for the paper:

| Use | Meaning |
|---|---|
| reuse | use the result of Mathlib as it is |
| prove | a full formal proof |
| port | a proof ported from a Lean source with a licence that permits it, then checked |
| state | a Lean statement, used as a named hypothesis of `proved-mod` nodes until it is proved |
| ex | certified examples from the computation lab |
| read | a source of ideas, definitions and text for the handbook, with no theorem on the map |

## Sources without a licence

riemann-lean and math-yiluo/Langlands-lib have no licence. The project reads them and cites them. It does not copy them.

## Fresh claims

A fresh claim of 2026 that experts have not accepted yet goes to the watch list with a claim record, not to the corpus. It is never a hypothesis of another node. It enters the corpus only after experts accept its paper.
