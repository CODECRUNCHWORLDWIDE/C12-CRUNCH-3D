# Exercise 1 — Extrude and Pocket a Bracket

**Goal:** Build a single-body L-bracket using all four extrude operations you learned in Lecture 1 — **New**, **Add**, **Remove (Blind)**, and **Remove (Through all)** — and prove it rebuilds cleanly when you change a driving dimension. No revolves, no dress-up features yet; this is pure extrude discipline.

**Estimated time:** 40 minutes.

**You build this in:** a Part Studio named `Ex1-Bracket` in your `C12-Week2` Document, units = mm.

---

## What you're making

A flat mounting bracket: an 80 × 50 × 8 mm base plate, with a raised cylindrical boss added on top, a milled pocket cut into the surface, and a bolt hole cut all the way through. By the end you'll edit one number and watch the whole thing rebuild.

Target dimensions (you'll be held to these so the rebuild test behaves):

- Base plate: **80 mm × 50 mm × 8 mm**.
- Boss: **⌀30 mm**, **6 mm** tall, centered 25 mm from the left edge, centered top-to-bottom.
- Pocket: **40 mm × 16 mm** rounded slot, **5 mm** deep, in the right half.
- Through-hole: **⌀10 mm**, Through all, in the boss.

---

## Step 1 — The base plate (New, Blind)

1. Open the `Ex1-Bracket` Part Studio. Press `n` over the **Top** plane (or click Top in the feature list) and start a **Sketch** on it.
2. Draw a **center-point rectangle** from the origin: pick the rectangle tool, click the origin as the center, drag out. This makes the rectangle automatically symmetric about both origin planes — the pro default.
3. Dimension it (`d`): **80 mm** wide, **50 mm** deep. The sketch should turn **black (fully defined)**. If it's blue, you're missing a constraint — check that the center is coincident with the origin.
4. Green-check the sketch. Press `Shift+E` to Extrude.
5. Operation **New**. End condition **Blind**. Depth **8 mm**. Confirm the arrow points **up** (+Z). Green check.
6. **Rename** the feature `Base plate` (double-click its name).

You now have an 80 × 50 × 8 mm plate centered on the origin.

---

## Step 2 — The boss (Add, Blind)

1. Click the **top face** of the plate. Press `n` to look straight down at it. Start a **Sketch** on that face.
2. Draw a **circle**. Dimension it **⌀30 mm**. Locate its center: **25 mm** from the left edge (dimension from the left vertical edge to the center) and **centered top-to-bottom** (add a *symmetric* constraint between the center point and the two long edges, or dimension 25 mm from the front edge). Fully define — **black**.
3. Green-check. `Shift+E`.
4. Operation should auto-select **Add** (because you sketched on an existing body). End condition **Blind**, **6 mm**. Arrow points **up, away from the plate**. Green check.
5. **Rename** `Boss`. The boss is now fused to the plate — one body, no seam.

---

## Step 3 — The pocket (Remove, Blind)

1. Sketch on the **top face** of the plate again (`n` to face it).
2. Draw a **center-point rectangle** in the right half of the plate. Use the **corner-fillet** option (or add a tangent arc at each end) to make it a rounded slot, OR just draw a plain rectangle for now — the slot shape is cosmetic here. Dimension it **40 mm × 16 mm**, located so its center sits **+22 mm** right of the origin and on the centerline. Fully define.
3. Green-check. `Shift+E`.
4. Operation **Remove**. End condition **Blind**, **5 mm**. **Critical:** confirm the arrow points **down, into the plate**. If it points up, hit the flip button.
5. Green check. You now have a 5 mm-deep blind pocket. **Rename** `Bolt pocket`.

---

## Step 4 — The through-hole (Remove, Through all)

1. Sketch on the **top of the boss**.
2. Draw a **circle concentric** with the boss (add a *concentric* constraint between this circle and the boss's circular edge — or *Use* the boss edge as reference). Dimension it **⌀10 mm**. Fully define.
3. Green-check. `Shift+E`.
4. Operation **Remove**. End condition **Through all**. Direction **down** (into the part). Green check.
5. **Rename** `Center hole`. Because it's **Through all**, this hole pierces the boss *and* the plate beneath, all the way through — and it stays a through-hole no matter how thick the plate gets.

---

## Step 5 — The rebuild test (the whole point)

This is where you earn the exercise.

1. Double-click **Base plate** in the feature list to edit it. Change the depth **8 mm → 16 mm**. Green check. Watch the part regenerate.
2. Inspect the result:
   - The **boss** still sits on top and is still 6 mm tall (Add Blind — correct).
   - The **bolt pocket** is still **5 mm** deep, *not* 10 — a blind pocket measured from the top (correct: Blind owns its own depth).
   - The **center hole** still goes **all the way through** the now-16 mm-thick part (correct: Through all is a relationship, not a number).
3. No feature should be red. If one is, roll back and read the error.
4. Now do the wrong thing on purpose to *see* the difference: edit `Center hole`, change its end condition from **Through all** to **Blind 8 mm**. Notice it now stops 8 mm down — a blind pocket in a 16 mm plate, *not* a through-hole. **Set it back to Through all.** This is the lesson: end conditions are design intent.
5. Restore **Base plate** to **8 mm**.

---

## Expected outcome

- A single solid body in `Ex1-Bracket`: 80 × 50 × 8 mm plate, ⌀30 × 6 mm boss, 40 × 16 × 5 mm pocket, ⌀10 mm through-hole.
- Feature list reads: `Base plate`, `Boss`, `Bolt pocket`, `Center hole` (plus their sketches) — all renamed.
- All sketches **black (fully defined)**.
- Editing the base thickness ±20% (8 → ~10 or ~6 mm) produces **zero red features** and keeps the pocket blind and the hole through.

---

## Acceptance criteria

You can mark this exercise done when:

- [ ] You used **New**, **Add**, and **Remove** operations, and a **Through all** end condition, at least once each.
- [ ] All driving sketches are fully defined (black).
- [ ] Every feature is renamed meaningfully.
- [ ] The rebuild test passes: change base thickness, no red features, pocket stays blind, hole stays through.
- [ ] You can state in one sentence why the center hole is Through all and the pocket is Blind.

---

## Stretch

- Mirror the boss + hole to the left half (you'll learn Mirror formally in Week 3, but try `Mirror` now — pick the Right plane as the mirror).
- Replace the plain through-hole with a proper **M5 clearance** hole using the **Hole feature** (preview of Exercise 3).
- Add a 1 mm × 45° chamfer around the top rim of the boss (preview of Lecture 2). Confirm it survives the rebuild test.

---

## Hints

<details>
<summary>My sketch won't turn black</summary>

Something is under-defined. The usual culprits: the rectangle's center isn't coincident with the origin; a dimension is missing; or a circle's center has no locating dimensions. Click any blue entity — it can still be dragged, which tells you what's free. Add the constraint or dimension that pins it.

</details>

<details>
<summary>The Remove extrude added material instead of cutting</summary>

The direction arrow pointed the wrong way (out of the part) or the operation was set to Add. Re-open the feature: set operation to **Remove**, and use the flip button so the arrow points **into** the solid.

</details>

<details>
<summary>The whole part disappeared after the Through-all cut</summary>

Your cut profile probably covered the entire body, so "through all" removed everything. Check the circle is ⌀10 and concentric with the boss — not a huge circle. Roll back, fix the sketch, roll forward.

</details>

---

When this feels comfortable, move to [Exercise 2 — Revolve a control knob](exercise-02-revolve-a-knob.md).
