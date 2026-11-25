# 08. Architecture

The project has four repositories and one site. It follows the shape of the singularity project (spec 2161). That project has four repositories: `tamnd/singularity`, `tamnd/singularity-lean`, `tamnd/singularity-agent` and `tamnd/singularity-handbook`. The singularity project follows the riemann project.

The Lean package is in its own repository from the start, `tamnd/langlands-lean`, because the singularity project had to move its package there later (2161, 00). The map, the records and the pages are in `tamnd/langlands`.

## 8.1 The repositories

| Repository | Holds | Language | Licence |
|---|---|---|---|
| `tamnd/langlands` | the blueprint (the map of statements and their dependencies); the paper records; the claim records of route R1; the trust and fidelity records; the lab specs and runs; the pages of the site; the deploy workflow | Markdown, YAML, JSON | prose CC BY-SA 4.0; data Apache-2.0 |
| `tamnd/langlands-lean` | the Lean package `Langlands`, with the ported sources under `Langlands/Ported/` (05.4) | Lean 4 | Apache-2.0 (as Mathlib, and as every ported source) |
| `tamnd/langlands-agent` | `lgl`, the toolchain: index the Lean code, check the trust rows, run the agent roles, run the lab, build and check the site | Go | MIT, as singularity-agent |
| `tamnd/langlands-handbook` | The Langlands Handbook: the mathematics, written as a textbook by and for mathematicians, as PDF and EPUB volumes; `lhb`, the builder | Markdown, LaTeX, Python | prose CC BY-SA 4.0; builder MIT |

The site is https://langlands.tamnd.com.
- `lgl site build` writes it from `tamnd/langlands`, from the index of `tamnd/langlands-lean` and from the release files of the handbook.
- The workflow `deploy` of `tamnd/langlands` deploys it to the Cloudflare Worker `langlands`. The Worker serves static files only (12).

The cross-check package `langlands-crosscheck` is in `tamnd/langlands-lean/crosscheck/`.
- It has its own toolchain pin.
- It reads riemann-lean at a pinned commit and proves that its global CFT and Tate's thesis agree with the project's statements (05.6).
- `Langlands` does not import it. It is not in a release while riemann-lean has no licence (05.3).

## 8.2 The boxes

```
                 literature (arXiv, journals, books, Lean repos)
                          │ ingest (lgl paper add, lgl claim add, lgl port add)
                          ▼
 ┌──────────────────── tamnd/langlands ──────────────────────────────┐
 │  papers/  claims/ ──►  blueprint/  ◄──── index ──── tamnd/langlands-lean
 │  (records)             (the map:                    Langlands/
 │                         nodes + edges)               Statements/ Ported/
 │      ▲                   ▲   │                       Local/ Global/ GL2/ ...
 │      │                   │   ▼                       Bridge/ Routes/
 │  records/  ◄─────────────┴── lgl index / lgl trust / lgl fidelity
 │  (trust, fidelity, status, runs)                         ▲
 │  lab/ (specs, runs, certificates) ──── certificates ─────┘
 │  site/ (pages)                                            │
 └──────┬────────────────────────▲──────────────────────────────┘
        │ lgl site build          │ pull requests from agent roles
        ▼                         │
 langlands.tamnd.com      tamnd/langlands-agent (lgl: roles, lab, site)
        ▲                         │
        │ release files           ▼
 tamnd/langlands-handbook ◄── chapters (writer role + people)
```

## 8.3 The central object: the map

The *map* is a directed acyclic graph.
- Its nodes are mathematical statements and definitions. Its edges are "uses".
- It is the blueprint of the project, and every other part reads it.
- It also holds the open conjectures and the routes, so it is the plan too.

A node is one YAML file in `blueprint/nodes/`. Its name is a stable tag: `LG` and 8 characters of base 32, as in Math 2.0.

```yaml
tag: LG4N8Q2KTB
slug: llc-gl1          # the working name of 04; lgl node new keeps it
kind: theorem            # definition | theorem | lemma | conjecture | example | counterexample | check
title: Local class field theory as LLC for GL(1)
statement: |
  For a nonarchimedean local field $K$ there is a unique topological isomorphism
  $\mathrm{rec}_K : K^\times \to W_K^{ab}$ that sends a uniformizer to a geometric Frobenius
  and is compatible with norms.
sources:
  - paper: serre1967local
    loc: "Cassels-Fröhlich, Ch. VI, Theorem 2"
  - port: nyll
    loc: "ClassFieldTheory/Local/Reciprocity.lean, finiteAbelianLocalReciprocity"
uses: [LG7Y2N0QBE, LGM4T9X1CD]
lean:
  statement: Langlands.LocalReciprocityGL1
  proof: Langlands.localReciprocityGL1   # absent while open
tier: T3
route: []
level: [G1, G2]
handbook: "Vol. 3, Ch. 4"
status: computed         # never written by hand; see below
math2: RZ66X0NAM5        # the Math 2.0 node, when there is one
```

Documents 04 and 07 refer to nodes by working names such as `LG-llc-gl2`. `lgl node new` assigns the tag and keeps the working name as `slug`, so both resolve on the site.

`lgl index` computes the status from the Lean environment and the records. It is never written by hand.

| Status | Meaning |
|---|---|
| `unstated` | the node has no Lean statement yet; `needs` lists the missing vocabulary (06.2.2, G1b) |
| `stated` | the Lean statement exists and builds |
| `faithful` | the statement passed the fidelity battery (06.3) for its class |
| `proved` | a Lean proof exists, depends on the three standard axioms only, and every node it uses is `proved` |
| `proved-mod` | a Lean proof exists that takes named nodes as hypotheses (a published theorem that is not yet formalized); the site lists them |
| `open` | the statement is an open conjecture; no proof is claimed |
| `claimed` | the statement is a fresh claim of route R1 (01.2); it is not a hypothesis of any node |
| `refuted` | a Lean proof of the negation exists |

The differences from a classical blueprint (Massot's `leanblueprint`, used by Imperial FLT, and the Verso blueprint of 2026):
- the nodes are data, not LaTeX;
- the status is computed;
- the map includes the open conjectures and the routes.

## 8.4 The five flows

1. **Ingest.**
   - `lgl paper add <arXiv id | DOI>` writes `papers/<key>.yaml`. It has the metadata, the arXiv version, the licence class and a list of the numbered results of the paper.
   - The `reader` role (10.3) proposes a node for each result that the project needs, with its uses. A person accepts or edits.
2. **Port.**
   - `lgl port add <repo> <commit> <paths>` copies Lean files from a licensed source into `Langlands/Ported/<source>/`. It keeps the licence header, adds a provenance line and records the commit in `manifests/ported.yaml` (05.4).
   - The `porter` role makes the files build at the pin. It also writes the bridge to the project's statements.
3. **Formalize.**
   - The `stater` role writes the Lean statement of a node, and the fidelity battery runs.
   - The `prover` role works on the proof, and `lgl index` computes the status.
   - Each step is a pull request to `tamnd/langlands-lean` with a matching change to `tamnd/langlands`, built by CI.
4. **Check claims and explore.**
   - `lgl claim add <arXiv id>` writes `claims/<key>.yaml` for a fresh claim (route R1). The `reader` and `stater` roles pick a self-contained part of it, and the `prover` and `refuter` roles work on it.
   - The `explorer` role runs the lab (13): Hecke eigenvalues, Galois representations of small conductor, character tables, tests of conjectured identities.
   - A result is a `lab/runs/<id>/` record. When it matters, it also becomes a new node of kind `example`, `counterexample`, `check` or `conjecture`.
5. **Explain.**
   - The `writer` role and people write the handbook chapters from the map and the Lean code.
   - The `explainer` role writes docstrings and the L2 text of each node on the site.

## 8.5 Cross-cutting decisions

- **Lean is the source of truth for status.** No status, count or claim on the site or in the handbook is written by hand. Each comes from a record that a tool wrote (the rule of riemann and singularity).
- **Pinned everything.**
  - Lean and Mathlib are pinned in `lean-toolchain` and `lake-manifest.json`.
  - Each ported source is pinned by commit.
  - Each paper record pins the version it read (the arXiv version number).
- **Port, do not depend.**
  - Large Lean projects are not Lake dependencies. Their pins differ: Imperial FLT is at v4.35.0, anthropics FLT at v4.33.1, NYLL at v4.36.0 and TauCeti follows Mathlib master.
  - Their size would make the build cost of the project their cost.
  - A port takes only the files that a node needs (05.4).
- **One writing style.**
  - Plain technical English (ASD-STE100): no em dash and no en dash, no "we" in the content of the site and the handbook, math in `$...$`. The style script of singularity is reused.
  - Names of theorems with several authors use a hyphen (Jacquet-Langlands, Fargues-Scholze).
- **People decide.**
  - The agent proposes pull requests, and a person merges.
  - Statements of open conjectures and their changes need two people (06.3, F6).
  - A page about a fresh claim needs the owner and a letter to the authors (14.4).
- **Budgets are explicit.** Every model call is in a ledger with its cost, under a daily and a per-run budget in `agent.yaml`. The rule is the one of singularity-agent: no file, no budget, no calls.
