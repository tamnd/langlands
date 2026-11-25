# 10. tamnd/langlands-agent: `lgl`

`lgl` is one Go binary. It does for this project what `sing` does for singularity and `rh` does for riemann:
- it indexes the Lean code and computes the status of the map;
- it runs the trust checks;
- it builds the site;
- it runs the agent roles that write statements, proofs, ports, examples and text;
- it runs the lab and the claim checks of route R1.

The code has the shape of singularity-agent: `cmd/`, `index/`, `trust/`, `site/`, `agent/`, `llm/`, `prompts/`, `lab/`. The packages `index`, `trust` and `site` are shared with singularity-agent through a common Go module (Q-09).

The name `lgl` is short and has no clash with a common command [U]. Q-18 records the alternatives.

## 10.1 Commands

```
lgl help | version
lgl index      -lean ../langlands-lean -out records/index.json      # Lean env → declarations, uses, sorry, axioms
lgl status     -content ../langlands                                # map + index → records/status.json
lgl trust      [-quick] -lean ../langlands-lean                     # 14: axioms, replay, comparator → records/trust.json
lgl fidelity   -node LG... | -all                                   # 06.3: run F1 to F5 for a node → records/fidelity.json
lgl paper add  <arXiv id | DOI> | list | show <key>
lgl claim add  <arXiv id | URL> | list | show <key>                 # route R1: a fresh claim record (07.12)
lgl claim plan <key>                                                # the self-contained parts, their statements, cost
lgl port add   [-plan] <repo> <commit> <paths> | list | diff <source>   # 05.4: copy licensed Lean files, record provenance; -plan measures the import closure
lgl port check                                                      # licence headers, provenance lines, manifest
lgl node new | check | graph [-route R2] [-tier T5] [-dot]
lgl queue      [-role prover] [-n 20]                               # the work queue, with the reason for each rank
lgl agent run  <role> [-node LG...] [-budget 5]                     # one run of a role; writes a run record and a branch
lgl agent report -week 2026-W49                                     # the weekly report (10.8)
lgl lab run    <spec> | list | show <run>                           # 13
lgl site build -content ../langlands -lean ../langlands-lean -handbook ../langlands-handbook/build -out public
lgl site check -dir public | serve -dir public
```

The exit codes are those of singularity-agent:
- 0: success;
- 1: a check failed;
- 2: a usage error;
- 3: not written yet. The message names the milestone.

## 10.2 Lean access

`lgl` talks to Lean in three ways, from cheap to expensive:

1. **Index.** One Lean program, run with `lake env lean --run`, imports `Langlands`. For each constant it writes:
   - the type;
   - the module;
   - the constants it uses;
   - whether it depends on `sorryAx`.

   This is `sing index`, adapted.
2. **Check a file.** `lake env lean <file>` with a JSON message log, for the edit and check loop of a role. A role always works in a fresh worktree of `tamnd/langlands-lean`, so a run cannot break `main`.
3. **Interactive.** A long-lived Lean REPL (the `repl` of leanprover-community, or Pantograph) for the prover role, so that a proof can be tried tactic by tactic against goal states. The REPL runs in a sandbox with no network and a read-only Mathlib.

For ports and claim checks a fourth mode is useful: build a pinned external repository in its own sandbox and extract its statements with `lean4export`. The bridge files of 06.4 come from that output.

## 10.3 The roles

Each role has three parts:
- a prompt in `prompts/<role>.md`, with front matter `role` and `version`;
- a Go driver in `agent/<role>.go`;
- a test with a fake model.

| Role | Input | Output | Checked by |
|---|---|---|---|
| `reader` | a paper or claim record and its text | the list of its numbered results with page and number; proposed nodes and `uses` edges; for a claim, the self-contained parts and their dependencies | a person accepts each node |
| `stater` | a node | the Lean statement in `Statements/` or in a module, with a docstring | build; F1, F2 of 06.3 |
| `prover` | a `stated` node whose uses are `proved` or `proved-mod` | a proof, or a decomposition into new lemma nodes with statements | build; `lgl index` shows no `sorry` |
| `planner` | a route and its nodes | the next nodes to state; a decomposition of a hard node into steps; a short note on why | a person, for any change of `routes.yaml` or `targets.yaml` |
| `refuter` | a statement, a conjecture or a step of a fresh claim | a Lean proof of the negation, a counterexample from the lab, or a trivial proof (F3, F4) | build; lab record |
| `explorer` | a question of a route (for example "do the Satake parameters of these forms satisfy the predicted identity") | a lab spec and its run; a conjecture node when the data suggests one | lab record; a person for a new conjecture node |
| `porter` | a file of a ported source, or a failing build after a bump | the file at the project pin, with its provenance line; the bridge to the project statement | build; `lgl port check` |
| `explainer` | a declaration or a node | a docstring, the L2 text of a node, the round-trip English of F5 | a person |
| `writer` | a handbook chapter brief | a chapter section, with examples and exercises (11.2) | a person; the handbook check |
| `linker` | a node | its Math 2.0 node, its LMFDB objects (13.1) and its references | `lgl site check` |

The research happens in two roles:
- **`planner`.** It reads the route documents (04), the status of the map, the lab results and the claim records, and it proposes the next steps. Its proposals are cheap to make and expensive to follow, so a person approves each change of a route.
- **`reader` on claims.** For route R1 the hard step is the choice of a self-contained part of a long preprint. That part must be small enough to formalize and central enough to matter. The `reader` proposes and a person decides.

## 10.4 The queue

The work queue has every node that a role can act on. The rank of a node is

$$
\text{rank} = \frac{w_{\text{route}} \cdot (1 + \text{unblocks}) \cdot (1 + \text{level bonus})}{1 + \text{attempts}} \cdot \text{age factor}
$$

- `unblocks` is the number of nodes that wait only on this node.
- `attempts` counts the failed runs.
- `level bonus` is 1 for a node on the path to a top theorem of the current milestone (15) and 0 otherwise.
- Library nodes (tiers T1 to T8) have the weight of the milestone that needs them. Route nodes have the weight of their route (04.1).

`lgl queue` prints the rank and the reason, so a person can see why the agent works on something. The weights are in `blueprint/routes.yaml`, and people set them.

## 10.5 The loop of one run

1. Take the top item of the queue for the role, or the node given with `-node`.
2. Make a worktree and a branch `agent/<role>/<tag>-<run>`.
3. Build the context:
   - the node, and its uses with their statements and docstrings;
   - the papers and the pages of the source;
   - nearby Lean declarations, found by name and by type, in the project, in Mathlib and in the ported sources;
   - the earlier failed attempts, with their error messages.
4. Call the model. For `prover`, iterate: propose a proof, check it in the REPL, read the errors, repair. Stop at the step limit or the budget limit.
5. Check the result with the checks of the role (10.3).
6. Write a run record. On success, open a pull request with the record in its body.

## 10.6 Models, budgets and the ledger

`agent.yaml` in `tamnd/langlands` sets the models and the budget:

```yaml
models:
  default: claude-sonnet-5-5
  prover: claude-opus-5-5
  planner: claude-opus-5-5
  refuter: claude-opus-5-5
  reader: claude-opus-5-5     # claim reading needs the strongest model
  linker: claude-haiku-5-5
budget:
  day: 200      # dollars
  run: 20
  role:
    prover: 110
    porter: 30
    refuter: 25
    reader: 15
  route:
    R1: 0.20    # share of the research part of the budget; 04.1
```

The rules are those of singularity-agent:
- With no `agent.yaml` the budget is zero and no call goes out.
- Every call goes into `agent/ledger.jsonl` with the run, the role, the model, the prompt version, the tokens and the cost.
- The model ids are configuration, not code. A new model is a change of `agent.yaml`, tested by the evaluation of 10.9.

In the first year, about two thirds of the budget goes to the library (tiers T1 to T8 and the ports), and one third to the routes. The share of the routes grows as the library is finished.

## 10.7 Untrusted text

Paper text, claim text, web pages, external Lean code and lab output are data, not instructions.
- A role puts them in the prompt inside a marked block. The prompt says that instructions in the block are ignored.
- A role never runs a command or fetches a URL that comes from such text.
- An external Lean repository is built only in a sandbox with no network and no secrets. Lean code can run arbitrary programs at elaboration time.
- The lab runs in a container with no network (13).

## 10.8 The weekly report

`lgl agent report` writes `reports/2026-Wnn.md` in `tamnd/langlands`. The report has:
- the nodes that changed status, by tier and by route;
- the pull requests opened and merged;
- the spend by role and by route;
- the lab runs;
- the claim checks: the parts done, the gaps found and the letters sent;
- the refuted conjectures;
- the five largest open nodes of each route, with what blocks them.

The site shows the reports as the timeline (12).

## 10.9 Evaluation of the agent

A fixed set of 200 tasks lives in `eval/tasks/`. Every task has a known answer.
- At S0 the tasks come from outside the project:
  - lemmas of Mathlib's `NumberTheory` and `RepresentationTheory` folders, with their proofs removed;
  - statements of the NYLL and Imperial FLT projects;
  - failed builds of the FLT ports.
- From S2 on, tasks also come from the project's own history.

Each model or prompt change runs the set and reports the pass rate and the cost. A change that lowers the pass rate by more than 5 points is not merged. The set grows by 10 tasks each month from the merged pull requests.

A second set, `eval/statements/`, tests the `stater` role. It has 50 informal statements with reviewed Lean statements, and 50 subtly wrong Lean statements that the battery must reject. An example of a wrong statement is LLC with the arithmetic normalization. Another is a bijection without the ε-factor condition.
