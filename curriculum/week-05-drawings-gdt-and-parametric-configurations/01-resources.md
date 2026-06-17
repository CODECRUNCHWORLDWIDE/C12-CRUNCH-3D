# Week 5 — Resources

Every resource on this page is reachable with a **free** OnShape account or is openly published. OnShape's Learning Center is free with any plan, including the free Standard plan. The GD&T primers linked here are free reading. No paywalled standards documents are required — we point at ASME Y14.5 for reference, but you can complete the week without buying it.

## Required reading (work it into your week)

- **OnShape Learning Center — Drawings learning path** — the canonical, kept-current course on creating drawings, views, and dimensions:
  <https://learn.onshape.com/learn/learning-paths>
- **OnShape Help — Drawings** — the reference docs for every drawing tool you'll touch:
  <https://onshape-public.document360.io/docs/drawings>
- **OnShape Help — Configurations** — how configuration inputs and tables work:
  <https://onshape-public.document360.io/docs/configurations>
- **OnShape Help — Variables and the Variable Studio** — `#name` references and equations:
  <https://onshape-public.document360.io/docs/variable>
- **GD&T Basics — "What is GD&T?"** — the friendliest free on-ramp to datums, feature control frames, and the common controls:
  <https://www.gdandtbasics.com/gdt-basics/>

## The standard (reference, don't memorize)

GD&T is governed by a published standard. You will not read it cover to cover, but the first time someone in a design review says "that's a position tolerance at MMC referenced to datum A," you'll want to know the vocabulary is *defined*, not improvised.

- **ASME Y14.5-2018, Dimensioning and Tolerancing** — the U.S. standard most shops follow. The standard itself is paid; the overview page is free:
  <https://www.asme.org/codes-standards/find-codes-standards/y14-5-dimensioning-tolerancing>
- **ISO GPS (Geometrical Product Specification)** — the ISO equivalent used internationally; good to know it exists:
  <https://www.iso.org/committee/53330.html>

## Official OnShape docs

- **OnShape Help home** — searchable docs for every feature:
  <https://onshape-public.document360.io/docs>
- **Drawing templates** — how to pick and customize sheet templates and title blocks:
  <https://onshape-public.document360.io/docs/create-template>
- **Bill of Materials** — generating and customizing a BOM and balloons:
  <https://onshape-public.document360.io/docs/bill-of-materials>
- **Part properties** — the part number, description, and material fields that feed the title block and BOM:
  <https://onshape-public.document360.io/docs/part-properties>
- **Export** — STEP, STL, DXF, DWG, PDF, and Parasolid out of OnShape:
  <https://onshape-public.document360.io/docs/export>

## GD&T learning, free

- **GD&T Basics (full free library)** — symbol-by-symbol explanations with examples; the best free GD&T resource online:
  <https://www.gdandtbasics.com/>
- **Engineering Essentials: GD&T overview** — a concise written primer if you prefer one long page:
  <https://www.machinedesign.com/learning-resources>
- **"GD&T Tips"** — short reference cards on common controls (flatness, position, profile):
  <https://www.gdandtbasics.com/gdt-symbols/>

## Tools you'll use this week

- **OnShape (browser)** — Part Studio, Assembly, Drawing tabs, Variable Studio, Configurations. Nothing to install; works in any modern browser. Sign in at <https://www.onshape.com/>.
- **A PDF viewer** — to check your exported drawing renders correctly outside OnShape (any browser does this).
- **A STEP/STL viewer (optional)** — to confirm exports. OnShape can re-import its own exports; <https://3dviewer.net/> is a free browser-based viewer if you want a second opinion.

## Videos (free, no signup)

- **OnShape's official YouTube channel** — short "tech tips" on drawings, configurations, and GD&T:
  <https://www.youtube.com/@Onshape>
- **"Onshape Tech Tips — Drawings"** — search that phrase on the channel above; the tip videos are 2–6 minutes each and surgical.
- **OnShape webinars (on-demand)** — longer recorded sessions, including configuration and drawing deep-dives:
  <https://www.onshape.com/en/resources/webinars>

## Public documents to study this week

You learn more from one hour reading a well-built public OnShape document than from three hours of tutorials. Browse the public document search and open a few that include a Drawing tab and a Configurations tab:

- **OnShape public document search** — filter for documents with drawings:
  <https://cad.onshape.com/documents?resourceType=filter&showCommonDocuments=false&q=drawing>
- Open a document, look at its **Drawing tab**, then double-click a dimension to see whether it's associative. Open its **Variable Studio** or **Configurations** tab if it has one and trace how a dimension is driven.

## Standards & symbols cheat sheet

Keep this open in a tab while you place feature control frames.

| Symbol / term | Plain English |
|---------------|---------------|
| **Datum (A, B, C)** | A theoretical reference (plane, axis, or point) that everything else is measured from. |
| **DRF** | Datum Reference Frame — the A-then-B-then-C ordered set of datums that locks all 6 degrees of freedom. |
| **FCF** | Feature Control Frame — the boxed callout: symbol \| tolerance value \| datum references. |
| **Basic dimension** | A theoretically exact location (boxed number) with no tolerance of its own; tolerance comes from a related FCF. |
| **Flatness** | How much a single surface may deviate from a perfect plane. A *form* control — no datum needed. |
| **Position** | How far a feature's axis/center may stray from its true (basic) location. References datums. |
| **Perpendicularity** | How much a feature may tilt away from 90° to a datum. |
| **MMC / LMC** | Maximum / Least Material Condition — the modifier that lets position tolerance grow as a hole gets bigger (or smaller). |
| **Associative dimension** | A drawing dimension whose value is read from the model; it updates when the model changes. |
| **Overridden dimension** | A dimension whose displayed value was typed by hand; it no longer tracks the model. Avoid. |
| **Configuration input** | The control (list, variable, or checkbox) that drives a part into different configurations. |
| **Variable Studio** | A tab holding named `#variables` that any sketch or feature in the document can reference. |
| **BOM** | Bill of Materials — the auto-generated parts table (item, qty, part number, description). |
| **STEP (AP242)** | The neutral CAD exchange format shops want for machining; can carry PMI (dimensions/tolerances). |
| **STL** | A mesh of triangles with no dimensions — what a 3D printer/slicer wants, never a machinist. |

---

*If a link 404s, please open an issue so we can replace it. OnShape occasionally reorganizes its Help URLs; search the Learning Center if a deep link moves.*
