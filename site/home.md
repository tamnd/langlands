---
title: The Langlands program in Lean
description: A public Lean project that states the Langlands program, proves its known parts and works on its open parts.
eyebrow: Open program
lead: The Langlands program predicts a correspondence between Galois representations and automorphic representations, for each reductive group $G$ and in particular for $GL_n$. For $GL_1$ it is class field theory, which is a theorem. In general it is open.
doors:
  - title: I know the mathematics
    path: program/
    text: The statements, the known cases, the open conjectures and the routes.
  - title: I referee
    path: trust/
    text: The checks that a claim must pass, and the state of each check.
  - title: I am a student
    path: learn/
    text: Paths through the handbook, from local fields to the open conjectures.
  - title: I know Lean
    path: map/
    text: The nodes of the map, their Lean names and their status.
  - title: I am a program
    path: llms.txt
    text: A text map of the site, and the data in JSON at /api/.
---
This project states the Langlands program in Lean 4 with Mathlib, proves the known parts in an order that leads to the open parts, and records each step on a map of nodes. Each node has a status that a tool computes from the Lean build. A person does not set the status by hand.

The general conjectures of the program are open. No result on this site is a proof of one of them. When a node of an open conjecture changes status, the [trust page](/trust/) shows which checks passed.

The project has four repositories. [tamnd/langlands](https://github.com/tamnd/langlands) has the map, the paper records and this site. [tamnd/langlands-lean](https://github.com/tamnd/langlands-lean) has the Lean code. [tamnd/langlands-agent](https://github.com/tamnd/langlands-agent) has the `lgl` command, which checks the map and builds the site. [tamnd/langlands-handbook](https://github.com/tamnd/langlands-handbook) has the handbook, a textbook in PDF and EPUB volumes.
