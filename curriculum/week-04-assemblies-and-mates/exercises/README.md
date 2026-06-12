# Week 4 — Exercises

Short, focused assembly drills in OnShape. Each one should take 30–50 minutes. Do them in order; later ones assume the connectors and mates from earlier ones.

These are **modeling tasks, not code.** Each exercise is a numbered click-by-click walkthrough you perform in your browser. Work in a single OnShape Document for the week (call it `C12-W4-Assemblies`) with a separate Part Studio per part and a separate Assembly tab per exercise — keep it tidy.

## Index

1. **[Exercise 1 — Insert, fasten, and a revolute hinge](exercise-01-insert-fasten-and-revolute.md)** — insert multiple parts, fix a base, fastened-mate a pin, and add a revolute mate so a leaf swings. The drag test earns its first `1 DOF`. (~40 min)
2. **[Exercise 2 — Slider, cylindrical, and a library bolt](exercise-02-slider-cylindrical-and-the-content-library.md)** — a sliding drawer (Slider with limits), a spinning-and-sliding shaft (Cylindrical), and a correctly-sized bolt pulled from the Standard Content library. (~50 min)
3. **[Exercise 3 — Sub-assembly + interference check](exercise-03-subassembly-and-interference-check.md)** — group a two-part mechanism into a sub-assembly, insert it, make it flexible, and run interference detection through the full range of motion. (~45 min)

## How to work the exercises

- **Read the step, then do it in OnShape.** Don't read the whole exercise first — perform each numbered step as you reach it.
- **Predict before you click the green check.** Before confirming any mate, say out loud how many DOF it will leave and which motion survives. Then drag and check you were right. This is the entire point of the week.
- **Rename every mate and connector as you go.** `Lid swing`, not `Revolute 1`. You'll thank yourself in Exercise 3.
- **Drag-test after every mate.** If the part doesn't move the way you predicted, stop and fix it before adding the next mate. Compounding a bad mate is how assemblies become unsolvable.
- **Units are millimeter**, length precision 2–3 decimals, angles in degrees. Set it once per Document.

Every exercise ends with the **C12 drag test** passing:

```
Drag test · <N> DOF · moves freely through full range · 0 interferences
```

## Checklist

Mark each done when its drag test passes and you can explain the DOF.

- [ ] **Exercise 1** — base fixed; pin fastened (0 DOF); leaf revolute (1 DOF) swings about the pin; optional 0–110° limit holds.
- [ ] **Exercise 2** — drawer slider (1 DOF) limited to its travel; shaft cylindrical (2 DOF) spins *and* slides; M5 bolt from Standard Content fastened into a correctly-sized hole.
- [ ] **Exercise 3** — two parts grouped into a named sub-assembly; inserted into a parent; made flexible so its joint moves; interference detection run at both motion extremes returns zero.
- [ ] For each exercise, you can **name the real-world joint** each mate represents and state the DOF it leaves.

There are no solutions checked in — the course is open source and solutions live in forks. After you finish, search the OnShape **Public** documents for `c12-week-04` to compare, and open a couple of other students' assemblies to read their Mate features lists.
