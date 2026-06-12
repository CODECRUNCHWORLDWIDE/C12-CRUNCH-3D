# Exercise 2 — Mate the mechanism so it has exactly the intended degrees of freedom

> **Estimated time:** ~120 minutes (20 min inserting parts, 50 min mating, 30 min the interference sweep, 20 min the writeup). **Cost:** free — one Assembly tab in your Document.

This is the exercise where your mechanism either moves or it does not. You insert the parts you modeled, ground exactly one of them, and add the mates — Revolute, Slider, Fastened — that turn a pile of solids into a machine with *one* degree of freedom. Then you do the thing most students skip: you drag it through the full range and run Interference Detection at the *extremes*, not just the comfortable home pose, because mechanisms fail at the ends of travel.

This walkthrough continues the slider-crank gripper from Exercise 1. You should already have modeled (in Part Studios) a **frame**, a **crank**, a **connecting rod**, and a **slider-jaw**, each with a **mate connector** placed at every joint location (on the centerline of each pin hole, on the rail face for the slider). If you skipped the mate connectors, place them now — assembling without them is the single biggest cause of fragile mates.

## Goal

Build an Assembly in which the mechanism has exactly **one degree of freedom**, drags smoothly through its full range, and has **zero interferences** at home, at mid-travel, and at *both* extremes of travel — verified, not eyeballed.

## Step 1 — Create the Assembly and insert the parts

1. In your Document, add an **Assembly** tab named `Mechanism`.
2. Use **Insert** to add the parts: `frame`, `crank`, `connecting-rod`, `slider-jaw`. They drop in unmated and floating.
3. Move them roughly into their assembled arrangement by dragging (this does not constrain anything; it just makes the next steps easier to see).

## Step 2 — Ground exactly one part

This is non-negotiable: **one** part is grounded, everything else is positioned by mates relative to it.

1. Right-click the **frame** → **Fix** (it gets a grounded/anchor icon and turns immovable).
2. Confirm nothing else is fixed. Two grounded parts will over-constrain the assembly the moment you add a mate between them. Zero grounded parts means everything floats and your mates have no fixed reference.

## Step 3 — Mate the crank to the frame (Revolute)

1. Start a **Revolute** mate.
2. Select the **mate connector** on the crank's pivot-hole centerline, then the matching mate connector on the frame's ground-pivot boss. OnShape snaps them coaxial.
3. The crank should now rotate freely about that axis and nothing else. Grab it and spin it to confirm — it rotates, it does not translate. That is one DOF added correctly.

## Step 4 — Mate the connecting rod (two Revolutes)

1. **Revolute** mate: the rod's first end connector to the **crank pin** connector. The rod now pivots on the crank.
2. **Revolute** mate: the rod's second end connector to the **slider-jaw's** rod-pin connector. The rod now also pins to the slider.
3. After both, the rod is constrained between crank and slider — it can no longer fly off, but the linkage as a whole can still move because the slider is not yet constrained to the frame.

## Step 5 — Mate the slider to the frame (Slider)

1. Start a **Slider** mate.
2. Select the slider-jaw's rail mate connector and the frame's rail mate connector, aligned along the rail axis.
3. The slider can now translate **along the rail only** — no rotation, no off-axis motion. This is the prismatic joint from your DOF budget.

## Step 6 — Verify the degrees of freedom

You designed for `M = 1`. Confirm the assembly actually has it:

1. **Drag the crank.** The entire mechanism should follow from that one input: crank rotates → rod transmits → slider translates → jaw closes. Everything moves *together* from one grab. That is one DOF.
2. **Grab the rod directly and try to move it independently of the crank.** It should *not* move on its own — it is fully constrained by the two Revolutes. If it floats freely, you are missing a mate.
3. **Grab the slider and try to rotate it.** It should only translate along the rail. If it rotates, your Slider mate is wrong (you may have used a Cylindrical, which allows rotation).
4. **Look for red over-constraint warnings** in the Mate features list. A red warning means you added a redundant mate that fights the others when you move — delete it. A common one: adding both a Revolute *and* a Cylindrical at the same joint over-constrains it.

If exactly one input drives everything, nothing floats, and there are no red warnings, your DOF is correct.

## Step 7 — The interference sweep (home, mid, both extremes)

This is the step that separates a passing capstone from a failing one. Run **Insert → Interference Detection** at four positions:

1. **Home position** (crank at 0°, jaw open). Run Interference Detection. Note any interferences and the worst clearance (use the **Measure** tool between the closest faces).
2. **Mid-travel** (crank at ~45°). Drag there, run it again.
3. **Full closure** (crank at 90°, jaw shut). Drag there, run it. This is where the jaws are closest — confirm they clear by a real, measured gap.
4. **The other extreme** (crank back the other way, jaw fully open). Drag there, run it. Watch for the connecting rod swinging into the frame, or the slider running off the rail.

Record the **worst clearance across all four positions** as a number. For an FDM-printed mechanism you want at least ~0.4mm at the tightest point so the printed parts do not bind. If anything interferes (red), you have a real collision to fix — adjust a link length or a part profile until the worst position clears.

## Step 8 — Write it up

In your design walkthrough, record:

1. Each mate, by name, and the degree of freedom it controls (e.g., "Revolute-1: ground pivot, 1 rotational DOF").
2. The confirmation that the assembly has exactly one input DOF (from Step 6).
3. The interference table: the four positions, interference yes/no at each, and the worst measured clearance (and at which position it occurs).

## Expected outcome

```
Grounded parts:      1 (frame)            [PASS: exactly one]
Mates:               Revolute x3, Slider x1
Drag test:           one input (crank) drives whole mechanism   [PASS: 1 DOF]
Over-constraint:     no red warnings       [PASS]
Interference sweep:
  home (0 deg):      none, min gap 6.0 mm
  mid (45 deg):      none, min gap 2.1 mm
  full close (90):   none, min gap 1.2 mm
  full open (other): none, min gap 0.9 mm  <-- worst position
Worst clearance:     0.9 mm at full-open (rod vs frame rail)   [PASS: > 0.4 mm]
```

If a position interferes, the three usual culprits are: (1) a link length that swings a part into the frame — shorten it or relieve the frame; (2) the slider running off the end of the rail at an extreme — lengthen the rail or limit the travel; (3) the jaws colliding at full closure — add clearance to the jaw faces.

## Acceptance criteria

- [ ] Exactly **one** part is grounded; everything else positioned by mates.
- [ ] The mate scheme uses the correct mate types (Revolute for pins, Slider for the rail), with **no** red over-constraint warnings.
- [ ] Dragging the single input (the crank) drives the whole mechanism — verified one DOF.
- [ ] Interference Detection run at **four** positions (home, mid, both extremes), with the worst clearance recorded as a measured number.
- [ ] Zero interferences at every position, worst clearance ≥ 0.4 mm (for an FDM capstone).
- [ ] A written table of each mate and the DOF it controls, plus the interference sweep results.
