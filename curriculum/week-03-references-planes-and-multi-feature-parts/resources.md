# Week 3 — Resources

Every resource on this page is **free**. OnShape's Help docs are public and need no account. The OnShape Learning Center is free with a free OnShape account. No paywalled books are linked. If a link 404s, please open an issue so we can replace it.

> A note on OnShape's UI: it ships continuous cloud updates, so a menu may have moved since a help page's screenshots were taken. The *concepts* below are stable; if a button isn't where a doc shows it, use OnShape's in-app search (press **`/`** or click the search field at the top of the toolbar) and type the feature name.

## Required reading (work it into your week)

- **Planes** — the canonical reference for every plane type you'll build this week:
  <https://cad.onshape.com/help/Content/planes.htm>
- **Mate connectors** — the persistent reference frame you plant now and mate in Week 4:
  <https://cad.onshape.com/help/Content/mate_connector.htm>
- **Linear pattern**:
  <https://cad.onshape.com/help/Content/linearpattern.htm>
- **Circular pattern**:
  <https://cad.onshape.com/help/Content/circularpattern.htm>
- **Sweep**:
  <https://cad.onshape.com/help/Content/sweep.htm>
- **Loft**:
  <https://cad.onshape.com/help/Content/loft.htm>

## OnShape Help — feature-by-feature

- **Mirror**: <https://cad.onshape.com/help/Content/mirror.htm>
- **Axis** (construction axes): <https://cad.onshape.com/help/Content/axis.htm>
- **Sketching** (sketch planes, on-face sketching): <https://cad.onshape.com/help/Content/sketdialog.htm>
- **Rollback bar & feature history**: <https://cad.onshape.com/help/Content/rollbackbar.htm>
- **Variables** (declare `#name` inline; full Variable Studio is Week 5): <https://cad.onshape.com/help/Content/variables.htm>
- **Use construction geometry**: <https://cad.onshape.com/help/Content/construction-geometry.htm>

## OnShape Learning Center (free with account)

The official, self-paced courses. Watch only the modules relevant to this week.

- **Learning Center home**: <https://learn.onshape.com/>
- **CAD learning path — Fundamentals** (Part Studios, planes, patterning): <https://learn.onshape.com/learn/learning-path/cad>
- **Self-paced course: Introduction to Part Studios** (covers planes and references): <https://learn.onshape.com/courses/introduction-to-part-studios>
- **Multi-part Part Studios & advanced features** (patterns, sweep, loft): <https://learn.onshape.com/learn/learning-path/cad>

## Reference & glossary

- **OnShape glossary** — official term definitions (Part Studio, mate connector, configuration): <https://cad.onshape.com/help/Content/Primer/glossary.htm>
- **Keyboard shortcuts** — pin this; the speed difference is real: <https://cad.onshape.com/help/Content/keyboard_shortcuts.htm>
- **FeatureScript** (OnShape's parametric scripting language — *optional, advanced* context for how features work under the hood; you do not write any this week): <https://cad.onshape.com/FsDoc/>

## Design intent & best practices

- **OnShape Resource Center** — technical briefs and webinars on modeling for design intent and robustness:
  <https://www.onshape.com/en/resource-center>
- **OnShape Blog — modeling best practices** (search "design intent" and "feature order"):
  <https://www.onshape.com/en/resources/blog>
- **GD&T and engineering-drawing fundamentals** (you'll need this in Week 5; skim now if curious):
  <https://www.gdandtbasics.com/>

## Free practice drawings & part references

To pull a "reproduce this part" target without buying anything:

- **GrabCAD Library** — free, huge library of real parts and drawings to study and re-model (account free):
  <https://grabcad.com/library>
- **GD&T Basics — free practice drawings**: <https://www.gdandtbasics.com/free-resources/>
- **McMaster-Carr** — vendor catalog with downloadable models and dimensioned drawings of real hardware (fasteners, brackets, fittings) you can re-model for practice:
  <https://www.mcmaster.com/>

## Videos (free, no signup)

- **OnShape's official YouTube channel** — tutorials, tech tips, and "OnShape Live" sessions:
  <https://www.youtube.com/@Onshable> *(if the handle has changed, search "Onshape" on YouTube; the official channel is verified and reposts.)*
- **OnShape Tech Tips playlist** — short, focused clips on planes, patterns, sweeps, and lofts:
  <https://www.youtube.com/@Onshable/playlists>
- **Search tip:** for any feature this week, search YouTube for `onshape <feature> tutorial` (e.g. `onshape loft tutorial`) — the official short clips are the most reliable.

## Tools you'll use this week

- **OnShape** — browser-based, no install. Sign in at <https://cad.onshape.com/>. Free **Public** plan: full modeling features; all documents are public (fine for coursework). Verify you can create a Document and a Part Studio before Monday.
- **A modern browser** — Chrome, Edge, Firefox, or Safari, kept current. OnShape is WebGL-heavy; a discrete GPU helps but is not required.
- **A mouse with a scroll wheel** — strongly recommended. Middle-drag to rotate, scroll to zoom. Modeling on a trackpad alone is slow and frustrating.
- **OnShape mobile/tablet app** (optional) — view and lightly edit your models on the go: <https://www.onshape.com/en/products/mobile>.

## Glossary cheat sheet

Keep this open in a tab.

| Term | Plain English |
|------|---------------|
| **Part Studio** | The workspace where you model parts (sketches + features). One Document can hold many. |
| **Construction plane** | An infinite reference plane with no thickness. Top/Front/Right are the defaults; you build more. |
| **Offset plane** | A construction plane parallel to another, a set distance away. |
| **Angled plane** | A construction plane tilted a set angle from a reference, hinged about an edge/axis. |
| **Point–normal plane** | A plane defined by a point and a normal direction — perpendicular to a path at that point. Used for sweep profiles. |
| **Mid plane** | The symmetry plane halfway between two faces/planes. The natural mirror reference. |
| **Construction axis** | An infinite reference line. A circular pattern spins about one. |
| **Mate connector** | A small named coordinate frame (origin + XYZ) you place on geometry; mates snap to it in Week 4. |
| **Feature tree** | The top-to-bottom recipe of sketches and features that regenerates the part. |
| **Rollback bar** | The blue bar you drag up the tree to view/edit the part as it was at an earlier step. |
| **Linear pattern** | Copies a seed feature evenly along one or two directions. |
| **Circular pattern** | Copies a seed feature evenly around an axis. |
| **Mirror** | Reflects a seed feature/body across a plane. |
| **Sweep** | Drags one cross-section profile along a path. |
| **Loft** | Blends between two or more different profiles on different planes. |
| **Seed** | The original feature a pattern/mirror copies. |
| **Dangling reference** | A sketch/feature whose host geometry was deleted or consumed — shows yellow/red. |
| **Design intent** | Choosing references and feature order so edits propagate the way you mean them to. |
| **BCD** | Bolt-circle diameter — the diameter of the ring a circular bolt pattern sits on. |

---

*If a link 404s, please open an issue so we can replace it. OnShape ships frequent UI updates; concepts are stable even when buttons move.*
