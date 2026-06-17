# Exercise 3 — Sweep & Loft

**Goal:** Model two shapes you cannot make with a straight extrude. First, **sweep** a round profile along a bent U-shaped path — starting the profile on a **point–normal plane** so the sweep begins clean. Then **loft** a smooth square-to-round transition between two profiles on stacked **offset planes**, pinning connection points so it doesn't twist.

**Estimated time:** 50 minutes.

**You'll use:** Sketch, Plane (Point–normal, Offset), Sweep, Loft, the rebuild test.

> This is a modeling task, not code. Follow the numbered steps in OnShape. Build it yourself.

---

## Part A — A swept handle

### A1 — The path

1. New **Part Studio** tab: `Ex3 - Sweep`.
2. **Sketch** on the **Front** plane the handle centerline as a **U-shape**:
   - Two vertical lines, 60 mm tall, 50 mm apart, joined at the top by a **180° arc** (radius 25 mm) so the three segments form a continuous, tangent U. Make the verticals **vertical** and **tangent** to the arc; dimension the height (60 mm) and the width (50 mm).
   - Fully define (**black**).
3. Accept. **Rename `Handle path`.**

### A2 — The point–normal profile plane

The profile must sit *perpendicular to the path at its start*. That's a point–normal plane.

1. Click the **Plane** tool. **Plane type → Point–normal** (sometimes "Point and normal").
2. **Point** = the bottom endpoint of one vertical line (the path's start vertex).
3. **Normal** = that vertical line itself (its direction is the path's starting tangent).
4. Green check. **Rename `Profile plane`.**

### A3 — The profile

1. **Sketch** on `Profile plane`.
2. Draw a circle **centered on the path start point**, Ø`#handleDia = 8 mm`. (Anchor the circle center coincident with the path endpoint so the sweep starts on-axis.) Fully define.
3. Accept. **Rename `Handle profile`.**

### A4 — The sweep

1. Click **Sweep**.
2. **Profile (sweep face/section)** = `Handle profile`.
3. **Path** = `Handle path`.
4. **Operation = New** (a standalone handle).
5. Leave orientation at the default (**follow path** / keep perpendicular).
6. Green check. **Rename `Handle`.**

You now have a round handle that bends through the U.

### A5 — Rebuild test

- Change `#handleDia` **8 → 12 mm**, regenerate. The handle thickens along its whole length. No red.
- Change the arc radius **25 → 15 mm**, regenerate. The U tightens; the handle follows. No red — *unless* the profile is too fat for the bend.
- **Push it to break:** raise `#handleDia` toward 30 mm with the 15 mm arc radius. At some point the sweep **self-intersects** on the inside of the tight bend and OnShape errors. That's geometry, not a bug: a section can't make a turn whose inner radius is smaller than the section. **Note the diameter where it failed in your write-up** — diagnosing this limit is the learning.
- Set values back to 8 mm / 25 mm.

---

## Part B — A square-to-round loft

### B1 — Bottom profile

1. New **Part Studio** tab: `Ex3 - Loft`.
2. **Sketch** on **Top**: a center-point **square**, 40 × 40 mm, centered on the Origin. Fully define. Accept. **Rename `Loft bottom (square)`.**

### B2 — Top profile on an offset plane

1. **Plane → Offset** from **Top**, distance `#loftHeight = 60 mm`. **Rename `Loft top plane`.**
2. **Sketch** on `Loft top plane`: a **circle** centered on the Origin projection, Ø30 mm. Fully define. Accept. **Rename `Loft top (circle)`.**

### B3 — The loft

1. Click **Loft**.
2. Add **Profile 1 = `Loft bottom (square)`**, then **Profile 2 = `Loft top (circle)`** (order = bottom then top).
3. **Operation = New.**
4. Look at the preview. If the transition **spirals/twists**, OnShape is connecting a square corner to a misaligned point on the circle. Drag the **connection point** dots so a square corner lines up with a sensible point on the circle (4 connections, one per corner, keeps it clean and symmetric).
5. Green check. **Rename `SQ-to-round`.**

### B4 — Rebuild test

- Change `#loftHeight` **60 → 90 mm**, regenerate. The transition stretches taller. No red.
- Change the circle **Ø30 → Ø50 mm** (now wider than the square is... still smaller than 40 across the flats but larger than the corner inset — observe how the blend bulges). Regenerate. No red, but watch the shape change.
- Optional: change the bottom square **40 → 25 mm** so the *top* is now wider than the bottom — the loft inverts cleanly. No red.
- Set values back.

---

## Part C — Sweep vs. loft, in writing

Write two sentences (in the Part Studio notes or your own log):

1. *Why was Part A a **sweep** and not a loft?* (The cross-section stayed the **same** circle along a path — that's sweep. Loft is for a section that **changes** shape between profiles.)
2. *Why did Part B need **offset planes** and a **point–normal plane wasn't** the right tool there?* (Loft profiles sit on parallel planes at different heights — offset planes. Sweep needed a plane **perpendicular to a path**, which is point–normal.)

Getting this distinction crisp now saves you from reaching for the wrong tool in the mini-project.

---

## Expected outcome

Two Part Studios:

- `Ex3 - Sweep`: a `Handle` swept along a `Handle path`, with its profile on a `Profile plane` (point–normal), diameter driven by `#handleDia`, and a documented self-intersection limit.
- `Ex3 - Loft`: a `SQ-to-round` loft between a square and a circle on stacked offset planes, twist-free via pinned connection points, height driven by `#loftHeight`.
- Every plane and feature renamed by its job.
- Both shapes proven parametric (and one documented geometric limit).

Create a **Version** named `Ex3 complete`.

---

## Acceptance criteria

- [ ] A **sweep** of a constant round profile along a bent path, profile on a **point–normal plane** at the path start.
- [ ] A **loft** between two profiles on two **offset planes**, twist-free (connection points pinned).
- [ ] Profile/height **driven by variables**; rebuild test run; the sweep's self-intersection limit documented.
- [ ] The two-sentence sweep-vs-loft note written.
- [ ] All driving sketches **black**; every plane and feature renamed; a Version created.

---

## Stretch

- Add a **Shell** (Week 2) to the handle to hollow it into a tube — or sweep a profile that's already an annulus (outer circle minus inner circle).
- Add **Twist** to the sweep (a half-turn over the path) and watch the section spin — the basis of springs and augers.
- Loft a **three-profile** stack: square (Top) → rounded-square (offset 30) → circle (offset 60). Pin connections at each stage; aim for a continuously fair transition.
- Add a **guide curve** to the loft (a sketched edge running corner-to-edge up the side) to control how the blend bulges, instead of letting OnShape interpolate freely.

---

## Hints

<details>
<summary>The sweep fails immediately, before I even resize it</summary>

Almost always the **profile plane isn't perpendicular to the path start**, or the profile isn't centered on the path's start point. Rebuild `Profile plane` as **Point–normal** with the point = path start vertex and the normal = the path's first segment, and make the circle's center **coincident** with that vertex.

</details>

<details>
<summary>My loft twists no matter what</summary>

You haven't pinned the **connection points**. In the Loft dialog, the preview shows draggable dots where each profile connects. Drag them so the square's corners map to evenly-spaced points on the circle (4 connections). A loft with no explicit connections lets OnShape guess, and it often guesses a spiral.

</details>

<details>
<summary>When I pick the second loft profile, the preview is empty or errors</summary>

Make sure both sketches are **closed** profiles (no open gaps) and on **different planes**. Two profiles on the same plane can't loft. Pick them in order (bottom, then top); picking out of order can invert the solid.

</details>

---

You've now drilled every multiplier and reference the mini-project needs. On to the [challenge](../04-challenges/challenge-01-parametric-heat-sink-or-pipe-elbow.md) and the [mini-project](../07-mini-project/00-overview.md).
