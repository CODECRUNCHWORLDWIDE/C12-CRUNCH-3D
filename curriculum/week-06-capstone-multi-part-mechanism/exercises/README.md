# Week 06 — Exercises

Three exercises, in the order you do them. They are the proof-of-readiness steps that gate the capstone delivery: you cannot model a mechanism whose motion you have not planned, you cannot defend an assembly whose degrees of freedom you have not verified, and you cannot ship a deliverable you have not configured, frozen, and exported. Do them against your *own* capstone OnShape Document (or a scaled-down practice version), not against a screenshot.

| # | File | What you do | Est. time |
|---|------|-------------|-----------|
| 1 | [exercise-01-concept-to-skeleton.md](./exercise-01-concept-to-skeleton.md) | Turn a concept sketch into a fully-defined, draggable kinematic skeleton and compute the degrees-of-freedom budget. | ~90 min |
| 2 | [exercise-02-mate-the-mechanism.md](./exercise-02-mate-the-mechanism.md) | Insert your parts and mate them so the mechanism has *exactly* the intended DOF, drags through its full range, and never interferes. | ~120 min |
| 3 | [exercise-03-configure-and-release.md](./exercise-03-configure-and-release.md) | Add a Variable Studio and a Configurations table, prove the rebuild across every configuration, tag a Version, and export STEP + STL. | ~120 min |

## Rules

- **Every exercise is a precise, numbered OnShape walkthrough.** There is no code this week — these are modeling, sketching, assembly, configuration, and export tasks. Follow the steps in order; each builds on the last.
- **Work in your own OnShape Document.** The free Public plan is sufficient for all three. Create one Document named `C12-Capstone-<your-mechanism>` and add tabs (Part Studios, an Assembly, a Drawing) as the exercises direct.
- **Use real units and real dimensions.** Set your Document units to millimeters before you start. Every dimension in these exercises is in mm.
- **Check the extremes, not just the home pose.** Exercise 2 in particular fails most students at the *ends* of travel; the steps make you check there on purpose.
- **Tag and check before you call it done.** Exercise 3 ends with a frozen Version and exports you have *opened in a neutral viewer* — an export you have not opened is not a deliverable (Lecture 2, §2.7).

## The bar

You have cleared the exercises when:

- Exercise 1 produces a kinematic skeleton sketch that is fully defined except for the single input DOF, drags to preview the motion without binding, and a DOF budget that computes to mobility = 1.
- Exercise 2 produces an assembly with exactly one grounded part, the intended degrees of freedom (verified by dragging and by the absence of red over-constraint warnings), and zero interferences at home, mid-travel, and both extremes (verified with Interference Detection).
- Exercise 3 produces a configured part that rebuilds cleanly across every configuration, a tagged `v1.0` Version, and a STEP + STL exported from that Version that both open clean in a neutral viewer at the correct scale.

Each exercise ends with explicit acceptance criteria. Do not move to the next until the current one's boxes are checked — the mini-project and Challenge 1 assume all three are done.
