---
title: The routes
description: The nine research routes of langlands on the open parts of the Langlands program, with their weights, ideas and key obstructions.
lead: A route is a group of open targets that use the same definitions, the same tiers of the library and the same kind of proof. Each route has an idea, the known results, a key obstruction and its first nodes.
---
## How to read the routes

Nobody can prove all of the open Langlands program on a schedule. Most open targets of the routes have a difficulty of 4 or 5 on a scale from 1 to 5. A difficulty of 5 means that experts have no plausible strategy. The project does not promise a date for any open target.

The weights set the share of the research budget of the agent for the first year. The work on the library for the levels G1 to G3 is outside this budget. The weights are higher where a route has a cheap first node that also serves G2 or G3 (R2, R3), or where the check is cheap and the information value is high (R1).

The weights change only at a milestone report, from the nodes that are proved, refuted or stalled. A route with no progress for two milestones loses half its weight to the route with the best cost per proved node. The milestone report says so in plain words. The project reports a negative result with the same care as a positive one.

## The computation lab

The lab is a method, not a route. It serves all routes and has a weight of 0.05. It takes examples from LMFDB and checks them with Sage, PARI/GP and Magma. It tests the Lean statements on certified examples. A computation enters the map only as a certificate that Lean checks. Data from the lab is not a proof. The [lab page](/lab/) lists the runs.

## A candidate first target

Spec 04 of the project names a candidate first research target, Target T. It is the guess of the project, and no expert has read it yet. Target T has three steps. First, prove the local correspondence for $\mathrm{GL}_2$ over a $p$-adic field with odd $p$ in Lean, after Bushnell-Henniart. Second, state the construction of supercuspidal types of Fintzen-Kaletha (arXiv:2611.31396) and prove its finite group core in Lean. Third, prove in Lean that for $\mathrm{GL}_2$ and $\mathrm{SL}_2$ this construction gives the same parameters as the tame correspondence of Bushnell-Henniart. The milestone report of S5 decides whether Target T stays.

## The routes
