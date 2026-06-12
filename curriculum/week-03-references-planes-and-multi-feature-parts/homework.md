# Week 3 Homework

Six practice problems that revisit the week's topics in OnShape. The full set should take about **5.5 hours**. Work in a Document named `C12-Week3-Homework` and create a **Version** after each problem so you can point to your progress later. Everything here is modeling — **no code**.

Each problem includes:

- A short **problem statement**.
- **Acceptance criteria** so you know when you're done.
- A **hint** if you get stuck.
- An **estimated time**.

A grading rubric for the whole set is at the bottom.

---

## Problem 1 — Build five plane types

**Problem statement.** In a Part Studio named `HW1-Planes`, model a simple 50 × 50 × 10 mm base block centered on the origin, then create **five different construction planes**, one of each type, each named by its job:

1. An **Offset** plane (parallel to Top, driven by a variable `#gap`).
2. An **Angle** plane (tilted off Front, hinged on an edge/axis).
3. A **Point–normal** plane (at a corner vertex, normal = an edge).
4. A **Mid plane** (between two faces of the block).
5. A **Three-point** plane (through three vertices of the block).

Put a tiny sketch on each one to prove a sketch can live there.

**Acceptance criteria.**

- All five planes built, each a *different* type, each **renamed by its job** (no `Plane 1`).
- A sketch on each plane.
- Changing `#gap` moves the offset plane and its sketch; nothing turns red.
- Version created.

**Hint.** The plane *type* dropdown is the first field in the Plane dialog. If three-point won't resolve, make sure your three points are non-collinear (not on one line).

**Estimated time.** 40 minutes.

---

## Problem 2 — A parametric bolt-circle flange

**Problem statement.** In `HW2-Flange`, model a Ø120 × 10 mm flange disc with a Ø50 bore, then add a **circular pattern** of M6 clearance holes on a bolt circle. Drive the **bolt count** with `#bolts` and the **bolt-circle diameter** with `#bcd`. The pattern must spin about a **named construction axis** through the bore.

Then prove parametric: change `#bolts` from 6 → 8 → 4, and `#bcd` from 90 → 100 mm. Nothing may turn red, and the holes must re-divide the circle evenly each time.

**Acceptance criteria.**

- A `Bore axis` (named construction axis) through the bore.
- One seed Hole feature; a circular pattern named `Bolt ring`, **360° / equal spacing**, count = `#bolts`.
- Seed positioned at `#bcd / 2` radius.
- All four parameter changes rebuild clean (document the values you tried).
- Version created.

**Hint.** Build the **Axis** off the bore's cylindrical face first; the circular pattern then references the named axis, not an inference.

**Estimated time.** 50 minutes.

---

## Problem 3 — A swept hook

**Problem statement.** In `HW3-Sweep`, model a wall hook: sketch a path (a vertical mounting segment, a horizontal arm, and a J-curve at the end — tangent throughout, fully defined) on the Front plane, build a **point–normal plane** at the path start, sketch a Ø6 mm round profile there, and **sweep** it. Then flex the profile diameter `#hookDia` and find the diameter at which the sweep **self-intersects** on the J-curve's inner radius.

**Acceptance criteria.**

- A fully-defined, tangent path; a `Profile plane` (point–normal) at the path start; a clean `Hook` sweep.
- `#hookDia` driven by a variable.
- You document the diameter where the sweep first self-intersects (the geometric limit), with a one-line explanation of *why* (section can't make a turn tighter than itself).
- Version created.

**Hint.** Make the circle's center **coincident** with the path's start vertex, and the profile plane **point–normal** with the normal = the path's first segment. If the sweep skews at the start, the plane isn't perpendicular to the path.

**Estimated time.** 50 minutes.

---

## Problem 4 — A symmetric bracket via mirror

**Problem statement.** In `HW4-Mirror`, model the **left half** of a symmetric U-bracket — one arm with a boss, a hole, and a fillet — referencing the origin so the part is centered. Then **mirror** the arm features across the symmetry plane to create the right half. Prove the link: change the left arm's hole diameter and confirm the right arm follows.

**Acceptance criteria.**

- The left arm modeled centered on the origin (so an origin plane *is* the symmetry plane).
- A **feature mirror** across an origin/mid plane creating the right arm.
- Editing the left hole diameter updates the mirrored right hole (document this).
- Every feature renamed; seed and mirror grouped into a folder.
- Version created.

**Hint.** If no origin plane lands on the symmetry line, build a **Plane → Mid plane** between the two outer arm faces and mirror across that.

**Estimated time.** 45 minutes.

---

## Problem 5 — A square-to-round lofted spout

**Problem statement.** In `HW5-Loft`, **loft** a transition: a 40 × 40 mm square on Top, a 35 × 35 mm rounded-square on an offset plane at 30 mm, and a Ø30 circle on an offset plane at 60 mm — a **three-profile** loft. Pin connection points so it doesn't twist. Then shell it to a 2 mm wall (Week 2 skill) to make a hollow spout.

**Acceptance criteria.**

- Three profiles on three correctly-named offset planes.
- A twist-free **loft** through all three (connection points pinned).
- A **Shell** to 2 mm wall.
- Changing `#loftHeight` (the top offset) rebuilds clean.
- Every plane/feature renamed; Version created.

**Hint.** Pick the profiles in stacking order (bottom → middle → top). If it spirals, drag the connection dots so a square corner maps to the matching point on each profile above it.

**Estimated time.** 50 minutes.

---

## Problem 6 — Feature-tree audit & design-intent note

**Problem statement.** Take **any one** of Problems 2–5 and write a 250–350 word design-intent note (in the Document notes or a Markdown file `notes/hw-design-intent.md`) answering:

1. Walk your feature tree top to bottom: name each feature/plane/axis and state **what it references**.
2. Identify the **one feature whose position in the tree matters most** — what breaks if you move it earlier or later?
3. Name **one reference you rejected** while building (e.g. a face you almost sketched on) and why you chose a different reference instead.
4. State the **rebuild test** you ran on that part: which dimension(s)/count you flexed, the range, and whether it stayed clean.

**Acceptance criteria.**

- The note exists, 250–350 words, each numbered question addressed.
- It refers to *your actual* renamed features (not generic placeholders).
- Committed/saved alongside the model.

**Hint.** This is the same thinking the mini-project walkthrough requires — do it well here and you can reuse the muscle memory there. Honesty beats polish: if a reference choice was a mistake you fixed, say so.

**Estimated time.** 35 minutes.

---

## Time budget recap

| Problem | Estimated time |
|--------:|--------------:|
| 1 | 40 min |
| 2 | 50 min |
| 3 | 50 min |
| 4 | 45 min |
| 5 | 50 min |
| 6 | 35 min |
| **Total** | **~4 h 30 min** |

(The remaining hour of the week's homework budget is slack for the inevitable "wait, why did that turn red" debugging — embrace it; that's where the learning is.)

---

## Grading rubric

| Criterion | Weight | What "great" looks like |
|----------|-------:|-------------------------|
| Correct features built | 30% | Each problem's required feature (plane types, circular pattern, sweep, mirror, loft) is present and correct |
| Parametric robustness | 30% | Variables drive counts/offsets; the flex tests in P2–P5 rebuild with **zero red features**; limits documented where relevant |
| Reference quality | 15% | Features ride named planes/axes, not magic numbers or fragile faces; circular pattern uses a named axis |
| Sketch discipline | 10% | Every driving sketch is **black** (fully defined) |
| Tree hygiene | 10% | Every feature/plane/axis/variable renamed by its job; folders where helpful |
| Design-intent note (P6) | 5% | The note is specific to the student's actual tree and shows real reasoning about references and order |

**Auto-deductions** (same standard as the mini-project): any `Plane 1 / Pattern 2 / Sweep 1` left unrenamed; any driving sketch left blue (under-defined); any required flex test that turns a feature red and is left unfixed.

When you've finished all six, create a final **Version** named `Week 3 homework complete`, share the Document, and post the link in your cohort tracker. Then open the [mini-project](./mini-project/README.md) and promote your running part.
