# Exercise 2 — Constraint Drills

**Goal:** Build constraint fluency. Six short, numbered drills, each isolating one or two geometric constraints. Every drill ends **fully defined** (all geometry black) using the **minimum** number of dimensions — the rest of the geometry is held by *relationships*. This is a modeling task, not code: do each drill in OnShape by hand.

**Estimated time:** 45 minutes (about 7 minutes per drill).

---

## How to run each drill

- Create **one** Document named `C12-W1-Ex2-Drills`. Put each drill in its **own sketch** on the **Top** plane (six sketches in one Part Studio — exit one, start the next). Rename each sketch `Drill 1` … `Drill 6`.
- Anchor each drill to the **origin**.
- End each one **all black**. Run the drag test before moving on.
- After each drill, note the **dimension count** you used. Lower is better — that's the point.

---

## Drill 1 — Horizontal / Vertical (a clean L-bracket profile)

**Build:** An L-shaped (6-sided) profile, like the cross-section of an angle bracket.

1. Start a sketch on Top. Using the **line** tool, draw a closed 6-sided L-shape starting *at the origin*. Don't fuss over angles — draw it roughly.
2. The lines will be slightly off-square (blue, various angles).
3. Apply **horizontal** to each horizontal-ish line and **vertical** to each vertical-ish line until all six are axis-aligned. (Watch the inference glyphs — many will already be horizontal/vertical from drawing.)
4. Confirm the start point is **coincident** with the origin.
5. **Dimensions (target: 4):** overall width, overall height, the horizontal leg thickness, the vertical leg thickness.

**Outcome:** All-black L-profile, fully defined with **4 dimensions** and a stack of horizontal/vertical + coincident constraints.

---

## Drill 2 — Parallel + Perpendicular (a parallelogram → rectangle)

**Build:** Start with a slanted parallelogram, then square it up with constraints — *without* dimensioning angles.

1. New sketch. Draw a 4-sided closed shape, deliberately slanted (a parallelogram), one corner on the origin.
2. Apply **parallel** between the two pairs of opposite sides (top∥bottom, left∥right). It stays a parallelogram but the opposite sides now track each other.
3. Apply **perpendicular** between one horizontal side and one vertical side. The parallelogram snaps into a true rectangle — and stays one.
4. **Dimensions (target: 2):** one width, one height.

**Outcome:** A rectangle held square by **perpendicular**, not by a 90° dimension. Edit the width — it stays a rectangle. Note: you used **zero angular dimensions**. That's the lesson — `perpendicular` beats "90°."

---

## Drill 3 — Equal (a true square from one dimension)

**Build:** A square locked with a single dimension.

1. New sketch. Draw a rough 4-sided closed shape near the origin, one corner anchored to the origin.
2. Make it a rectangle first: **perpendicular** between adjacent sides (or horizontal/vertical on all four).
3. Apply **equal** between one horizontal side and one vertical side. Now width = height permanently.
4. **Dimensions (target: 1):** dimension **one** side `40 mm`.

**Outcome:** A 40×40 square, fully defined with **one** dimension. Change the `40` to `60` — it grows but *stays square* forever, because squareness is a constraint, not two numbers you keep in sync. This is the single most important drill of the week.

---

## Drill 4 — Concentric (a washer)

**Build:** Two circles sharing a center — a flat washer profile.

1. New sketch. Draw an **outer** center-point circle with its center on the **origin** (coincident).
2. Draw an **inner** circle anywhere inside it (blue, off-center).
3. Apply **concentric** between the two circles. The inner circle snaps to share the outer's center (= the origin).
4. **Dimensions (target: 2):** outer **diameter** `30 mm`, inner **diameter** `12 mm`. (Dimension circles by ⌀, not radius — that's how holes are specified.)

**Outcome:** A fully-defined washer with **2 dimensions**. The hole can *never* drift off-center because **concentric** holds it. Change the outer ⌀ — the hole stays centered.

---

## Drill 5 — Symmetric (a symmetric hexagon-ish bracket)

**Build:** A profile that's mirror-symmetric left-to-right, built by drawing half and mirroring intent with a `symmetric` constraint.

1. New sketch. Draw a **construction** vertical centerline through the origin (toggle construction with `q`).
2. Draw a closed 6-point profile that's roughly symmetric about that centerline — say a "home plate" / pentagon-ish bracket shape, anchored to the origin.
3. For each pair of points/lines that should mirror, select the pair **plus the centerline** and apply **symmetric**. Work through every pair.
4. Constrain the overall height (the points on the centerline) with vertical/coincident as needed.
5. **Dimensions (target: 3):** overall width, overall height, and one feature offset. The symmetry handles the matching of left and right.

**Outcome:** A symmetric bracket fully defined with **3 dimensions**. Edit the width — both sides move together because **symmetric** is doing the work. Drawing half + mirroring intent is the senior pattern for any symmetric part.

---

## Drill 6 — Midpoint + Coincident (a centered notch)

**Build:** A rectangle with a notch centered exactly on its top edge.

1. New sketch. Draw a centered rectangle on the origin (center-point rectangle). Dimension width `60 mm`, height `30 mm`. (2 dimensions; fully defined rectangle.)
2. On the **top** edge, cut a small notch: draw three short lines forming a rectangular notch *into* the top edge, splitting the top edge into two segments.
3. Constrain the notch's two vertical sides **vertical** and its bottom **horizontal**.
4. Center the notch on the top edge: select the notch's center point (or a midpoint of its bottom) and apply **midpoint** to the top edge — or apply **symmetric** about the plate's vertical centerline.
5. **Dimensions (target: 2 more):** notch width and notch depth.

**Outcome:** A notched plate, the notch perfectly centered by **midpoint**/**symmetric**, fully defined with **4 dimensions total**. Change the plate width — the notch stays centered.

---

## Acceptance criteria

You can mark this exercise done when:

- [ ] All six drills live in one Document, each in its own renamed sketch.
- [ ] **Every** drill is fully defined — all geometry **black**, status bar "Fully defined."
- [ ] Each drill is anchored to the **origin**.
- [ ] You used the **minimum** dimensions per drill (Drill 3 with exactly **one**; Drill 4 with exactly **two**).
- [ ] You applied, across the six drills, at least: horizontal, vertical, parallel, perpendicular, equal, concentric, symmetric, midpoint, coincident.
- [ ] For at least two drills, you edited a driving dimension and confirmed the constrained relationship held (square stayed square; hole stayed centered).
- [ ] You can state, for each constraint you used, **which degrees of freedom it removed**.

---

## Stretch

- Re-do Drill 1 (the L-bracket) using **symmetric** about a 45° construction line — does the L have a symmetry you can exploit? (Trick question: a plain L doesn't, but a **T** does — try a T-profile instead and mirror it.)
- In Drill 4, add a **bolt-circle**: three small ⌀4 holes, equally spaced on a construction circle concentric with the washer, all made **equal**. (Equal spacing by hand is fiddly — note how much you'd want a *circular pattern*, which arrives in Week 3.)
- Take any drill and deliberately **over-define** it (add a redundant dimension). Watch it turn red/yellow. Read OnShape's conflict message, then delete the offending dimension. Knowing how to *read and clear* a conflict is as important as avoiding one.

---

When the constraints feel automatic, move to [Exercise 3 — Arc and slot lever profile](exercise-03-arc-and-slot-profile.md).
