# Week 3 — Challenges

The exercises drill each tool in isolation. **The challenge makes you combine them under a constraint**: build one real multi-feature part that *requires* a non-default plane, a swept or lofted feature, and a pattern — and that rebuilds cleanly when you change a single driving dimension. That last requirement is the hard part and the whole point.

## Index

1. **[Challenge 1 — Parametric heat sink or pipe elbow](./challenge-01-parametric-heat-sink-or-pipe-elbow.md)** — model a finned heat sink *or* a flanged pipe elbow that combines a non-default plane, a sweep/loft, and a pattern, built so one driving dimension rebuilds the whole part. (~90–120 min)

## How it's assessed

Challenges are optional — you can pass the week without one. But doing this one puts you measurably ahead, because it forces the exact skill the mini-project (and Week 4's assembly, and Week 5's configurations) depend on: **building parametric robustness in on purpose.**

The challenge is graded on a simple rubric, weighted toward robustness over polish:

| Criterion | Weight | What "great" looks like |
|-----------|-------:|-------------------------|
| Required features present | 25% | At least one non-default plane, one sweep **or** loft, and one pattern — each genuinely load-bearing, not bolted on |
| Parametric rebuild | 35% | Changing the one nominated driving dimension cleanly rebuilds the whole part; **zero red features** across the tested range |
| Reference quality | 20% | Features reference named planes/axes and variables, not magic numbers or fragile faces; you can justify each reference |
| Tree hygiene | 10% | Every feature, plane, axis, and variable renamed by its job; logical order; folders where helpful |
| Documentation | 10% | A short written walkthrough: the nominated driving dimension, the range tested, and a one-line rebuild confirmation |

A part that's beautiful but turns red on the first edit scores *worse* than a plain part that flexes cleanly. In CAD, robustness is the craft.

## What it sets up

The discipline here — non-default plane + multiplier + variable-driven rebuild — is exactly what the **mini-project** asks you to add to your running part this week, and it's the foundation for **Week 5's Configurations** (one model, a family of sizes). Nail the challenge and the mini-project's rebuild test becomes routine.
