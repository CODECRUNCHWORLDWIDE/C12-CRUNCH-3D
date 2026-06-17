# Exercise 2 — Section Views & GD&T

**Goal:** Communicate internal geometry with a section view, then add the three GD&T essentials — datums A/B/C, a flatness control, and a position feature control frame located by a basic dimension. This is a CAD modeling/drawing task: every step is a precise click sequence in OnShape, no code.

**Estimated time:** 50 minutes.

---

## The part you'll document

You need a part with an internal feature so a section view is worth drawing. Use your Week 2 shelled part, or model this practice **bored boss block**:

1. New Part Studio. On the Top plane, sketch an `80 mm × 50 mm` rectangle, corner at origin, fully defined.
2. **Extrude** `20 mm` (Blind, New). This is the base block.
3. On the top face, sketch a `⌀30 mm` circle centered at `(40, 25)` (the block's center). **Extrude** it `15 mm` up (Add) to make a raised cylindrical **boss**.
4. On the top of the boss, sketch a `⌀16 mm` circle, same center. **Extrude** it `Remove`, `Through All` — a bore straight down through the boss and base. *This is the internal feature your section will reveal.*
5. Add a `⌀6 mm` **Hole** (Simple, Through All) `12 mm` in from the lower-left corner — this is the located feature you'll position-tolerance.
6. No errors in the tree? Good.

Set part properties: Part number `CC-BOSS-001`, Description `Bored Boss Block`, Material `6061 Aluminum`.

---

## Step 1 — Drawing with a front view

1. **Create drawing of CC-BOSS-001**, A3/C-size, third-angle.
2. Place a **Front** base view at `1:1` on the left of the sheet (orient so the boss rises and you can see the block's height).
3. Project a **Top** view above it (you'll cut the section from this one) and an **Iso** in the corner.
4. Turn on **centerlines / center marks** so the bore and the ⌀6 hole show their centers.

---

## Step 2 — Add a full section view

1. Select the **Section view** tool.
2. Click to draw the **cutting-plane line** through the **Top** view, straight through the center of the boss/bore (use the centerline as a snap). Drag the line all the way across the part — this is a **full section**.
3. Click off to one side to place the resulting section. OnShape projects the cut and **hatches** the solid material; the bore now appears as a clean hole through the cut, not a tangle of hidden lines.
4. OnShape labels it `SECTION A-A` with arrows on the cutting-plane line showing the viewing direction. Confirm the label and arrows are present.

> **Why this beats hidden lines:** in the unsectioned front view, the ⌀16 bore was two dashed lines buried behind the boss face. In the section it's a solid, dimensionable opening. **You dimension the bore and the wall thickness on the section, not the exterior view** — you can't dimension a wall you can't see.

---

## Step 3 — Dimension the section

On `SECTION A-A`, place associative dimensions:

- **Bore diameter** `⌀16` (click the two cut edges of the hole, or the hole if OnShape offers diameter).
- **Boss outer diameter** `⌀30`.
- **Boss height** `15` and **base thickness** `20` (overall `35`).
- **Wall thickness** of the boss around the bore: `(30 − 16) / 2 = 7` on each side — dimension it; it's the number a fabricator cares about most on a bored boss.

All associative — verify one by nudging a model dimension and watching it track, then undo.

---

## Step 4 — Place the datum reference frame (A, B, C)

Now GD&T. First, establish what everything is measured from — the **Datum Reference Frame**.

1. Select the **Datum** annotation tool.
2. Attach **datum A** to the part's **bottom face** (the seating surface) in the front view — drag a leader to the bottom edge and label it `A`. *A is primary: the part sits on this; it removes 3 DOF.*
3. Attach **datum B** to the **left vertical edge** (a locating edge) — label it `B`. *Secondary: removes 2 DOF.*
4. Attach **datum C** to the **front/bottom edge** in the top view (the third reference) — label it `C`. *Tertiary: removes the last 1 DOF.*

You've now defined `A | B | C` — the part is fully located in space, the drawing equivalent of fully mating it in an assembly.

---

## Step 5 — Add a flatness control (form, no datum)

The bottom face (datum A) is a seating surface; demand it be flat.

1. Select the **Geometric tolerance** (feature control frame) tool.
2. Attach the FCF to the **bottom face** (the same surface as datum A).
3. Choose characteristic **Flatness** (`▱`), tolerance value `0.1`. Flatness references **no datum** — leave the datum boxes empty. OnShape draws:

```
┌─────┬───────┐
│  ▱  │  0.1  │
└─────┴───────┘
```

Read it: *"this face must lie between two parallel planes 0.1 mm apart."*

---

## Step 6 — Position the ⌀6 hole (location, references A|B|C)

This is the workhorse control. First make the hole's location **basic**, then add the position tolerance.

1. **Basic-dimension the hole's true location.** Place the two location dimensions for the ⌀6 hole (`12` from datum B edge, `12` from datum C edge). Select each dimension and toggle it to **Basic** — it gets boxed (`[12]`) and loses its ± tolerance. A basic dimension is *theoretically exact*; the tolerance comes from the FCF, not from the location number.
2. **Add the position FCF on the hole.** Attach a Geometric tolerance to the ⌀6 hole. Choose **Position** (`⌖`), tolerance `⌀0.2` (a diameter zone), and reference datums **A, B, C** in order. OnShape draws:

```
┌─────┬────────┬───┬───┬───┐
│  ⌖  │ ⌀0.2   │ A │ B │ C │
└─────┴────────┴───┴───┴───┘
```

Read it: *"the hole's axis must lie within a ⌀0.2 cylindrical zone, located by the basic dimensions from A, then B, then C."*

> **The double-definition trap:** do **not** leave the `12` location dimensions as ± toleranced *and* add a position FCF — that defines the hole's location twice and contradicts itself. Basic dimension for location + position FCF for tolerance. One says *where*, the other says *how far it may stray*.

---

## Step 7 — Title block and export

Fill the title block (part number/description/material flow from properties; add drawn-by, date, rev `A`). Confirm the general tolerance block is present — it backs every dimension that *doesn't* carry an explicit tolerance or FCF. Export **PDF**.

---

## Acceptance criteria

- [ ] A **full section view** labeled `SECTION A-A` with a cutting-plane line and direction arrows, hatching on the cut solid.
- [ ] The **bore, boss OD, heights, and wall thickness** dimensioned on the section (not guessed from the exterior).
- [ ] **Datum feature symbols A, B, C** placed on the seating face, a locating edge, and a third reference, in the correct primary/secondary/tertiary roles.
- [ ] One **flatness** FCF (`▱ 0.1`) on datum A's face, with **no** datum reference.
- [ ] The ⌀6 hole's location given by **basic** dimensions (boxed, no ±).
- [ ] One **position** FCF (`⌖ ⌀0.2 | A | B | C`) on the ⌀6 hole.
- [ ] No double-definition (location is basic, not basic *and* ± toleranced).
- [ ] All dimensions associative; no out-of-date views; PDF exported.

---

## Stretch

- Add a **perpendicularity** (`⊥ 0.1 | A`) FCF on the boss's outer cylinder so it must stand square to the seating face.
- Add the **MMC modifier** (`Ⓜ`) to the position tolerance and write one sentence in a sheet note explaining what bonus tolerance it grants as the hole grows.
- Add a **detail view** at `4:1` of a small chamfer or the hole edge and dimension it there.
- Replace the full section with a **half section** and decide which communicates this symmetric part better.

---

## Hints

<details>
<summary>The section hatching looks wrong / covers a feature it shouldn't</summary>

Hatching represents solid material the cutting plane passed through. If a feature is hatched that should be open (like the bore), your cutting-plane line probably didn't pass through its center — re-draw the cutting-plane line snapped to the bore's centerline.

</details>

<details>
<summary>I can't make a dimension "basic"</summary>

Place a normal associative dimension first, then select it and look for the **Basic** toggle/box in its property panel (it converts the dimension to a boxed, tolerance-free basic). You can't add a position FCF meaningfully until the location it references is basic.

</details>

<details>
<summary>Which surface should be datum A?</summary>

Primary datum A is normally the surface the part **functionally seats on** — the face that contacts its mating part first and constrains the most degrees of freedom. For this block that's the bottom face. B and C are the edges that then locate it in the plane. Function decides datum order, not convenience.

</details>

---

When this feels comfortable, move to [Exercise 3 — Configurations: one part, three sizes](./exercise-03-configurations-part-family.md).
