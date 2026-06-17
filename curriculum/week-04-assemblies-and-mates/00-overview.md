# Week 4 — Assemblies & Mates

Welcome to **C12 · Crunch 3D**, Week 4. For three weeks you have been a part modeler: sketch, extrude, dress up, pattern, build off references. This week you become an **assembly** engineer. We leave the Part Studio and move into the **Assembly** tab, where separate parts come together, get **mated**, and — if you do it right — actually move.

The shift is bigger than it sounds. In a Part Studio, geometry is welded into one feature tree; there is no notion of "this hinge pin can rotate relative to that bracket." In an Assembly, every part starts as a free-floating rigid body with **six degrees of freedom** (three translations, three rotations), and your job is to take those degrees of freedom away — deliberately, one mate at a time — until the assembly has exactly the motion you intend and nothing more.

By Friday you will have built an assembly that articulates: a hinge that swings, a drawer that slides, a shaft that spins. You will pull a real fastener from the **Standard Content library**, group parts into a **sub-assembly**, and run an **interference check** to prove your moving parts don't pass through each other. And you'll promote the running mini-project from a single part into a multi-part mechanism with at least one working joint.

The big idea this week: **a mate is not glue, it is a constraint on motion.** A fastened mate removes all six DOF (the part is locked solid relative to its neighbor). A revolute mate removes five and leaves one rotation. A slider removes five and leaves one translation. Choosing the right mate is choosing which degrees of freedom survive. Get that mental model and assemblies stop being mysterious.

## Learning objectives

By the end of this week, you will be able to:

- **Explain** the six degrees of freedom of a rigid body and describe what each OnShape mate type removes and leaves.
- **Insert** parts and sub-assemblies into an Assembly from the same Document and from other Documents.
- **Fasten** a base/ground part so it cannot move, and understand why every assembly needs one fixed reference.
- **Apply** the core mates — **Fastened, Revolute, Slider, Cylindrical, Planar, Ball, Pin-Slot** — and predict the resulting motion before you click the green check.
- **Place and reuse mate connectors** explicitly, and recognize the implicit connectors OnShape offers on faces, edges, and vertices.
- **Choose** between **bottom-up** (model parts, then assemble) and **top-down / in-context** (design a part inside the assembly against neighboring geometry) strategies, and state the trade-offs.
- **Build sub-assemblies** and insert them as rigid or flexible units.
- **Pull standard fasteners** (bolts, nuts, washers) from the **Standard Content library** and configure their size.
- **Run interference detection** and a **clearance check**, and read the results.
- **Drag-test** an assembly to confirm it has exactly the intended degrees of freedom.

## Prerequisites

This week assumes you have completed **C12 Weeks 1–3**, or have equivalent OnShape part-modeling fluency. Specifically:

- You can create a Document, set units to millimeter, and navigate Part Studios, Assemblies, and the feature/instance lists.
- You can draw a fully-defined sketch and build a solid part with Extrude, Revolve, Hole, Fillet, and Chamfer.
- You can use construction planes, patterns, mirror, sweep, and loft (Week 3) and you understand design intent — ordering features so edits propagate.
- You have a **Week 3 multi-feature part** in a Document you can open. The mini-project this week mates a new component to it. If you joined late, the mini-project brief tells you how to produce a stand-in part in the first hour.
- You can create a **Version** of a Document and share a public link.

You do **not** need any prior assembly experience. We start at degrees of freedom and build up. If you have used SolidWorks "mates" or Fusion "joints," good news: the concepts transfer, but the OnShape mate vocabulary and the **mate connector** workflow are specific — we will be precise about both.

## Topics covered

- **Degrees of freedom (DOF):** the six DOF of an unconstrained rigid body; how mates subtract DOF; the "fully constrained vs under-constrained vs over-constrained" spectrum.
- **The Assembly tab:** the instance list, the Mate features list, fix/group/insert, and how it differs from a Part Studio feature tree.
- **Mate connectors:** implicit connectors on faces/edges/vertices, explicit named connectors, the connector triad (origin + X/Y/Z axes), and re-orienting a connector (flip, offset, re-align).
- **The mate types:** Fastened (0 DOF), Revolute (1 rotation), Slider (1 translation), Cylindrical (1 rotation + 1 translation along the same axis), Planar (2 translations + 1 rotation in a plane), Ball (3 rotations), Pin-Slot (1 rotation + 1 translation, decoupled), and the lightweight Parallel/Tangent **mate relations**.
- **Fixing a base:** why every assembly needs a grounded reference; Fix vs a Fastened-to-origin mate.
- **Assembly strategy:** bottom-up vs top-down; **in-context** design (editing a part against assembly geometry) and its update behavior; when each is the right call.
- **Sub-assemblies:** grouping parts into a reusable unit; rigid vs flexible sub-assemblies; why mechanisms belong in sub-assemblies.
- **Standard Content library:** inserting ANSI/ISO bolts, nuts, washers; configuring size; why you never model a hex bolt by hand.
- **Mate connectors as design intent:** building connectors in the Part Studio so parts "snap" together predictably in the assembly.
- **Validation:** interference detection, clearance checks, and drag-testing to confirm DOF.

## Weekly schedule

The schedule below adds up to approximately **36 hours**. Treat it as a target, not a contract — some days you'll run long on the mini-project, some days the exercises click fast.

| Day       | Focus                                                   | Lectures | Exercises | Challenge | Quiz/Read | Homework | Mini-Project | Self-Study | Daily Total |
|-----------|---------------------------------------------------------|---------:|----------:|----------:|----------:|---------:|-------------:|-----------:|------------:|
| Monday    | DOF, the mate system, fastened & revolute               |    2h    |    1.5h   |    0h     |    0.5h   |   1h     |     0h       |    0.5h    |     5.5h    |
| Tuesday   | Slider, cylindrical, planar, ball, pin-slot; connectors |    2h    |    2h     |    1h     |    0.5h   |   1h     |     0h       |    0h      |     6.5h    |
| Wednesday | Strategy: insert vs in-context, sub-assemblies, library |    1h    |    2h     |    1h     |    0.5h   |   1h     |     0h       |    0.5h    |     6h      |
| Thursday  | Interference, clearance, drag-testing; project kickoff  |    1h    |    1h     |    0h     |    0.5h   |   1h     |     2h       |    0.5h    |     6h      |
| Friday    | Mini-project build: model & mate the new component      |    0h    |    1h     |    0h     |    0.5h   |   1h     |     3h       |    0.5h    |     6h      |
| Saturday  | Mini-project deep work: articulation + interference     |    0h    |    0h     |    0h     |    0h     |   1h     |     3h       |    0h      |     4h      |
| Sunday    | Quiz, walkthrough write-up, version & share             |    0h    |    0h     |    0h     |    1h     |   0h     |     0.5h     |    0h      |     1.5h    |
| **Total** |                                                         | **6h**   | **7.5h**  | **2h**    | **3.5h**  | **6h**   | **8.5h**     | **2h**     | **35.5h**   |

## How to navigate this week

| File | What's inside |
|------|---------------|
| [README.md](./00-overview.md) | This overview (you are here) |
| [resources.md](./01-resources.md) | Curated OnShape Learning Center, docs, and community references for assemblies & mates |
| [lecture-notes/01-the-mate-system-and-degrees-of-freedom.md](./02-lecture-notes/01-the-mate-system-and-degrees-of-freedom.md) | DOF, mate connectors, and choosing Fastened / Revolute / Slider / Cylindrical |
| [lecture-notes/02-assembly-strategy-insert-in-context-subassemblies.md](./02-lecture-notes/02-assembly-strategy-insert-in-context-subassemblies.md) | Bottom-up vs top-down, in-context design, sub-assemblies, the Standard Content library |
| [exercises/README.md](./03-exercises/00-overview.md) | Index of the assembly drills and a checklist |
| [exercises/exercise-01-insert-fasten-and-revolute.md](./03-exercises/exercise-01-insert-fasten-and-revolute.md) | Guided: insert parts, fasten a base, add a revolute hinge that swings |
| [exercises/exercise-02-slider-cylindrical-and-the-content-library.md](./03-exercises/exercise-02-slider-cylindrical-and-the-content-library.md) | Modeling task: a sliding drawer, a spinning shaft, and a library bolt |
| [exercises/exercise-03-subassembly-and-interference-check.md](./03-exercises/exercise-03-subassembly-and-interference-check.md) | Modeling task: group a mechanism into a sub-assembly, then interference-check it |
| [challenges/README.md](./04-challenges/00-overview.md) | What the challenge is and how it's assessed |
| [challenges/challenge-01-four-bar-linkage.md](./04-challenges/challenge-01-four-bar-linkage.md) | Build a working 4-bar linkage with exactly 1 DOF and no interference |
| [quiz.md](./05-quiz.md) | 10 questions on DOF, mate types, and strategy, with an answer key |
| [homework.md](./06-homework.md) | Six practice problems with a grading rubric |
| [mini-project/README.md](./07-mini-project/00-overview.md) | Promote the running part into a multi-part articulating assembly |

## The "exactly one DOF" promise

C12 uses a small recurring marker in every assembly that is supposed to move. After you finish mating, you **grab a moving part and drag it**. The assembly passes when:

```
Drag test · 1 DOF · moves freely through full range · 0 interferences
```

If a part you expect to move is frozen, you over-constrained it. If a part wobbles in a direction it shouldn't, you under-constrained it. If two parts pass through each other as you drag, you have an interference and the mechanism is not real. "It looks assembled" is not the bar this week — "it moves exactly as intended and never collides" is.

## A note on units and the metric default

Every assembly this week is in **millimeter**, length precision 2–3 decimals, angles in degrees. Set this once per Document under **Document → Workspace units**. Mixing inch parts into a metric assembly is a classic source of "why is this part 25× too big" bugs — if you insert a part that looks absurdly scaled, check its source units first.

## Stretch goals

If you finish the regular work early and want to push further:

- Read the OnShape Learning Center path **"Introduction to Assemblies"** end to end and do its in-app exercises: <https://learn.onshape.com/>.
- Rebuild one of your exercise assemblies using **in-context** design instead of bottom-up — model the second part *inside* the assembly against the first part's geometry — and write a paragraph on which felt better and why.
- Take any revolute joint you built and add a **mate limit** (min/max angle) so the hinge stops at, say, 0° and 110° like a real laptop lid. Confirm the drag test respects the limit.
- Insert the same sub-assembly twice into a parent assembly and toggle one instance to **flexible**; observe how its internal joints can now move independently. Note where you'd want that in a real design.

## Up next

Continue to **Week 5 — Drawings, Dimensions, GD&T & Configurations** once you have versioned and shared your Week 4 assembly. Week 5 takes the part you configured this week and produces a manufacturing-ready drawing package for it.

---

*If you find errors in this material, please open an issue or send a PR. Future learners will thank you.*
