# Week 1 Homework

Five practice tasks that revisit the week's topics. The full set should take about **6 hours**. Do all modeling in **one** Document named `C12-W1-Homework` (one sketch per task, on the Top plane, renamed `HW1`…`HW5`), except where a task says otherwise. There is no code — every task is a precise OnShape modeling/sketching task.

Each task includes a **problem statement**, **acceptance criteria**, a **hint**, and an **estimated time**. Capture a screenshot of each finished sketch (with the "Fully defined" status visible) for submission.

---

## Task 1 — OnShape orientation audit

**Problem statement.** Create the `C12-W1-Homework` Document. Then write a short file `NOTES.md` (in your course repo) answering, in your own words:

1. What is the difference between a **Document**, a **Part Studio**, and an **Assembly**?
2. Where do you set the **workspace units**, and what did you set yours to?
3. What does the **Feature tree** contain *before* you've drawn anything? (Name the four items.)
4. What is a **Version**, how is it different from the live workspace, and why would you create one?
5. There is no Save button. In one sentence, explain how your work is preserved.

**Acceptance criteria.**
- `NOTES.md` exists with all five answers in your own words.
- The Document exists with millimeter units.

**Hint.** Re-read Lecture 1 §1, §8, and §10. The four Feature-tree items before you draw are the **Origin**, **Top**, **Front**, and **Right** planes.

**Estimated time.** 25 minutes.

---

## Task 2 — Fully define a bracket profile with minimum dimensions

**Problem statement.** In sketch `HW2` (Top plane), reproduce this flat bracket:

- A rectangular body **100 mm wide × 40 mm tall**, bottom-left **anchored to the origin**.
- Two **⌀8 mm** mounting holes, **15 mm** from each end and **vertically centered** on the 40 mm height.
- The two holes must be tied with an **equal** constraint and the **same** vertical-center relationship — so you dimension hole size once and hole height once.

Fully define it using the **minimum** dimensions.

**Acceptance criteria.**
- Sketch `HW2` is **fully defined** (all black, "Fully defined").
- Both holes are ⌀8 via a single **equal** constraint; changing one changes both.
- Anchored to the origin.
- You used **5 dimensions or fewer** (width, height, hole ⌀, hole vertical position, hole horizontal position — and the second hole's horizontal position can be a 6th *or* you can mirror it for 5). Note your count.

**Hint.** Use a **symmetric** constraint about a vertical construction centerline to place the second hole, so you dimension only one hole's horizontal position. Dimension holes by **diameter (⌀)**.

**Estimated time.** 45 minutes.

---

## Task 3 — Constraint substitution challenge

**Problem statement.** In sketch `HW3`, draw a slanted parallelogram (4 closed sides, one corner on the origin). Then, **without using any angular dimension**, turn it into a true **rectangle** and fully define it. You may use only: horizontal, vertical, parallel, perpendicular, and at most **two** linear dimensions.

Then, in your `NOTES.md`, list *which constraints* removed the angular freedom and explain why a `perpendicular` constraint is better than a `90°` dimension.

**Acceptance criteria.**
- Sketch `HW3` is a rectangle, **fully defined**, with **zero angular dimensions** and **≤2 linear dimensions**.
- `NOTES.md` explains the constraint substitution.

**Hint.** `parallel` on the two pairs of opposite sides + one `perpendicular` between adjacent sides squares it up. The angle is then *implied*, not dimensioned. A `perpendicular` constraint survives a resize; a `90°` dimension is just an editable number that could be changed by accident.

**Estimated time.** 40 minutes.

---

## Task 4 — Concentric washer with a parametric edit

**Problem statement.** In sketch `HW4`, build a flat washer profile: an outer circle ⌀**36 mm** and an inner hole ⌀**16 mm**, both centered on the **origin**, held together with a **concentric** constraint (not just two coincident-to-origin circles — use concentric so you can *see* the relationship in Show constraints).

Then perform a **parametric edit**: change the outer ⌀ to **50 mm**, screenshot the result (hole must stay centered), then restore to 36. Document the before/after in `NOTES.md`.

**Acceptance criteria.**
- Sketch `HW4` fully defined, **2 dimensions** (the two diameters), one **concentric** constraint visible.
- Screenshots of the ⌀36 and ⌀50 states; hole stays centered in both.
- Restored to ⌀36.

**Hint.** Draw the outer circle on the origin, draw the inner anywhere, then select both and apply **concentric**. Dimension by ⌀, not radius.

**Estimated time.** 35 minutes.

---

## Task 5 — Lever profile with tangent arcs and a slot

**Problem statement.** In sketch `HW5`, build a simplified version of Exercise 3's lever **from memory** (don't copy the exercise step-by-step):

- A pivot boss centered on the origin: ⌀**28** outer, ⌀**10** pivot hole, **concentric**.
- A body **18 mm** wide, **tangent** to the boss and **symmetric** about a horizontal construction centerline.
- A **slot** at the far end, **8 mm** wide, **20 mm** long, on the centerline, with the pivot-to-slot center distance **75 mm**.

Fully define it. Then change the **75 mm** reach to **100 mm**, confirm a clean rebuild, and restore it.

**Acceptance criteria.**
- Sketch `HW5` is **one closed profile**, **fully defined**, anchored to the origin.
- Uses **concentric**, **tangent**, **symmetric**, and a slot.
- **6 dimensions or fewer** (⌀28, ⌀10, body width 18, slot width 8, slot length 20, reach 75).
- The 75→100 reach edit rebuilt cleanly (note it in `NOTES.md`).

**Hint.** Use the **slot tool** (it arrives mostly constrained), make body edges **tangent** to the boss circle, and **symmetric** about the construction centerline so one width dimension does the job. Re-read Exercise 3 only if you're stuck for more than 10 minutes.

**Estimated time.** 1 hour 15 minutes.

---

## Time budget recap

| Task | Estimated time |
|-----:|---------------:|
| 1 | 25 min |
| 2 | 45 min |
| 3 | 40 min |
| 4 | 35 min |
| 5 | 1 h 15 min |
| **Total** | **~4 h** (allow 6 h with screenshots, NOTES.md, and re-tries) |

---

## Grading rubric

Submit your Document (shared read-only or as screenshots) plus `NOTES.md`. Graded out of **100**.

| Criterion | Points | What earns full marks |
|-----------|-------:|-----------------------|
| All five sketches **fully defined** | 30 | Every sketch all-black, "Fully defined," no conflicts, anchored to origin |
| **Minimum-dimension** discipline | 20 | Dimension counts at or below targets; constraints (`equal`, `concentric`, `symmetric`, `tangent`, `perpendicular`) carry relationships |
| Correct geometry & values | 20 | Each sketch matches the stated dimensions; holes dimensioned by ⌀ |
| **Parametric edits** demonstrated | 15 | Tasks 4 & 5 edits rebuilt cleanly, before/after captured, relationships held |
| `NOTES.md` quality | 10 | Clear, correct, in your own words; constraint-vs-dimension reasoning is sound |
| Cloud hygiene | 5 | Sketches renamed `HW1`…`HW5`, Document sensibly named, a Version created |

**Passing is 70.** If you score below 70, the most common reason is **leftover blue geometry** — run the drag test on every sketch before submitting. The second most common is **over-dimensioning** — go back and replace redundant numbers with `equal`/`symmetric`/`concentric` constraints.

When you've finished all five tasks, push your `NOTES.md` and screenshots, then start the [mini-project](./mini-project/README.md) — the master sketch you carry through the rest of C12.
