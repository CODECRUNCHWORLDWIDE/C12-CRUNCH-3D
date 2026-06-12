# Exercise 2 — Patterns & Mirror

**Goal:** Populate geometry without re-sketching. You'll build a 6-bolt flange ring with a **circular pattern** about a named axis, a vent grille with a **linear pattern** centered on its face, and a symmetric tab with **mirror** — each from a single seed feature, each driven by a variable so it re-lays-out on edit.

**Estimated time:** 50 minutes.

**You'll use:** Sketch, Extrude, Hole, Axis, Circular pattern, Linear pattern, Mirror, inline variables, the rebuild test.

> This is a modeling task, not code. Follow the numbered steps in OnShape. Build it yourself; pattern, don't copy-paste.

---

## Part A — A 6-bolt flange (circular pattern)

### A1 — The flange disc

1. New **Part Studio** tab: `Ex2 - Patterns`.
2. **Sketch** on **Top**: a circle centered on the **Origin**, Ø120 mm. Fully define (just the diameter, since it's centered). Accept.
3. **Extrude** 10 mm up. Rename `Flange disc`.
4. **Sketch** on **Top** again: a circle centered on Origin, Ø50 mm. Accept. **Extrude → Remove, Through all** to bore the center. Rename `Center bore`.

### A2 — A named centerline axis

1. Click the **Axis** tool.
2. Pick the **cylindrical face** of the `Center bore`. OnShape infers its centerline.
3. Green check. **Rename `Bore axis`.**

This is the reference your circular pattern will spin about. Do **not** rely on an inferred axis — build the named one.

### A3 — One seed bolt hole

1. Declare a bolt-circle variable: add a **Variable** feature, `#bcd = 90 mm` (bolt-circle diameter). (Or type `#bcd = 90 mm` inline in the next dimension.)
2. **Sketch** on the **top face** of the flange (a face is fine here — it's a stable primary face): a point located on the bolt circle. Dimension it **`#bcd / 2`** (= 45 mm) radially from the Origin, and place it on the vertical centerline (12 o'clock). Fully define. Accept.
3. **Hole** feature: select the point. Set **Hole type = Simple/Clearance**, **size = M6 clearance (~Ø6.6 mm)**, **end = Through**. Rename `Bolt hole (seed)`.

### A4 — The circular pattern

1. Declare `#bolts = 6` (Variable feature, or inline in the next field).
2. Click **Circular pattern**.
3. **Pattern type = Feature.** **Features to pattern = `Bolt hole (seed)`.**
4. **Axis = `Bore axis`.**
5. **Angle = 360°**, **Instance count = `#bolts`**, **Equal spacing = on**.
6. Green check. **Rename `Bolt ring`.**

You now have six evenly-spaced bolt holes from one seed.

### A5 — Prove it's parametric

- Change `#bolts` **6 → 8**, regenerate. Eight evenly-spaced holes. No red.
- Change `#bcd` **90 → 100 mm**, regenerate. The whole ring moves outward (the seed moved; the pattern followed). No red.
- Set them back to 6 and 90.

---

## Part B — A vent grille (linear pattern)

### B1 — A panel and one seed slot

1. New **Part Studio** tab (or continue in `Ex2 - Patterns` with a separate body): `Ex2 - Grille`.
2. **Sketch** on **Front**: a center-point rectangle on the Origin, 120 mm wide × 80 mm tall. Accept. **Extrude** 4 mm. Rename `Panel`.
3. **Sketch** on the **front face** of the panel: one **slot** (use the Slot tool, or a rounded rectangle), 4 mm wide × 30 mm tall, located by dimension. Fully define. Accept.
4. **Extrude → Remove, Through all**. Rename `Vent slot (seed)`.

### B2 — The 2-D centered linear pattern

1. Declare `#cols = 5` and `#rows = 3` (Variable features or inline).
2. Click **Linear pattern**, **Pattern type = Feature**, **Features = `Vent slot (seed)`**.
3. **Direction 1** = the panel's horizontal edge. Set **Instance count = `#cols`**, **Spacing = 16 mm**. Turn on the **symmetric / centered** option so the columns grow both ways from the seed (keeps the grille centered on the panel).
4. Turn on **Direction 2** = the panel's vertical edge. **Instance count = `#rows`**, **Spacing = 22 mm**, centered.
5. Green check. **Rename `Vent grille`.**

You have 15 slots (5 × 3) from one seed sketch.

### B3 — Prove it stays centered

- Change `#cols` **5 → 7**, regenerate. Seven columns, still centered on the panel.
- Change the panel **width 120 → 150 mm**, regenerate. The centered grille re-centers on the wider panel. No red.
- Set them back.

> If your grille drifts to one side when the panel resizes, your pattern is corner-anchored. Turn on the **centered/symmetric** option (B2.3–4) — that's the whole point of this part.

---

## Part C — A symmetric tab (mirror)

### C1 — One half, then reflect

1. In the `Ex2 - Grille` Part Studio, **sketch** on the **top edge** region of the panel a small tab on the **left** side only: a 15 × 10 mm rectangle with a Ø5 mm hole, on a sketch on the panel's top face, located by dimension to the left of center. Accept. **Extrude** the tab (Add), then **Hole** the Ø5. Rename `Left tab` and `Left tab hole`.
2. Click **Mirror**, **Pattern type = Feature**.
3. **Entities to mirror** = `Left tab` and `Left tab hole`.
4. **Mirror plane** = the **Right** origin plane (the part's vertical symmetry plane, because you centered the panel on the origin).
5. Green check. **Rename `Right tab (mirror)`.**

### C2 — Prove the mirror tracks

- Edit the **left tab's** hole from Ø5 → Ø6, regenerate. The mirrored right tab's hole follows to Ø6. You maintain one half; symmetry maintains the other.
- Move the left tab 5 mm; the right tab mirrors the move. No red.

---

## Expected outcome

Across this exercise you should have:

- A `Flange disc` with a **`Bolt ring`** circular pattern of one seed `Bolt hole`, about a named `Bore axis`, driven by `#bolts` and `#bcd`.
- A `Panel` with a **`Vent grille`** centered 2-D linear pattern of one seed `Vent slot`, driven by `#cols` and `#rows`.
- A symmetric tab maintained by **`Mirror`** across an origin plane.
- A feature tree with **every** feature, axis, and variable renamed by its job.
- All seeds proven parametric: changing a count or a base dimension re-lays-out the copies with **zero red features**.

Create a **Version** named `Ex2 complete`.

---

## Acceptance criteria

- [ ] A **circular pattern** of a single seed Hole feature about a **named construction axis** (not an inferred one).
- [ ] A **centered 2-D linear pattern** of a single seed slot that stays centered when the panel resizes.
- [ ] A **mirror** of a feature across an origin/mid plane, proven to track the seed.
- [ ] Counts and BCD driven by **inline variables**, each changed once to prove re-layout.
- [ ] All driving sketches **black**; rebuild test passes with no red features.
- [ ] Every feature/axis/variable renamed; a Version created.

---

## Stretch

- Replace the four-corner holes on a Week-2 part with a single **circular pattern** off a named axis; drive the count with a variable.
- Pattern a **pattern**: cluster two slots, then linear-pattern the cluster — note how the tree nests, and group it into a folder.
- On the flange, **suppress** the `Bolt ring` (right-click → Suppress) to get a blank flange, then unsuppress. This is the precursor to Week 5's configuration-driven variants.

---

## Hints

<details>
<summary>My circular pattern spreads holes unevenly or only part-way around</summary>

Make sure **Equal spacing = on** and **Angle = 360°** with the instance count set. If you instead used "angle between instances," 60° × 6 also gives a full ring — but 360° / equal-spacing is the robust choice because changing the count re-divides the full circle automatically.

</details>

<details>
<summary>The grille isn't centered on the panel</summary>

Your linear pattern is anchored at the seed and grows in one direction only. Turn on the pattern's **symmetric / centered** toggle for each direction so copies grow both ways from the seed. Alternatively, place the seed at a corner and dimension the start offset as a function of panel size and count — but the centered toggle is far simpler.

</details>

<details>
<summary>Mirror says "nothing to mirror" or fails</summary>

You must select the **features** (in the tree) for a feature mirror, and a valid **planar** mirror plane. If you picked a curved face as the mirror plane, it won't work — use a flat origin plane or a Plane → Mid plane.

</details>

---

When this feels comfortable, move to [Exercise 3 — Sweep & loft](exercise-03-sweep-and-loft.md).
