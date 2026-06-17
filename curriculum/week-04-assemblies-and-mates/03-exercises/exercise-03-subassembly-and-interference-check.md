# Exercise 3 — Sub-Assembly + Interference Check

**Goal:** Learn to *organize* and *validate* a mechanism, not just mate it. You'll take the hinge from Exercise 1's parts, build it as a **reusable sub-assembly**, insert that sub-assembly into a parent assembly, make it **flexible** so its joint still moves, and then run **interference detection** through the **full range of motion** to prove the moving leaf never passes through anything it shouldn't.

**Estimated time:** 45 minutes.

Work in the same Document `C12-W4-Assemblies`. You'll reuse `Leaf-A`, `Leaf-B`, and `Pin` from Exercise 1, plus one new part. You'll create a sub-assembly tab `Sub-Hinge` and a parent assembly tab `Ex3-Lid-Box`.

---

## The scenario

You're building a small **hinged-lid box**: a box base with a lid that flips open on a hinge. The hinge itself is a self-contained mechanism, so it belongs in its **own sub-assembly** that you can reuse and that encapsulates the swing motion. The parent assembly holds the box base, the lid, and an instance of the hinge sub-assembly.

---

## Step 1 — Add a new part: `Box-Base`

In a Part Studio **`Box-Base`**:

1. Sketch **100 mm × 70 mm** on the Top plane; extrude **40 mm**.
2. **Shell** to **4 mm**, removing the **top face** (an open-top box).
3. Along the top of one **70 mm-wide back wall**, add a **knuckle boss** (Ø8 mm cylinder, 60 mm long) so the hinge pin can mount to the box. Cut a **Ø4.2 mm** bore through it for the pin.
4. Rename **`Box-Base`**.

You'll treat `Box-Base` as the lid's frame; the hinge sub-assembly will carry the swinging lid.

---

## Step 2 — Build the `Sub-Hinge` sub-assembly

1. Add a new **Assembly** tab; rename it **`Sub-Hinge`**.
2. Insert **`Pin`** and **`Leaf-B`** (the swinging leaf will become the lid bracket). **Fix** the `Pin`.
3. **Revolute**-mate `Leaf-B` to the `Pin` (bore-axis connector to pin-axis connector), exactly as in Exercise 1. Rename it **`Lid swing`**.
4. Add a **0–110°** limit to `Lid swing`.
5. Drag `Leaf-B` — it swings about the pin, 1 DOF. The hinge mechanism is now a tidy, self-contained sub-assembly.

```
Sub-Hinge: Drag test · 1 DOF · swings 0–110° · 0 interferences
```

> Why a sub-assembly? Because the hinge is a *unit*. If this box needed three hinges, you'd insert this one sub-assembly three times instead of re-mating a pin and leaf nine times. Encapsulating mechanism is the habit that scales to the Week 6 capstone.

---

## Step 3 — Build the parent assembly `Ex3-Lid-Box`

1. Add a new **Assembly** tab; rename it **`Ex3-Lid-Box`**.
2. Insert **`Box-Base`**; **Fix** it (it's the world).
3. Insert the **`Sub-Hinge`** sub-assembly — it appears as a **single instance** node in the instance list, with its internal parts nested under it.
4. **Fastened**-mate the `Sub-Hinge`'s `Pin` into the **`Box-Base` knuckle bore** so the hinge's pin axis lines up with the box's back-wall knuckle. Rename **`Hinge mount`**.

At this point the sub-assembly is **rigid** by default: even though `Lid swing` exists inside it, the parent treats `Sub-Hinge` as one frozen unit. Drag `Leaf-B` in the parent — **it won't move yet.** That's expected.

---

## Step 4 — Make the sub-assembly flexible

1. In the parent's instance list, **right-click the `Sub-Hinge` instance → Make flexible.**
2. Now the sub-assembly's internal `Lid swing` DOF is alive in the parent.
3. **Drag `Leaf-B`** in the parent — it swings about the pin, **0–110°**, relative to the fixed box. The lid opens.

```
Ex3-Lid-Box: Drag test · 1 DOF (flexible sub-assembly) · lid swings 0–110° · interference TBD
```

> This is the key lesson: a sub-assembly is **rigid until you flex it**. Mechanisms you want to actuate in the parent must be made flexible. Rigid is the default because most placed sub-assemblies (a bracket bolted on, a fixed module) shouldn't wiggle.

---

## Step 5 — Interference detection through the full range

A lid that swings into its own box wall is a broken design. Prove it doesn't.

1. **Pose the lid closed (0°):** set the `Lid swing` mate value to 0°. Run **Interference detection** across the whole assembly. Expect **0** (or note any intentional fit).
2. **Pose the lid open (110°):** set the mate value to 110°. Run **Interference detection** again. Expect **0**.
3. **Sweep the middle:** drag the lid slowly from 0° to 110°, watching for any point where the leaf clips the box's back wall or knuckle. If you suspect a tight spot, set the mate value there and run interference at that angle.

If interference appears at some angle:

- **At a specific mid-angle:** geometry collision. Either trim the offending corner of the leaf, move the pin axis outward, or tighten the **mate limit** so the lid stops before the collision.
- **At rest (0°), always:** a static modeling error — the knuckle bore is too small for the pin, or two solids overlap. Fix the geometry.

> **The C12 rule (from Lecture 2):** an assembly that moves passes only when it moves through its **full range with zero interferences**. Checking only the rest pose is not enough — check the extremes and the sweep.

---

## Step 6 — Final drag test

With interference cleared at both extremes:

```
Drag test · 1 DOF · lid swings 0–110° through full range · 0 interferences
```

---

## Acceptance criteria

You can mark this exercise done when:

- [ ] A **`Sub-Hinge` sub-assembly** exists, self-contained, with a renamed `Lid swing` revolute (0–110° limit) and a 1-DOF internal drag test.
- [ ] A **parent assembly `Ex3-Lid-Box`** with `Box-Base` fixed and `Sub-Hinge` inserted as a single instance, fastened to the box.
- [ ] The sub-assembly is **made flexible**, and the lid swings in the parent — you can demonstrate that it does **not** move while rigid and **does** move once flexible.
- [ ] **Interference detection** run at **0°, 110°, and across the sweep** returns **zero** interferences (or only a documented intentional fit).
- [ ] You can explain, in your own words: why the hinge is a sub-assembly, why it's rigid by default, what "make flexible" changed, and why you check interference at the extremes rather than only at rest.

---

## Stretch

- Insert the `Sub-Hinge` **a second time** on the other end of the box (a two-hinge lid). Make both flexible; confirm the lid still swings cleanly with both hinges (this is now slightly over-constrained in a benign, real-world way — note what you observe).
- Add a **Measure**-verified clearance: confirm the lid's edge keeps ≥1 mm gap from the box rim throughout the swing by measuring at the tightest angle.
- Add the actual **lid panel** as a separate part fastened to `Leaf-B`, so the swinging element looks like a real lid, then re-run interference with the panel included.

---

## Hints

<details>
<summary>The lid won't move in the parent even though the sub-assembly's mate exists</summary>

The sub-assembly is **rigid**. Right-click its instance in the parent → **Make flexible**. Rigid sub-assemblies freeze their internal mates by design.

</details>

<details>
<summary>Interference is reported at every angle, including 0°</summary>

That's a static error, not a motion one. Check the pin/bore fit — the Ø4.2 mm bore should clear the Ø4 mm pin. Also confirm the `Hinge mount` Fastened didn't bury the pin inside the box wall; offset it so the pin sits in the knuckle bore, not through solid material.

</details>

<details>
<summary>The lid clips the box only between ~95° and 110°</summary>

The lid is swinging into the back wall near full-open. Either reduce the max **limit** (e.g., stop at 95°) or move the pin axis up/out so the lid clears. Set the mate value to the failing angle and run interference there to see exactly which faces clash.

</details>

---

You've now built, organized, and *validated* a mechanism. That's the full Week 4 loop. Take it into the [challenge](../04-challenges/challenge-01-four-bar-linkage.md) (a 1-DOF four-bar linkage) and the [mini-project](../07-mini-project/00-overview.md) (your running part, now articulating).
