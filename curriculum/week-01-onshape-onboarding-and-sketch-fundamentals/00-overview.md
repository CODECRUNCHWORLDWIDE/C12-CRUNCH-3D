# Week 1 — OnShape Onboarding & Sketch Fundamentals

Welcome to **C12 · Crunch 3D**. Week 1 is the foundation week. By Friday you should be able to create an OnShape Document from a blank workspace, set its units, draw lines, arcs, rectangles, and circles on a default plane, constrain them with coincident / horizontal / vertical / parallel / perpendicular / tangent / equal / concentric relations, add the few driving dimensions a profile actually needs, and watch the whole thing turn black — **fully defined** — and update parametrically when you drag a dimension. We do all of this *before extruding a single thing*, on purpose.

This is a CAD course, not a programming course. There is no code. The "exercises" are precise, numbered modeling walkthroughs you perform inside OnShape's browser window. Read them at the keyboard with OnShape open in another tab, and *do every step* — sketching is a motor skill as much as a conceptual one.

The first thing to internalize is that **a 3D model is only as good as the 2D sketch underneath it**. Every extrude, revolve, sweep, and loft you build in the next five weeks starts from a sketch. A sketch that is under-defined will move when you don't want it to; a sketch that is over-defined will refuse to rebuild when a colleague edits an upstream dimension. The whole discipline of parametric CAD lives in the gap between those two failures, and that gap is called a **fully-defined sketch**. We spend the entire first week there.

## Learning objectives

By the end of this week, you will be able to:

- **Distinguish** the three layers of OnShape you'll work in all course: the **Document** (the cloud container), the **Part Studio** (where you model geometry and sketches live), and the **Assembly** (where parts get mated). People conflate these constantly; we won't.
- **Create** a Document from scratch, set its default length unit and precision, and navigate the **Feature tree**, the graphics area, and the view cube.
- **Sketch** lines, arcs (three-point and tangent), rectangles (corner and center-point), circles, and slots on the **Top, Front, or Right** default plane.
- **Read the color of a sketch**: blue = under-defined (draggable), black = fully defined (locked), and recognize over-defined (red/yellow) entities on sight.
- **Apply geometric constraints** — coincident, horizontal, vertical, parallel, perpendicular, tangent, equal, concentric, midpoint, symmetric — and explain what *degrees of freedom* each one removes.
- **Add driving dimensions** with the Dimension tool, and tell a *driving* dimension (controls geometry) from a *driven* (reference) dimension.
- **Fully define** a sketch using the **minimum** dimension count by leaning on constraints first and dimensions last.
- **Use the origin** deliberately to anchor a sketch so it never floats in space.
- **Understand cloud versioning**: how OnShape auto-saves, what the **Versions and history** graph is, and why you create a named Version before sharing or branching.

## Prerequisites

This is the first week of C12, so the bar is intentionally low. You need:

- A free **OnShape** account (the free/education plan is sufficient for the entire course): <https://www.onshape.com/en/products/free>.
- A modern browser — Chrome, Edge, or Firefox. OnShape runs fully in the browser; there is **nothing to install** on desktop, and the iPad/Android apps mirror the same model.
- A three-button mouse (or a mouse with a clickable scroll wheel). You *can* drive OnShape on a trackpad, but a real mouse with a middle button makes rotate/pan/zoom dramatically less painful. This is the one piece of hardware advice we give early and often.
- The ability to read a basic dimensioned 2D drawing — what a linear dimension, a radius (R), and a diameter (⌀) callout mean. If you've never read a drawing, the first lecture covers exactly enough.

You do **not** need any prior CAD experience, any engineering background, or any math beyond middle-school geometry. If you have used SolidWorks, Fusion 360, or Inventor before, most concepts transfer — but the *interaction model* (cloud, no save button, the constraint inferencing) is different enough that you should read the first lecture anyway.

## Topics covered

- The three things people call "OnShape": the **Document** (cloud container with its own history), the **Part Studio** (the parametric modeling environment), and the **Assembly** (the mating environment).
- The OnShape window: **Feature tree**, graphics area, the **view cube**, the toolbar, the context menu, and the bottom **Feature toolbar**.
- Mouse navigation: rotate (right-drag), pan (middle-drag / Ctrl-right-drag), zoom (scroll), and **view normal to** a face or plane.
- The three default planes — **Top, Front, Right** — and the **Origin**, and why every first sketch should touch the origin.
- The **Sketch** environment: entering and exiting a sketch, the sketch toolbar, and the difference between sketch geometry and **construction geometry**.
- Sketch entities: **line**, **corner rectangle**, **center-point rectangle**, **center-point circle**, **three-point arc**, **tangent arc**, **slot**, **point**.
- **Sketch color states**: blue (under-defined), black (fully defined), and over-defined (the constraint conflict).
- **Geometric constraints**: coincident, horizontal, vertical, parallel, perpendicular, tangent, equal, concentric, midpoint, symmetric, fix.
- **Constraint inferencing**: the little glyphs OnShape shows while you draw, and how to accept or suppress an inferred constraint.
- **Driving vs driven dimensions**, linear / aligned / radial / diameter / angular dimensions, and the Dimension tool's smart behavior.
- **Degrees of freedom** — the mental model that makes "fully defined" make sense.
- **Units and precision**: setting the document's default unit, and typing units inline (e.g., `25 mm`, `1 in`).
- **Cloud versioning**: auto-save, the Versions and history graph, named Versions, and why you tag a Version before sharing.

## Weekly schedule

The schedule below adds up to approximately **36 hours**. Treat it as a target, not a contract — a slow, careful first week pays off for five weeks afterward.

| Day       | Focus                                              | Lectures | Exercises | Challenges | Quiz/Read | Homework | Mini-Project | Self-Study | Daily Total |
|-----------|----------------------------------------------------|---------:|----------:|-----------:|----------:|---------:|-------------:|-----------:|------------:|
| Monday    | OnShape tour: Documents, Part Studios, versioning  |    2h    |    1.5h   |     0h     |    0.5h   |   1h     |     0h       |    0.5h    |     5.5h    |
| Tuesday   | Sketch entities + first constrained drills         |    2h    |    2h     |     0h     |    0.5h   |   1h     |     0h       |    0h      |     6.5h    |
| Wednesday | Constraints, inferencing, degrees of freedom       |    1h    |    2h     |     1h     |    0.5h   |   1h     |     0h       |    0.5h    |     6h      |
| Thursday  | Driving dimensions, fully-defining a profile       |    1h    |    1h     |     0h     |    0.5h   |   1h     |     2h       |    0.5h    |     6h      |
| Friday    | Challenge profile + mini-project master sketch      |    0h    |    1h     |     0.5h   |    0.5h   |   1h     |     3h       |    0.5h    |     6.5h    |
| Saturday  | Mini-project deep work                             |    0h    |    0h     |     0h     |    0h     |   1h     |     3h       |    0h      |     4h      |
| Sunday    | Quiz, review, polish, write the walkthrough        |    0h    |    0h     |     0h     |    1h     |   0h     |     0.5h     |    0h      |     1.5h    |
| **Total** |                                                    | **6h**   | **7.5h**  | **1.5h**   | **3.5h**  | **6h**   | **11.5h**    | **2h**     | **36h**     |

## How to navigate this week

| File | What's inside |
|------|---------------|
| [README.md](./00-overview.md) | This overview (you are here) |
| [resources.md](./01-resources.md) | Curated OnShape Learning Center, docs, and CAD references |
| [lecture-notes/01-onshape-tour-documents-and-versioning.md](./02-lecture-notes/01-onshape-tour-documents-and-versioning.md) | What a Document, Part Studio, and Assembly are; the window; navigation; the Feature tree; cloud versioning |
| [lecture-notes/02-sketching-with-intent-constraints-and-dimensions.md](./02-lecture-notes/02-sketching-with-intent-constraints-and-dimensions.md) | Degrees of freedom; every geometric constraint; driving dimensions; fully-defining a sketch |
| [exercises/README.md](./03-exercises/00-overview.md) | Index of the sketching drills + a checklist |
| [exercises/exercise-01-first-document-and-sketch.md](./03-exercises/exercise-01-first-document-and-sketch.md) | Create a Document, set units, draw and fully-define a first rectangle-with-circles plate |
| [exercises/exercise-02-constraint-drills.md](./03-exercises/exercise-02-constraint-drills.md) | Six numbered constraint drills, each fully defined with the minimum dimensions |
| [exercises/exercise-03-arc-and-slot-profile.md](./03-exercises/exercise-03-arc-and-slot-profile.md) | Tangent arcs, slots, and concentric circles in one fully-defined lever profile |
| [challenges/README.md](./04-challenges/00-overview.md) | What the weekly challenge is and how it's graded |
| [challenges/challenge-01-gasket-profile.md](./04-challenges/challenge-01-gasket-profile.md) | Reproduce a dimensioned gasket drawing as one minimal, fully-defined sketch |
| [quiz.md](./05-quiz.md) | 10 questions on Documents, constraints, and fully-defined sketches |
| [homework.md](./06-homework.md) | Five practice tasks with a grading rubric |
| [mini-project/README.md](./07-mini-project/00-overview.md) | Full spec for the running project's Week-1 deliverable: the master sketch |

## The "fully defined" promise

C12 uses one recurring marker in every sketch you finish:

```
Sketch fully defined · 0 under-defined entities · 0 conflicts · all geometry black
```

If any line in your sketch is still **blue**, you are not done. If anything is **red or yellow**, you have a conflict to resolve, and you are also not done. The bottom-right of the OnShape window literally tells you when a sketch is "Fully defined" — make that status line ordinary. A blue line that you *meant* to be black is the single most common Week-1 mistake, and it causes parts to silently shift two weeks from now.

## Stretch goals

If you finish the regular work early and want to push further:

- Read the OnShape Learning Center's **"Sketching"** primer end to end: <https://learn.onshape.com/learn/learning-path/onshape-fundamentals-cad>.
- Take the same gasket profile from the challenge and try to fully-define it **two different ways** — once leaning on `symmetric`, once leaning on `equal` + mirror lines. Notice how the dimension count changes.
- Turn on the **"Show constraints"** display filter and screenshot your master sketch with every constraint glyph visible. Learning to *read* a constraint-decorated sketch is a senior skill; start now.
- Open any public OnShape Document (search the public Documents at <https://cad.onshape.com/documents?nav=true&resourceType=document&q=>) and inspect a stranger's Feature tree. Find their first sketch and see how *they* anchored it to the origin.

## Up next

Continue to **Week 2 — Extrudes, Revolves & Solid Part Modeling** once you've delivered the fully-defined master sketch for the mini-project. In Week 2 we finally turn 2D into 3D — and your Week-1 master sketch becomes the profile we extrude.

---

*If you find errors in this material, please open an issue or send a PR. Future learners will thank you.*
