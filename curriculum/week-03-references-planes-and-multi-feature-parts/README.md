# Week 3 — References, Planes & Multi-Feature Parts

Welcome to Week 3 of **C12 · Crunch 3D**. Weeks 1 and 2 kept you on the three origin planes: you drew fully-defined sketches (Week 1) and pushed them into solids with extrude, revolve, holes, and dress-up features (Week 2). That was deliberate scaffolding. Real parts can't live on three planes — they have faces tilted at angles, features stacked at offsets, ribs that follow curves, and rings of identical holes. This week you learn to **manufacture the geometry you build on** (construction planes, axes, mate connectors) and to **multiply one feature into many** (patterns, mirror, sweep, loft) — all while ordering features so a single dimension change rebuilds the whole part cleanly.

The theme of the week is **design intent**. Anyone can click features into existence. The skill is choosing *which geometry to reference* so the part stays editable. A bracket built on smart references flexes when the boss height changes; the same bracket built on magic numbers and stray faces turns red on the first edit. By Friday you should be able to look at a feature tree and say, for every feature, *what it references and why* — and reorder it so edits propagate the way you intend.

This is a CAD course. You will write **zero code**. The "exercises" are precise, numbered OnShape modeling walkthroughs. Everything is done in OnShape's free browser-based, cloud-native, fully parametric workspace — no install, no license, same on every OS.

## Learning objectives

By the end of this week, you will be able to:

- **Create** offset and angled construction planes, and choose the right plane *type* (offset, angle, point–normal, mid plane, three-point, tangent) for a given modeling job.
- **Build** construction axes — especially the centerline of a cylindrical face — and explain why a named axis beats a transient inferred one.
- **Sketch** confidently on a non-default plane and on a part face, and **decide deliberately** between the two based on which is more robust to downstream edits.
- **Place** an explicit mate connector as a persistent, oriented reference frame, with its primary (Z) axis pointing where the future joint needs it.
- **Read** the feature tree as a top-to-bottom recipe, use the **rollback bar** to insert references mid-history, and diagnose a broken reference by finding its upstream cause.
- **Populate** geometry with **linear** and **circular patterns** and **mirror** — a bolt-hole circle, a vent grille, a symmetric half — without re-sketching.
- **Sweep** a profile along a bent path and **loft** between two dissimilar profiles, using the correct reference plane for each.
- **Order and name** features so a multi-feature part survives the C12 rebuild test (flex two driving dimensions ±20%, nothing turns red).

## Prerequisites

This week assumes you have completed **C12 Weeks 1 and 2**, or have equivalent OnShape fluency. Specifically:

- You can create a Document, set units to millimeters, and draw a **fully-defined (black)** sketch using geometric constraints and driving dimensions (Week 1).
- You can turn a sketch into a solid with **Extrude** and **Revolve**, place a **Hole** feature, and apply **Fillet**, **Chamfer**, and **Shell** (Week 2).
- You understand the feature tree well enough to rename features and read it top to bottom.
- You have an OnShape account (free Public plan is fine) and a browser.
- You have a **running-project part** from Week 2 — a finished single-body solid built from your Week 1 master sketch. This week promotes that part; if yours is thin, fix it first (see the mini-project brief).

You do **not** need any prior multi-feature, sweep, or loft experience. We start at construction planes.

## Topics covered

- The three default planes (Top/Front/Right) as the first members of a *family* of construction planes.
- The **Plane** feature: offset, angle, point–normal, three-point, line–point, mid plane, tangent, curve-point types.
- Construction **axes**: through a cylindrical face, through two points, plane intersection, perpendicular-through-point.
- **Sketching on a construction plane vs. on a part face** — the robustness trade-off, and the dangling-reference failure mode.
- The feature tree as a **history-based recipe**; the **rollback bar** for inserting references mid-history.
- **Mate connectors** as persistent, oriented reference frames (planted now, mated in Week 4); primary/secondary axis orientation.
- **Linear pattern** (1-D and 2-D grids; centering for robustness).
- **Circular pattern** about a named axis; the bolt-circle-diameter (BCD) variable trick.
- **Mirror** of features vs. bodies; the mid-plane symmetry reference.
- **Sweep**: profile + path, the point–normal profile plane, follow-path orientation, twist.
- **Loft**: two+ profiles on offset planes, connection points to avoid twist, loft vs. sweep.
- **Design intent**: feature ordering, variable-driven counts/dimensions, and passing the rebuild test.
- Tree hygiene: renaming every feature and construction reference, grouping into folders.

## Weekly schedule

The schedule below adds up to approximately **36 hours**. Treat it as a target, not a contract — some of you model fast, some slow.

| Day       | Focus                                              | Lectures | Exercises | Challenge | Quiz/Read | Homework | Mini-Project | Self-Study | Daily Total |
|-----------|----------------------------------------------------|---------:|----------:|----------:|----------:|---------:|-------------:|-----------:|------------:|
| Monday    | Construction planes, axes, on-face sketching       |   2h     |   1.5h    |    0h     |   0.5h    |   1h     |     0h       |    0.5h    |    5.5h     |
| Tuesday   | Mate connectors, references, rollback, tree order  |   1h     |   1.5h    |    1h     |   0.5h    |   1h     |     0h       |    0.5h    |    5.5h     |
| Wednesday | Linear & circular patterns, mirror                 |   2h     |   2h      |    1h     |   0.5h    |   1h     |     0h       |    0h      |    6.5h     |
| Thursday  | Sweep & loft                                       |   1h     |   1.5h    |    0h     |   0.5h    |   1h     |     1.5h     |    0.5h    |    6.5h     |
| Friday    | Design intent; mini-project work                   |   0h     |   0.5h    |    0h     |   0.5h    |   1h     |     3h       |    0.5h    |    5.5h     |
| Saturday  | Mini-project deep work                             |   0h     |   0h      |    0h     |   0h      |   0.5h   |     3h       |    0h      |    3.5h     |
| Sunday    | Quiz, rebuild-test, tree audit, polish             |   0h     |   0h      |    0h     |   1h      |   0h     |     1.5h     |    0h      |    2.5h     |
| **Total** |                                                    | **6h**   | **8.5h**  | **2h**    | **3.5h**  | **5.5h** | **12.5h**    | **2.5h**   | **35.5h**   |

## How to navigate this week

| File | What's inside |
|------|---------------|
| [README.md](./README.md) | This overview (you are here) |
| [resources.md](./resources.md) | Curated OnShape Help, Learning Center, and reference links |
| [lecture-notes/01-reference-geometry-planes-axes-and-mate-connectors.md](./lecture-notes/01-reference-geometry-planes-axes-and-mate-connectors.md) | Construction planes, axes, on-face vs. on-plane sketching, the feature tree as a recipe, mate connectors |
| [lecture-notes/02-multiplying-geometry-patterns-mirror-sweep-and-loft.md](./lecture-notes/02-multiplying-geometry-patterns-mirror-sweep-and-loft.md) | Linear & circular patterns, mirror, sweep, loft, and keeping them parametric |
| [exercises/README.md](./exercises/README.md) | Index of the modeling exercises and a checklist |
| [exercises/exercise-01-offset-and-angled-planes.md](./exercises/exercise-01-offset-and-angled-planes.md) | Guided: build offset & angled planes and sketch on them and on a face |
| [exercises/exercise-02-patterns-and-mirror.md](./exercises/exercise-02-patterns-and-mirror.md) | Modeling task: a bolt-hole circle and a vent grille via pattern + mirror |
| [exercises/exercise-03-sweep-and-loft.md](./exercises/exercise-03-sweep-and-loft.md) | Modeling task: a swept handle and a square-to-round loft |
| [challenges/README.md](./challenges/README.md) | What the challenge is and how it's graded |
| [challenges/challenge-01-parametric-heat-sink-or-pipe-elbow.md](./challenges/challenge-01-parametric-heat-sink-or-pipe-elbow.md) | A multi-feature, non-default-plane, patterned part that rebuilds on one dimension |
| [mini-project/README.md](./mini-project/README.md) | Promote the running project to a multi-feature part |
| [quiz.md](./quiz.md) | 10 questions with an answer key |
| [homework.md](./homework.md) | Six practice problems with a grading rubric |

## The "fully defined, rebuilds clean" promise

C12 has one recurring quality marker, and Week 3 sharpens it:

> **Every driving sketch is black (fully defined), and the whole part survives the rebuild test: flex its two most important driving dimensions ±20% and no feature turns red.**

If a sketch is still blue (under-defined) or any feature goes red when you edit a dimension, you are not done. This week adds a twist: patterns, sweeps, and lofts can fail in new ways (instances falling off the part, a sweep self-intersecting, a loft twisting). Building reference-first — named planes, named axes, variable-driven counts — is what makes the part pass. Building on magic numbers and stray faces is what makes it fail.

## Stretch goals

If you finish the regular work early and want to push further:

- Read OnShape's article on **design intent and feature order**, then re-audit your mini-project tree against it: <https://www.onshape.com/en/resource-center>.
- Rebuild your Week 2 part's holes as a **single circular pattern** off a named axis instead of individually-placed holes — then drive the count with a variable.
- Add a **helical sweep** (sweep with Twist) to make a coarse thread or a coil, and note where it self-intersects as you tighten the pitch.
- Loft a **three-profile** transition (square → rounded-square → circle on three stacked offset planes) and tune the connection points until it's twist-free.
- Write a short note for your future self: for one feature in your part, list every other feature it references, and one alternative reference you *rejected* and why.

## Up next

Continue to **Week 4 — Assemblies & Mates** once you have promoted your mini-project part to a clean multi-feature part and created a Version. The mate connectors you plant this week are the references Week 4's mates snap to — so place them with intent.

---

*If you find errors in this material, please open an issue or send a PR. Future learners will thank you.*
