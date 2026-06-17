# Week 2 — Extrudes, Revolves & Solid Part Modeling

Welcome back to **C12 · Crunch 3D**. Week 1 ended with a fully-defined master sketch and no solid geometry. That was deliberate. This week we turn flat sketches into real, manufacturable solid bodies — and by Friday you will be able to take any constrained profile and turn it into a part with the right wall thickness, mounting holes, fillets, chamfers, and a hollowed interior, all parametric, all rebuildable from a single edited dimension.

The mental model to internalize first: **in OnShape, every solid feature is a verb that acts on geometry.** Extrude *pushes a profile*. Revolve *spins a profile around an axis*. Fillet *rounds an edge*. Shell *scoops out a wall*. Each feature is recorded as a step in the Part Studio's feature list, and the part you see is the result of replaying those steps top to bottom. Change a sketch dimension at the top and every downstream feature reruns. That replay engine — the parametric history — is the whole reason CAD beats pushing polygons around by hand.

We work entirely in **OnShape Part Studios** this week. Part Studios are where parts are *modeled*; Assemblies (where parts are *mated together*) come in Week 4. Keep that boundary clear: this week there are no mates, no joints, no inserting one part into another. One Part Studio, one or two solid bodies, built from sketches.

The second thing to internalize: **a good part is judged by whether it rebuilds cleanly when a driving dimension changes.** A part that looks right but throws a red error the moment you widen it by 2 mm is a broken part. We will design for the edit, not just for the screenshot.

## Learning objectives

By the end of this week, you will be able to:

- **Extrude** a sketch profile as a New body, and use the **Add** and **Remove** Boolean operations to fuse to or cut from existing bodies.
- **Choose the correct end condition** — Blind, Symmetric, Through all, Up to face, Up to vertex, Up to next — and explain when each is the robust choice.
- **Cut a pocket** with a Remove extrude and reason about which body it removes from.
- **Revolve** a profile a full 360° and a partial angle around a sketch line or construction axis to produce turned parts like knobs, pulleys, and shafts.
- **Place holes** correctly with the dedicated **Hole feature** — simple, counterbored, and countersunk — and understand why the Hole feature beats a sketched-circle-plus-cut.
- **Apply dress-up features**: **Fillet** (constant and variable radius), **Chamfer** (equal distance, two distances, distance-and-angle), and **Draft**.
- **Shell** a solid to a uniform wall thickness, choosing which faces to remove to open the part.
- **Order features for design intent** so that editing one driving dimension cleanly rebuilds the entire part with no errors.
- **Read and repair** a feature list when a feature turns red, using the rollback bar to diagnose where the model broke.

## Prerequisites

This week assumes you completed **Week 1 — OnShape Onboarding & Sketch Fundamentals**, or have equivalent OnShape sketching fluency. Specifically, you should be able to:

- Create an OnShape Document, open a Part Studio, and set document units (mm).
- Draw lines, arcs, rectangles, and circles, and trim/extend them.
- Apply geometric constraints (coincident, horizontal/vertical, parallel, perpendicular, tangent, equal, concentric, symmetric) until a sketch is **fully defined** (turns black).
- Add driving dimensions and watch geometry update parametrically.
- Read the feature list, rename a feature, and use the rollback bar.

You do **not** need any prior solid-modeling experience. We start at the Extrude dialog. If you have learned a different CAD package (SolidWorks, Fusion 360, Inventor) the concepts map almost one-to-one; the vocabulary is nearly identical, and we will flag the few OnShape-specific names as we go.

You need a free OnShape account (the free **Public** plan is sufficient for the whole course — be aware that documents on the free plan are publicly visible) and a modern browser. No install. OnShape runs in Chrome, Edge, Safari, and Firefox, and on the OnShape mobile/tablet apps.

## Topics covered

- The feature list as a replay engine; the rollback bar; what "regeneration" means.
- **Extrude**: New / Add / Remove / Intersect operation types; the difference between a "New" body and adding to an existing one.
- **End conditions**: Blind, Symmetric, Through all, Up to next, Up to face, Up to vertex, Up to part; the *second end position* for two-directional extrudes.
- **Boolean solids**: union (Add), subtraction (Remove), intersection (Intersect), and the "merge scope" question.
- **Revolve**: full and partial angle, choosing the axis (a sketch line vs a construction line vs a Mate connector axis), and the rule that the profile must not cross the axis.
- The **Hole feature**: simple, counterbore, countersink; blind vs through; standard tap/clearance sizes; why it carries manufacturing intent a plain cut does not.
- **Fillet**: constant radius, multiple radii in one feature, variable-radius, full-round; tangent propagation.
- **Chamfer**: equal-distance, two-distance, distance-and-angle.
- **Shell**: uniform thickness, removed faces, per-face thickness overrides; why shell ordering relative to fillets matters.
- **Draft**: neutral plane, pull direction, draft angle, and why molded/cast parts need it.
- **Design intent**: feature ordering, building dress-up last, and the "rebuild on edit" test.
- Diagnosing a red feature: reading the error, rolling back, and the most common causes (lost references, zero-thickness geometry, self-intersection).

## Weekly schedule

The schedule below adds up to approximately **36 hours**. Treat it as a target, not a contract.

| Day       | Focus                                              | Lectures | Exercises | Challenges | Quiz/Read | Homework | Mini-Project | Self-Study | Daily Total |
|-----------|----------------------------------------------------|---------:|----------:|-----------:|----------:|---------:|-------------:|-----------:|------------:|
| Monday    | Feature list, Extrude, end conditions, Booleans    |    2h    |    1.5h   |     0h     |    0.5h   |   1h     |     0h       |    0.5h    |     5.5h    |
| Tuesday   | Remove cuts, pockets, Intersect; design intent     |    1h    |    2h     |     1h     |    0.5h   |   1h     |     0h       |    0.5h    |     6h      |
| Wednesday | Revolve: full/partial, axis rules, turned parts    |    2h    |    2h     |     1h     |    0.5h   |   0.5h   |     0h       |    0h      |     6h      |
| Thursday  | Hole feature; Fillet, Chamfer, Shell, Draft        |    1h    |    1.5h   |     0h     |    0.5h   |   1h     |     1.5h     |    0h      |     5.5h    |
| Friday    | Repairing broken features; mini-project work        |    0h    |    1h     |     0h     |    0.5h   |   0.5h   |     3h       |    0.5h    |     5.5h    |
| Saturday  | Mini-project deep work                             |    0h    |    0h     |     1h     |    0h     |   0.5h   |     3.5h     |    0h      |     5h      |
| Sunday    | Quiz, review, polish, version & label              |    0h    |    0h     |     0h     |    1h     |   0h     |     0.5h     |    1h      |     2.5h    |
| **Total** |                                                    | **6h**   | **8h**    | **4h**     | **3.5h**  | **4.5h** | **12h**      | **2.5h**   | **36h**     |

## How to navigate this week

| File | What's inside |
|------|---------------|
| [README.md](./00-overview.md) | This overview (you are here) |
| [resources.md](./01-resources.md) | Curated OnShape Learning Center, Help, and reference links with annotations |
| [lecture-notes/01-extrude-end-conditions-and-booleans.md](./02-lecture-notes/01-extrude-end-conditions-and-booleans.md) | From 2D to 3D: Extrude operations, end conditions, the merge scope, and Boolean solids |
| [lecture-notes/02-revolves-holes-and-dress-up-features.md](./02-lecture-notes/02-revolves-holes-and-dress-up-features.md) | Revolve, the Hole feature, Fillet, Chamfer, Shell, and Draft — making a part manufacturable |
| [exercises/README.md](./03-exercises/00-overview.md) | Index of the week's modeling drills + a checklist |
| [exercises/exercise-01-extrude-and-pocket-a-bracket.md](./03-exercises/exercise-01-extrude-and-pocket-a-bracket.md) | Guided: extrude a base, add a boss, cut a pocket, verify dimensions |
| [exercises/exercise-02-revolve-a-knob.md](./03-exercises/exercise-02-revolve-a-knob.md) | Modeling task: revolve a profile into a knurled-grip control knob |
| [exercises/exercise-03-holes-fillets-shell.md](./03-exercises/exercise-03-holes-fillets-shell.md) | Modeling task: place counterbored holes, fillet, and shell an enclosure base |
| [challenges/README.md](./04-challenges/00-overview.md) | What the challenge is and how it's assessed |
| [challenges/challenge-01-shelled-bottle.md](./04-challenges/challenge-01-shelled-bottle.md) | Reproduce a bottle/cup from a photo: revolve, shell, filleted base |
| [mini-project/README.md](./07-mini-project/00-overview.md) | Promote Week 1's master sketch into a finished solid part |
| [quiz.md](./05-quiz.md) | 10 multiple-choice questions with answer key |
| [homework.md](./06-homework.md) | Six modeling problems with a grading rubric |

## The "rebuilds clean" promise

C12 uses one recurring marker for every modeling task that ends in a finished part:

```
Edit a driving dimension by ±20% → no red features → part regenerates → still manufacturable.
```

If you double a wall thickness or widen a base and a feature turns red, you are **not done**. We treat a broken rebuild the way C9 treats a compiler warning: it is a defect in the part, not a cosmetic annoyance. A robust parametric part is the entire point of CAD; a part that only works at the one set of numbers you happened to type is a 3D doodle. By Friday, "edit it and watch it rebuild clean" should feel ordinary.

## Stretch goals

If you finish the regular work early and want to push further:

- Read OnShape's official guide on **direction of pull and draft** and add draft to a part you have already modeled: <https://cad.onshape.com/help/Content/draft.htm>.
- Rebuild one of your parts using **only one sketch** plus features (extrude up-to-face, revolve, mirror) and compare the feature count to your first attempt. Fewer features that survive edits is the goal.
- Learn the **Up to face** and **Up to part** end conditions cold by building a part where a boss must always meet a curved top surface no matter how tall the base gets.
- Read about **named views and section views** in a Part Studio (`right-click a face → Section view`) to inspect your shell wall thickness from the inside.
- Right-click your Part Studio tab → **Versions and history**, and create a named Version after you finish the mini-project, so you can branch from it in Week 3.

## Up next

Continue to **Week 3 — References, Planes & Multi-Feature Parts** once you have created a Version of your finished mini-project part and pasted its public OnShape link into your cohort tracker.

---

*If you find errors in this material, please open an issue or send a PR. Future learners will thank you.*
