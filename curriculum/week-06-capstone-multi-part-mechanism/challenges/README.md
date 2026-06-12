# Week 06 — Challenges

One challenge this week, and it is the whole point of the course: deliver the capstone live. No solution is provided — only acceptance criteria. The challenge subsumes the mini-project's build work and adds the *live delivery* bar: the reviewer opens your live model, drags it through its full range of motion, changes a driving variable to prove it rebuilds, reads your drawings, and checks your exports.

| # | File | What you prove | Est. time |
|---|------|----------------|-----------|
| 1 | [challenge-01-deliver-the-capstone-live.md](./challenge-01-deliver-the-capstone-live.md) | Deliver the original multi-part mechanism live in OnShape: full range of motion, parametric rebuild, complete drawing package, exports, and a defended design review. | The capstone itself (multi-day) |

## How it's assessed

This is the headline portfolio artifact, and it is assessed *live*, not from a static submission. A reviewer (a cohort lead, a peer panel, or a recorded camera) does the following, in order, and every step must pass:

1. **Opens your live OnShape Document** at the tagged `v1.0` Version and confirms the mechanism is present and clean (no red errors in the feature tree or the mate list).
2. **Drags the mechanism through its full range of motion** and confirms it articulates with the intended degrees of freedom and never interferes — including at the extremes of travel.
3. **Changes a key driving variable** (or switches a Configuration) and confirms the whole assembly rebuilds with zero errors and still moves.
4. **Reads your drawing package** — the assembly drawing with its balloon-and-BOM, and at least one key part drawing with a section view, full dimensioning, tolerances on the fits, and one GD&T frame — and judges whether a machinist could build a part from it.
5. **Inspects your exports** — opens the STEP and the STL in a neutral viewer and confirms they are complete and at the correct scale.
6. **Runs the design review** — you present, you drag a motion, you change a variable on camera, you answer the senior-designer questions (Lecture 1, §1.4), and the reviewer produces a risk list tagged accept / fix-now / fix-later.

The single hardest gate is the **live parametric rebuild**: a mechanism that throws a red error when a driving variable changes, or breaks in one Configuration, does not pass — regardless of how good the render looks. Build the rebuild discipline in from day one: every working session this week, change a driving variable and confirm the clean regen before you stop. The reviewer will, and a model that only works at the one set of dimensions you happened to model it at is a fragile shape, not a parametric mechanism.

This challenge maps to the **Capstone delivery** line of the assessment, plus the **mock review** and the **drawing-package** components. Treat it like a release, not an assignment.
