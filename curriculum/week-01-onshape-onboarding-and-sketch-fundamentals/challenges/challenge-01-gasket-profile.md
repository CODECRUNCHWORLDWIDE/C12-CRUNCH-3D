# Challenge 1 — Gasket Profile from a Dimensioned Drawing

**Time estimate:** ~90 minutes.

## Problem statement

You're handed a dimensioned 2D engineering drawing of a **flat gasket** — the kind that seals a flange. Reproduce it in OnShape as **one single, fully-defined sketch** on the Top plane, using the **minimum number of driving dimensions**, leaning on geometric constraints (`equal`, `concentric`, `symmetric`, `tangent`, `parallel`) instead of over-dimensioning every feature. No 3D — just the sketch. It's a modeling task; build it by hand.

This is exactly the skill a real CAD job tests in the first week: "here's a drawing, give me a robust parametric sketch."

## The drawing (read it carefully)

The gasket is **symmetric about both** a vertical and a horizontal centerline through the origin. Geometry:

```
                 ⌀10  (×4 bolt holes, one per corner region)
        ●·····················●
       ·   ┌───────────────┐   ·
       ·   │               │   ·            outer corners: R15 fillet
   ●···┘   │   ⌀40         │   └···●        center: large bore ⌀40
       ·   │   (center bore)│   ·
       ·   └───────────────┘   ·
        ●·····················●
                 |←──── 120 ────→|   (overall width, hole-center to hole-center span)

  Overall plate: 140 wide × 90 tall, all four outer corners rounded R15.
  Center bore:   ⌀40, centered on the origin.
  Bolt holes:    ⌀10, four of them, at ±60 (x) and ±30 (y) from the origin.
```

**Dimensioned facts from the drawing (these are the *given* numbers):**

| Feature | Value |
|---------|-------|
| Overall plate width | 140 mm |
| Overall plate height | 90 mm |
| Outer corner radius (all 4) | R15 mm |
| Center bore diameter | ⌀40 mm |
| Bolt hole diameter (all 4) | ⌀10 mm |
| Bolt hole X offset from origin | ±60 mm |
| Bolt hole Y offset from origin | ±30 mm |

Everything else — that all four corners share R15, that all four bolt holes share ⌀10, that the bore is centered, that the four holes are placed symmetrically — should be carried by **constraints**, not by repeating numbers.

## What "minimum dimensions" means here

A naive sketcher dimensions everything: 4 corner radii, 4 hole diameters, 8 hole positions, the bore, the width, the height. That's ~18 dimensions and a fragile, hard-to-edit sketch.

**Target: 7 driving dimensions or fewer.** Here's the intended scheme:

1. **Width** `140` and **height** `90` — 2 dimensions. (Plate is a center-point rectangle on the origin, so it's symmetric for free.)
2. **One** corner radius `R15`, with the other three corners made **equal** to it — 1 dimension.
3. **Center bore** `⌀40`, concentric/coincident with the origin — 1 dimension.
4. **One** bolt hole `⌀10`, the other three made **equal** — 1 dimension.
5. **One** bolt hole position: `X=60`, `Y=30` from the origin — 2 dimensions. The other three holes are placed by **symmetric** (across both centerlines), so they need **zero** position dimensions.

Total: **7 dimensions.** Everything else is `equal`, `concentric`, `symmetric`, `tangent` (the corner fillets must be tangent to the plate edges), and `coincident` (bore to origin).

## Build approach (suggested order)

1. **Document & centerlines.** New Document `C12-W1-Challenge-Gasket`, mm units. Sketch on Top. Draw a **vertical** and a **horizontal** construction centerline through the **origin** (toggle construction with `q`). These are your two mirror axes.
2. **Plate.** Center-point rectangle on the origin → width `140`, height `90`. (Symmetric about both centerlines automatically.)
3. **Corner fillets.** Use **sketch fillet** on all four corners. Set the first to `R15`; make the other three **equal**. Confirm each fillet is **tangent** to both adjoining edges (the sketch-fillet tool does this).
4. **Center bore.** Center-point circle on the origin → `⌀40`.
5. **Bolt holes.** Draw **one** hole in, say, the top-right region. Dimension its center `X=60`, `Y=30` from the origin. Draw the other three holes; constrain each pair **symmetric** across the appropriate centerline (top-right ↔ top-left across the vertical axis; top ↔ bottom across the horizontal axis). Make all four **equal**, then dimension *one* `⌀10`.
6. **Drive out the blue.** Drag test. Everything black, status bar "Fully defined."

## Acceptance criteria

- [ ] A Document named `C12-W1-Challenge-Gasket`, mm units, one sketch on the Top plane.
- [ ] The sketch is **fully defined** — all geometry **black**, status bar "Fully defined," **no** red/yellow conflicts.
- [ ] Geometry matches the drawing: 140×90 plate, four R15 corners, ⌀40 bore, four ⌀10 holes at (±60, ±30).
- [ ] You used **7 driving dimensions or fewer**. (Count them. If you used more, find the relationship you missed.)
- [ ] All four corner radii are tied with **equal**; all four bolt holes are tied with **equal**; the holes are placed by **symmetric** across the centerlines; the bore is **coincident** with the origin.
- [ ] **Robustness test:** change the plate width `140` → `160`. The whole gasket rebuilds cleanly — corners stay R15 and tangent, holes stay symmetric, bore stays centered. *(If anything breaks or goes blue, your constraint scheme is too dimension-dependent; fix it.)*
- [ ] You created a named **Version** `challenge-gasket-defined`.
- [ ] You wrote a short note (3–5 sentences) listing the constraints you used to *avoid* dimensions, and how many dimensions you saved versus the naive approach.

## Stretch

- Fully-define the *same* gasket a **second way**: instead of `symmetric` for the holes, use a construction circle/rectangle and place holes on it. Compare dimension counts and which scheme is more robust under a width change.
- Add a fifth, *non-symmetric* alignment hole (an asymmetric ⌀6 near one corner) so the gasket can only mount one way ("poka-yoke"). Notice it *can't* use symmetry, so it costs full position dimensions — a good illustration of why asymmetry is more expensive to define.
- Turn on **Show constraints** and screenshot the decorated sketch. A reviewer should be able to read your *intent* from the glyphs alone.

## Submission

Share your Document (the `challenge-gasket-defined` Version) read-only with your reviewer, or export a screenshot of the fully-defined sketch *with constraints shown* plus your dimension-count note. Make sure the robustness test passes on the shared Version — that's what proves the constraint scheme, not just the geometry.

## Why this matters

The gasket is trivial geometry on purpose. The challenge isn't drawing it — it's drawing it *robustly*, the way a colleague can edit safely six months from now. Every downstream skill in C12 (extruding this profile in Week 2, patterning the holes in Week 3, drawing and tolerancing it in Week 5) depends on the sketch underneath being **fully defined and minimally dimensioned**. Master that here and the rest of the course is building on rock instead of sand.
