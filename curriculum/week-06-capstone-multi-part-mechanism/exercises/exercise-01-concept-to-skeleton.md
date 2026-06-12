# Exercise 1 — Concept sketch to a draggable kinematic skeleton, with a DOF budget

> **Estimated time:** ~90 minutes (15 min concept sketch, 45 min building the skeleton in OnShape, 30 min the DOF budget and writeup). **Cost:** free — one Part Studio sketch in your Document.

This is the capstone planning step everyone is tempted to skip and everyone who skips it regrets, because they discover on assembly day that the motion they imagined cannot physically happen. You will design the *motion* first — as a single draggable OnShape sketch — and verify it moves the way you intend, before you model one solid. A skeleton that drags correctly is a mechanism that will work; a skeleton that binds saved you a day of wasted modeling.

We use a **slider-crank gripper** as the worked example (one crank rotation closes a jaw). Substitute your own mechanism's skeleton — a four-bar linkage, a scissor lift, a gear train — and the method is identical.

## Goal

Produce, in a Part Studio sketch on the Top plane, a kinematic skeleton of your mechanism: links as fixed-length lines, joints as coincident points, fully constrained *except* for the single input degree of freedom, which you can drag to preview the full range of motion. Then compute the mobility (DOF budget) and confirm it equals 1.

## Step 1 — Draw the concept sketch (on paper or a scratch sketch)

Before OnShape, sketch the mechanism as pure intent. For the slider-crank gripper:

1. Draw the **frame** as a fixed reference (a ground symbol — hatching).
2. Mark the **ground pivot** where the crank rotates.
3. Draw the **crank** as a short line from the ground pivot.
4. Draw the **connecting rod** from the crank tip to the **slider**.
5. Draw the **slider** on a straight rail (the frame).
6. Draw the **jaw** that the slider drives.
7. Label the **input** (crank rotation) and the **output** (jaw closing).

You now know what moves relative to what. Photograph this; it is the first artifact in your design walkthrough.

## Step 2 — Create the Document and set units

1. In OnShape, create a Document named `C12-Capstone-<mechanism>`.
2. In the Part Studio, open **Document menu → Workspace units** (or the units control) and set length units to **Millimeter**, 2 decimal places. Every dimension below is in mm.
3. Rename the default Part Studio tab to `Skeleton`.

## Step 3 — Build the skeleton geometry

Open a sketch on the **Top plane**. You will draw lines (links) and points (joints), then constrain them.

1. Draw a **line** from the origin going right; this is the crank. The origin is your **ground pivot**.
2. From the end of the crank line, draw a second **line** down-and-right; this is the connecting rod.
3. From the end of the rod, draw a short **line**; this is the slider's pin location, which will ride the rail.
4. Draw a horizontal **construction line** through the slider pin's intended height; this is the **rail** the slider travels along.
5. From the slider pin, draw the **jaw link** line up to the jaw tip.

Do not worry about exact positions yet — get the topology (which line connects to which) right first.

## Step 4 — Apply the geometric constraints

This is where the skeleton becomes a real linkage. Apply constraints until the sketch is fully defined *except* the input:

1. **Coincident** — the crank's start point to the **origin** (the ground pivot is fixed).
2. **Coincident** — the crank's end to the rod's start (the crank pin joint).
3. **Coincident** — the rod's end to the slider pin (the rod-slider joint).
4. **Point-on-line** (coincident to the construction rail line) — the slider pin must stay on the rail. This is the prismatic/slider constraint: the slider pin can move *along* the rail but not off it.
5. **Coincident** — the jaw link's start to the slider pin (jaw rides the slider).

## Step 5 — Dimension the links (drive from variables)

The link *lengths* are what define the motion, so make them variables you can change later:

1. Add dimensions to set: crank length = **12 mm**, connecting rod = **40 mm**, jaw link = **30 mm**, and the rail height (the offset of the construction rail from the origin) = **38 mm**.
2. Better: define variables first. Add a **Variable** feature: `#crank = 12 mm`, `#rod = 40 mm`, `#jaw = 30 mm`. Then dimension each link by typing `#crank`, `#rod`, `#jaw` into the dimension box instead of a raw number. Now one edit changes the motion consistently.
3. At this point the sketch should be **fully defined for the link lengths** but the crank's *angle* should still be free — the sketch line for the crank should still be blue (under-defined) in its rotation. That free rotation is your single input DOF.

## Step 6 — Drag to preview the motion

This is the payoff. Grab the **crank tip** and drag it in a circle around the origin:

1. The crank should sweep a 12mm-radius circle.
2. As it sweeps, the connecting rod should pull the slider pin **along the rail** (it stays on the construction line).
3. The jaw link should move with the slider — the jaw opens and closes.
4. Drag through the **full range**: from the crank pointing one way (jaw open) to the other (jaw closed). Watch for the slider pin running off the *end* of the rail, or the rod folding back through the crank (a toggle/bind). If it binds, your link lengths are wrong — fix them now, on the skeleton, where it costs minutes instead of a day.

If the skeleton drags smoothly through the full intended range without binding, your mechanism will work. **This is the most important check in the whole capstone.**

## Step 7 — Compute the DOF budget (the mobility equation)

For a planar mechanism, Kutzbach mobility is `M = 3(N − 1) − 2·J1 − J2`, where `N` is links including ground, `J1` is one-DOF joints, `J2` is two-DOF joints. For the slider-crank gripper:

- Links: frame (ground), crank, connecting rod, slider-jaw. `N = 4`.
- One-DOF joints: ground-crank revolute, crank-rod revolute, rod-slider revolute, slider-rail prismatic. `J1 = 4`, `J2 = 0`.

```
M = 3(4 − 1) − 2(4) − 0 = 9 − 8 = 1
```

Mobility = 1: exactly one input drives the whole mechanism. That matches your one free DOF (the crank angle) from Step 5. Write this calculation into your design walkthrough — it is the answer to the reviewer's "how many degrees of freedom" question. If your number comes out to 0 (a rigid structure that cannot move) or 2 (a floppy mechanism with an unintended extra DOF), you have a design problem to fix before modeling parts.

## Expected outcome

```
Skeleton sketch:   fully defined except crank angle (1 free DOF)
Drag test:         crank sweeps full range, slider stays on rail, jaw opens/closes, no bind
Link variables:    #crank=12, #rod=40, #jaw=30  (motion driven from one place)
DOF budget:        N=4, J1=4, J2=0  ->  M = 3(4-1) - 2(4) = 1   (PASS: one input DOF)
```

## Acceptance criteria

- [ ] A concept sketch (photo or scratch sketch) labeling the input and the output of the motion.
- [ ] A kinematic skeleton sketch in a Part Studio, link lengths driven by variables (`#crank`, `#rod`, `#jaw`).
- [ ] The skeleton is fully defined *except* the single input DOF (the crank angle is draggable).
- [ ] Dragging the input sweeps the **full** intended range of motion with **no bind and no off-rail** behavior.
- [ ] A DOF budget written out with the mobility equation, computing to `M = 1`.
