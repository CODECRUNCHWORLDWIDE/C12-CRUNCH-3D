# Week 3 — Quiz

Ten questions on references, planes, and multi-feature parts. Take it with your lecture notes closed. Aim for 9/10 before moving to Week 4. Answer key is at the bottom — don't peek.

---

**Q1.** You need a sketch surface exactly 25 mm above the Top plane, and the 25 mm should track a boss-height variable. Which is the most robust approach?

- A) Sketch on the Top plane and extrude up 25 mm to reach the right height.
- B) Sketch directly on the boss's top face.
- C) Create an **Offset plane** from Top with distance `#bossHeight`, and sketch on it.
- D) Eyeball a plane near the boss top and sketch on it.

---

**Q2.** What is the defining difference between a **sweep** and a **loft**?

- A) Sweep works in 2-D; loft works in 3-D.
- B) Sweep drags **one constant** cross-section along a path; loft blends between **two or more different** profiles.
- C) Sweep is for solids; loft is for surfaces only.
- D) They are the same feature with different names.

---

**Q3.** You're building a 6-bolt circular pattern. The single most important reference to get right is:

- A) the bolt's diameter.
- B) the **axis** the pattern spins about — ideally a named construction axis, not a transient inferred one.
- C) the color of the seed feature.
- D) the order of the holes in the feature tree.

---

**Q4.** You sketched a small cut on a part face. Later you added a fillet that rounds that exact face away, and now the cut's sketch shows yellow/red with "the entity this sketch is on no longer exists." What happened, and what's the cleanest fix?

- A) OnShape has a bug; re-launch the browser.
- B) A **dangling reference** — the sketch's host face was consumed by the fillet. Fix: sketch on the stable plane that defined the face, or move the fillet *after* the cut in the tree.
- C) The cut is too small; make it bigger.
- D) Delete the fillet permanently; you can never fillet a face that has a sketch near it.

---

**Q5.** To sweep a round handle along a bent path so the sweep starts cleanly, the profile should be sketched on a plane that is:

- A) parallel to the Top plane.
- B) the same plane as the path.
- C) **perpendicular to the path at its start point** — i.e. a **point–normal plane**.
- D) tangent to the part's largest face.

---

**Q6.** Your part is symmetric about its centerline. You modeled the left half (a tab with a hole). What's the right way to create the right half?

- A) Sketch and model the right half again by hand.
- B) Copy the sketch and paste it 30 mm over.
- C) **Mirror** the left-half features across the part's symmetry plane (an origin or mid plane).
- D) Rotate the whole part 180°.

---

**Q7.** Why does C12 insist a circular bolt pattern be built from a **single seed Hole feature** rather than by sketching all six circles in one sketch and extruding them together?

- A) It looks neater in screenshots.
- B) A single seed keeps each copy **parametric and editable** (change the seed, all copies follow; change the count via a variable) and preserves the Hole feature's counterbore/countersink intelligence. Six welded circles lose all of that.
- C) OnShape charges per sketch entity.
- D) There is no real reason; both are identical.

---

**Q8.** A linear-patterned vent grille drifts off-center when you make the panel wider. The fix is to:

- A) delete the pattern and place each slot by hand.
- B) turn on the pattern's **centered/symmetric** option (or tie the start offset to panel-size and count) so copies grow both ways from the seed.
- C) make the slots smaller.
- D) accept it; patterns can't stay centered.

---

**Q9.** The feature tree in OnShape is best understood as:

- A) an alphabetical list of parts in the Document.
- B) a **top-to-bottom recipe** that regenerates the part each time; a feature can only reference geometry created **above** it.
- C) a folder of unrelated files.
- D) a render-order list that has no effect on geometry.

---

**Q10.** You place a **mate connector** on a hinge knuckle this week, even though you won't mate anything until Week 4. The most important thing to get right when placing it is:

- A) its color.
- B) that its **primary (Z) axis** points along the hinge centerline, so the future revolute mate rotates about the correct line.
- C) that it's placed exactly at the global origin.
- D) nothing — orientation doesn't matter for mate connectors.

---

## Answer key

<details>
<summary>Click to reveal answers</summary>

1. **C** — An offset plane driven by `#bossHeight` is parametric and stable; the sketch tracks the variable and survives downstream fillets/reorders. A duplicates a magic number; B is fragile (faces get consumed); D is undefined geometry, never acceptable.
2. **B** — Sweep = one constant section along a path; loft = a blend between two or more *different* profiles. This is the whole decision rule: constant section → sweep, changing section → loft.
3. **B** — The pattern axis is the critical reference. A *named* construction axis survives edits; an inferred face axis vanishes when the face changes, breaking the pattern. This is why Lecture 1 builds explicit axes.
4. **B** — Classic dangling reference: the host face was consumed. Fix the *cause* — sketch on the stable plane that defined the face, or reorder so the fillet runs after the cut. The red feature is the victim, not the problem.
5. **C** — A point–normal plane (perpendicular to the path at its start) lets the section sweep without skewing or self-intersecting at the start. Sketching the profile on the path plane or a parallel plane produces a broken or skewed sweep.
6. **C** — Mirror the features across the symmetry plane. The right half then tracks the left automatically (change the left hole's diameter, the right follows). Hand-modeling or copy-paste breaks that link.
7. **B** — A single seed keeps every copy live and parametric and preserves the Hole feature's intelligence. Twelve sketched circles in one extrude are welded into one un-editable feature. "Define once, let OnShape copy" is the week's core principle.
8. **B** — Turn on the centered/symmetric option (or tie the layout to panel size and count). A corner-anchored pattern drifts when the panel resizes; a centered one re-centers.
9. **B** — The tree is a history-based recipe executed top to bottom; a feature can only reference geometry above it. This single fact drives every feature-ordering and reference decision. The rollback bar lets you insert features mid-history.
10. **B** — A mate connector's primary (Z) axis is what revolute mates rotate about (and slider mates translate along, fastened mates align). Z along the hinge centerline now makes the Week 4 hinge correct; Z pointing sideways makes it swing about the wrong line.

</details>

---

If you scored under 7, re-read the lectures for the questions you missed — especially anything about references and feature order, which everything this week depends on. If you scored 9 or 10, you're ready for the [homework](./06-homework.md).
