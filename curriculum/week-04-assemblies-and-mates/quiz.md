# Week 4 — Quiz

Ten questions on degrees of freedom, mate types, and assembly strategy. Take it with your lecture notes closed. Aim for 9/10 before moving to Week 5. Answer key at the bottom — don't peek.

---

**Q1.** How many degrees of freedom does a single, unconstrained rigid body have in 3D space?

- A) 3 — one translation per axis.
- B) 6 — three translations and three rotations.
- C) 9 — three each of translation, rotation, and scale.
- D) It depends on the part's geometry.

---

**Q2.** In OnShape, a mate is best described as:

- A) glue that bonds two parts into one body.
- B) a constraint that removes degrees of freedom between two parts.
- C) a feature that merges two Part Studios.
- D) a fastener like a bolt or weld.

---

**Q3.** You want a hinge that swings about one axis and nothing else. Which mate?

- A) Fastened
- B) Slider
- C) Revolute
- D) Cylindrical

---

**Q4.** A **Cylindrical** mate leaves which degrees of freedom?

- A) 1 rotation only (like a hinge).
- B) 1 translation only (like a drawer).
- C) 1 rotation **and** 1 translation, both about/along the same axis.
- D) 0 — the part is locked solid.

---

**Q5.** You insert the first part into a new Assembly and drag a second part — the **entire assembly slides around together** as one unit. What's wrong?

- A) The parts are over-constrained.
- B) Nothing is grounded; you need to **Fix** a base part.
- C) The mate connector axes are flipped.
- D) The parts are in different units.

---

**Q6.** Mates in OnShape attach to:

- A) faces directly — you pick two faces and OnShape bonds them.
- B) **mate connectors** — coordinate frames (origin + X/Y/Z) on each part.
- C) the part's center of mass.
- D) the assembly origin only.

---

**Q7.** You insert a sub-assembly that contains an internal revolute joint. In the parent assembly you drag the part that should swing, but it **won't move**. Why?

- A) Sub-assemblies can't contain mates.
- B) The sub-assembly is **rigid** by default; you must **make it flexible** for its internal DOF to act in the parent.
- C) The internal mate was deleted on insertion.
- D) You need to re-fix the parent.

---

**Q8.** Using the Kutzbach criterion `DOF = 3·(n − 1) − 2·j`, a planar **four-bar linkage** (4 links, 4 revolute joints) has how many degrees of freedom?

- A) 0
- B) 1
- C) 2
- D) 3

---

**Q9.** You need eight M4 cap screws around a flange. The best workflow is:

- A) model one hex screw in a Part Studio and copy-paste it eight times.
- B) insert eight separate screws from the library and mate each by hand.
- C) pull **one** correctly-sized screw from the **Standard Content library**, fasten it, then **Replicate** it to all eight holes.
- D) draw the screws as cosmetic sketches in the assembly.

---

**Q10.** Your hinged lid is fine at 0° but, dragged to 120°, the lid passes **through** the box's back wall. Interference detection at rest (0°) showed zero. What's the correct conclusion?

- A) The assembly is fine — interference at 0° was zero, so it passes.
- B) This is a **motion interference**; you must check interference across the **full range of motion**, then add a **mate limit** or change geometry so the lid clears.
- C) Interference detection is unreliable for moving parts; ignore it.
- D) The lid is under-constrained and needs a second revolute.

---

**Q11.** *(Bonus)* You apply a Revolute mate expecting a swing, but when you drag the part it both swings **and** slides along the pin. The most likely cause is:

- A) you actually used a **Cylindrical** mate, which adds the translation.
- B) the part is grounded.
- C) the units are wrong.
- D) the mate connector has an offset.

---

**Q12.** *(Bonus)* In-context (top-down) design references the surrounding assembly geometry. After you move the neighboring parts, your in-context part doesn't follow. Why?

- A) In-context design is broken in OnShape.
- B) The in-context reference is a **snapshot**; you must **update the context** for the part to pick up the changes.
- C) You need to delete and re-create the part.
- D) In-context parts never update.

---

## Answer key

<details>
<summary>Click to reveal answers</summary>

1. **B** — A free rigid body has six DOF: three translations (along X, Y, Z) and three rotations (about X, Y, Z). Mates subtract from these.
2. **B** — A mate is a *constraint on motion*, not glue. It removes some of the six DOF. This is the core mental model of the whole week.
3. **C** — Revolute leaves exactly 1 rotational DOF about the connectors' shared axis and removes the other five. A hinge.
4. **C** — Cylindrical leaves 1 rotation **and** 1 translation, both tied to the same axis (a shaft that spins and slides). Revolute is rotation-only; Slider is translation-only.
5. **B** — Nothing is fixed, so the whole assembly is one free body. Every assembly needs a grounded reference: **Fix** the base part.
6. **B** — Mates connect **mate connectors** (origin + X/Y/Z triads), not faces directly. OnShape offers implicit connectors as you hover, and you can create explicit ones.
7. **B** — An inserted sub-assembly is **rigid** by default (internal mates frozen). Right-click → **Make flexible** to let its internal DOF act in the parent.
8. **B** — `DOF = 3·(4−1) − 2·4 = 9 − 8 = 1`. The four-bar linkage is the canonical 1-DOF closed-loop mechanism. Drive one link, the others follow.
9. **C** — Mate one correct, library-sized screw, then **Replicate** it across the hole pattern. Never hand-model fasteners; never hand-place eight of them (one will be subtly wrong).
10. **B** — Interference at rest is not enough. This is a **motion interference**; check the full range, then clamp the swing with a **mate limit** or change geometry so the lid clears the wall.
11. **A** — Cylindrical adds a translation that Revolute doesn't. If a "hinge" also slides along its axis, you picked Cylindrical. Delete and reapply as Revolute.
12. **B** — In-context references are snapshots by design (so the assembly doesn't thrash on every nudge). When neighbors change, **update the context** to refresh the dependent geometry.

</details>

---

If you scored under 7, re-read the lectures for the questions you missed — especially the DOF-per-mate table in Lecture 1. If you scored 9 or 10, you're ready for the [homework](./homework.md).
