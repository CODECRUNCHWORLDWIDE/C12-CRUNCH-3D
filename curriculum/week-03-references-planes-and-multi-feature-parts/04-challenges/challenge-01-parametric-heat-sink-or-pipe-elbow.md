# Challenge 1 — Parametric Heat Sink or Pipe Elbow

**Time estimate:** ~90–120 minutes.

## Problem statement

Model **one** multi-feature part — your choice of a **finned heat sink** or a **flanged pipe elbow** — that combines everything this week taught. The part **must** include:

1. **At least one non-default construction plane** (offset, angled, point–normal, or mid plane) that a feature genuinely sits on.
2. **At least one swept or lofted feature** that does real work in the part (not a token throwaway).
3. **At least one pattern** (linear, circular, or mirror) of a single seed feature.
4. **One nominated driving dimension** such that changing it cleanly rebuilds the *whole* part — every dependent feature follows, nothing turns red.

You reproduce the part from the spec below (pick A or B). Use real millimeter dimensions; don't eyeball.

---

## Option A — Finned heat sink

A rectangular base with a bank of thin fins and four mounting holes.

**Target dimensions (your nominated driving dimension is `#finCount`):**

- Base: 60 mm × 60 mm × 5 mm thick, **centered on the origin**.
- Fins: 1.5 mm thick, 25 mm tall, spanning the full 60 mm depth.
- Fin bank: `#finCount` fins (start at 15) at `#finPitch` = 4 mm pitch, **centered** on the base.
- Four M4 clearance mounting holes near the corners.
- A **swept or lofted** feature somewhere real — e.g. a **swept** rounded lead-in rail along the base's front edge, or a **lofted** transition boss on the underside for a fan duct.
- Break all sharp edges with a chamfer or fillet (dress-up last).

**The required pieces map like this:** the fins on the **Front plane** extruded full-depth, **linear-patterned** centered (pattern ✔); a **mid plane** or **offset plane** for the swept rail or lofted boss (non-default plane ✔); the **sweep/loft** itself (✔); `#finCount` as the nominated driving dimension (✔).

---

## Option B — Flanged pipe elbow

A 90° elbow pipe with a flange at each end and a bolt circle on each flange.

**Target dimensions (your nominated driving dimension is `#bolts`):**

- Pipe bore: Ø30 mm, wall 4 mm (so Ø38 mm outer), **swept** along a 90° centerline path of bend radius 40 mm.
- A **flange** at each end: Ø80 mm × 10 mm thick disc, concentric with the pipe end. (Sketch each flange on a **point–normal plane** at the path's end, or on the pipe's end face.)
- A **bolt circle** of `#bolts` (start at 4) M6 clearance holes on each flange, BCD = 60 mm — built as a **circular pattern** about each flange's named **axis**, then the second flange's ring **mirrored** or independently patterned.
- Fillet the pipe-to-flange junctions; break sharp edges.

**The required pieces map like this:** the **swept** pipe along the 90° path with a **point–normal** profile plane (sweep ✔, non-default plane ✔); the **circular-patterned** bolt holes (pattern ✔); `#bolts` as the nominated driving dimension (✔).

---

## Acceptance criteria

- [ ] One OnShape Part Studio in a Document named clearly (e.g. `C12-Week3-Challenge`), single connected part.
- [ ] **Units: millimeter.** Length precision 2–3 decimals.
- [ ] **At least one non-default construction plane** that a feature actually sits on (named meaningfully).
- [ ] **At least one swept or lofted feature** doing real work, with its profile on a correct reference plane (point–normal for sweep, offset planes for loft).
- [ ] **At least one pattern** (linear/circular/mirror) from a **single seed** feature, about a **named axis** if circular.
- [ ] **Every driving sketch fully defined (black).**
- [ ] **Every feature, plane, axis, and variable renamed** by its job. No `Plane 1 / Extrude 2 / Sweep 1` survivors.
- [ ] **The parametric rebuild test passes (heavily weighted):** change your **nominated driving dimension** across the tested range and confirm the whole part rebuilds with **zero red features** (see below).
- [ ] A created **Version** named `Week 3 challenge` and a **shared public link**.
- [ ] A short **walkthrough** (Document notes or a Markdown/PDF) covering the documentation points below.

### The parametric rebuild test (heavily weighted)

1. State your **nominated driving dimension** (`#finCount` for A, `#bolts` for B — or another you choose and justify).
2. Change it across a sensible range and regenerate at each step:
   - **Option A:** `#finCount` from 15 → 10 → 20. (Optionally also flex `#finPitch` and the base size.)
   - **Option B:** `#bolts` from 4 → 6 → 8 on both flanges. (Optionally also flex the bend radius and bore.)
3. **No feature may turn red** anywhere in the range. The part must stay manufacturable — no fins falling off the base, no bolt holes missing the flange, no sweep self-intersecting.
4. **Document it:** the dimension tested, the values tried, and a one-line confirmation it rebuilt clean. If something *did* break and you fixed it (e.g. you tied `#finCount × #finPitch` to the base width so fins can't fall off), **describe the fix** — that earns more credit than a part that never broke, because it proves you understand *why* it's robust.

---

## Walkthrough requirements

Your write-up must include:

1. **Which option** (A or B) and a one-line description of the part.
2. The **nominated driving dimension** and the **range tested**, with the rebuild confirmation.
3. For your **non-default plane**: which type, what it references, and why you used a plane instead of a face there.
4. For your **sweep/loft**: the profile plane and path/profiles used, and why sweep-vs-loft was the right choice.
5. For your **pattern**: the seed, the axis/direction, the variable driving the count, and how you kept it centered/on-part.
6. One **reference you rejected** and why (e.g. "I almost sketched the fins on the base's top face, but that face gets chamfered later, so I used the Front plane instead").

---

## Stretch

- **Make it a family.** Add a second nominated dimension and confirm *both* flex independently and together. (This is a dry run for Week 5 Configurations.)
- **Helical sweep.** On Option A, replace a straight rail with a **twisted** sweep, or add a coiled feature; note where it self-intersects.
- **Three-profile loft.** On Option B, replace a flange's flat face with a **lofted** square-mount-to-round-pipe transition (square bolt plate → round pipe) using three stacked profiles.
- **Measure it.** Use OnShape's **Measure** and **Mass properties** tools to report the part's volume and (with a material assigned) mass. Sanity-check it against a hand estimate.

---

## Hints

<details>
<summary>Heat-sink fins: how to keep them centered when the count changes</summary>

Model **one** fin on the **Front plane**, extruded the full base depth. Linear-pattern that fin feature in one direction with **Instance count = `#finCount`**, **Spacing = `#finPitch`**, and the pattern's **centered/symmetric** option **on**. Centered means the bank always straddles the base midline, so adding fins grows it both ways instead of running it off one edge. Tie nothing to a corner.

</details>

<details>
<summary>Pipe elbow: getting the sweep to start clean</summary>

Sketch the 90° centerline path (two tangent lines and a 40 mm arc, or a single arc) on the **Front** plane. Build a **Point–normal plane** at the path's start vertex (normal = the starting tangent), sketch the **annular** pipe cross-section there (Ø38 outer, Ø30 inner) centered on the start point, and sweep. The point–normal plane is what keeps the section square to the path so it doesn't skew at the start.

</details>

<details>
<summary>My circular bolt pattern breaks when I change the count</summary>

Confirm the pattern spins about a **named construction Axis** through the flange center (not an inferred face axis), uses **Angle = 360° / Equal spacing**, and the **seed hole** is positioned at `#bcd / 2` radius. With those three in place, changing `#bolts` just re-divides the circle.

</details>

---

## Submission

1. Create a **Version** named `Week 3 challenge`.
2. **Share** the Document publicly (or to your cohort) — copy the share link.
3. Post the link plus your walkthrough in your cohort tracker.
4. Confirm a fresh viewer can open it, read your renamed tree, and change your nominated dimension to watch it rebuild. If they can't, the tree isn't clean enough yet.

## Why this matters

Every part you'll build for the rest of C12 — the Week 4 assembly components, the Week 5 configured family, the Week 6 capstone mechanism — has to *flex without breaking*. The teams that ship robust CAD aren't the ones who model the prettiest first version; they're the ones whose models survive the inevitable "can you make it 20% bigger?" without a rebuild from scratch. This challenge is where you build that reflex.
