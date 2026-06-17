# Exercise 1 — Offset & Angled Planes, and On-Face Sketching

**Goal:** Build offset and angled construction planes, sketch on each, then sketch on a part face — and *feel*, hands-on, the difference between a robust plane reference and a fragile face reference. By the end you'll have a small part whose features ride parametric planes and survive a dimension change.

**Estimated time:** 45 minutes.

**You'll use:** Plane (Offset, Angle), Sketch (on a plane and on a face), Extrude, inline variables, the rollback bar, the rebuild test.

---

## Setup

1. Sign in to OnShape: <https://cad.onshape.com/>.
2. Create a Document named `C12-Week3-Exercises` (or reuse it). Add a **Part Studio** tab named `Ex1 - Planes`.
3. Confirm units are **millimeter**: bottom-right unit indicator, or **Document menu → Workspace units → Length = Millimeter**, precision 2–3 decimals.

---

## Step 1 — A centered base block

1. Click **Sketch**, pick the **Top** plane.
2. Draw a **Center point rectangle** anchored on the **Origin**, 80 mm wide × 50 mm deep. Dimension both. The sketch should turn **black** (fully defined) — if it's blue, you're missing a constraint or dimension.
3. Accept the sketch. **Extrude** it **6 mm** up (Blind, New). Rename the extrude `Base block`.
4. Rename the sketch `Base profile`.

Centering on the origin now is deliberate — it makes the symmetry references in later exercises (and the mini-project) free.

---

## Step 2 — An offset plane, driven by a variable

You want a boss face floating 40 mm above the base, with the 40 mm being a *named* parameter, not a magic number.

1. Click the **Plane** tool.
2. **Plane type → Offset.**
3. **Entities** = the **Top** plane.
4. In the **Distance** field, type `#bossHeight = 40 mm` (this declares an inline variable `#bossHeight` and sets the offset to it in one go).
5. If the preview offsets downward, click the **flip** arrow so it's above the base.
6. Green check. **Rename the plane `Boss-face plane`.**

> If the inline `#name = value` syntax doesn't take in your build, just type `40 mm`, finish the plane, then add a Variable feature (`#bossHeight = 40 mm`) above it and edit the plane's distance to `#bossHeight`. Same result.

---

## Step 3 — Sketch and extrude on the offset plane

1. Click **Sketch**, pick **Boss-face plane**.
2. Draw a **Center point rectangle** on the **Origin** projection, 30 mm × 20 mm. Fully define it (black).
3. Accept. **Extrude** it **8 mm**, end condition **Blind**, operation **New** (a separate boss) — or **Add** to fuse it to a column; for this drill keep it as its own boss so you can see it float. Rename `Boss`.

Now the key observation: this boss sits 40 mm up because of `#bossHeight`, not because you measured from the base top. In Step 7 you'll change `#bossHeight` and watch the boss rise as one unit.

---

## Step 4 — An angled plane

1. Click the **Plane** tool.
2. **Plane type → Angle.**
3. **First entity** (the plane you measure the angle from) = the **Top** plane.
4. **Second entity** (the hinge) = the **back top edge** of the base block (the 80 mm edge along the far side). If picking an edge is awkward, use the origin **X axis** (turn on origin axes in the tree).
5. **Angle** = `30 deg`. Flip if it tilts the wrong way (you want it leaning up off the back edge).
6. Green check. **Rename `Stiffener plane @30`.**

---

## Step 5 — Sketch and extrude on the angled plane

1. **Sketch** on `Stiffener plane @30`.
2. Draw a small rectangle, 10 mm × 20 mm, dimensioned and constrained to the plane's origin/edges so it's **black**.
3. Accept. **Extrude 4 mm**. Rename `Angled stiffener`.

You've now built features on two non-default planes — one offset, one angled — both parametric.

---

## Step 6 — Sketch on a part face (and feel the trade-off)

Now do the *other* kind of reference on purpose, so you understand it.

1. **Sketch** directly on the **top face of the base block** (not a plane — the actual face).
2. Draw a small Ø6 mm circle near a front corner, fully defined to the corner.
3. Accept. **Extrude → Remove**, **Through all**, to cut a hole. Rename `Face-referenced hole`.

This hole rides the *face*. That's fine here — a hole on a plate genuinely belongs to that face. But note what you just did: this sketch depends on `Base block`'s top face existing and keeping its identity.

**Write a one-line note** (in the Part Studio's notes, or a comment to yourself): *"Face-referenced hole sketches on the base top face; acceptable because the face is a large, stable primary face that no later feature consumes."*

> **See the failure mode (optional, instructive):** roll back, insert a big **Fillet** on the base's top edges *before* the face-referenced hole, then roll forward. If the fillet eats the edge the hole was dimensioned to, the hole sketch goes yellow/red — a dangling reference. Undo it. That 30 seconds of breakage teaches the lesson better than any paragraph.

---

## Step 7 — The rebuild test

1. Double-click `#bossHeight` (or the offset plane's distance) and change **40 → 55 mm**. Regenerate.
   - **Expected:** the offset plane and the boss rise together. Nothing red.
2. Edit the angled plane's **30° → 45°**. Regenerate.
   - **Expected:** the angled plane and the stiffener re-tilt. Nothing red.
3. Edit the base width **80 → 100 mm**. Regenerate.
   - **Expected:** the centered base grows symmetrically; the centered boss stays centered. The face-referenced hole stays near its corner (it was dimensioned to the corner). Nothing red.

Set the values back to 40 / 30° / 80 when you're done admiring it.

---

## Expected outcome

A Part Studio containing:

- A centered `Base block`.
- A `Boss` on a variable-driven `Boss-face plane` (offset).
- An `Angled stiffener` on a `Stiffener plane @30` (angle).
- A `Face-referenced hole` sketched on the base's top face.
- A feature tree where **every** plane and feature is renamed by its job, no `Plane 1 / Extrude 2` survivors.
- A part that passes the three-edit rebuild test with **zero red features**.

Create a **Version** named `Ex1 complete`.

---

## Acceptance criteria

- [ ] One **offset plane** (variable-driven) and one **angled plane**, both renamed, each with a sketch and feature on it.
- [ ] One sketch built **on a part face**, with a written one-line justification.
- [ ] All driving sketches are **black** (fully defined).
- [ ] The rebuild test passes for all three edits with no red features.
- [ ] Every plane and feature renamed; a Version created.

---

## Stretch

- Replace the angled-plane hinge with a **mid plane** (Plane → Mid plane between the two 50 mm faces) and rebuild the stiffener centered on it.
- Add a **point–normal plane** at one corner vertex (normal = an edge) and sketch a tiny feature on it — preview for Exercise 3's sweep.
- Group `Boss-face plane + boss sketch + Boss` into a folder named `Boss`. Do the same for the stiffener. Notice how much faster the tree reads.

---

## Hints

<details>
<summary>My sketch won't go fully defined (black) on the offset plane</summary>

You need to constrain it *to* the plane's geometry. Use the origin projection (the plane carries the origin's projection as a reference point) and add a coincident/centered constraint plus your two dimensions. A center-point rectangle anchored on the projected origin needs only width and height to be fully defined.

</details>

<details>
<summary>The angled plane tilts the wrong way</summary>

Click the **flip** toggle in the Plane dialog, or enter the angle as a negative value. The hinge edge and the "from" plane together determine the sign; flipping is normal.

</details>

<details>
<summary>Changing #bossHeight didn't move the boss</summary>

The boss must reference the **offset plane**, and the offset plane must reference `#bossHeight`. If you accidentally sketched the boss on the base's top face and extruded it 40 mm tall, it's not riding the variable — re-do Step 3 sketching on `Boss-face plane`.

</details>

---

When this feels comfortable, move to [Exercise 2 — Patterns & mirror](./exercise-02-patterns-and-mirror.md).
