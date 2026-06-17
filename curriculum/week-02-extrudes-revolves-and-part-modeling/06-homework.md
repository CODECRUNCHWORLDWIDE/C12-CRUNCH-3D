# Week 2 Homework

Six modeling problems that revisit the week's features. The full set should take about **4.5 hours**. Work in your `C12-Week2` OnShape Document — create a **new Part Studio per problem** (name them `HW1` … `HW6`) so each produces a part you can point to later. Share the single Document link when you're done.

> These are **CAD tasks, not code.** Each one is built by hand in OnShape. Each problem includes a **problem statement**, **acceptance criteria** so you know when you're done, a **hint** if you get stuck, and an **estimated time**.

---

## Problem 1 — Spacer with a counterbore

**Problem statement.** Model a cylindrical standoff spacer: ⌀16 mm outer, **20 mm** tall, with an **M4 clearance** through-hole on the axis and a **⌀8 mm × 3 mm** counterbore on the top. Build it however you like (extrude a circle, or revolve a half-section), but the through-hole must be a **Hole feature**, not a sketched cut.

**Acceptance criteria.**

- A single solid in `HW1`: ⌀16 × 20 mm, M4 clearance through-hole, ⌀8 × 3 mm counterbore on top.
- The hole is a **Hole feature**, located concentric with the cylinder (point coincident with origin).
- All sketches fully defined (black); every feature renamed.

**Hint.** Extrude a ⌀16 circle 20 mm (New, Blind). Then a points sketch with one point on the origin on the top face. Hole → Counterbore, M4 clearance, Through all; OnShape can do the bore + counterbore in one Hole feature.

**Estimated time.** 25 minutes.

---

## Problem 2 — Revolved pulley with a partial relief

**Problem statement.** Revolve a **V-groove pulley**: ⌀50 mm outer, **16 mm** wide, with a 60° V-groove cut into the rim, and a ⌀10 mm bore through the hub. Then add **one partial-revolve relief** — a 90° pie-slice pocket cut into one face of the hub (a balancing relief), using a **partial Revolve-Remove**.

**Acceptance criteria.**

- A revolved solid in `HW2` with a recognizable V-groove rim and a ⌀10 mm bore.
- The half-section is **fully defined** and lies **entirely on one side of the axis**.
- A **partial revolve (one-direction, 90°) Remove** relief is present.
- Rebuild test: change outer diameter ⌀50 → ⌀60; no red features.

**Hint.** Draw the half-section with the V-groove as a triangular notch in the rim. For the relief, sketch a small profile on a plane through the axis and Revolve-Remove it 90° (One direction). Keep the bore as part of the main half-section or as a separate Hole.

**Estimated time.** 50 minutes.

---

## Problem 3 — The end-condition comparison

**Problem statement.** Build **one** part that uses **at least three different end conditions** in a way you can defend. For example: a base block (Blind), a boss that reaches a top reference plane (Up to face), and a through-bolt hole (Through all). In your notes, write one sentence per feature stating *why* that end condition is the robust choice.

**Acceptance criteria.**

- A single part in `HW3` using at least **three distinct end conditions** (from: Blind, Symmetric, Through all, Up to next, Up to face, Up to vertex, Up to part).
- A short note (Document notes or text) justifying each end-condition choice in one sentence.
- Rebuild test: change the overall height ±20%; the **Up to…** features track the geometry, no red features.

**Hint.** The "Up to face" feature is the star here — make a boss that must always reach a top plate, and prove that raising the plate raises the boss with it (whereas a Blind boss would fall short).

**Estimated time.** 45 minutes.

---

## Problem 4 — Shelled enclosure lid

**Problem statement.** Model a **lid** that mates to the enclosure base from Exercise 3 (90 × 60 mm footprint, 6 mm corner radius). The lid is a **90 × 60 × 10 mm** rounded box, **shelled to 2.5 mm** with the **bottom open**, with **four ⌀3.4 mm clearance holes** positioned to line up with the base's M3 bosses (10 mm in from each corner). Add a small **lip** (a 1.5 mm recessed rim on the underside) so it nests into the base.

**Acceptance criteria.**

- A shelled lid in `HW4`: same footprint and corner radius as the Ex3 base, 2.5 mm wall, bottom open.
- Four **M3 clearance** holes aligned to the base's boss positions.
- A nesting **lip** on the underside (a recessed rim or stepped edge).
- Rebuild test: change wall thickness 2.5 → 3 mm; no red features; lip survives.

**Hint.** Build the box, fillet the outer corners (before shell), shell removing the bottom. The lip is a thin Remove-extrude (or a stepped outer edge) on the underside perimeter. Match hole positions to Ex3 by reusing the same 10 mm corner inset.

**Estimated time.** 50 minutes.

---

## Problem 5 — Break a part on purpose, then fix it

**Problem statement.** Take **any** part you've built this week. Deliberately make an edit that turns a feature **red** (e.g. set a shell thicker than a wall, set a fillet bigger than its edge can hold, delete a sketch a later feature references). Then **diagnose and repair** it using the rollback workflow. Document the failure and the fix.

**Acceptance criteria.**

- A note in `HW5` (Document notes or text) describing: the edit you made, the exact error message, which feature went red, *why* it broke, and the steps you took to fix it.
- A screenshot of the **red feature** and a screenshot of the **repaired** part.
- The part ends **green** (no red features).

**Hint.** The diagnostic loop is always the same: roll back until the red clears, look at the feature just below the bar, edit it (re-pick a reference, or relax a dimension), roll forward. The *understanding* of why it broke is the graded part, not just the fix.

**Estimated time.** 30 minutes.

---

## Problem 6 — Modeling reflection

**Problem statement.** Write a 300–400 word reflection in `HW6` (Document notes or a Markdown file) answering:

1. Which felt easiest this week: extrudes and Booleans, revolves, or the dress-up features (hole/fillet/chamfer/shell)? Which felt hardest? Why?
2. Describe one time a feature turned red this week. What caused it, and what did fixing it teach you about feature order or end conditions?
3. In your own words, why is "the part must rebuild cleanly when I change a dimension" a better standard than "the part looks right"?
4. What's one thing you want to learn next that this week didn't cover (patterns? assemblies? drawings?)?

**Acceptance criteria.**

- 300–400 words, each numbered question addressed in its own paragraph.
- Saved in the Document (notes) or as a file alongside your parts.

**Hint.** This is for *you*, not for a grade beyond completion. Be honest. Future-you, reading it before the Week 6 capstone, will be grateful you wrote down what actually tripped you up.

**Estimated time.** 30 minutes.

---

## Time budget recap

| Problem | Estimated time |
|--------:|--------------:|
| 1 | 25 min |
| 2 | 50 min |
| 3 | 45 min |
| 4 | 50 min |
| 5 | 30 min |
| 6 | 30 min |
| **Total** | **~3 h 50 min** |

---

## Grading rubric

| Criterion | Weight | What "great" looks like |
|----------|-------:|-------------------------|
| Features used correctly | 30% | Right operation, end condition, and hole type for each problem; Hole feature used where required |
| Sketch + feature hygiene | 20% | Every driving sketch fully defined (black); every feature renamed; short ordered trees |
| **Rebuild robustness** | 25% | Parts that name a rebuild test pass it with zero red features; Problem 3's "Up to…" features track geometry |
| Diagnosis (Problem 5) | 15% | The red-feature failure is correctly explained (cause + fix), not just patched |
| Reflection (Problem 6) | 10% | All four questions answered thoughtfully in the word count |

---

When you've finished all six, **create a Version** of the Document (`Week 2 homework`), confirm every part is green, and share the public link in your cohort tracker. Then open the [mini-project](./07-mini-project/00-overview.md) if you haven't already — the homework parts are good warm-up for it.
