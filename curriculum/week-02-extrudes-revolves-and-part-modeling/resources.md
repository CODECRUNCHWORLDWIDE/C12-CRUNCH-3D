# Week 2 — Resources

Every resource on this page is **free**. OnShape's Learning Center and Help are free with any OnShape account, including the free Public plan. The reference sites linked here are open. No paywalled books are linked. If a link 404s, please open an issue so we can replace it.

A note on OnShape's free plan: documents you create are **public** (anyone with the link can view them). That is fine for coursework and is in fact how we share parts for review. Never put anything confidential in a free-plan document.

## Required reading (work it into your week)

- **OnShape Help — Extrude**: the canonical reference for every end condition and operation type you use Monday and Tuesday.
  <https://cad.onshape.com/help/Content/extrude.htm>
- **OnShape Help — Revolve**: full and partial revolves, the axis rule, thin revolves.
  <https://cad.onshape.com/help/Content/revolve.htm>
- **OnShape Help — Hole feature**: simple/counterbore/countersink, standard sizes, blind vs through.
  <https://cad.onshape.com/help/Content/hole.htm>
- **OnShape Help — Fillet**: constant, multiple, variable radius, and tangent propagation.
  <https://cad.onshape.com/help/Content/fillet.htm>
- **OnShape Help — Shell**: removing faces and per-face thickness.
  <https://cad.onshape.com/help/Content/shell.htm>

## OnShape Learning Center (free, self-paced courses)

The Learning Center is OnShape's official training. Create the free account, then work these in order — they map almost exactly onto this week.

- **Learning Center home** (browse all paths):
  <https://learn.onshape.com/>
- **"Introduction to Part Studios"** — the core modeling course; the Extrude and Revolve lessons match Lectures 1 and 2.
  <https://learn.onshape.com/learn/learning-plan/introduction-to-onshape>
- **"Fundamentals: Part Design Using Part Studios"** — a deeper guided path; do the Extrude, Revolve, and "modify with features" units.
  <https://learn.onshape.com/courses>
- **OnShape Learning Center courses on dress-up features** (fillet, chamfer, shell, draft) — search "fillet" and "shell" in the course catalog.
  <https://learn.onshape.com/courses>

## OnShape Help — the dress-up and editing features

- **Chamfer**: <https://cad.onshape.com/help/Content/chamfer.htm>
- **Draft**: <https://cad.onshape.com/help/Content/draft.htm>
- **Boolean (Union / Subtract / Intersect)**: <https://cad.onshape.com/help/Content/booleanmf.htm>
- **Using the rollback bar / editing features**: <https://cad.onshape.com/help/Content/rollbackbar.htm>
- **Sketch (refresher from Week 1)**: <https://cad.onshape.com/help/Content/sketching.htm>

## Reference and standards (so your holes and threads are real)

- **OnShape Help — Tapped and clearance hole standards** (the size tables behind the Hole feature dialog):
  <https://cad.onshape.com/help/Content/hole.htm>
- **ISO metric screw thread reference** (Wikipedia; good enough for picking M3/M4/M5 clearance and tap drill sizes):
  <https://en.wikipedia.org/wiki/ISO_metric_screw_thread>
- **Engineering drawing / GD&T primer** (you don't need GD&T until Week 5, but skim the dimensioning conventions):
  <https://en.wikipedia.org/wiki/Geometric_dimensioning_and_tolerancing>

## OnShape official channels (videos, free, no signup beyond YouTube)

- **OnShape on YouTube** — official channel; "Tech Tips" series is short and excellent:
  <https://www.youtube.com/@onshape>
- **OnShape "Tech Tips" playlist** — 2–5 minute focused clips; search "extrude," "revolve," "shell."
  <https://www.youtube.com/@onshape/playlists>

## Community channels (free, consistently good on OnShape modeling)

You learn fastest watching someone model a real part end to end. Pick one and follow along.

- **OnShape's own webinars and Learning Center videos** (linked from the Learning Center above) — vendor-made but genuinely instructional.
- **Search YouTube for "OnShape revolve knob" or "OnShape shell enclosure"** — there is a healthy community of mechanical-design creators; watch how they order their feature lists, not just the final result.

## Tools you'll use this week

- **OnShape** (browser) — your CAD environment. Verify you can open a Part Studio and that units read **Millimeter** under the document **Workspace units** (`⚙ → Workspace units`).
- **A reference image / dimensioned sketch** — for the challenge you will model from a photo plus a few key dimensions. A phone camera and a ruler or caliper are enough.
- **(Optional) A digital caliper** — if you have one, measuring a real bottle/knob makes the challenge far more satisfying.
- **OnShape mobile/tablet app** (optional) — handy for orbiting a model on a second screen while you read.

## Keyboard shortcuts worth memorizing this week

Keep this open in a tab. OnShape shortcuts (default, browser):

| Action | Shortcut |
|--------|----------|
| Sketch | `s` (then pick a tool) or `Shift+S` for the sketch dialog |
| Extrude | `Shift+E` |
| Revolve | `Shift+R` |
| Fillet | `Shift+F` |
| Line | `g`, `l` |
| Dimension | `d` |
| Normal-to view (look straight at a face/plane) | `n` |
| Fit to screen | `f` |
| Rotate view | middle-mouse drag (or `Shift` + right-drag) |
| Roll back one feature | drag the **rollback bar**, or right-click a feature → *Roll back* |

## Glossary cheat sheet

Keep this open in a tab.

| Term | Plain English |
|------|---------------|
| **Part Studio** | The OnShape environment where you *model* parts (sketches + features). Not where you assemble them. |
| **Feature list** | The ordered history of every sketch and feature; the part is the replay of this list top-to-bottom. |
| **Rollback bar** | The blue bar in the feature list you drag up to "rewind" the model to an earlier state for diagnosis or insertion. |
| **Profile** | The closed sketch region(s) a feature acts on (what you extrude or revolve). |
| **Extrude** | Push a profile perpendicular to its sketch plane to make/modify a solid. |
| **End condition** | How far an extrude/cut goes: Blind, Symmetric, Through all, Up to face, Up to next, Up to vertex. |
| **Boolean** | Combining solids: Add (union), Remove (subtract), Intersect (keep only the overlap). |
| **Merge scope** | Which existing bodies an Add/Remove operation is allowed to affect. |
| **Revolve** | Spin a profile around an axis to make a turned (rotationally symmetric) solid. |
| **Hole feature** | A dedicated feature that places manufacturing-aware holes (counterbore, countersink, tapped) with standard sizes. |
| **Fillet** | A rounded edge (adds material on a concave edge, removes on a convex edge). |
| **Chamfer** | A flat angled cut across an edge (a "beveled" edge). |
| **Shell** | Hollows a solid to a uniform wall thickness, optionally opening selected faces. |
| **Draft** | A slight taper on faces so a molded/cast part can release from its mold. |
| **Regenerate / rebuild** | OnShape re-running the feature list after an edit. A "clean rebuild" has no red errors. |
| **Construction geometry** | Reference-only sketch entities (the dashed lines/axes) that drive geometry but aren't part of the profile. |

---

*If a link 404s, please open an issue so we can replace it.*
