# Week 3 — Exercises

Three focused modeling drills in OnShape. Each one should take 30–50 minutes. Do them in order; later ones reuse skills (and sometimes geometry) from earlier ones. These are **not** code — they are precise, numbered OnShape walkthroughs. Model them yourself; don't just read them.

## Index

1. **[Exercise 1 — Offset & angled planes, and on-face sketching](exercise-01-offset-and-angled-planes.md)** — build offset and angled construction planes, sketch on each, then sketch on a part face and learn when each reference is the right one. (~45 min)
2. **[Exercise 2 — Patterns & mirror](exercise-02-patterns-and-mirror.md)** — populate a 6-bolt flange with a circular pattern, a vent grille with a linear pattern, and a symmetric tab with mirror — all from single seed features, all parametric. (~50 min)
3. **[Exercise 3 — Sweep & loft](exercise-03-sweep-and-loft.md)** — sweep a round handle along a U-shaped path using a point–normal profile plane, and loft a square-to-round transition between two offset planes. (~50 min)

## How to work the exercises

- **Read the step, then do the step.** Don't read the whole exercise first and try to reproduce from memory — follow it click by click the first time.
- **Model it yourself.** Watching is not learning; muscle memory in the OnShape UI is the entire point of these drills.
- **Rename every feature and construction plane/axis as you create it.** `Plane 1 / Plane 2` is never acceptable in C12. Name it by its job: `Bolt-face plane`, `Bore axis`, `Fin pitch dir`.
- **Keep every driving sketch fully defined (black).** A blue (under-defined) sketch means the exercise isn't done.
- **Run the rebuild test where the exercise asks.** Flexing a dimension and watching the part rebuild (or fail) is where the real learning happens.
- **Work in one Document.** Create a Document called `C12-Week3-Exercises` and add a new **Part Studio** tab for each exercise. Create a **Version** at the end of each so you can roll back.

There are no checked-in solution models. C12 is open: solutions live in students' public OnShape documents. After you finish, you can search the OnShape public-document gallery, or your cohort tracker, to compare.

## Per-exercise checklist

Mark an exercise done only when **all** boxes are true:

**Exercise 1 — Offset & angled planes**
- [ ] An **offset plane** built from Top, named meaningfully, with a sketch on it.
- [ ] An **angled plane** built at a set angle off a reference, hinged on an edge/axis, with a sketch on it.
- [ ] One sketch built **on a part face**, and a one-line written note on why a face was the right (or wrong) reference there.
- [ ] You flexed the offset distance and the angle and confirmed the dependent sketches/features followed without going red.
- [ ] Every plane and feature renamed; a Version created.

**Exercise 2 — Patterns & mirror**
- [ ] A **circular pattern** of a single seed Hole feature about a **named construction axis** (a 6-bolt ring).
- [ ] A **linear pattern** (2-D grid) of a single seed slot (a vent grille), **centered** on its face.
- [ ] A **mirror** of a feature across an origin or mid plane.
- [ ] Counts driven by inline **variables** (`#bolts`, `#vents`), changed once to prove they re-lay-out.
- [ ] The rebuild test passes: change a base dimension and confirm patterns stay centered/on-part; every feature renamed; a Version created.

**Exercise 3 — Sweep & loft**
- [ ] A **sweep** of a round profile along a bent path, with the profile on a **point–normal plane** perpendicular to the path start.
- [ ] A **loft** between two profiles on two **offset planes**, twist-free (connection points pinned if needed).
- [ ] You flexed the sweep profile diameter and the loft height and confirmed both rebuilt clean (or you documented the geometric limit where one failed).
- [ ] Every plane and feature renamed; a Version created.

When all three are comfortable, you're ready for the [challenge](../challenges/challenge-01-parametric-heat-sink-or-pipe-elbow.md) and the [mini-project](../mini-project/README.md).
