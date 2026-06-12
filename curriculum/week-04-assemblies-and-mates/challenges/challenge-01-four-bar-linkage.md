# Challenge 1 — A Working 4-Bar Linkage

**Time estimate:** ~90 minutes.

## Problem statement

Build a **planar four-bar linkage** in OnShape that actually articulates: four rigid links joined in a closed loop by four revolute joints, mated so the mechanism has **exactly one degree of freedom**. Drive one link and the other two must follow predictably; the whole thing must cycle through its range **without any link passing through another**.

The four-bar linkage is the most important mechanism in machine design — it's the windshield-wiper drive, the bicycle-brake caliper, the folding-table leg, the backhoe arm. It's also the textbook example of a **1-DOF closed-loop mechanism**, which is exactly why it's the right Week 4 challenge: it forces you to count and control degrees of freedom in a loop, not just a chain.

### The four links

A four-bar has four links; one is the fixed **ground**:

1. **Ground (frame)** — the fixed link. In a real four-bar this is the bar between the two fixed pivot points; you'll model it as a base plate with two pivot bosses.
2. **Crank** — the input link, fully rotating (driven).
3. **Coupler** — the floating link connecting crank to rocker (it neither is fixed nor pivots about a fixed point).
4. **Rocker (or output crank)** — the output link, pivoting about the second ground pivot.

Joined: ground→crank, crank→coupler, coupler→rocker, rocker→ground. Four links, four revolute joints, **closed loop**.

### Suggested dimensions (a crank-rocker)

To get a clean crank-rocker (crank fully rotates, rocker oscillates), pick link lengths that satisfy the **Grashof condition** (shortest + longest ≤ sum of the other two, with the shortest adjacent to ground as the crank):

| Link | Length (pivot-to-pivot) |
|------|------------------------:|
| Ground (fixed pivot spacing) | 100 mm |
| Crank (shortest) | 30 mm |
| Coupler | 90 mm |
| Rocker | 80 mm |

Shortest (30) + longest (100) = 130 ≤ 90 + 80 = 170 → **Grashof satisfied**, crank adjacent to ground → **crank-rocker**. The crank will spin all the way around; the rocker will swing back and forth. (You may pick your own lengths; just check Grashof so the motion is interesting.)

## The DOF you're aiming for (Kutzbach)

For a planar mechanism, the **Kutzbach/Gruebler criterion** is:

```
DOF = 3·(n − 1) − 2·j
```

where `n` = number of links (including ground) and `j` = number of single-DOF joints (revolutes).

For a four-bar: `n = 4`, `j = 4` →

```
DOF = 3·(4 − 1) − 2·4 = 9 − 8 = 1
```

**Exactly one degree of freedom.** That number is your target. If your assembly drag-tests to 0 DOF, you over-constrained it (a Fastened sneaked in, or a revolute is mis-axised). If it drag-tests to 2+ DOF, the loop isn't closed (you're missing a revolute, or one link floats out of plane).

## Build outline

1. **Model the parts** (one Part Studio each, or one Part Studio with four bodies): `Ground`, `Crank`, `Coupler`, `Rocker`. Give each link a Ø6 mm pivot hole at each pivot location at the lengths above, in a flat bar ~10 mm wide × 4 mm thick. Add Ø6 mm pins (or use library shoulder screws as the pivots).
2. **Insert** all four links into an Assembly `Ex-FourBar`.
3. **Fix the `Ground`.**
4. **Revolute** crank→ground at ground pivot A.
5. **Revolute** coupler→crank at the crank's far pivot.
6. **Revolute** rocker→coupler at the coupler's far pivot.
7. **Close the loop:** **Revolute** rocker→ground at ground pivot B. *This fourth mate is the one that turns a floppy chain into a 1-DOF mechanism.* Watch the DOF drop as you add it.
8. **Drag the crank** — it should rotate, driving the coupler and rocker through the linkage. The rocker should oscillate.

> **Keep it planar.** All four pivot axes must be **parallel** (all pointing out of the same plane, e.g., all along Z). If one revolute's axis is even slightly off-plane, the loop won't close and you'll get a stubborn over/under-constraint. Use coaxial bore-to-pin connectors and make sure every pin is perpendicular to the link plane.

## Acceptance criteria

- [ ] An Assembly with four links (`Ground` fixed) joined by **four revolute joints** in a closed loop.
- [ ] Drag-testing the crank gives **exactly 1 DOF**: drive the crank, both other links follow; nothing floats freely, nothing is locked solid.
- [ ] The crank rotates fully (Grashof crank-rocker) **or**, if you chose a non-Grashof double-rocker, both rockers oscillate through their range — either way the motion is real and repeatable.
- [ ] **Interference detection** run at **at least 4 poses** across the cycle returns **0 interferences** (links don't pass through each other or the ground).
- [ ] Every link and every mate is **renamed** meaningfully (`Crank pivot A`, not `Revolute 1`).
- [ ] A created **Version** of the Document and a shared **public link**.
- [ ] A short `linkage-notes.md` (or a text panel in the Document) that:
  - States your four link lengths and shows the **Grashof check**.
  - Shows the **Kutzbach DOF calculation** = 1.
  - Names which link is crank, coupler, rocker, and ground, and **why** (which one you chose to drive).

## Strong-pass extras

- [ ] Add a **driving mate value** on the crank revolute and sweep it 0°→360°, confirming a smooth full cycle with no interference at any angle.
- [ ] Add **mate limits** to the rocker if your geometry needs them, and explain why (or why a Grashof crank-rocker needs none on the crank).
- [ ] Trace the **coupler curve**: pick a point on the coupler and describe (or screenshot at several angles) the path it sweeps — the famous coupler curve that makes four-bars useful.

## Hints

<details>
<summary>It locked solid (0 DOF) after the fourth revolute</summary>

One of your revolute axes isn't parallel to the others, so closing the loop over-constrains it. Confirm **all four pivot axes are parallel** (all along Z, perpendicular to the link plane). Re-pick the offending revolute using clean coaxial bore-to-pin connectors. A truly planar four-bar with four parallel revolutes solves to exactly 1 DOF.

</details>

<details>
<summary>It's floppy (2+ DOF) — a link swings out of plane</summary>

You're missing a constraint or a link is free to tilt out of the plane. Make sure every pivot is a **Revolute** (not a looser mate) and that the loop is genuinely closed (four joints: ground-crank, crank-coupler, coupler-rocker, rocker-ground). A missing fourth joint leaves the chain open and floppy.

</details>

<details>
<summary>It won't move at all and OnShape says "over-constrained"</summary>

Either two revolutes fight (a duplicate), or a pin is Fastened where it should be Revolute. Suppress mates one at a time to find the culprit. Remember: only the **ground** is Fixed; all four pivots are Revolute.

</details>

<details>
<summary>Choosing crank vs rocker</summary>

In a Grashof crank-rocker, the **shortest link adjacent to ground** is the crank (fully rotates); the link opposite it across the coupler is the rocker (oscillates). Drive the crank. If you made all links similar lengths (non-Grashof), you'll get a double-rocker — neither input fully rotates — which is fine, just note it.

</details>

## Submission

1. Create a **Version** of your Document and copy a **public share link**.
2. Make sure the mechanism drag-tests to **1 DOF** and passes interference at multiple poses on a fresh open of the Version.
3. Include `linkage-notes.md` with the Grashof check, the Kutzbach DOF = 1 calculation, and your crank/coupler/rocker/ground labeling.
4. Post the public link in your cohort tracker.

## Why this matters

The four-bar linkage is the "hello world" of mechanism design, and the skills it forces — **closing a loop to a controlled DOF**, keeping joints **coplanar**, and **validating through the full sweep** — are exactly what your **Week 6 capstone** mechanism will demand. A gripper, a scissor lift, a gear train: all are loops or chains of the same revolute/slider/cylindrical joints, controlled to a deliberate DOF. Master the four-bar and the capstone becomes "more of the same, bigger."
