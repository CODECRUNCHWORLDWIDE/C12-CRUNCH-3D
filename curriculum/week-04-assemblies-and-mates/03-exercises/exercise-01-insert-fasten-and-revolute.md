# Exercise 1 — Insert, Fasten, and a Revolute Hinge

**Goal:** Build your first working mechanism — a two-leaf hinge that swings about a pin. You'll model three simple parts, insert them into an Assembly, **Fix** a base, **Fastened**-mate a pin, and add a **Revolute** mate so the second leaf swings with exactly **1 degree of freedom**. By the end the C12 drag test reads `1 DOF`.

**Estimated time:** 40 minutes.

---

## Setup

You need a free OnShape account and a browser. Create a new Document named `C12-W4-Assemblies`. Set **Document → Workspace units** to **millimeter**, length precision **2 decimals**, angle **degrees**. Everything below assumes millimeter.

You'll make three Part Studios (`Leaf-A`, `Leaf-B`, `Pin`) and one Assembly tab (`Ex1-Hinge`).

---

## Step 1 — Model `Leaf-A` (the fixed leaf)

In a Part Studio renamed **`Leaf-A`**:

1. On the **Top** plane, sketch a rectangle **60 mm wide × 40 mm deep**, one corner at the origin. Fully define it (dimension width and depth; the origin corner gives you the rest).
2. **Extrude** it **3 mm** (Blind, New). This is the flat plate of the leaf.
3. On the **front edge** of the plate, you need a **knuckle** — a cylinder the pin passes through. Sketch on the front face: a circle of **Ø8 mm** centered **5 mm** above the bottom and running along the front edge. (Center the circle on a construction line so it's fully defined.)
4. **Extrude** that circle **15 mm** as a cylinder boss (Add, merged to the plate) to form a knuckle on the left third of the front edge.
5. **Cut the pin bore:** sketch a **Ø4.2 mm** circle concentric with the knuckle and **Extrude → Remove → Through all** so the pin (Ø4 mm) passes through with a little clearance.
6. Rename the part **`Leaf-A`**. Confirm one solid body.

---

## Step 2 — Model `Leaf-B` (the swinging leaf)

In a new Part Studio **`Leaf-B`**, make a mirror-handed leaf whose knuckle fills the gap left by `Leaf-A`:

1. Repeat the **60 × 40 × 3 mm** plate.
2. Add a **Ø8 mm knuckle, 15 mm long**, but positioned to sit **beside** `Leaf-A`'s knuckle along the same pin axis (offset it to the right two-thirds of the front edge). The two knuckles will be coaxial in the assembly.
3. Cut the same **Ø4.2 mm** pin bore through the knuckle.
4. Rename the part **`Leaf-B`**.

> Don't obsess over the knuckles interleaving perfectly — for this exercise it's fine if they're simply two coaxial knuckles side by side. The point is the mate, not a museum-grade hinge.

---

## Step 3 — Model `Pin`

In a Part Studio **`Pin`**:

1. On the **Top** plane sketch a **Ø4 mm** circle at the origin.
2. **Extrude 35 mm** (Blind, New). That's the pin.
3. Add a tiny **0.3 mm chamfer** to both ends so it leads into the bore cleanly.
4. Rename the part **`Pin`**.

---

## Step 4 — Create the Assembly and insert parts

1. Add a new **Assembly** tab; rename it **`Ex1-Hinge`**.
2. Click **Insert**. From the current Document, insert **`Leaf-A`**. When OnShape offers to **Fix** the first inserted part, accept it — `Leaf-A` is your ground.
3. Insert **`Leaf-B`** and **`Pin`**; drop them in open space near the leaf. They're free bodies (6 DOF each).

You now have: `Leaf-A` fixed (0 DOF), `Leaf-B` and `Pin` free (12 DOF between them).

---

## Step 5 — Fasten the pin into `Leaf-A`

The pin shouldn't move relative to the fixed leaf — it's the axle.

1. Click **Fastened** in the mate toolbar.
2. Hover the **cylindrical face of `Pin`** — OnShape offers a mate connector on its axis (origin at the end, Z down the pin). Click it.
3. Hover the **bore of `Leaf-A`'s knuckle** — click the connector on its axis.
4. The pin snaps coaxial with the knuckle. If it's sticking out lopsided, edit the mate and **Offset** the pin connector along Z until the pin is centered through the knuckle (offset ≈ such that ~10 mm protrudes each side).
5. **Predict:** Fastened leaves **0 DOF** — the pin is now locked to the fixed leaf. Green check.
6. **Drag `Pin`.** It should not move. ✔

(12 → 6 DOF: only `Leaf-B` is still free.)

---

## Step 6 — Revolute-mate `Leaf-B` to the pin

Now the joint that matters.

1. Click **Revolute**.
2. Pick the connector on **`Leaf-B`'s knuckle bore** (its Z is the swing axis).
3. Pick the connector on the **`Pin` axis**.
4. `Leaf-B` snaps coaxial with the pin. **Predict:** Revolute leaves **1 rotational DOF** about the pin.
5. If `Leaf-B` lands flipped (pointing the wrong way), edit the mate and **Flip** one connector's axis.
6. Green check.
7. **Rename the mate `Lid swing`** (double-click it in the Mate features list).

---

## Step 7 — Drag test

Grab **`Leaf-B`** and drag.

- It should **swing about the pin axis** and do **nothing else** — no sliding along the pin, no floating.
- `Leaf-A` and `Pin` should stay put.

If `Leaf-B` slides along the pin as well as swinging, you accidentally used **Cylindrical**, not Revolute — delete and redo. If it doesn't move at all, you over-constrained it (an extra Fastened mate sneaked in) — check the Mate features list.

```
Drag test · 1 DOF · swings freely · 0 interferences
```

---

## Step 8 — Add a mate limit (the "laptop lid")

1. Edit the **`Lid swing`** Revolute mate.
2. Enable **Limits**: minimum **0°**, maximum **110°**.
3. Green check, drag `Leaf-B` again. It now **stops** at 0° (closed) and 110° (open), like a real lid.

---

## Acceptance criteria

You can mark this exercise done when:

- [ ] The Assembly `Ex1-Hinge` contains `Leaf-A` (fixed), `Pin` (fastened), and `Leaf-B` (revolute).
- [ ] `Leaf-A` does not move when dragged (it's the ground).
- [ ] `Leaf-B` swings about the pin with **exactly 1 DOF** and nothing else.
- [ ] The Revolute mate is renamed (e.g., `Lid swing`) — not `Revolute 1`.
- [ ] A 0–110° limit stops the swing at both ends.
- [ ] You can state, in your own words, the DOF bookkeeping: 18 → fix base → fasten pin → revolute leaf → **1 DOF**.

---

## Stretch

- Add a real **interleaved** knuckle (three knuckles on one leaf, two on the other) so it looks like a piano hinge. The mate is identical; only the geometry changes.
- Pose the hinge at exactly **45°** using a fixed **mate value** (not a limit) and take a screenshot of the open position.
- Replace the Fastened pin with an **interference (press) fit**: make the pin Ø4.2 mm into a Ø4.0 mm bore, fasten it, then run interference detection — observe the small intentional overlap and note it as a press fit.

---

## Hints

<details>
<summary>OnShape isn't offering a connector on the bore</summary>

Hover slowly over the *circular edge* of the bore or the *cylindrical inner face* — the connector appears on the axis with Z along it. If you get a face-normal connector instead, you're hovering the flat end face; move onto the curved surface.

</details>

<details>
<summary>The leaf swings but also drifts/floats</summary>

You have an under-constraint — likely the Revolute connected to the wrong entity. Delete the mate and re-pick the **bore axis** connectors specifically, not a face. Revolute on two coaxial bore connectors leaves exactly one rotation.

</details>

<details>
<summary>"Over-constrained" warning appears</summary>

You probably have two mates fighting (e.g., a leftover Fastened on `Leaf-B` plus the Revolute). Open the Mate features list, suppress mates one at a time until the warning clears, and delete the redundant one.

</details>

---

When this feels comfortable, move to [Exercise 2 — Slider, cylindrical, and a library bolt](./exercise-02-slider-cylindrical-and-the-content-library.md).
