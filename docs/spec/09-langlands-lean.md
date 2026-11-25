# 09. tamnd/langlands-lean: the Lean package

## 9.1 Layout

```
langlands-lean/
├── README.md  CHANGELOG.md  CONTRIBUTING.md  CITATION.cff  NOTICE  LICENSES/
├── lakefile.toml  lean-toolchain  lake-manifest.json
├── Langlands.lean                   # imports every proved module
├── Langlands/
│   ├── Statements/                  # the pinned statements (06); comments; Mathlib + Basic only
│   │   ├── Basic.lean               # WeilGroup, WeilDeligneRep, IsSmooth, IrrSmooth, IsLanglandsFamily
│   │   ├── ClassField.lean          # LocalReciprocityGL1, LocalExistence, GlobalReciprocity, ...
│   │   ├── LocalLanglands.lean      # LocalLanglandsGL, ...GL2, ...SL2, ...GSp4, ...G2, LocalLanglands shapes
│   │   ├── Modularity.lean          # ModularityEllipticQ, ...SemistableQ, SerreModularity, FontaineMazurGL2Q
│   │   ├── Reciprocity.lean         # ReciprocityGL, AutomorphicToGalois, LocalGlobalCompatibility
│   │   ├── Functoriality.lean       # FunctorialityGL, SymPowerFunctoriality, BaseChangeCyclic, shapes
│   │   ├── Ramanujan.lean           # RamanujanPeterssonHolomorphic, RamanujanGL, RamanujanMaass, SelbergEigenvalue
│   │   ├── LFunctions.lean          # HeckeFunctionalEquation, ArtinConjecture, ArtinOdd2Q, HasseWeil...
│   │   ├── TraceFormula.lean        # FundamentalLemma, ArthurClassification (shapes until T2)
│   │   ├── FunctionField.lean       # ReciprocityFunctionFieldGL, VLafforgueParametrization
│   │   ├── PAdic.lean               # PadicLanglandsGL2Qp, BreuilMezardGL2Qp (shapes)
│   │   └── Geometric.lean           # GeometricLanglands (the shape and its `needs`)
│   ├── Ported/                      # ported sources, licence headers kept (05.4)
│   │   ├── NYLL/  ImperialFLT/  AnthropicFLT/  TauCeti/  EpsilonFML/  ...
│   ├── Foundations/                 # tier T1: local fields, adeles, ideles, Haar measure on them
│   ├── Groups/                      # tier T2: reductive groups over fields, root data, dual groups, L-groups
│   ├── ClassField/                  # tier T3: Weil groups, local and global CFT, Lubin-Tate, Tate's thesis
│   ├── GL2/                         # tier T4: modular forms, Hecke operators, adelic GL(2), newforms
│   ├── Local/                       # tier T5: smooth representations, Bernstein-Zelevinsky, LLC
│   ├── LFunctions/                  # tier T6: Rankin-Selberg, Godement-Jacquet, converse theorems
│   ├── TraceFormula/                # tier T7: Selberg, orbital integrals, endoscopy
│   ├── Galois/                      # tier T8: Galois representations, deformations, patching
│   ├── PAdic/                       # tier T9: (φ,Γ)-modules, p-adic and mod p
│   ├── FunctionField/               # tier T10: shtukas, Drinfeld, Lafforgue
│   ├── Routes/                      # one folder per route of document 04
│   │   ├── R1Claims/  R2ExplicitLLC/  R3Modularity/  ...
│   ├── Examples/                    # worked examples and certificates from the lab, each a node
│   └── Bridge/                      # the project's statements ↔ Mathlib, formal-conjectures, ports (06.4)
├── Langlands/WIP/                   # work with sorry; not imported by Langlands.lean
├── crosscheck/                      # the package langlands-crosscheck (05.6); own pin; not released
├── manifests/
│   ├── statements.sha256
│   └── ported.yaml                  # source, commit, licence, paths, date for each port
├── scripts/style.sh  scripts/forbidden.sh
└── .github/workflows/  check.yml  build.yml  bump.yml  trust.yml
```

The map, the records and the site live in `tamnd/langlands`:

```
langlands/
├── README.md  CHANGELOG.md  CONTRIBUTING.md  CITATION.cff  LICENSES/
├── blueprint/
│   ├── nodes/*.yaml                 # the map (08.3)
│   ├── routes.yaml                  # the routes of 04 and their nodes
│   ├── targets.yaml                 # the open targets O-Rk-n of 04
│   └── tiers.yaml                   # the tiers of 07
├── papers/*.yaml                    # one record per paper (07.13)
├── claims/*.yaml                    # one record per fresh claim (route R1)
├── lab/                             # computation specs, runs and certificates (13)
├── records/                         # written by lgl; never edited by hand
│   ├── status.json  trust.json  fidelity.json  axioms.json  index.json  runs.jsonl
├── site/                            # pages that are not generated: home, about, trust, routes, learn
├── formalization.yaml               # Palomar registration, schema v0.4 (14.5)
├── agent.yaml                       # budget and models for lgl (10.6); no file, no calls
├── wrangler.jsonc
└── .github/workflows/  check.yml  deploy.yml
```

## 9.2 Rules for the Lean code

1. **No `sorry` in the main tree.**
   - `Langlands.lean` imports everything outside `WIP/` and `crosscheck/`.
   - CI fails there on `sorry`, `admit`, a new `axiom`, `opaque`, `native_decide`, `implemented_by` and `@[extern]`.
   - A node with an unfinished proof keeps the proof in `WIP/` and has status `stated`.
2. **Hypotheses, not axioms.**
   - A published theorem that is not yet formalized enters as a named `def ... : Prop` in `Statements/`. It is a hypothesis of the theorems that use it, never an `axiom`.
   - The status of those theorems is `proved-mod` (08.3), and the site lists the hypotheses.
   - Examples:
     - `LocalLanglandsGL` with the hypothesis `HarrisTaylorCohomology`, the cohomology of the Lubin-Tate tower, until tier T8 proves it;
     - `ModularityEllipticQ` with `BCDTLocalDeformation`, the local deformation rings at 3, until a port supplies it.
3. **Fresh claims are not hypotheses.** A `claimed` node (01.2) is never a hypothesis of another node. `lgl index` fails if one is.
4. **Statement files are small and commented.** Everything else may be long. A statement file has a docstring for each definition and each statement, with the informal statement and a reference.
5. **Mathlib style, Mathlib names.** The code follows the Mathlib naming and style guide, so that parts can go upstream (9.5).
6. **Ported files keep their licence.**
   - A ported file keeps its header and gets a provenance line: `-- Ported from <repo>@<commit>:<path>`.
   - A change to a ported file is a commit of its own with the label `port-change`. Then a diff to the source is always possible.

## 9.3 The toolchain pin

The project starts on Lean `v4.35.0` with the Mathlib tag `v4.35.0` (`56a005855e`). This is the pin of Imperial FLT, singularity-lean, AxiomMath/Stacks, AxiomMath/CFSG and hironaka (05.1), so the main port sources and the sister project build without change.

The other ports:
- NYLL is at `v4.36.0`.
- anthropics FLT is at `v4.33.1`.
- TauCeti follows Mathlib master (`b5aed57ecb` on `v4.37.0-rc1` on 2026-11-25).
- The `porter` role moves these to the project pin file by file (05.4).

The first monthly bump is to `v4.36.0` at S1. After that, the `bump` workflow runs once a month:
1. It opens a pull request with the new `lake-manifest.json`.
2. The `porter` role fixes what breaks.
3. A person merges.

The cross-check package keeps its own pin, `v4.33.1`, the pin of riemann-lean (05.6).

## 9.4 CI

| Workflow | Repository | When | What |
|---|---|---|---|
| `check` | both | each pull request and push | the style script; the forbidden words scan (9.2); `zizmor` on the workflows; for `tamnd/langlands`, a schema check of `blueprint/`, `papers/` and `claims/` |
| `build` | langlands-lean | each pull request and push | `lake exe cache get`, `lake build`, `lgl index`, `lgl trust -quick` (axioms of the changed top theorems); the job uploads `records/` as an artifact |
| `deploy` | langlands | push to `main`, daily, by hand | `lgl site build`, `lgl site check`, `wrangler deploy`; a pull request builds and checks the site but does not deploy |
| `bump` | langlands-lean | monthly, by hand | the toolchain bump of 9.3 |
| `trust` | langlands-lean | weekly, by hand | the full trust run of document 14 |

The full trust run does these checks:
- `lake build` and `lake check`;
- `#print axioms` and a constant walk for every `proved` node;
- replay in `lean4checker --fresh`;
- `lake comparator --paranoid` for the pinned statements, which replays in the independent checkers lean4lean and nanoda;
- the cross-check package of 05.6.

The actions are pinned by commit hash, as in singularity.

## 9.5 Upstream

Tiers T1 to T3 are mostly general number theory that Mathlib does not have yet: the Weil group, local and global CFT, Tate's thesis and smooth representations.
- Several Mathlib pull requests are open in these areas (05.1): #40934, #41277 and #43087 for Hecke operators; #41520, #41525 and #45067 for smooth representations; #42687 for class formations.
- The project does not compete with them. When an open pull request covers a node, the project uses its statement shape and offers its proofs to the author.
- The project writes in Mathlib style and sends parts upstream when they are stable, with the authors listed.

Upstreaming is slow. The project never waits for it. A module stays in `Langlands/` until Mathlib has it, and then becomes a thin file of aliases. The CFT and Tate's thesis parts are the first candidates (Q-11).

## 9.6 The trusted statements

`manifests/statements.sha256` has the SHA-256 of each file in `Langlands/Statements/`.
- A change to one of those files fails CI unless the same pull request changes the manifest and has the label `statement-change`. That label needs two approvals.
- `lake comparator` (in the trust workflow) checks that each top theorem has exactly the type of its pinned statement.
- The bridge files of 06.4 hold word-for-word copies of external statements with their source commits. They are pinned in the same manifest.
