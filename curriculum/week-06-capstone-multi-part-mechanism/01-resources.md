# Week 06 — Resources

Capstone week. The reading here is split into five buckets: the OnShape documentation you will lean on while you build, mechanism- and kinematics-design references, the drawing / GD&T references for the documentation package, the export-and-release references, and the design-review templates. Everything is free; the only thing that costs anything is an OnShape paid plan, which you do **not** need — the free Public plan models, assembles, configures, draws, and exports everything this week requires (your documents are public, which is fine for a portfolio piece).

## OnShape — the docs you'll actually open

- **OnShape Help — Assemblies and mates** — the canonical reference for every mate type and how mate connectors define degrees of freedom:
  <https://cad.onshape.com/help/Content/Primary/Topics/assembly.htm>
- **OnShape Help — Mate connectors** — the implicit/explicit mate-connector mechanics behind every joint you place this week:
  <https://cad.onshape.com/help/Content/Primary/Topics/mate-connector.htm>
- **OnShape Help — Configurations** — how to build a configuration table, input types (configuration variable, list, checkbox), and what a configured part does to the assembly:
  <https://cad.onshape.com/help/Content/Primary/Topics/configurations.htm>
- **OnShape Help — Variable Studio and variables** — the `#variable` mechanism that lets one number drive many features and survive a change:
  <https://cad.onshape.com/help/Content/Primary/Topics/variables.htm>
- **OnShape Help — Drawings** — views, dimensions, the title block, the BOM table, and balloons:
  <https://cad.onshape.com/help/Content/Primary/Topics/drawings.htm>
- **OnShape Help — Versions and history (the version graph)** — immutable Versions, branches, and how a release tag works:
  <https://cad.onshape.com/help/Content/Primary/Topics/versions-and-history.htm>
- **OnShape Help — Import and export (STEP, Parasolid, STL, and more)** — which neutral format carries what, and the per-format options:
  <https://cad.onshape.com/help/Content/Primary/Topics/import-export.htm>
- **OnShape Learning Center** — free, current, official guided courses; the "Introduction to Assemblies" and "Configurations" paths map directly onto this week:
  <https://learn.onshape.com/>

## Mechanism & kinematics design

- **Degrees of freedom & the Gruebler / Kutzbach mobility equation** — the math behind "how many joints do I need for exactly one DOF"; you use this to budget your mechanism before modeling:
  <https://en.wikipedia.org/wiki/Chebychev%E2%80%93Gr%C3%BCbler%E2%80%93Kutzbach_criterion>
- **Four-bar linkage — Grashof's criterion** — whether your linkage can fully rotate, rock, or jams; the single most useful idea for a linkage capstone:
  <https://en.wikipedia.org/wiki/Four-bar_linkage>
- **507 Mechanical Movements** — the classic illustrated catalog of mechanisms (cranks, cams, ratchets, escapements); pick your capstone mechanism from here:
  <https://507movements.com/>
- **KMODDL — Cornell's Kinematic Models for Design Library** — animated reference models of historical mechanisms, good for choosing and understanding a motion:
  <https://digital.library.cornell.edu/collections/kmoddl>
- **GrabCAD Library** — real, downloadable assemblies to study (study, do not copy) the way other designers structured mates and feature trees:
  <https://grabcad.com/library>

## Drawings, dimensioning & GD&T

- **ASME Y14.5 (the GD&T standard) — overview** — the standard your GD&T frames reference; read for datums, position, and flatness even if you only use one frame:
  <https://en.wikipedia.org/wiki/Geometric_dimensioning_and_tolerancing>
- **ISO 128 / first-angle vs third-angle projection** — which projection convention your title block declares; getting this wrong makes a drawing un-machinable:
  <https://en.wikipedia.org/wiki/Multiview_orthographic_projection>
- **OnShape Help — Geometric tolerance (GD&T) in drawings** — how to place a feature control frame and a datum in an OnShape drawing:
  <https://cad.onshape.com/help/Content/Primary/Topics/geometric-tolerance.htm>
- **Engineering drawing fits and tolerances (ISO 286 hole/shaft system)** — the H7/g6-style fit callouts you use so a pin actually slides in a hole:
  <https://en.wikipedia.org/wiki/Engineering_fit>
- **OnShape Help — Bill of Materials (BOM)** — auto-generated, balloon-linked, and how part metadata (part number, description) flows into it:
  <https://cad.onshape.com/help/Content/Primary/Topics/bill-of-materials.htm>

## Export, release & downstream

- **STEP (ISO 10303) — what a STEP file carries** — boundary-representation solids with assembly structure; the format for handing a model to another CAD package:
  <https://en.wikipedia.org/wiki/ISO_10303>
- **STL format reference** — the triangle-mesh format for 3D printing; resolution, the chord-tolerance tradeoff, and why it loses parametric history:
  <https://en.wikipedia.org/wiki/STL_(file_format)>
- **OnShape Help — Export STL (resolution / chord tolerance options)** — the dialog you set when you export the printable part, and what coarse-vs-fine costs:
  <https://cad.onshape.com/help/Content/Primary/Topics/export-stl.htm>
- **3MF Consortium** — the modern successor to STL (carries color, units, and metadata); a stretch export if your printer toolchain accepts it:
  <https://3mf.io/>

## Design review & delivery

- **The Pragmatic Engineer — how design reviews actually run (Gergely Orosz)** — the meeting itself; the question style transfers cleanly from software to a CAD design review:
  <https://blog.pragmaticengineer.com/>
- **Mermaid live editor** — sketch the kinematic skeleton / DOF diagram you put in your design walkthrough; it renders in GitHub:
  <https://mermaid.live/>
- **A screen recorder** — Loom, OBS Studio (cross-platform, free), or QuickTime (macOS) for the 5-minute video; OnShape itself has no built-in recorder.
- **OnShape Public document sharing** — how to share a read-only link to your capstone document so a reviewer (or hiring manager) can open the live model:
  <https://cad.onshape.com/help/Content/Primary/Topics/sharing-documents.htm>

## Tools you'll use this week

- **OnShape** in any modern browser — no install. Chrome, Edge, Safari, and Firefox all work; the iPad and Android apps work too but the review is easier on a desktop.
- **A STEP/STL viewer for the export sanity-check** — OnShape's own viewer, [3dviewer.net](https://3dviewer.net/) (browser, free), or your slicer (for the STL).
- **A spreadsheet or Markdown table** — for the parts list and the DOF budget before you model.

## Career pack (cross-referenced)

The capstone is the headline portfolio artifact. The supporting docs live one level up in the track root:

- `interview-prep/` — the design-defense prompts and OnShape deep-dive drills used for the mock review.
- `portfolio.md` — the templates for writing up the capstone, the feature-tree screenshots, and the rendered turntable.

---

*If a link 404s, please open an issue so we can replace it.*
