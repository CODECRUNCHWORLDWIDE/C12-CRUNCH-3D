# Exercise 3 — Arc and Slot Lever Profile

**Goal:** Combine everything — tangent arcs, the slot tool, concentric circles, a construction centerline, and `equal`/`symmetric`/`tangent` constraints — into **one fully-defined lever profile**. This is the most complete sketch of the week and a direct rehearsal for the mini-project. It's a modeling task; build it in OnShape by hand, no code.

**Estimated time:** 45 minutes.

---

## The target part

A flat **pivot lever**: a long body with a rounded pivot boss at one end (a hole through it) and a straight slot near the other end. Picture a control-arm or a wiper-style link. Key facts:

- The body runs **horizontally**, centered on a construction centerline through the origin.
- The **pivot** end is a rounded boss centered on the origin, with a concentric pivot hole.
- The **far** end carries a **slot** aligned along the centerline.
- The two long edges of the body are **tangent** to the pivot boss arc and **parallel** to each other.

Target dimensions (metric):

| Feature | Value |
|---------|-------|
| Pivot boss outer diameter | ⌀30 mm |
| Pivot hole diameter | ⌀12 mm |
| Body width (between long edges) | 20 mm |
| Pivot-center to slot-center distance | 90 mm |
| Slot overall length | 24 mm |
| Slot width (and end-arc) | 8 mm |

---

## Step 1 — Document, units, centerline

1. Create a Document **`C12-W1-Ex3-Lever`**, units **millimeter**.
2. Start a **sketch** on the **Top** plane.
3. Toggle **construction** (`q`) and draw a **horizontal construction centerline** starting at the **origin**, running to the right. Make it **horizontal** and anchor its start to the origin. This is the spine of the whole part.

---

## Step 2 — The pivot boss (concentric circles)

1. Draw an **outer** center-point circle centered on the **origin** (coincident).
2. Draw an **inner** center-point circle; apply **concentric** to the outer so they share the origin as center.
3. Dimension: outer **⌀30 mm**, inner **⌀12 mm**.

The pivot boss is now fully defined and centered on the origin.

---

## Step 3 — The slot at the far end (slot tool)

1. Pick the **slot** tool (the straight-slot variant — center-to-center).
2. Place the slot **along the construction centerline**, out to the right of the pivot. The slot tool draws two parallel lines capped by two equal semicircular end-arcs, already mostly constrained (parallel sides, equal/tangent end arcs).
3. Make the slot's long axis **collinear** with the construction centerline (select the slot centerline / its center points and the construction line; apply **coincident**/**collinear** so the slot sits exactly on the spine). This keeps it aligned when the lever lengthens.
4. Dimension the slot: **length 24 mm** (center-to-center of the end arcs plus the arcs — use the slot's length dimension) and **width 8 mm**.
5. Dimension the **pivot-center to slot-center distance** along the centerline: **90 mm**. This is the one dimension that defines the lever's *reach*.

The slot should now be black. The 90 mm is your "real" functional dimension.

---

## Step 4 — The body (tangent + parallel + equal)

Now connect the pivot boss to the slot with the lever body's two long edges.

1. Using the **line** tool, draw the **top** long edge: start it at the **top of the pivot boss arc** and end it near the slot's top edge. Start a **tangent arc** or let the line meet the boss — then apply a **tangent** constraint between this line and the pivot boss outer circle so the edge blends smoothly into the boss (no kink).
2. Draw the **bottom** long edge similarly, **tangent** to the pivot boss on the lower side.
3. Apply **parallel** between the top and bottom long edges (they must stay parallel as the part flexes its dimensions).
4. Make the body **symmetric about the construction centerline:** select the top edge, bottom edge, and the centerline → apply **symmetric**. Now both edges mirror the spine.
5. Constrain the **body width**: dimension the perpendicular distance between the two long edges → **20 mm**. (Because they're symmetric about the centerline, this is the one width dimension you need.)
6. Trim/close the profile at the slot end so the body forms one closed loop with the slot's outer boundary (use **trim** to clean up overlap where the body edges meet the slot end arc, and apply **coincident**/**tangent** where they join).

---

## Step 5 — Drive out the last blue

Run the **drag test**. Grab any edge or point and try to drag it. If anything moves:

- A long edge not **tangent** to the boss? Add tangent.
- The slot not **collinear** with the centerline? Add coincident/collinear.
- A junction point not **coincident** where two edges meet? Add coincident.
- The body width missing? Dimension it (20 mm).

Keep going until **every entity is black** and the status bar reads **"Fully defined."**

Total dimensions you should need: **6** (⌀30, ⌀12, slot length 24, slot width 8, reach 90, body width 20). Everything else — tangency, parallelism, symmetry, concentricity — is carried by **constraints**. That ratio (6 dimensions, many constraints) is what a well-built profile looks like.

---

## Step 6 — Test the parametrics, then version

1. Double-click the **90 mm** reach → change to **`120 mm`**. The lever *stretches*; the body edges stay tangent to the boss and parallel; the slot rides out to the new position. This is the payoff.
2. Change the **body width 20** → **`16`**. Both edges close in symmetrically about the spine.
3. Restore `90` and `20`.
4. Exit the sketch (✓), rename it **`Lever master profile`**.
5. **Versions and history** → **Create version** → **`ex3-lever-defined`**.

---

## Acceptance criteria

You can mark this exercise done when:

- [ ] The lever sketch is **fully defined** — all geometry **black**, status bar "Fully defined."
- [ ] It is **one closed profile** (pivot boss outer + body edges + slot outer), anchored to the **origin**.
- [ ] The pivot circles are **concentric**; the body edges are **tangent** to the boss and **parallel**/**symmetric** about the construction centerline.
- [ ] You used exactly **6** driving dimensions (or fewer) — the rest is constraints.
- [ ] Changing the 90 mm reach cleanly stretched the lever with no broken geometry.
- [ ] The sketch is renamed and you created a named **Version**.

---

## Stretch

- Add a **second** slot mirrored across the centerline... no — instead add a small ⌀5 oil hole on the centerline, **midpoint** between pivot and slot, and notice it needs **zero** dimensions (it's pinned to the centerline and a midpoint).
- Replace the straight-slot tool with a **hand-built** slot: two parallel lines, two tangent end arcs, an `equal` between the arcs. Fully define it manually. Appreciate how much the slot tool did for you.
- Turn on **Show constraints** and screenshot the fully-decorated lever. Count the constraints. You'll likely have 15+ constraints to just 6 dimensions — that's a robust profile.

---

## Hints

<details>
<summary>My body edge meets the pivot boss at a kink, not a smooth blend</summary>

Select the edge line and the pivot boss outer circle, then apply the **tangent** constraint. The line will rotate so it meets the circle tangentially. If it flips to the wrong side, undo and re-draw the line starting nearer the correct tangent point so inferencing picks the right one.
</details>

<details>
<summary>The slot won't stay on the centerline</summary>

Select the slot's internal centerline (or its two arc-center points) together with your construction centerline and apply **coincident** (or **collinear** for the lines). That ties the slot's axis to the spine so it can't drift off-axis.
</details>

<details>
<summary>It went red/yellow when I added the body width dimension</summary>

You probably already locked the width another way (e.g., both edges dimensioned to the centerline *and* a width dimension between them). Delete the redundant one — keep either the symmetric-about-centerline relationship *or* explicit edge offsets, not both. The over-definition prompt is telling you the width is already determined.
</details>

---

This profile is the template for the mini-project. When it's solid, open the [mini-project spec](../07-mini-project/00-overview.md) and build your own running-project master sketch.
