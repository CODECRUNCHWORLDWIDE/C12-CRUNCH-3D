# Week 4 — Resources

Every resource on this page is **free**. OnShape's Learning Center is free with the same account you use to model. The documentation site is public. The community forum is open. You do not need a paid OnShape plan to complete C12 — the free **OnShape for Makers / educational** plan covers everything this week needs (assemblies, mates, the Standard Content library, interference detection are all in the free tier; the only catch is that free-plan Documents are public).

## Required reading (work it into your week)

- **OnShape Learning Center — Introduction to Assemblies** — the canonical guided path; do its in-app exercises, not just the videos:
  <https://learn.onshape.com/>
- **Mates (help docs)** — the reference page for every mate type, with the DOF each removes:
  <https://cad.onshape.com/help/Content/mate.htm>
- **Mate connectors (help docs)** — implicit vs explicit connectors, the triad, re-orienting:
  <https://cad.onshape.com/help/Content/mateconnector.htm>
- **Degrees of freedom & the assembly workflow** — OnShape's own overview of how mates constrain motion:
  <https://cad.onshape.com/help/Content/assembly.htm>
- **Standard Content / inserting fasteners** — pulling bolts, nuts, washers from the library:
  <https://cad.onshape.com/help/Content/standardcontent.htm>

## The mate-type reference (keep open in a tab)

You will look these up constantly until they're memorized. The help docs split them by page, but this is the set you need this week:

- **Fastened mate**: <https://cad.onshape.com/help/Content/fastened_mate.htm>
- **Revolute mate**: <https://cad.onshape.com/help/Content/revolute_mate.htm>
- **Slider mate**: <https://cad.onshape.com/help/Content/slider_mate.htm>
- **Cylindrical mate**: <https://cad.onshape.com/help/Content/cylindrical_mate.htm>
- **Planar mate**: <https://cad.onshape.com/help/Content/planar_mate.htm>
- **Ball mate**: <https://cad.onshape.com/help/Content/ball_mate.htm>
- **Pin-slot mate**: <https://cad.onshape.com/help/Content/pinslot_mate.htm>
- **Mate connectors & relations (gear, screw, tangent)**: <https://cad.onshape.com/help/Content/mate_relations.htm>

## Validation tools

- **Interference detection** — find clashing solids in an assembly:
  <https://cad.onshape.com/help/Content/interferencedetection.htm>
- **Measure tool** — clearances, distances, angles between assembly entities:
  <https://cad.onshape.com/help/Content/measure.htm>
- **Assembly performance & display** — flexible sub-assemblies, mate limits, replicate:
  <https://cad.onshape.com/help/Content/assembly.htm>

## Official OnShape resources

- **OnShape Help home** — searchable, version-current docs:
  <https://cad.onshape.com/help/>
- **OnShape Learning Center** — free courses, learning paths, and "Onshape Fundamentals" certification:
  <https://learn.onshape.com/>
- **OnShape Community forum** — ask a real question, get a real answer, usually within a day:
  <https://forum.onshape.com/>
- **What's new in OnShape** — OnShape ships updates every ~3 weeks; the release notes tell you what changed:
  <https://cad.onshape.com/help/Content/Primary_Whats_New.htm>

## Standards & engineering background (skim, don't memorize)

A mechanism that moves is a kinematics problem. You don't need a degree, but two ideas pay off all week:

- **Degrees of freedom & Gruebler/Kutzbach (planar mechanisms)** — why a 4-bar linkage has exactly 1 DOF. A practical primer:
  <https://en.wikipedia.org/wiki/Chebychev%E2%80%93Gr%C3%BCbler%E2%80%93Kutzbach_criterion>
- **Four-bar linkage** — the canonical 1-DOF mechanism you'll build in the challenge:
  <https://en.wikipedia.org/wiki/Four-bar_linkage>
- **ISO metric screw thread / fastener sizing** — so the bolt you pull from the library is the right one:
  <https://en.wikipedia.org/wiki/ISO_metric_screw_thread>

## Video (free, no signup)

- **OnShape's official YouTube channel** — short, current, version-accurate tutorials; search "assemblies" and "mates":
  <https://www.youtube.com/@Onshape>
- **"Onshape Tech Tips"** playlist — bite-size feature walkthroughs from the OnShape team:
  <https://www.youtube.com/@Onshape/playlists>

## Public Documents to study this week

You learn assemblies faster by **opening someone else's working mechanism, expanding its Mate features list, and reading what they did** than by watching another tutorial. Use the OnShape **Public** search (top bar → Public) and look for assemblies you can open read-only:

- Search **"4 bar linkage"** — dozens of public examples; open one, expand Mates, drag it, see the single DOF.
- Search **"hinge"** or **"box hinge"** — the simplest revolute case, done many ways.
- Search **"gripper"** or **"scissor lift"** — the kind of multi-mate mechanism your Week 6 capstone will resemble.

> **How to learn from a public Document:** open it, switch to the Assembly tab, expand the **Mate features** list in the left panel, and click each mate to see which entities it connects. Then grab a part and drag. Reading three good assemblies this way is worth an hour of video.

## Tools you'll use this week

- **OnShape (browser)** — Chrome, Edge, Safari, or Firefox; no install. The iPad/Android apps work too but mating is far easier with a mouse.
- **A three-button mouse (or trackpad with modifiers)** — rotate/pan/zoom and mate-connector picking are much faster with a real middle button.
- **OnShape mobile app (optional)** — handy for drag-testing an assembly on your phone to show someone it moves.

## Glossary cheat sheet

Keep this open in a tab.

| Term | Plain English |
|------|---------------|
| **Assembly** | A Document tab where separate parts/sub-assemblies are positioned and **mated**. Distinct from a Part Studio. |
| **Instance** | One placed copy of a part or sub-assembly in an assembly. The same part can appear as many instances. |
| **Degree of freedom (DOF)** | An independent way a part can still move. A free rigid body has 6 (3 translate + 3 rotate). |
| **Mate** | A constraint between two parts that removes some DOF. Not glue — a relationship that defines motion. |
| **Mate connector** | A coordinate frame (origin + X/Y/Z) on a part that a mate attaches to. Mates connect connector-to-connector. |
| **Fastened mate** | Removes all 6 DOF. Two parts locked rigid relative to each other. |
| **Revolute mate** | Leaves 1 rotational DOF. A hinge. |
| **Slider mate** | Leaves 1 translational DOF. A drawer rail. |
| **Cylindrical mate** | Leaves 1 rotation + 1 translation about the same axis. A shaft that can spin and slide. |
| **Planar mate** | Leaves 2 translations + 1 rotation in a plane. A puck on a table. |
| **Ball mate** | Leaves 3 rotations, 0 translations. A ball joint. |
| **Pin-slot mate** | Leaves 1 rotation + 1 translation, but the two are decoupled (independent). |
| **Fix / ground** | Lock a part to the assembly origin so it cannot move. Every assembly needs one. |
| **Sub-assembly** | An assembly inserted into another assembly as a single unit (rigid by default, can be flexible). |
| **In-context** | Editing a part's geometry inside the assembly, referencing neighboring parts. Top-down design. |
| **Standard Content** | OnShape's built-in library of off-the-shelf fasteners (bolts, nuts, washers) you insert and size. |
| **Interference** | Two solids occupying the same space — they overlap. Real parts can't do this; the check finds it. |

---

*If a link 404s, please open an issue so we can replace it. OnShape reorganizes its help URLs occasionally; if a specific page moved, search the help site for the mate-type name.*
