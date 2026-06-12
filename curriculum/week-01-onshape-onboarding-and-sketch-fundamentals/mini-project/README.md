# Mini-Project — The Running Project: Master Sketch

> Begin the project you will carry through all six weeks of C12. This week you choose a simple flat part — a **hobby name plate** or a **flat washer-style part** — and deliver **only its fully-defined master sketch** (no 3D yet) plus a short written walkthrough of every constraint and dimension you used and why the sketch is fully defined.

This is the first installment of a sequential, compounding project. **Week 2** extrudes this exact sketch into a solid. **Week 3** adds patterned/mirrored features and a feature on a non-default plane. **Week 4** mates a second part to it. **Week 5** parameterizes and draws it. **Week 6** folds it into the capstone mechanism. So the sketch you build this week is load-bearing for five more weeks — invest in making it clean, fully defined, and minimally dimensioned.

**Estimated time:** ~8 hours (split across Thursday, Friday, Saturday in the suggested schedule), including the walkthrough write-up.

---

## Choose your part

Pick **one** (or design your own flat part of comparable complexity — get it approved if it's wildly different):

### Option A — Hobby name plate
A flat rectangular plate with rounded corners that will eventually carry your name or a hobby logo as cut/engraved text. This week: just the **outer profile** plus **two mounting holes** and at least **one internal cut-out region** (a rounded window or a slot) so the sketch has more than four lines. Good if you like the idea of a desk nameplate you 3D-print or laser-cut later.

### Option B — Flat washer-style part
A flat disk-shaped spacer/washer with a center bore and a **bolt-circle of smaller holes** (you'll place them by hand this week; circular-pattern them in Week 3). Good if you prefer round, mechanical geometry.

Either way the part must be **flat** (we don't extrude until Week 2) and must contain enough features to exercise the week's constraints — at minimum: an anchored outer profile, at least one circular feature (hole/bore), and at least one relationship that lets you dimension *once and apply many* (`equal`, `concentric`, or `symmetric`).

---

## What you deliver this week

1. A **Document** named `C12-Project-<yourname>` containing **one Part Studio** with **one sketch** (your master profile).
2. The sketch is **fully defined** — all geometry black, status bar "Fully defined," zero conflicts.
3. A named **Version** of the Document tagged `w1-master-sketch`.
4. A **written walkthrough** (a Markdown file `WALKTHROUGH.md` in your course repo, ~400–600 words) documenting every constraint and dimension and *why the sketch is fully defined*.

That's it. **No 3D this week.** The discipline is to make the sketch perfect before anything is extruded. The temptation to extrude will be strong; resist it.

---

## Rules

- **Master profile must anchor to the origin.** Not floating in space. A `coincident` to the origin somewhere is mandatory.
- **Fully defined, minimum dimensions.** Use constraints (`equal`, `concentric`, `symmetric`, `tangent`, `parallel`, `perpendicular`, `midpoint`) wherever a relationship can replace a number. We grade on the constraint-to-dimension ratio.
- **Holes dimensioned by diameter (⌀)**, not radius.
- **One sketch, one closed (or properly nested) profile.** Outer boundary plus internal hole/cut-out loops are fine; stray open lines are not.
- **No 3D features.** No extrude, no revolve. The Parts list stays empty this week — that's correct.
- **Units: millimeters** (unless your drawing is explicitly imperial — then inches, consistently).

---

## Acceptance criteria

- [ ] A Document `C12-Project-<yourname>` with a single Part Studio and a single master sketch.
- [ ] The sketch is **fully defined**: all geometry **black**, status bar reads "Fully defined," **no** red/yellow conflicts.
- [ ] The sketch is **anchored to the origin** (verifiable: drag-test the whole sketch — nothing moves).
- [ ] The part has at least: an outer profile, **one** circular feature, and **one** "dimension-once" relationship (`equal`/`concentric`/`symmetric`).
- [ ] You used the **minimum** reasonable number of driving dimensions; redundant numbers are replaced by constraints.
- [ ] You changed **one** key driving dimension, confirmed the sketch rebuilt cleanly and stayed fully defined, then restored it. (Document this in the walkthrough.)
- [ ] The sketch is **renamed** meaningfully (e.g., `Master profile`), not "Sketch 1."
- [ ] A named **Version** `w1-master-sketch` exists.
- [ ] `WALKTHROUGH.md` exists and meets the spec below.
- [ ] **Zero `Fix` constraints** used as a crutch. (Anchoring to the origin and using real relationships only.)

---

## The walkthrough (`WALKTHROUGH.md`)

This document is half the grade. It teaches the reader — and future-you — *how and why* your sketch holds together. Required sections:

1. **The part.** One paragraph: which option you chose and what the finished part will eventually be.
2. **Anchoring.** How you tied the sketch to the origin and why.
3. **Constraint inventory.** A bulleted list of *every* geometric constraint you used (coincident, equal, concentric, symmetric, tangent, etc.), and for each, **what it does in your sketch** and **which degrees of freedom it removed**.
4. **Dimension inventory.** A bulleted list of *every* driving dimension, the value, and **why that measurement genuinely needs to be a number** (rather than a relationship).
5. **Why it's fully defined.** A short argument: "every entity is black because the following DOF are all removed…" Explain the bookkeeping in plain language.
6. **Robustness demonstration.** State which dimension you changed, what you changed it to, and confirm the sketch stayed fully defined and rebuilt cleanly. (A before/after screenshot is ideal.)
7. **Minimum-dimension reflection.** How many dimensions did you use? Could you have used fewer? Where did a constraint save you a number?

Write it in plain English, as a handoff to a developer who's never seen your model. If they can read it and understand exactly why your sketch is robust, it's doing its job.

---

## Suggested order of operations

### Phase 1 — Choose and rough out (~1h)
Pick Option A or B (or get a custom one approved). Sketch the part on paper first — mark the dimensions that *genuinely matter* (the ones a customer or a mating part would specify) versus the ones that are just "make these match" (those become constraints). This pencil step is worth doing; it's where the minimum-dimension scheme is actually decided.

### Phase 2 — Document & anchor (~0.5h)
Create the Document, set mm units, start a sketch on the Top plane, lay in any construction centerlines, and anchor your first geometry to the origin.

### Phase 3 — Outer profile (~1.5h)
Build the outer boundary with the right tools (rectangle/circle/slot, tangent arcs for rounds). Constrain it (horizontal/vertical, tangent, symmetric). Dimension only the overall sizes that matter. Get the outer loop **black** before moving inward.

### Phase 4 — Internal features (~2h)
Add holes / bores / cut-outs. Use `concentric`, `equal`, and `symmetric` so you dimension one feature and propagate to the rest. Dimension diameters with ⌀. Position one of each repeated feature and mirror the rest.

### Phase 5 — Drive out the blue (~1h)
Run the drag test relentlessly. Hunt every remaining blue entity. Get to "Fully defined." Turn on **Show constraints** and verify the geometry is held by relationships, not just numbers.

### Phase 6 — Robustness + Version (~0.5h)
Change one key driving dimension; confirm clean rebuild; restore it. Rename the sketch. Create the `w1-master-sketch` Version.

### Phase 7 — Walkthrough (~1.5h)
Write `WALKTHROUGH.md` per the spec above. Take the screenshots. This is where you cement your understanding — don't rush it.

---

## Rubric

| Criterion | Weight | What "great" looks like |
|----------|-------:|-------------------------|
| Fully defined | 25% | All geometry black, "Fully defined" status, zero conflicts, anchored to origin |
| Minimum dimensions / constraint use | 20% | Constraints carry the relationships; no redundant numbers; `equal`/`concentric`/`symmetric` used well |
| Geometry quality | 15% | Clean closed profile, right tools used, no stray entities, sensible plane choice |
| Robustness | 15% | The key-dimension change rebuilds cleanly and stays fully defined |
| Walkthrough quality | 20% | All seven sections present; a stranger can understand why the sketch is robust |
| Cloud hygiene | 5% | Sketch renamed, named Version created, Document sensibly named |

---

## What this prepares you for

- **Week 2** extrudes *this* master sketch into a real solid part, adds a mounting hole and fillets/chamfers for manufacturability. A clean, fully-defined sketch makes that trivial; a sloppy one makes it painful.
- **Week 3** promotes the part to multi-feature: patterned/mirrored features and a feature on a non-default plane, with a documented design-intent ordering of your feature tree.
- **Week 4** mates a second component to your part so a joint articulates.
- **Week 5** parameterizes the part with Variables and a Configurations table and produces a real drawing with a BOM.
- **Week 6** folds it into an original multi-part mechanism for the capstone.

The Document you create this week is the *same Document* you carry to the capstone. Name it well and version it deliberately — you'll live in it for six weeks.

---

## Submission

When done:

1. Create the `w1-master-sketch` **Version**.
2. Share the Document read-only with your reviewer (or export screenshots of the fully-defined sketch, with constraints shown).
3. Commit `WALKTHROUGH.md` (and screenshots) to your course repo for Week 1.
4. Post your Document link in your cohort tracker. You built the foundation the next five weeks stand on — show it.
