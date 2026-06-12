# Week 2 — Quiz

Ten multiple-choice questions on extrudes, revolves, holes, and dress-up features. Take it with your lecture notes closed. Aim for 9/10 before moving to Week 3. Answer key at the bottom — don't peek.

---

**Q1.** You sketch a circle on the top face of an existing solid block and want to make a raised cylindrical boss fused to the block. Which Extrude **operation** is correct?

- A) New
- B) Add
- C) Remove
- D) Intersect

---

**Q2.** You need a bolt-clearance slot that must pass **completely through** a plate, and the plate's thickness might be changed later. Which end condition keeps the slot a through-cut no matter how thick the plate becomes?

- A) Blind, set to the current plate thickness
- B) Symmetric
- C) Through all
- D) Up to vertex

---

**Q3.** When using the **Revolve** feature, what is the one rule the profile must obey?

- A) The profile must be a single straight line.
- B) The profile must cross the revolve axis exactly once.
- C) The profile must not cross the revolve axis — it sits entirely on one side.
- D) The profile must be drawn on the Top plane only.

---

**Q4.** A bolt **passes through** Part A and **threads into** Part B. Which Hole-feature types are correct for each?

- A) A: tapped; B: clearance.
- B) A: clearance (simple); B: tapped.
- C) Both clearance.
- D) Both tapped.

---

**Q5.** You want a socket-head cap screw's cylindrical head to sit flush or recessed below the surface. Which hole type do you choose?

- A) Simple clearance hole
- B) Countersink
- C) Counterbore
- D) Tapped

---

**Q6.** You have a solid block and want to hollow it into an open-top enclosure with a uniform 2 mm wall. Which feature does this in one step, and what do you select as "faces to remove"?

- A) Shell; select the top face as the face to remove.
- B) Fillet; select all edges.
- C) Remove extrude; select the whole block.
- D) Draft; select the top face.

---

**Q7.** You want a cup with a **rounded inner base** (the fillet carried through the wall). What is the correct feature order?

- A) Shell first, then fillet the inner base edge.
- B) Fillet the base edge first, then shell.
- C) Order doesn't matter; the result is identical.
- D) You must use Draft instead of Fillet.

---

**Q8.** Your **Shell** feature turns red with a "thickness too large" type error. What is the most likely cause?

- A) The shell thickness is larger than some feature it must carve (e.g. the gap between two bosses), causing self-intersection.
- B) You forgot to rename the feature.
- C) The part isn't on the Top plane.
- D) Shell only works on revolved parts.

---

**Q9.** What is the practical difference between a **Fillet** and a **Chamfer** on an edge?

- A) A fillet is a flat angled cut; a chamfer is a rounded edge.
- B) A fillet is a rounded (arc) edge; a chamfer is a flat angled (beveled) cut.
- C) They are identical; the names are interchangeable.
- D) A fillet only works on internal edges; a chamfer only on external edges.

---

**Q10.** You change a part's base sketch and a downstream Fillet feature turns **red** because the edge it referenced no longer exists. What is the standard OnShape diagnostic-and-repair workflow?

- A) Delete the entire part and start over.
- B) Drag the rollback bar up until the error clears, find the feature just below the bar, edit it to re-pick the reference, then roll forward.
- C) Add a `!` to silence the warning.
- D) Switch to an Assembly and re-insert the part.

---

## Answer key

<details>
<summary>Click to reveal answers</summary>

1. **B** — **Add** fuses the new material into the existing body (a union). New would make a separate body; Remove would cut; Intersect would keep only the overlap. Sketching on an existing face usually auto-selects Add.
2. **C** — **Through all** is a *relationship* ("go through everything"), not a number, so it survives a thickness change. A Blind cut set to the current thickness silently becomes a blind pocket the moment the plate gets thicker — the classic rookie defect.
3. **C** — The revolve profile must lie entirely on **one side** of the axis and **not cross** it; crossing it self-intersects the spin and errors. (It may touch the axis along an edge, e.g. the bottom of a knob, but it cannot straddle it.)
4. **B** — The part the bolt **passes through** gets a **clearance** (simple) hole, slightly larger than the bolt nominal. The part the bolt **threads into** gets a **tapped** (threaded) hole, drilled to tap-drill size.
5. **C** — A **counterbore** is a flat-bottomed recess for a cylindrical cap-screw head. A **countersink** is conical, for flat-head screws. A simple hole gives no recess; tapped is for threading.
6. **A** — **Shell** hollows a solid to a uniform wall in one step; the **faces to remove** are the faces left open (the top, for an open-top enclosure). Pick no faces and you get a sealed hollow shell.
7. **B** — **Fillet before shell**: the shell then offsets the rounded base inward, rounding both the outer and inner base surfaces. Filleting *after* the shell only rounds the outer skin and a base fillet larger than the wall will error. Order is design intent.
8. **A** — The wall thickness exceeds the room available somewhere (often the gap between bosses, or a tight internal radius), so the inner offset self-intersects. Fixes: reduce thickness, increase the spacing/radius, or use a per-face thickness override.
9. **B** — A **fillet** is a rounded (arc) edge; a **chamfer** is a flat angled bevel. Use fillets for stress relief and ergonomics, chamfers for lead-ins and edge breaks.
10. **B** — The standard workflow: **roll back** past the broken feature, find the culprit just below the bar, **edit** it to re-pick the lost reference (or relax the dimension), then **roll forward**. Red features are recoverable; the rollback bar is the diagnostic tool.

</details>

---

If you scored under 7, re-read the lecture for the questions you missed — Lecture 1 covers Q1, Q2, Q10; Lecture 2 covers Q3–Q9. If you scored 9 or 10, you're ready for the [homework](./homework.md).
