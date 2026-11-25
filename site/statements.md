---
title: The statements
description: The planned Lean statement files of the Langlands program in langlands-lean, and the 44 statements that they will hold.
lead: "Each main statement of the program is a `def ... : Prop` in a small statement file of langlands-lean. A referee reads these files. The status of each statement comes from the Lean build."
---
## The statement files

The statements live in `Langlands/Statements/` of [tamnd/langlands-lean](https://github.com/tamnd/langlands-lean), one file for each family. Each file imports only Mathlib and `Langlands/Statements/Basic.lean`. Each file has a docstring for each definition and each statement, with the informal statement and a reference. A proof is a separate `theorem` in another file. The files are pinned by hash in `manifests/statements.sha256`.

| File | Content |
|---|---|
| `Langlands/Statements/Basic.lean` | the vocabulary: `WeilGroup`, `WeilDeligneRep`, `IsSmooth`, `IrrSmooth`, `IsLanglandsFamily` |
| `Langlands/Statements/ClassField.lean` | `LocalReciprocityGL1`, `LocalExistence`, `GlobalReciprocity` and the other statements of class field theory |
| `Langlands/Statements/LocalLanglands.lean` | `LocalLanglandsGL`, `LocalLanglandsGL2`, `LocalLanglandsSL2`, `LocalLanglandsGSp4`, `LocalLanglandsG2`, and the shape of `LocalLanglands` |
| `Langlands/Statements/Modularity.lean` | `ModularityEllipticQ`, `ModularitySemistableQ`, `SerreModularity`, `FontaineMazurGL2Q` |
| `Langlands/Statements/Reciprocity.lean` | `ReciprocityGL`, `AutomorphicToGalois`, `LocalGlobalCompatibility` |
| `Langlands/Statements/Functoriality.lean` | `FunctorialityGL`, `SymPowerFunctoriality`, `BaseChangeCyclic`, and the shapes of the general statements |
| `Langlands/Statements/Ramanujan.lean` | `RamanujanPeterssonHolomorphic`, `RamanujanGL`, `RamanujanMaass`, `SelbergEigenvalue` |
| `Langlands/Statements/LFunctions.lean` | `HeckeFunctionalEquation`, `ArtinConjecture`, `ArtinOdd2Q`, `HasseWeil` and the related statements |
| `Langlands/Statements/TraceFormula.lean` | `FundamentalLemma`, `ArthurClassification`, as shapes until tier T2 exists |
| `Langlands/Statements/FunctionField.lean` | `ReciprocityFunctionFieldGL`, `VLafforgueParametrization` |
| `Langlands/Statements/PAdic.lean` | `PadicLanglandsGL2Qp`, `BreuilMezardGL2Qp`, as shapes |
| `Langlands/Statements/Geometric.lean` | `GeometricLanglands`, as a shape with the list of the vocabulary that it needs |

None of these files exists yet. The project is at milestone S0. The exit criterion of S0 is that `Basic.lean` and `ClassField.lean` build at the pinned toolchain with no `sorry`, and that the fidelity checks F1 to F3 pass for `LocalReciprocityGL1`, `GlobalReciprocity`, `ModularityEllipticQ` and `SatoTate`.

## The status of a statement

The status of each statement comes from the Lean build of langlands-lean, through the node of the statement on the [map](/map/). This page does not give a status by hand. The fidelity checks F1 to F7 of each statement are on the [trust page](/trust/).

## The classes and the vocabulary

Each statement has a class. A **theorem** has a published proof that experts accept. An **open** statement is a conjecture. A **claimed** statement is a fresh claim that experts have not accepted yet.

Each statement also has a vocabulary state. A statement is **ready** when it can be written at the pinned toolchain with the vocabulary of `Basic.lean`. It is **partial** when it needs a definition that the project writes in the tiers T1 to T4. It is **missing** when it needs a theory that does not exist in Lean, for example reductive group schemes, D-modules on stacks or diamonds. Until its vocabulary exists, a statement of the third kind has a node with status `unstated`.

## The list

The column "Planned" gives the milestone or the route at which the statement is planned.

| Statement | Class | Vocabulary | Planned |
|---|---|---|---|
| `LocalReciprocityGL1` | theorem | ready | S0 |
| `LocalExistence` | theorem | ready | S0 |
| `GlobalReciprocity` | theorem | ready | S0 |
| `GlobalExistence` | theorem | ready | S0 |
| `KroneckerWeber` | theorem | ready | S0 |
| `LocalLanglandsTorus` | theorem | ready | S1 |
| `HeckeFunctionalEquation` | theorem | partial | S1 |
| `LocalLanglandsGL n` | theorem | partial | S0 shape, S3 full |
| `LocalLanglandsGL2` | theorem | partial | S3 |
| `LocalLanglandsSL2` | theorem | partial | S5 |
| `LocalLanglandsGSp4` | theorem | partial | S6 |
| `LocalLanglandsG2` | theorem | missing | S6 |
| `LocalLanglands G` | open | missing | S3 shape |
| `FormalDegree` | open, a theorem for some groups | missing | S8 |
| `LocalGGP` | a theorem in many cases | missing | S8 |
| `FarguesScholzeCompatible` | theorem | missing | R9 |
| `ModularityEllipticQ` | theorem | ready | S0 |
| `ModularitySemistableQ` | theorem | ready | S0 |
| `EichlerShimuraDeligne` | theorem | partial | S4 |
| `RamanujanPeterssonHolomorphic` | theorem | ready | S0 |
| `SerreModularity` | theorem | ready | S4 |
| `FontaineMazurGL2Q` | theorem with conditions | partial | S8 |
| `ArtinOdd2Q` | theorem | partial | S4 |
| `ArtinConjecture` | open | partial | S2 |
| `SatoTate` | theorem | ready | S0 |
| `HasseWeilEllipticQ` | theorem | ready | S0 |
| `HasseWeil` | open | partial | S8 |
| `JacquetLanglandsGL2` | theorem | partial | S6 |
| `SelbergEigenvalue` | open | ready | S2 |
| `RamanujanMaass` | open | partial | S4 |
| `RamanujanGL n K` | open | partial | S4 |
| `AutomorphicToGalois n K` | theorem | partial | S8 |
| `ReciprocityGL n K` | open | partial | S4 |
| `FunctorialityGL n m r` | open | partial | S4 |
| `SymPowerFunctoriality` | theorem | partial | S8 |
| `BaseChangeCyclic` | theorem | partial | S8 |
| `Functoriality G H r` | open | missing | S3 shape |
| `FundamentalLemma` | theorem | partial | S8 |
| `ArthurClassification` | theorem, `proved-mod` the twisted weighted fundamental lemma | missing | S8 shape |
| `ReciprocityFunctionFieldGL n` | theorem | partial | S6 |
| `VLafforgueParametrization` | theorem | missing | R7 |
| `GeometricLanglands` | theorem | missing | R8 |
| `PadicLanglandsGL2Qp` | theorem | missing | R9 |
| `BreuilMezardGL2Qp` | theorem | partial | R9 |

A statement of class theorem counts for the level G1 after the fidelity checks F1 to F5. A statement of class open needs all seven checks F1 to F7 before any proof of it is announced.
