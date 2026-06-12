# Exercise 1 — Your First Drawing

**Goal:** Take a finished part and produce a clean, dimensioned, associative drawing — ortho + iso views, a filled title block, exported to PDF. No view goes out of date; no dimension is overridden.

**Estimated time:** 45 minutes.

---

## Setup

You need a finished single part in an OnShape document. **Use the mounting bracket (or whichever part) from your Week 2–3 mini-project.** If you'd rather start clean, model this 60-second practice part first:

1. New Document → Part Studio.
2. On the Top plane, sketch a `60 mm × 40 mm` rectangle, corner at the origin. Fully define it.
3. **Extrude** it `10 mm` (Blind, New).
4. Add a **Hole** (Simple, ⌀6 mm, Through All) `15 mm` in from one corner in each direction — one hole is enough for this exercise; two is better practice.
5. Add a `2 mm` **Fillet** to the four vertical edges.

You now have a part to document. Confirm it has no feature-tree errors before drawing it.

---

## Step 1 — Set the part's properties (so the title block fills itself)

Before drawing, give the part an identity. Right-click the part in the **Parts** list → **Properties**:

- **Name / Part number:** `CC-PLATE-001`
- **Description:** `Practice Mounting Plate`
- **Material:** assign `6061 Aluminum` (Material → search the library).

These flow into the title block and any future BOM. Setting them now means you never type them into the drawing by hand.

---

## Step 2 — Create the drawing

Right-click the part (or the tab bar at the bottom) → **Create drawing of CC-PLATE-001**. In the dialog:

- **Template:** choose an ANSI inch or ISO mm template — pick **C-size / A3 landscape** so you have room. (For a part this small you could use A4, but give yourself space to learn.)
- Confirm the projection angle is **third-angle** (ANSI default). Note the projection symbol in the title block.

A new Drawing tab opens with an empty sheet and a "place view" cursor.

---

## Step 3 — Place the base view and project from it

1. The **Insert view** dialog is open. Choose **Front** as the orientation and set the **scale** to `1:1`. Click on the **left-center** of the sheet to place it. This is your base view.
2. Without closing the projection, **drag upward** from the base view and click — that's your **Top** view, auto-aligned above.
3. **Drag right** and click — your **Right** view, auto-aligned beside.
4. **Drag diagonally** (up-right) and click — an **Isometric** pictorial in the corner.
5. Press Escape / close the dialog.

Move the base view a little. Notice the top and right views move with it and stay aligned. That alignment is enforced — you can't knock a projected view out of line by accident.

---

## Step 4 — Clean up the views

Select each ortho view (click its border) and in the view properties:

- Turn **center marks** and **centerlines** ON so the hole shows its center.
- Decide on **tangent edges**: hide them for a cleaner look (the fillet blend lines disappear).
- Leave **hidden lines** ON for the front view if the hole is hidden behind a face in that orientation; otherwise off.

The iso view: leave it shaded or as hidden-line removed — it's for human readability, you won't dimension it.

---

## Step 5 — Dimension associatively

Use the **Dimension** tool. For this plate, place at minimum:

1. Overall **width** `60` (front or top view) — select the two vertical edges.
2. Overall **height/depth** `40` — select the two horizontal edges in the top view.
3. **Thickness** `10` — in the right view, the two horizontal edges.
4. **Hole diameter** `⌀6` — click the hole circle in the top view; OnShape writes the diameter.
5. **Hole location** — `15` from one edge and `15` from the adjacent edge (use **baseline** from a common corner, not a chain).

As you place each, watch OnShape *read the number from the model* — you are not typing values. That's an **associative dimension**.

> **Prove associativity (do this, it's the lesson):** go back to the Part Studio, change the extrude depth from `10` to `12`, and return to the Drawing tab. The right view updates and the `10` thickness dimension now reads `12` — you never touched the drawing. Change it back to `10`. **Do not** double-click the dimension and type a value; that creates an overridden (lying) dimension, which is forbidden this week.

---

## Step 6 — Fill the title block

Double-click into the title block. Most fields auto-populate from the part properties you set in Step 1 (part number, description, material). Fill the rest:

- **Drawn by:** your name.
- **Date:** today.
- **Revision:** `A`.
- **Scale:** confirm it reads `1:1`.
- **Units:** confirm `mm` (or `in`).

Confirm the **general tolerance block** note is present (the "unless otherwise specified" block). You don't edit it — just read it and understand it backs every un-toleranced number on your sheet.

---

## Step 7 — Export to PDF

Top-right of the drawing → **Export** → **PDF**. Open the PDF outside OnShape (your browser's PDF viewer) and confirm:

- All views render with their dimensions.
- The title block is filled and legible.
- Nothing is clipped off the sheet edge.

---

## Acceptance criteria

You can mark this exercise done when:

- [ ] A Drawing tab exists with **front, top, right, and iso** views, correctly aligned, third-angle.
- [ ] The part is **fully dimensioned**: overall width, height, thickness, hole diameter, and hole location — and **not over-dimensioned** (nothing measured twice).
- [ ] Every dimension is **associative** — you proved it by changing the model and watching a dimension update.
- [ ] **Zero overridden dimensions** (none typed by hand).
- [ ] The **title block** is filled, with part number/description/material flowing from part properties.
- [ ] The drawing shows **no out-of-date banner**.
- [ ] You exported a **PDF** that renders cleanly outside OnShape.

When all boxes are checked you should be looking at:

```
Drawing up to date · 0 out-of-date views · all dimensions associative
```

---

## Stretch

- Add a **bottom** or **left** view and decide whether it adds information or just clutter (remove it if it's redundant — restraint is a skill).
- Override the iso view's scale to `1:2` so it sits smaller in the corner.
- Add a **note** on the sheet: `BREAK ALL SHARP EDGES 0.2 MAX`.
- Set the hole location with **ordinate** dimensions from a 0,0 corner instead of baseline, and compare readability.

---

## Hints

<details>
<summary>My projected view won't stay aligned with the base view</summary>

Projected views are *meant* to stay aligned — that's correct behavior. If you want a view that floats freely (rare), you can break alignment via the view's right-click menu, but for orthographic drawings you almost never should. Keep them aligned.

</details>

<details>
<summary>A dimension shows in a weird color / OnShape warns it's overridden</summary>

You (or a misclick) typed a value into the dimension instead of letting OnShape read it. Delete that dimension and re-place it by selecting the geometry — never by typing the number. Overridden dimensions are the cardinal sin of model-based drawing.

</details>

<details>
<summary>The title block fields are blank</summary>

They pull from **part properties**, not from the drawing. Go back to the Part Studio, right-click the part → Properties, and set Part number / Description / Material. Return to the drawing; the block fills in. If a custom field still won't populate, double-click the block and type it directly as a last resort.

</details>

---

When this feels comfortable, move to [Exercise 2 — Section views & GD&T](exercise-02-section-views-and-gdt.md).
