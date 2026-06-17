# Week 1 — Resources

Every resource on this page is **free**. OnShape's Learning Center is free with the same account you model in. OnShape's free/education plan is free forever for personal and learning use. No paywalled books are linked.

## Required reading & watching (work it into your week)

- **OnShape Learning Center — "Onshape Fundamentals: CAD" learning path** — the canonical onboarding path; do the first two modules this week:
  <https://learn.onshape.com/learn/learning-path/onshape-fundamentals-cad>
- **Introduction to Sketching (Learning Center course)** — the single most relevant course to Week 1; watch the sketch-entity and constraint videos:
  <https://learn.onshape.com/courses/introduction-to-sketching>
- **OnShape Help — Sketching** — the reference docs for every sketch tool and constraint; keep it open in a tab:
  <https://cad.onshape.com/help/Content/sketch.htm>
- **OnShape Help — Sketch constraints** — the definitive list of every geometric constraint and what it does:
  <https://cad.onshape.com/help/Content/Primary/Tutorials/sketch_constraints.htm>
- **OnShape Help — Dimension tool** — driving vs driven dimensions, and the smart-dimension behavior:
  <https://cad.onshape.com/help/Content/dimensiontool.htm>

## OnShape product & account

- **OnShape free / education plan** (sign up here): <https://www.onshape.com/en/products/free>
- **OnShape sign-in / the modeler itself**: <https://cad.onshape.com/>
- **System requirements & supported browsers**: <https://cad.onshape.com/help/Content/system-requirements.htm>
- **Keyboard shortcuts** (print this and tape it to your monitor):
  <https://cad.onshape.com/help/Content/keyboard-shortcuts.htm>

## Documents, versions & cloud workflow

- **OnShape Help — Documents** — what a Document is and how it differs from a "file":
  <https://cad.onshape.com/help/Content/documents.htm>
- **OnShape Help — Versions and history** — the version graph, named Versions, and history:
  <https://cad.onshape.com/help/Content/version_manager.htm>
- **OnShape Help — Branches and merging** — how OnShape does Git-style branching for CAD (we use it lightly this week, heavily by Week 6):
  <https://cad.onshape.com/help/Content/branch_and_merge.htm>

## The Part Studio & Feature tree

- **OnShape Help — Part Studios** — the modeling environment where your sketches live:
  <https://cad.onshape.com/help/Content/partstudios.htm>
- **OnShape Help — Feature list (the Feature tree)** — reading, reordering, renaming, and rolling back features:
  <https://cad.onshape.com/help/Content/featurelist.htm>
- **OnShape Help — Planes** — the default Top/Front/Right planes and the origin:
  <https://cad.onshape.com/help/Content/plane.htm>

## CAD theory (vendor-neutral, helpful background)

- **Wikipedia — Constraint (CAD) / Parametric design** — the general idea of constraints and degrees of freedom in any CAD package:
  <https://en.wikipedia.org/wiki/Parametric_design>
- **Wikipedia — Engineering drawing** — how to read the dimensioned drawings you'll reproduce in the challenge:
  <https://en.wikipedia.org/wiki/Engineering_drawing>
- **Wikipedia — Technical drawing — dimensioning** — what R, ⌀, and linear callouts mean:
  <https://en.wikipedia.org/wiki/Dimensioning>

## Video channels (free, no signup)

- **OnShape's official YouTube channel** — "Tech Tips" shorts are gold; search "Onshape sketch constraints":
  <https://www.youtube.com/@onshape>
- **OnShape Tech Tips playlist** — short, focused, current-version videos by the OnShape team:
  <https://www.youtube.com/playlist?list=PLDPlDdoChygtBkAhAFwfeYfwz9bTvyAVm>

## Public models to study this week

You learn more from one hour inspecting a well-built Document than from three hours of tutorials. Open one of these public Documents (read-only — make your own copy if you want to poke at it) and look at how its *first sketch* is anchored to the origin and fully defined:

- **Public Documents search** — filter to "Public" and search a part name like "bracket" or "gasket":
  <https://cad.onshape.com/documents?nav=true&resourceType=document&q=bracket>
- **OnShape's official sample Documents** are linked throughout the Learning Center courses above; open them and inspect the Feature tree.

## Tools you'll use this week

- **OnShape** — runs entirely in the browser; verify by signing in at <https://cad.onshape.com/> and creating a blank Document.
- **A three-button mouse** — strongly recommended for rotate/pan/zoom (see the README).
- **A screenshot tool** — your OS built-in (macOS: Shift-Cmd-4; Windows: Win-Shift-S) for capturing your fully-defined sketches for homework submission.
- **A PDF reader** — to open the dimensioned drawing in the challenge.

## Glossary cheat sheet

Keep this open in a tab.

| Term | Plain English |
|------|---------------|
| **Document** | The cloud container that holds your Part Studios, Assemblies, drawings, and their full history. The closest thing OnShape has to a "file." |
| **Part Studio** | The environment where you build geometry. Sketches and 3D features live here. A Document can have many. |
| **Assembly** | The environment where you insert parts and connect them with mates. We get there in Week 4. |
| **Feature tree** | The ordered list of everything you've done in a Part Studio, top to bottom. Also called the Feature list. |
| **Sketch** | A collection of 2D geometry on a plane or face, governed by constraints and dimensions. The basis of every 3D feature. |
| **Constraint** | A geometric rule between sketch entities (e.g., two lines are parallel). Removes degrees of freedom without a number. |
| **Driving dimension** | A numeric dimension that *controls* geometry. Change the number, the geometry moves. |
| **Driven (reference) dimension** | A numeric dimension that *reports* a measurement but does not control it. Shown in parentheses/grey. |
| **Degree of freedom (DOF)** | A way a sketch entity can still move. A point has 2 (x, y); fully defining means removing all of them. |
| **Under-defined** | The sketch still has free DOF; entities are **blue** and draggable. |
| **Fully defined** | Every DOF is removed; all geometry is **black** and locked. The goal. |
| **Over-defined** | Conflicting constraints/dimensions; entities turn **red/yellow**. Must be resolved. |
| **Construction geometry** | Sketch lines/points used as references (centerlines, axes) that do not become part of a 3D feature. |
| **Origin** | The (0,0,0) point where the three default planes meet. Anchor your first sketch to it. |
| **Version** | A named, immutable snapshot of a Document's history you create deliberately before sharing or branching. |

---

*If a link 404s, please open an issue so we can replace it. OnShape ships updates every three weeks, so screenshots in older videos may differ slightly from the live UI — the concepts hold.*
