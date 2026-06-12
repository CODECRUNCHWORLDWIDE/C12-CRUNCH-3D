# Exercise 2 — Revolve a Control Knob

**Goal:** Model a stepped control knob entirely from one revolved half-section, respecting the "profile must not cross the axis" rule, then add a chamfered lead-in and a partial-revolve flat. This is your first turned (rotationally symmetric) part.

**Estimated time:** 45 minutes.

**You build this in:** a Part Studio named `Ex2-Knob` in your `C12-Week2` Document, units = mm.

> **This is a CAD modeling task, not code.** You build it by hand in OnShape. Read the whole sequence, then model it. Every dimension below is load-bearing — hit them so the part matches and the rebuild test works.

---

## What you're making

A grippable control knob: a wide ⌀40 mm base flange that steps up to a ⌀22 mm grip, ~28 mm tall overall, with a chamfered top lip, a counterbored hole on the underside for a ⌀6 mm shaft, and one flat ground onto the grip so it can't spin on the shaft. You draw **half** of the cross-section and let the revolve do the rest.

Target dimensions:

| Feature | Value |
|---------|-------|
| Base flange diameter | **⌀40 mm** |
| Base flange height | **6 mm** |
| Grip diameter | **⌀22 mm** |
| Overall height | **28 mm** |
| Top chamfer | **1.5 mm × 45°** |
| Shaft bore | **⌀6 mm**, blind, **18 mm** deep |
| Counterbore at base | **⌀12 mm × 4 mm** deep |
| Flat on grip | cuts the ⌀22 grip to a chord **8 mm** from the axis, over the top **16 mm** |

---

## Step 1 — Sketch the half-section (the hard part)

The revolve is trivial; the *sketch* is where the work is. Take your time here.

1. Open `Ex2-Knob`. Start a **Sketch** on the **Front** plane. Press `n` to face it.
2. Draw a **vertical construction line** from the **origin** straight up, about 30 mm. Make it **construction geometry** (toggle the construction button, or press `q`). This is your **revolve axis**. Constrain it **vertical** and its bottom endpoint **coincident with the origin**.
3. **To the right of the axis**, draw the closed half-profile of the knob — a series of connected lines tracing: 
   - bottom edge running right from the axis (the underside),
   - up the outside of the **⌀40 base flange** (so this edge is **20 mm** from the axis — half of 40),
   - in across the top of the flange,
   - up the outside of the **⌀22 grip** (this edge is **11 mm** from the axis),
   - across the top,
   - back to the axis.
4. **Dimension everything from the axis or the origin:**
   - Flange outer edge to axis: **20 mm** (gives ⌀40).
   - Flange height: **6 mm**.
   - Grip outer edge to axis: **11 mm** (gives ⌀22).
   - Overall height (axis bottom to top edge): **28 mm**.
5. **Verify the profile is closed and entirely on the right of the axis.** It must not cross or touch across the axis except where the bottom edge starts at it. Drive the sketch to **fully defined (black)**.

> If the sketch won't go black: the most common gap is the bottom edge not being constrained *horizontal*, or the profile not actually closing. Hover the endpoints — coincident points show a small marker.

---

## Step 2 — Revolve it (New, Full)

1. Green-check the sketch. Press `Shift+R` (Revolve).
2. Operation **New**. **Sketch region:** the closed half-profile. **Revolve axis:** click the construction line. **Revolve type:** **Full** (360°).
3. Green check. You now have a solid stepped knob. Orbit it (middle-drag) to confirm.
4. **Rename** `Knob body`.

---

## Step 3 — The top chamfer (dress-up)

1. Invoke **Chamfer** (toolbar, or search). 
2. Select the **top circular edge** of the grip (the ⌀22 rim).
3. Mode **Equal distance**, distance **1.5 mm** (a 1.5 × 45° break). Green check.
4. **Rename** `Top chamfer`. This makes the knob comfortable and removes the sharp molding edge.

---

## Step 4 — The shaft bore + counterbore (Hole feature)

The knob mounts on a ⌀6 mm shaft from below, with a counterbore so a retaining feature seats flush.

1. Sketch a single **point** on the **bottom face**, constrained **coincident with the origin** (so the bore is concentric with the knob). Fully define. Close the sketch.
2. Invoke the **Hole** feature.
3. Type **Counterbore**. (We'll set custom sizes rather than a fastener standard here.) Set the **hole diameter ⌀6 mm**, **counterbore diameter ⌀12 mm**, **counterbore depth 4 mm**. Main bore end condition **Blind**, depth **18 mm**.
4. Pick the point. Confirm the hole goes **up into** the knob from the bottom. Green check.
5. **Rename** `Shaft bore`.

> If your OnShape Hole dialog drives only from fastener standards, use **Simple** + manual diameter for the ⌀6 bore, then a second small **Remove extrude** (⌀12, 4 mm) for the counterbore — and rename both. Either path is acceptable; the Hole feature is preferred when it exposes manual sizes.

---

## Step 5 — The anti-rotation flat (partial cut)

So the knob can't spin freely on the shaft, grind one flat onto the grip.

1. Sketch on the **Right** plane (or any plane through the axis). Draw a vertical line offset **8 mm** from the axis, on the grip side, spanning the **top 16 mm** of the grip. Close a thin region between that line and a box safely outside the grip's ⌀22 surface (so the Remove has material to cut). Fully define.
2. `Shift+E`. Operation **Remove**. End condition **Through all** (so the flat is a clean chord through the round grip). Confirm the cut removes only the bit of grip **outside** the 8 mm chord. Green check.
3. **Rename** `Anti-rotation flat`. The grip now has a D-shaped cross-section over its top 16 mm.

---

## Step 6 — The rebuild test

1. Edit `Knob body`'s sketch. Change **overall height 28 → 34 mm**. Regenerate.
2. Confirm: the chamfer stays on the top rim, the shaft bore stays 18 mm deep from the bottom, the flat stays on the grip. **No red features.**
3. Change **grip diameter 22 → 26 mm** (edit the 11 mm half-dimension to 13 mm). Regenerate. The flat (8 mm chord) still cuts; the chamfer still sits on the rim. No red features.
4. Restore original values.

---

## Expected outcome

- A single revolved solid in `Ex2-Knob`: ⌀40 base flange, ⌀22 grip, 28 mm tall, chamfered top, ⌀6/⌀12 counterbored shaft bore, one anti-rotation flat.
- Feature list: `Knob body`, `Top chamfer`, `Shaft bore`, `Anti-rotation flat` — all renamed.
- The half-section sketch is **black (fully defined)** and lives **entirely to one side of the axis**.
- Rebuild test passes for both height and grip-diameter edits.

---

## Acceptance criteria

- [ ] The knob is made with a **single Full revolve** from one fully-defined half-section.
- [ ] The revolve **axis is on the centerline** and the profile **does not cross it**.
- [ ] A **chamfer** and a **partial/flat cut** are present and renamed.
- [ ] A bore + counterbore exists (Hole feature preferred).
- [ ] Rebuild test passes for height and grip-diameter edits with zero red features.

---

## Hints

<details>
<summary>The revolve errors with "self-intersecting" or won't preview</summary>

Your profile crosses the axis, or it isn't a single closed region. Roll back into the sketch: make sure every profile entity is on the **right** of the construction line, the region is **closed**, and the axis is **construction** geometry (it shouldn't be part of the profile).

</details>

<details>
<summary>The revolve made a thin ring instead of a solid knob</summary>

You revolved an *open* profile (it didn't close back to the axis), so OnShape made a thin-walled shape. Close the bottom edge all the way to the axis so the region is solid.

</details>

<details>
<summary>The flat cut removed the wrong side / too much</summary>

The Remove took the material on the wrong side of your chord line. Re-check which side of the 8 mm line your closed cut region is on — it should enclose the sliver *outside* the ⌀22 surface, not the core of the grip. Flip the region or re-draw it.

</details>

---

When this feels comfortable, move to [Exercise 3 — Holes, fillets, and a shell](exercise-03-holes-fillets-shell.md).
