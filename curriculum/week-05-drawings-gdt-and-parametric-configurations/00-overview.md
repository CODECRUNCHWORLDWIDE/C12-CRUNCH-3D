# Week 5 — Drawings, Dimensions, GD&T & Configurations

Welcome to **C12 · Crunch 3D**. Week 5 is where your model stops being a private CAD file and becomes a thing other people can read, manufacture, inspect, and order in three sizes. By Friday you should be able to take a finished part, generate a fully dimensioned multi-view drawing with a section view and a basic GD&T frame, fill out a real title block, auto-generate a BOM from an assembly, and then drive that same part into a family of sizes from a Variable Studio and a Configurations table — all inside OnShape's browser tab, no installs.

We assume you have completed Weeks 1–4: you can draw a fully-defined sketch, build a multi-feature parametric part, and assemble parts with mates that articulate. This week we do **not** make new geometry the headline. Instead we take the assembly you already built and answer the two questions a shop floor and a sales catalog actually ask: *"How do I make this exactly?"* (the drawing + GD&T) and *"Can I get it 20% bigger?"* (variables + configurations). Those are the deliverables that turn a hobby model into a product.

The first thing to internalize is that **a drawing and a model are two different documents that stay linked.** In OnShape a Drawing is its own tab (and its own document type) that *references* a Part Studio or Assembly. Change the model, the drawing's views and dimensions update — but only the ones that are *associative*. Manually-typed numbers do not. We will spend real time on the difference between an associative dimension that tracks the geometry and a "dumb" overridden value that lies to your machinist. The second thing to internalize: **a tolerance is not decoration.** Every dimension you place implies a tolerance whether you write one or not, and GD&T is the grammar engineers use to say *exactly* how much a feature is allowed to wander. We cover the basics — datums, flatness, position — not the whole ASME Y14.5 standard, but enough to read a real drawing and not embarrass yourself.

## Learning objectives

By the end of this week, you will be able to:

- **Distinguish** a Part Studio, an Assembly, and a Drawing tab — three OnShape document types people regularly conflate — and explain what "associative" means between them.
- **Create** a Drawing from a part, place orthographic views (front / top / right / iso) using third-angle projection, and set the sheet size and scale deliberately.
- **Place** a section view and a detail view, and explain when each communicates better than another orthographic projection.
- **Dimension** a view with associative dimensions, and recognize when a value has been overridden and is no longer tracking the model.
- **Fill** a title block and read the standard fields (part number, revision, scale, material, sheet, drawn-by, units).
- **Auto-generate** a Bill of Materials from an assembly, control its columns, and balloon the parts in an assembly view.
- **Read and write** basic GD&T: identify datums A/B/C, apply a flatness control, and apply a position tolerance with a feature control frame, including the difference between a basic dimension and a toleranced one.
- **Build** a Variable Studio (or in-part `#variables`) and reference variables in sketches and features with `#name` syntax and simple equations.
- **Configure** a part into a family of sizes with a Configurations table, using a configuration input (list or variable) that drives dimensions, suppresses features, and switches the part from a dropdown.
- **Export** a drawing to PDF and DXF and a part to STEP/STL, and explain which format a shop actually wants.

## Prerequisites

This week assumes you have completed **C12 · Crunch 3D** Weeks 1–4, or have equivalent OnShape fluency. Specifically:

- You can draw a sketch and drive it fully defined with constraints and dimensions (Week 1).
- You can build a solid part with Extrude, Revolve, Hole, Fillet, Chamfer, and Shell (Week 2).
- You can work off construction planes and use patterns, mirror, sweep, and loft (Week 3).
- You can insert parts into an Assembly and join them with Fastened, Revolute, Slider, and Cylindrical mates (Week 4).
- You have an OnShape account (the free Standard plan is enough — Drawings, Configurations, and Variable Studios are all included) and you have your running mini-project document from Weeks 1–4 in your account.

You do **not** need any prior drafting or GD&T experience. We start at "what is a drawing tab." If you have used SolidWorks or Fusion drawings before, the concepts transfer directly; OnShape's terminology and the associative/cloud behavior are what's new.

## Topics covered

- The three OnShape document types this week touches: Part Studio (geometry), Assembly (mates + BOM), Drawing (documentation), and how a Drawing references the others.
- Creating a Drawing: choosing a template, sheet size (A/B/C or A4/A3), and projection angle (first vs third).
- Orthographic views: the base view and projected views, view scale, hidden lines, tangent edges, and centerlines.
- Section views (full, half, aligned, broken-out) and detail views; the cutting-plane line and hatching.
- Associative vs overridden dimensions; driven dimensions; dimension chains, baseline, and ordinate dimensioning.
- Title block fields and what a shop reads first: part number, revision, material, finish, scale, units, tolerance block.
- The general tolerance block (the "unless otherwise specified" note) and how it backs every un-toleranced dimension.
- GD&T fundamentals: the datum reference frame (A/B/C), the feature control frame, basic dimensions, and three controls you'll actually place — flatness, position, and perpendicularity.
- Bill of Materials: auto-generation from an Assembly, item numbers, balloons, quantity rollup, and custom columns.
- Part Properties and custom properties (part number, description, material) that feed the title block and BOM.
- Variables: the Variable Studio tab, in-feature `#name` references, units on variables, and equations between variables.
- Configurations: configuration inputs (list, configuration variable, checkbox), the configuration table, configuring a dimension, suppressing a feature per configuration, and the configurations dropdown.
- Configured parts in assemblies and drawings; one drawing that documents multiple configurations.
- Export formats: PDF and DXF for the drawing, STEP (AP242) and STL for the model, and which to hand to which audience.

## Weekly schedule

The schedule below adds up to approximately **36 hours**. Treat it as a target, not a contract.

| Day       | Focus                                                | Lectures | Exercises | Challenges | Quiz/Read | Homework | Mini-Project | Self-Study | Daily Total |
|-----------|------------------------------------------------------|---------:|----------:|-----------:|----------:|---------:|-------------:|-----------:|------------:|
| Monday    | Drawing tabs, views, projection, sheet setup         |    2h    |    1.5h   |     0h     |    0.5h   |   1h     |     0h       |    0.5h    |     5.5h    |
| Tuesday   | Section/detail views, dimensioning, title block, BOM |    2h    |    2h     |     1h     |    0.5h   |   1h     |     0h       |    0h      |     6.5h    |
| Wednesday | GD&T basics: datums, flatness, position, FCFs        |    1h    |    2h     |     1h     |    0.5h   |   1h     |     0h       |    0.5h    |     6h      |
| Thursday  | Variables, equations, Variable Studio                |    1h    |    1h     |     0h     |    0.5h   |   1h     |     2h       |    0.5h    |     6h      |
| Friday    | Configurations & part families; mini-project work    |    0h    |    1h     |     0h     |    0.5h   |   1h     |     3h       |    0.5h    |     6h      |
| Saturday  | Mini-project deep work (configure + drawing + BOM)   |    0h    |    0h     |     0h     |    0h     |   1h     |     3h       |    0h      |     4h      |
| Sunday    | Quiz, review, export & polish                        |    0h    |    0h     |     0h     |    1h     |   0h     |     0.5h     |    0h      |     1.5h    |
| **Total** |                                                      | **6h**   | **7.5h**  | **2h**     | **3.5h**  | **6h**   | **8.5h**     | **2h**     | **35.5h**   |

## How to navigate this week

| File | What's inside |
|------|---------------|
| [README.md](./00-overview.md) | This overview (you are here) |
| [resources.md](./01-resources.md) | Curated OnShape Learning Center, ASME/GD&T, and reference links |
| [lecture-notes/01-the-drawing-package.md](./02-lecture-notes/01-the-drawing-package.md) | Drawing tabs, ortho & section views, dimensioning, title blocks, BOM, and GD&T basics |
| [lecture-notes/02-parametric-power-variables-and-configurations.md](./02-lecture-notes/02-parametric-power-variables-and-configurations.md) | Variable Studios, equations, configuration inputs, configuration tables, part families |
| [exercises/README.md](./03-exercises/00-overview.md) | Index of the week's modeling/drawing drills |
| [exercises/exercise-01-first-drawing.md](./03-exercises/exercise-01-first-drawing.md) | Guided: make your first drawing — views, dimensions, title block |
| [exercises/exercise-02-section-views-and-gdt.md](./03-exercises/exercise-02-section-views-and-gdt.md) | Section view + datums + flatness + position feature control frames |
| [exercises/exercise-03-configurations-part-family.md](./03-exercises/exercise-03-configurations-part-family.md) | Variable Studio + Configurations table → one part, three sizes |
| [challenges/README.md](./04-challenges/00-overview.md) | Index of the weekly challenge |
| [challenges/challenge-01-manufacturing-ready-drawing.md](./04-challenges/challenge-01-manufacturing-ready-drawing.md) | A manufacturing-ready, toleranced, configured drawing of an earlier part |
| [quiz.md](./05-quiz.md) | 10 multiple-choice questions |
| [homework.md](./06-homework.md) | Six practice problems for the week |
| [mini-project/README.md](./07-mini-project/00-overview.md) | Full spec: parameterize the assembly's key part + ship its drawing |

## The "fully defined, fully documented" promise

C12 uses a small recurring marker in every exercise that ends in a finished drawing:

```
Drawing up to date · 0 out-of-date views · all dimensions associative
```

If your Drawing tab shows an out-of-date banner, or a dimension is showing a value you typed instead of a value the model computed, you are not done. We treat overridden dimensions like compiler warnings: a manually overridden number is a lie waiting to ship to a machinist. The point of Week 5 is to make a clean, associative, up-to-date drawing ordinary.

## Stretch goals

If you finish the regular work early and want to push further:

- Read OnShape's **"Drawings"** topic in the Learning Center end to end: <https://learn.onshape.com/learn/learning-paths>.
- Skim the free **"GD&T 101"** primer at GD&T Basics and identify, on a real drawing, every symbol you can name: <https://www.gdandtbasics.com/>.
- Add a **second configuration axis** to a part (e.g., size *and* a with-/without-mounting-tabs checkbox) and watch the configuration table become a 2D grid.
- Make a single drawing sheet that shows the **same part in two configurations** side by side, each in its own view with its own dimensions.
- Export the part to **STEP AP242** and reopen it in a fresh OnShape document; note what survives the round-trip (geometry, PMI) and what doesn't (the feature tree).

## Up next

Continue to **Week 6 — Capstone: Multi-Part Mechanism & Drawing Package** once you have pushed the configured part and its drawing PDF to your project folder.

---

*If you find errors in this material, please open an issue or send a PR. Future learners will thank you.*
