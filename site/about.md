---
title: About
description: Who runs langlands, how the work is done, and how the project uses AI tools.
lead: The project is run by its owner, Tam Nguyen Duc. It uses AI tools for much of the work, and it says so.
---
## How the work is done

A person sets the goals and reviews the results. A program, `lgl`, checks the map and builds this site. AI tools write drafts of the Lean code, of the handbook and of the records. An agent proposes each change as a pull request, and a person merges it.

Lean checks the proofs, so a proof does not depend on who wrote it. A statement and a text do depend on who wrote them. A Lean statement can be wrong in a way that Lean does not see, and a text can misstate a result. So each statement and each text needs a human review before the project calls it checked.

## The repositories

| Repository | Content |
|---|---|
| [tamnd/langlands](https://github.com/tamnd/langlands) | the map, the paper records, the claim records, the trust records, the lab and the pages of this site |
| [tamnd/langlands-lean](https://github.com/tamnd/langlands-lean) | the Lean package `Langlands` |
| [tamnd/langlands-agent](https://github.com/tamnd/langlands-agent) | `lgl`, which checks the map, runs the agent roles and the lab, and builds the site |
| [tamnd/langlands-handbook](https://github.com/tamnd/langlands-handbook) | The Langlands Handbook, in PDF and EPUB volumes |

The project follows the shape of its sister projects, riemann and singularity. The three sites look like one family.

## Claims

The project does not claim a proof of an open conjecture. It is at milestone S0, and nothing is proved in Lean yet. It calls a node proved only when the Lean build has the proof with the standard axioms. For an open conjecture it also needs the checks of the [trust page](/trust/) and the reading of two outside experts.

## Contact

Use the issues of [tamnd/langlands](https://github.com/tamnd/langlands/issues). Experts who want to review a statement are very welcome.
