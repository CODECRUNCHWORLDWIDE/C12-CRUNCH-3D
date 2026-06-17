# Week 5 — Exercises

Three focused OnShape drills. Each one should take 30–50 minutes. Do them in order; later ones reuse the part and the skills from earlier ones. These are CAD tasks — you'll be clicking in OnShape's Drawing, Variable, and Configurations tools, not writing code.

## Index

1. **[Exercise 1 — Your first drawing](./exercise-01-first-drawing.md)** — create a Drawing from a part, place ortho + iso views, dimension associatively, fill the title block, export a PDF. (~45 min)
2. **[Exercise 2 — Section views & GD&T](./exercise-02-section-views-and-gdt.md)** — add a full section view, place datums A/B/C, a flatness control, and a position feature control frame with a basic dimension. (~50 min)
3. **[Exercise 3 — Configurations: one part, three sizes](./exercise-03-configurations-part-family.md)** — add a Variable feature, then a Configurations table that drives one part into three sizes from a dropdown, and document it on one sheet. (~50 min)

## How to work the exercises

- Read the step list first, then do it in OnShape with the instructions beside you.
- **Do the clicks yourself.** Don't watch a video of someone else doing it — muscle memory in the Drawing and Configurations tools is the entire point of these drills.
- After each major step, look at what changed in the model/drawing and ask *why*. CAD rewards understanding the rebuild, not memorizing button locations.
- If you get stuck for more than 10 minutes, peek at the inline hints at the bottom of each file.
- Every drawing exercise must end with **no out-of-date views** and **zero overridden dimensions**. An overridden dimension is a bug this week.

## The completion checklist

You can mark the exercise set done when:

- [ ] Exercise 1: a drawing with front/top/right/iso views, fully dimensioned, title block filled from part properties, exported to PDF. No out-of-date banner.
- [ ] Exercise 2: a section view labeled `SECTION A-A`, datum symbols A/B/C placed, one flatness FCF, one position FCF referencing A|B|C, and the located feature's center given by a **basic** dimension (not a ±toleranced one).
- [ ] Exercise 3: a part driven by a Variable feature, a configuration list (`Small`/`Medium`/`Large`) that changes at least one dimension and switches the part number, verified by cycling through all three with no rebuild errors, documented on one sheet.
- [ ] Every dimension in every drawing is **associative** (reads from the model), confirmed by changing a model value and watching the drawing update.

There are no solution documents checked in — the course is open source and solutions live in learners' own OnShape accounts. After you finish, copy a *public link* to your document into your cohort tracker so a peer can review your drawing.
