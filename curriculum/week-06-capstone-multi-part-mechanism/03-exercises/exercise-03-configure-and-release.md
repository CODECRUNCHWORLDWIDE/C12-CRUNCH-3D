# Exercise 3 — Configure a part, prove the rebuild, tag a Version, and export STEP + STL

> **Estimated time:** ~120 minutes (40 min configuring, 30 min the rebuild proof, 20 min tagging the Version, 30 min exporting and sanity-checking). **Cost:** free — configuration, versioning, and export are all on the free Public plan.

This is the exercise that turns a working mechanism into a *shippable* one. You make one part a family of sizes with a Configurations table, prove the whole assembly rebuilds across every configuration without a red error, freeze the design as an immutable Version, and export the two neutral formats — STEP for engineers, STL for printers — that you then *open in a neutral viewer* to confirm they are real. An export you have not opened is not a deliverable.

This walkthrough continues the slider-crank gripper. We configure the **jaw** part into three sizes, but the method applies to any part you choose to make a family.

## Goal

Produce a configured part (≥ 2 configurations) that rebuilds the entire assembly cleanly in *every* configuration, a tagged `v1.0` Version, and a STEP (assembly) + STL (printable part) exported from that Version that both open clean in a neutral viewer at the correct scale.

## Step 1 — Decide the configuration input

Pick the dimension that should vary across the family. For the jaw, the natural one is the **jaw opening width** — how wide it grips. Decide three values: `Small = 18 mm`, `Medium = 24 mm`, `Large = 30 mm`.

1. Confirm that dimension is already driven by a **variable** in the part's Part Studio (e.g., `#jaw_width`). If it is a raw number, change it to a variable first — configurations drive variables cleanly and raw numbers messily.

## Step 2 — Add the Configurations table

1. In the part's Part Studio, open the **Configurations panel** (the table icon, upper-left of the Part Studio).
2. Add a **configuration input** of type **Configuration variable** (or a List input named `Size` with three values: Small / Medium / Large).
3. For each configuration value, set `#jaw_width` to its number: Small → 18, Medium → 24, Large → 30.
4. Switch between the three configurations in the panel and watch the part regenerate at each width. Each must rebuild with **zero errors** — if a feature goes red at one size, you have a brittle reference (a sketch dimensioned to geometry that moved); fix it before continuing.

## Step 3 — Test the configuration boundaries

A configuration that works at the middle value but breaks at an extreme is a latent bug:

1. Switch to **Small (18 mm)**. Does every feature survive? Does the part still make physical sense (no self-intersecting geometry)?
2. Switch to **Large (30 mm)**. Same checks.
3. If either extreme breaks, the failure tells you the *valid range* of the configuration. Either fix the reference so the full range works, or document the valid range explicitly.

## Step 4 — Prove the assembly rebuilds across configurations

The part configuring cleanly is necessary but not sufficient — the *assembly* must stay valid as the part changes:

1. Open the `Mechanism` Assembly.
2. Select the configured jaw instance and, in its properties, switch its configuration to **Small**. The assembly should regenerate — the mates should still resolve, nothing should go red.
3. **Drag the mechanism** in the Small configuration. It must still articulate through its range (a different jaw width may change the geometry, but the motion must survive).
4. Repeat for **Medium** and **Large**, dragging each. Confirm: every configuration rebuilds, every configuration still moves, and no configuration interferes (spot-check Interference Detection at full closure for at least the Small and Large jaws, since closure clearance is the most configuration-sensitive).

If the assembly rebuilds and still articulates in all three configurations, your parametric robustness is proven. **This is the rebuild proof the grader and the reviewer test.**

## Step 5 — Get the design clean, then tag Version v1.0

A Version is immutable — tag it only when the design is *clean*:

1. Confirm: the mechanism drags through its range, has one DOF, no interferences across the sweep, and rebuilds across all configurations. (Exercises 1 and 2 plus Step 4.)
2. Open the **version graph** (the clock/branch icon, lower-left) → **Create version**. Name it `v1.0` with a description: "Released capstone mechanism — clean drag, 1 DOF, 3 jaw configurations, rebuild verified."
3. The Version is now frozen. Every export and drawing you generate next will reference *this* exact geometry.

## Step 6 — Export the STEP (assembly, for engineers)

1. Switch the configured jaw to the configuration you want to ship as the default (say **Medium**).
2. Right-click the `Mechanism` Assembly tab → **Export**.
3. Choose format **STEP** (AP242 or AP214 — AP242 carries the most). Confirm **units = millimeter**. Export.
4. STEP carries the exact B-rep geometry *and* the assembly structure — the parts and how they nest — but **not** the feature tree or variables. That is correct: the engineer who receives it gets precise geometry to continue from, not your editable history.

## Step 7 — Export the STL (a printable part, for the printer)

1. Pick one part to ship printable — the **jaw** is the natural choice.
2. Right-click the jaw part (in its Part Studio) → **Export**.
3. Choose format **STL**. Set the **chord tolerance** fine enough that curves look round — about **0.05 mm** for a hobby FDM print (coarser and a cylindrical bore looks faceted; far finer just bloats the file). Confirm **units = millimeter** and **Binary** (smaller than ASCII).
4. STL carries only a triangle mesh — no curves, no assembly structure, no guaranteed units. That is correct: the slicer just needs the outer shape.

## Step 8 — The export sanity check (open everything in a neutral viewer)

**Never ship an export you have not opened.**

1. Open the **STEP** in a viewer that is *not* OnShape — [3dviewer.net](https://3dviewer.net/) in a browser is free and immediate. Confirm: all four parts present, in the right relative positions, none imported as a hollow shell.
2. Open the **STL** in your slicer (or the same viewer). Confirm three things:
   - The **bounding box** dimensions match the model *in millimeters* (this catches the units bug — an STL that imports 25.4× too big means the units were wrong).
   - The mesh is **watertight** (no holes the slicer flags — a non-manifold mesh will not slice).
   - The facets are fine enough that the **bore looks round**, not hexagonal.
3. If anything is wrong, fix it and re-export *from the v1.0 Version*. A STEP missing a part or an STL at the wrong scale is a failed handoff even if the model is perfect.

## Expected outcome

```
Configured part:     jaw, 3 configs (Small 18 / Medium 24 / Large 30 mm)
Part rebuild:        clean at all 3 sizes      [PASS: 0 errors]
Assembly rebuild:    articulates in all 3 configs, no interference   [PASS]
Version:             v1.0 tagged (immutable)
STEP export:         Mechanism.step, 4 parts, mm, opens clean in viewer   [PASS]
STL export:          jaw.stl, 0.05mm chord, mm, watertight, bbox 30x16x10 mm   [PASS]
Sanity check:        both exports opened in a neutral viewer            [PASS]
```

## Acceptance criteria

- [ ] A part configured into **≥ 2** (target 3) sizes via a Configurations table driving a variable.
- [ ] The part rebuilds with **zero errors** in every configuration, including the extremes.
- [ ] The **assembly** rebuilds and still articulates in every configuration, with no interference at full closure for the smallest and largest.
- [ ] An immutable **`v1.0` Version** tagged only after the design is clean.
- [ ] A **STEP** of the assembly and an **STL** of a printable part, both exported from `v1.0` at **millimeter** units.
- [ ] **Both exports opened** in a neutral viewer: STEP shows all parts, STL is watertight and at the correct bounding-box scale.
