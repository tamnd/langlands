# 12. The site: langlands.tamnd.com

The site is static. `lgl site build` writes it from three sources:
- `tamnd/langlands`: the map, the records, the claims and the pages;
- `tamnd/langlands-lean`: the Lean index;
- the handbook build.

The deploy workflow of `tamnd/langlands` puts it on the Cloudflare Worker `langlands`. The Worker has no script and serves the files of `public/`:

```jsonc
// The Worker that serves langlands.tamnd.com. It has no script: Cloudflare serves the files of public/, which lgl site build writes.
{
  "name": "langlands",
  "compatibility_date": "2026-11-01",
  "workers_dev": true,
  "routes": [{ "pattern": "langlands.tamnd.com", "custom_domain": true }],
  "assets": {
    "directory": "public",
    "html_handling": "auto-trailing-slash",
    "not_found_handling": "404-page"
  }
}
```

The templates, the CSS and the search start as a copy of the `site/` package of singularity-agent, so the three sites (riemann, singularity, langlands) look like one family.

## 12.1 The home page and its doors

The home page has three parts:
- **The program in one paragraph.** Reciprocity, functoriality and the local correspondence, and why they matter.
- **One status line, computed from the records.** For example: "statements: N of 44 faithful; GL(1): proved; LLC for GL(2): stated; nodes proved: P of Q; claims checked: C".
- **Doors**, as on riemann and singularity:

| Door | For | Goes to |
|---|---|---|
| I know the mathematics | experts | `/program/`: the statements, what is known, the open targets and routes |
| I referee | anyone who checks a claim | `/trust/` and `/claims/` |
| I am a student | learners | `/learn/`: the paths through the handbook, by background |
| I teach | teachers | `/teach/`: volumes and chapters that fit a one-semester course, with exercises |
| I know Lean | Lean users | `/code/`: the package, the statements, how to contribute, the ports |
| I am a program | agents and tools | `/llms.txt` and `/api/` |

The `/teach/` door is new. The handbook is a textbook (11), and a course is the main way in which students meet it. Each course page lists the chapters, the prerequisites, the exercises and the parallel textbook. Example courses:
- "Class field theory through Lean" (Volume 3);
- "Modular forms" (Volume 4);
- "Local Langlands for GL(2)" (Volume 6, part 1).

## 12.2 The pages

| Path | Content | Source |
|---|---|---|
| `/program/` | the statements of 03 and 06.2, the table of what is proved and what is open, each with its Lean statement and its fidelity state | `site/program.md` and `records/` |
| `/statements/` and `/statements/<name>/` | each statement of 06.2: informal statement, Lean statement in full, class, vocabulary status, fidelity rows F1 to F7, bridges | `Langlands/Statements/`, `records/fidelity.json` |
| `/map/` | the map as a graph, filtered by tier, route, level or status; a node opens its page | `blueprint/nodes`, `records/status.json` |
| `/node/<tag>/` | statement, proof sketch, Lean statement and proof (with a link to the source line), uses and used-by, papers, ports, LMFDB objects, Math 2.0 link, handbook section, history | all of the above |
| `/paper/<key>/` | the paper record: metadata, the results the project uses, their nodes and status | `papers/` |
| `/claims/` and `/claims/<key>/` | each fresh claim of route R1: what it claims, the part checked, the result, the letters to the authors and their answers; a page goes public only after the authors had 30 days to answer (14.4) | `claims/` |
| `/routes/` and `/routes/<R>/` | each route of 04: the idea, the open targets, the key obstruction, its nodes and its progress bar | `blueprint/routes.yaml`, `blueprint/targets.yaml` |
| `/ports/` | each ported source: licence, commit, files, what the project uses, the bridge | `manifests/ported.yaml` |
| `/lab/` and `/lab/<run>/` | the computations: spec, environment, results, certificates, the node it supports or refutes | `lab/runs/` |
| `/trust/` | the trust table (14) and the fidelity table (06.3) | `records/trust.json`, `records/fidelity.json` |
| `/learn/` | learning paths through the handbook volumes, with links to Math 2.0 | `paths/` |
| `/teach/` | course plans built from the handbook | `site/teach/` |
| `/handbook/` | the volumes, the PDF and EPUB downloads, the HTML chapters | the handbook build |
| `/code/` | the layout of the package, the pinned toolchain, how to build, the statement files in full | `Langlands/`, `lean-toolchain` |
| `/timeline/` | the weekly reports and the releases | `reports/` |
| `/search/` | search over nodes, papers, claims, Lean names and the handbook | built index |
| `/api/nodes.json`, `/api/papers.json`, `/api/claims.json`, `/api/status.json` | the data, for programs | `records/` |
| `/llms.txt` | a short text map of the site for language models | generated |

## 12.3 Rules

1. **Every number on the site comes from a record.** No page has a hand-written count or status.
2. **No claim without the trust rows.**
   - The home page and `/program/` show the status of each open statement from `records/status.json`.
   - If a node of an open statement becomes `proved`, the site shows "Lean proof, checks C1 to Cn passed" and links the trust page.
   - The words "solved" or "proved" for an open conjecture appear only after the claim policy of 06.6 is met.
3. **No judgement of other people's work.** A claim page reports what a Lean check found, in neutral words. It never says that a paper is wrong. It says that "step X as stated does not follow from Y; here is the Lean counterexample" (06.6, 14.4).
4. **Math renders without JavaScript where possible.** KaTeX runs at build time, as on riemann and singularity.
5. **`lgl site check`** checks these things:
   - every internal link;
   - every node tag;
   - every Lean link, which must resolve to a line of the pinned commit;
   - every LMFDB label;
   - the style rules;
   - that each page has a title and a description.
