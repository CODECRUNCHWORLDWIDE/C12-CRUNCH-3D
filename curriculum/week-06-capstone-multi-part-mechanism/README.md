# Week 06 — Capstone: Multi-Part Mechanism & Drawing Package

Welcome to the last week of **C12 · Crunch 3D: CAD & Modeling**. You do not learn a new OnShape feature this week. You ship.

Everything you have built since Week 01 — disciplined fully-defined sketches, solid parts from extrudes and revolves, multi-feature parts on construction geometry, articulating assemblies with real mates, and parametric drawings with GD&T and Configurations — comes together into one deliverable: an **original multi-part mechanism that moves**, modeled in OnShape, assembled with the correct mates, driven by at least one configured part, and shipped with a complete drawing package and neutral-format exports. Then you defend it.

"Defend it" is not a metaphor. This week you run a real design review. You stand in front of peers (or a cohort lead, or a recorded camera a hiring manager will eventually watch), you drag the mechanism through its full range of motion live, you change a single driving variable and prove the whole assembly rebuilds without a single red error, and you answer the questions a senior mechanical designer asks when they decide whether to trust your model in a real product. You produce a 5-minute video walkthrough, an assembly drawing plus key part drawings with a bill of materials, a STEP and an STL of the released version, and a written design walkthrough that is honest about the tradeoffs you made.

The week has a rhythm: scope and concept-sketch early, model and mate the mechanism mid-week, then configure, document, export, and present at the end. If your Week 05 part did not rebuild cleanly when you flipped a Configuration, fix that first — the grader changes a driving variable on your live document and a feature tree that throws a rebuild error is the difference between a pass and a fail.

This is the week the course has been building toward. Treat it like a release.

## Learning objectives

By the end of this week, you will be able to:

- **Scope** an original mechanism from a concept sketch to a parts list with a clear degrees-of-freedom plan, before opening a single Part Studio.
- **Model** each component as a clean, fully-defined parametric part whose feature tree reads top-to-bottom like a build sequence and survives a driving-dimension change.
- **Assemble** three or more parts with the correct mate types so the mechanism has *exactly* the intended degrees of freedom and articulates through its full range without interference.
- **Parameterize** at least one part with a Variable Studio and a Configurations table so one model yields a family of sizes, and prove the assembly rebuilds across every configuration.
- **Produce** a complete drawing package — an assembly drawing with a balloon-and-BOM, plus dimensioned drawings of the key parts with at least one section view and one GD&T frame.
- **Release** a clean version: tag an immutable Version, export a STEP (assembly) and an STL (a printable part), and confirm the exports open in a neutral viewer.
- **Present** the design in a live review: drag the mechanism, demonstrate parametric robustness on camera, and answer the standard senior-designer questions about degrees of freedom, manufacturability, and failure modes without flinching.
- **Record** a 5-minute walkthrough a hiring manager can watch and a peer can reproduce from your feature tree.

## Prerequisites

This week assumes you have completed Weeks 01–05 of C12 and that those mini-projects produced working, fully-defined OnShape documents. Specifically, you need:

- An OnShape account (the free Public plan is fine) and fluency with Documents, Part Studios, Assemblies, Versions, and the feature tree. (Week 01.)
- The ability to build a solid part from a sketch with Extrude, Revolve, the Hole feature, Fillet, Chamfer, and Shell. (Week 02.)
- Construction planes, axes, mate connectors, patterns, mirror, sweep, and loft, plus a feel for design-intent feature ordering. (Week 03.)
- The mate system end to end — Fastened, Revolute, Slider, Cylindrical, Planar, Ball, Pin-Slot — and how mate connectors define degrees of freedom, plus sub-assemblies and the Standard Content library. (Week 04.)
- Drawings with orthographic and section views, dimensioning, a title block, a BOM, basic GD&T, plus Variables and Configurations for part families. (Week 05.)

If any of those is shaky, this week will expose it. That is the point.

## Topics covered

- How a real design review runs: the agenda, the artifacts, the questions, and the failure modes of the *reviewer* as well as the reviewed.
- The senior-designer question set: degrees of freedom, the over- and under-constrained mate, the interference at the extremes of travel, the "what breaks when you double a dimension" walk, and manufacturability.
- Designing a mechanism from intent: the concept sketch, the kinematic skeleton, the degrees-of-freedom budget, and choosing mates before you model parts.
- Parametric robustness: building a feature tree and a mate scheme that survive a driving-variable change, and proving it on camera.
- The drawing package as a deliverable: the assembly drawing, the balloon-and-BOM, the key part drawings, the one section view and one GD&T frame that show you can communicate to a machinist.
- Shipping a CAD deliverable: immutable Versions and the release branch, STEP for downstream CAD, STL for print/mesh, and which export format answers which question.
- The 5-minute video walkthrough: what to show, what to skip, and how to drag one mechanism through its range on camera.
- Mock review structure: one design-defense round and one OnShape deep-dive round.

## Weekly schedule

The schedule below adds up to approximately **36 hours**. Treat it as a target, not a contract; the capstone deserves whatever it takes.

| Day       | Focus                                                       | Lectures | Exercises | Challenges | Quiz/Read | Homework | Mini-Project | Self-Study | Daily Total |
|-----------|-------------------------------------------------------------|---------:|----------:|-----------:|----------:|---------:|-------------:|-----------:|------------:|
| Monday    | Scope & concept-sketch; the design-review playbook          |    2h    |    0.5h   |     0h     |    0.5h   |   1h     |     2h       |    0.5h    |     6.5h    |
| Tuesday   | Model each part as a clean parametric Part Studio            |    0h    |    2h     |     1h     |    0.5h   |   1h     |     2h       |    0h      |     6.5h    |
| Wednesday | Assemble & mate; drag through full range of motion          |    1h    |    2h     |     1h     |    0.5h   |   1h     |     1.5h     |    0h      |     7h      |
| Thursday  | Configure a part; build the drawing package & BOM           |    1h    |    1.5h   |     0h     |    0.5h   |   1h     |     1.5h     |    0.5h    |     6.5h    |
| Friday    | Export STEP/STL, tag the Version; deliver the live review    |    0h    |    0h     |     0h     |    0.5h   |   0h     |     3h       |    0.5h    |     4h      |
| Saturday  | Mock review; portfolio polish; rebuild-robustness drill      |    0h    |    0h     |     0h     |    0h     |   1h     |     2h       |    0.5h    |     3.5h    |
| Sunday    | Quiz, retrospective, course wrap                            |    0h    |    0h     |     0h     |    1h     |   0h     |     0.5h     |    0.5h    |     2h      |
| **Total** |                                                             | **4h**   | **8h**    | **2h**     | **3.5h**  | **5h**   | **12.5h**    | **2.5h**   | **36h**     |

## How to navigate this week

| File | What's inside |
|------|---------------|
| [README.md](./README.md) | This overview (you are here) |
| [resources.md](./resources.md) | OnShape docs, mechanism-design references, GD&T and export references, review templates |
| [lecture-notes/01-designing-a-working-mechanism.md](./lecture-notes/01-designing-a-working-mechanism.md) | From concept sketch to a kinematic skeleton to an articulating, parametrically robust assembly |
| [lecture-notes/02-shipping-a-cad-deliverable.md](./lecture-notes/02-shipping-a-cad-deliverable.md) | Versions and releases, the drawing package, STEP vs STL, and running the design review |
| [exercises/README.md](./exercises/README.md) | Index of the three exercises |
| [exercises/exercise-01-concept-to-skeleton.md](./exercises/exercise-01-concept-to-skeleton.md) | Turn a concept sketch into a fully-defined kinematic skeleton sketch and a DOF budget |
| [exercises/exercise-02-mate-the-mechanism.md](./exercises/exercise-02-mate-the-mechanism.md) | Insert and mate the parts so the mechanism has exactly the intended degrees of freedom |
| [exercises/exercise-03-configure-and-release.md](./exercises/exercise-03-configure-and-release.md) | Configure a part, prove the rebuild, tag a Version, and export STEP/STL |
| [challenges/README.md](./challenges/README.md) | Index of the weekly challenge |
| [challenges/challenge-01-deliver-the-capstone-live.md](./challenges/challenge-01-deliver-the-capstone-live.md) | Deliver the mechanism live: full range of motion, parametric rebuild, design review |
| [quiz.md](./quiz.md) | 12 questions, answer key at the bottom |
| [homework.md](./homework.md) | The week's deliverables with a rubric |
| [mini-project/README.md](./mini-project/README.md) | The full capstone mechanism brief |

## The "it rebuilds on demand" promise

C12 has one recurring marker, and Week 06 is where it cashes out:

```
Regenerate complete · 0 errors · 0 warnings · all configurations valid
```

The grader will open your live OnShape document, drag the mechanism through its full range of motion, change a key driving variable, switch through every Configuration, and read your drawings and exports. If a driving-variable change throws a single red rebuild error, or a Configuration leaves a part broken, or the assembly interferes at the extremes of travel, the capstone does not pass — regardless of how good the render looks. A model you cannot edit and rebuild on demand is not a parametric model; it is a fragile shape you are afraid to touch.

## Stretch goals

If you finish the regular work early and want to push further:

- Make the configured part drive a *family table* of three or more sizes and produce a drawing for each from one model. Document whether the BOM and the assembly stay valid as the configuration changes.
- Add a second articulating joint, or replace a Revolute joint with a Pin-Slot or a Gear mate relation so the mechanism's motion is geometrically coupled (e.g., two gears that stay meshed, or a rack-and-pinion).
- Build a Mate Connector-driven exploded view and use it for the assembly drawing instead of a static iso, so the BOM balloons read cleanly.
- Run an Interference Detection pass at three points across the range of travel (not just the home position) and document the clearance at the worst point with a measured number.
- Read one published mechanism teardown or a real assembly drawing from GrabCAD or a manufacturer's site and write a one-page note on what their drawing communicates that yours does not.

## Up next

There is no Week 07. After you ship the capstone and clear the review, you are done with C12. The intended next track is **C13 Crunch Fabricate** — take the printable part you just exported and learn slicing, tolerancing for real-world fits, and design-for-manufacturing on FDM and resin printers. Read the [Crunch Labs Charter](../../../CRUNCH-LABS-CHARTER.md) for the full pathway.

---

*If you find errors in this material, please open an issue or send a PR. Future learners will thank you.*
