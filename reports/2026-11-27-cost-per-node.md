# The first measurement of the cost per proved node

This report gives the first measurement of the cost per proved node. It is an exit criterion of milestone S2 (spec 15, section S2), and it is the input for open question Q-17 on the agent budget (spec 16).

## Method

The measurement covers the work from 2026-11-25 to 2026-11-27. In this period, a coordinating session ran each task as a separate agent with a written brief. The agents ran in Claude Code and not through `lgl agent`, so the ledger `agent/ledger.jsonl` of spec 10.6 has no entries for them. For each agent, the harness reports three numbers when the agent stops: the tokens, the tool calls and the wall time. The file `reports/data/2026-11-27-agent-runs.csv` gives these numbers for each of the 116 agents, with the area of the task.

The unit of cost is the token count that the harness reports. This report does not give a cost in dollars, because the token count does not separate the input, output and cached tokens, and the price of each kind is different. The work of the coordinating session (the briefs, the review, the pull requests and the releases) is not in the numbers.

A proved node is a node of the map in `blueprint/nodes` that has a Lean proof. A proved declaration is an entry of `formalization.yaml` in langlands-lean with the status `proved`.

## Results

| Area | Agents | Tokens | Tool calls | Agent minutes |
| --- | --- | --- | --- | --- |
| Lean | 62 | 6244837 | 3973 | 2031 |
| Handbook | 38 | 4171123 | 2164 | 1585 |
| Tooling | 6 | 618743 | 445 | 132 |
| Research and site | 10 | 1092920 | 679 | 115 |
| Total | 116 | 12127623 | 7261 | 3861 |

On 2026-11-27, langlands-lean has 335 proved declarations, and 13 of the 46 nodes of the map have a Lean proof. The Lean agents used 6244837 tokens. This gives these two rates:

- about 480000 tokens for each proved node of the map;
- about 18600 tokens for each proved declaration.

The handbook agents used about 0.67 tokens for each token of the Lean agents.

## Limits

- The rate per node is high because most of the Lean work is below the level of the map. For example, the Gauss sums, the Jacquet modules and the theta series are many declarations but no new node. The rate per declaration is the better measure of the work on the library.
- Some Lean agents only wrote statements. Their tokens are in the Lean total, but their output has the status `known` or `open` and not `proved`.
- A failed or partial agent run is in the total. This is correct for a cost, but it makes the rate depend on the difficulty of the tasks in the period.
- The period is three days. The next measurement must use the ledger of spec 10.6, with the tokens of each kind and the cost in dollars.

## Consequence for Q-17

The measurement does not support a change of the budget yet. The owner decides Q-17 after the first measurement from the ledger.
