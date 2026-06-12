# Lecture 2 — Shipping a CAD Deliverable: Versions, Releases, Export Formats, and the Drawing Package

> **Reading time:** ~70 minutes. **Hands-on time:** ~50 minutes (you tag a Version, build a drawing sheet with a BOM, and export a STEP and an STL of your capstone).

C12 has said it since Week 01: *a model that lives only in your head, or only at "current state" in a Document that anyone can change, is not a deliverable*. This is the lecture that cashes that promise. The deliverable is the artifact a downstream person — a machinist, a print-shop operator, another CAD engineer, a teammate who picks up your file in six months — actually consumes. By the end of this lecture you can take your articulating mechanism and *ship* it: tag an immutable Version so "the released design" means one exact thing forever, produce a drawing package a machinist can build from, and export the right neutral format for each downstream consumer. You will also understand the design review as the gate the deliverable passes through, which is the framing that makes you a designer people trust with real parts.

## 2.1 — Why a release, and why now

People hear "release" and think it is bureaucracy. It is not. You tag a release for three reasons, none of which is paperwork:

1. **"The design" must mean one exact thing.** Your OnShape Document has a *current* state that anyone with edit access — including future-you at 2am — can change. If your drawing, your STEP file, your video, and your teammate's downstream part all say "I used the gripper design" but the Document has moved on since, they each refer to a *different* gripper. An immutable **Version** is a frozen snapshot: "Released v1.0" is the same geometry today, next month, and after you have made forty more edits on a branch. Without it, "the design" is a moving target and nobody can reproduce your result.

2. **Downstream artifacts must reference a fixed point.** The drawing you hand the machinist, the STEP you hand the other CAD team, the STL you hand the print shop — all of them must be generated from *the same* frozen Version, or they disagree with each other. A release is the single source the whole deliverable package hangs off.

3. **It proves the model is finished and reproducible.** This is the reason that matters for *you*, this week. A capstone you can tag, export, and hand off is a capstone someone else can build. A capstone that exists only as "whatever's in the Document right now" is a capstone you are afraid to touch. The grader opens a *specific Version* and expects the geometry, the drawings, and the exports to all agree.

The honesty rule is absolute: a "release" that is really just "the current state of the Document, which I'll probably keep editing" is not a release. The real release for the capstone is an immutable Version named `v1.0`, with the drawing PDF, the STEP, and the STL all generated from *that* Version, and the value of the release is that every downstream artifact provably came from one frozen design.

## 2.2 — Versions, history, and branches: the version graph

OnShape's version control is built into the Document, and the capstone is where you finally use it for real. Three concepts:

- **The edit history** is the continuous, automatic record of every change. It is *not* a release — it is the undo timeline. You can roll back to any point, but it is mutable and granular; it is not what you hand someone.
- **A Version** is an *immutable, named snapshot* you create deliberately (Insert → Create Version, or the version-graph "+"). Once created it never changes. `Released v1.0` is a Version. This is the unit of release.
- **A Branch** lets you keep working past a Version without disturbing it. You tag `v1.0`, then branch to keep iterating toward `v1.1` while `v1.0` stays frozen for the people consuming it. This is exactly the software pattern — tag a release, branch for the next one — applied to CAD.

The capstone workflow is: build the mechanism, get it clean (drags through range, rebuilds parametrically), then **Create Version `v1.0`**. Generate the drawing, the STEP, and the STL *from that Version*. If you find a bug after, branch, fix on the branch, and tag `v1.1` — never silently edit the released geometry out from under the artifacts that reference it. A reviewer who asks "which version is this drawing from" and hears "v1.0, same as the STEP and the video" knows you understand release discipline. One who hears "uh, the current one, I think" does not.

A subtle but important rule: a **Drawing references the Version (or the current state) of the part it documents.** If you make the drawing point at `v1.0`, it shows `v1.0` geometry forever, even as you keep editing. If you make it point at the live state, it updates as you edit — convenient while iterating, dangerous at release time, because the released drawing must show the released geometry. At release, lock the drawing to the Version.

## 2.3 — The drawing package: what a machinist actually needs

A drawing is not a pretty picture of your part. It is a *specification* — the legally and practically binding description of what to make, complete enough that a machinist who has never spoken to you can build the part and an inspector can check it. The capstone drawing package has three parts, and each answers a specific downstream question.

### The assembly drawing (answers "how do the parts go together")

One sheet showing the whole mechanism, typically an isometric or an exploded view, with:

- **Balloons** — numbered bubbles pointing at each unique part.
- **A bill of materials (BOM)** — the table keyed to the balloons: item number, part name/number, quantity, material, description. OnShape auto-generates this from the assembly and keeps it in sync with the balloons.
- **The overall envelope dimensions** — how big the whole thing is, so a downstream consumer knows if it fits their space.

The assembly drawing answers the integration question. A reviewer reads the balloon-and-BOM to understand the part count and structure at a glance.

### The key part drawings (answer "how do I make this one part")

One sheet per critical part, each with:

- **Orthographic views** — the standard front/top/right (or whatever set fully describes the part), in a declared projection convention (third-angle in the US, first-angle in much of Europe — your title block must say which).
- **A section view** — at least one, cutting through the part to dimension internal features (a bore, a counterbore, a pocket) that no external view can show. The capstone requires at least one section view; the bore through a hub or the internal step of a slider is the natural candidate.
- **Full dimensioning** — every dimension a machinist needs, no more and no fewer. A part that is missing one dimension cannot be made; a part with redundant dimensions invites contradiction.
- **Tolerances on the critical dimensions** — the dimensions that control *fit* must be toleranced (more in §2.4).
- **At least one GD&T frame** — a feature control frame referencing a datum, controlling something the dimensions alone cannot (position of a hole pattern, flatness of a mating face). The capstone requires one; §2.5 walks it.

### The title block (answers "what is this, who made it, can I trust it")

Every sheet carries a title block: part name, part number, material, units, scale, projection convention, the designer, the date, and the *version/revision*. The revision tie-back is what connects the printed drawing to the frozen `v1.0` Version — so a drawing in someone's hand is provably the released design, not a draft.

## 2.4 — Tolerances and fits: the dimensions that make it actually assemble

The single most common drawing failure is dimensions without tolerances on the features that *fit*. A nominal "6mm pin into a 6mm hole" is meaningless — made exactly, the pin will not go in; made loose, it rattles. The drawing has to say *how much* slop is allowed, and the answer determines whether your mechanism's joints work.

The vocabulary, from Week 05, applied to the capstone's pins and holes:

- **Clearance fit** — the hole is always larger than the pin, so it always slides. This is what a *Revolute joint* wants: a 6mm pin in a 6.2mm hole has 0.2mm diametral clearance and rotates freely. You write this as a hole tolerance like `⌀6.2 +0.1/−0.0` and a pin tolerance like `⌀6.0 +0.0/−0.1`.
- **Interference fit** — the pin is larger than the hole, so it must be pressed in and stays put. This is what a *Fastened* press-fit pin wants.
- **Transition fit** — somewhere between, used for locating features that must be precise but removable.

For a 3D-printed capstone there is a process reality that goes on the drawing as a note: **FDM holes shrink and FDM pins swell** by a few tenths of a millimeter, so a joint that is a perfect clearance fit in the nominal CAD jams when printed. The competent move is to *design in extra clearance* — make the printed Revolute holes 0.3–0.4mm larger than the pin — and to *say so on the drawing* as a note: "Holes sized for FDM; ream to nominal if machined." A reviewer who asks "this pin in this hole — what's the fit, and does it survive your process" wants exactly this answer: the diametral clearance as a number, and the process note that protects it.

The discipline: **tolerance the dimensions that fit, leave the rest at the default block tolerance, and never tolerance a cosmetic dimension.** A drawing where every dimension has a tight tolerance is as broken as one with none — it tells the machinist nothing about what actually matters and triples the inspection cost. Tolerance the joints; default the rest.

## 2.5 — The one GD&T frame, done right

GD&T (geometric dimensioning and tolerancing, ASME Y14.5) controls things plus/minus dimensions cannot: the *position* of a hole relative to a datum, the *flatness* of a mounting face, the *perpendicularity* of a bore to a face. The capstone requires one feature control frame, and the natural one is **true position on the joint hole pattern**, because the *position* of your pivot holes is what makes the mechanism assemble.

The frame reads as a stack of boxes: the symbol (a crosshair for position), the tolerance zone (a diameter, e.g. `⌀0.2`), and the datum references (A, B, C — the faces and features the position is measured from). In plain language, "the center of this hole must lie within a 0.2mm-diameter cylinder located true to datums A and B." That is a far more honest control than `±0.1` in X and `±0.1` in Y, because it gives a round tolerance zone instead of a square one and ties the position to real datum features.

To place it in an OnShape drawing: select the hole's dimension or edge, add the geometric-tolerance symbol from the drawing toolbar, choose **Position**, enter the zone diameter, and reference your datums (which you place as datum-feature symbols on the relevant faces first). The reviewer who asks "why a position frame and not just plus-minus" wants to hear: "because the *pattern* of pivot holes has to line up for the linkage to assemble, and position-to-datum controls the pattern as a unit, which is what actually matters for the fit." Naming *why* the GD&T frame is the right control — not just *that* you placed one — is the senior answer.

## 2.6 — STEP vs STL: which neutral format answers which question

You export so a downstream consumer who does not use OnShape can use your design. There are two neutral formats that matter for the capstone, and they answer *different* questions. Choosing wrong is a real error a reviewer will catch.

| Format | What it carries | What it loses | Who consumes it |
|---|---|---|---|
| **STEP (ISO 10303)** | Exact boundary-representation (B-rep) solids — true curved surfaces, edges, and **assembly structure** (the parts and how they nest). | The *parametric history* — the feature tree, the sketches, the variables. A STEP is "dumb solids," geometrically exact but not editable as features. | Another CAD engineer, a CNC/CAM programmer, anyone who needs precise geometry in a different CAD package (SolidWorks, Fusion, Creo). |
| **STL** | A *triangle mesh* approximation of the surface — no curves, just facets. One solid body, no assembly structure, no units guaranteed. | Curves (everything is faceted), assembly structure, history, and precision (it is an approximation tuned by a chord-tolerance setting). | A 3D printer / slicer, a mesh tool, anything that just needs the outer shape to manufacture or visualize. |

The capstone asks for **both**, deliberately, because they prove different things:

- **STEP of the assembly** is the "hand this to another engineer" deliverable. It carries the structure, so the recipient sees the same parts you do, and the geometry is exact. This is the right format when the question is "can someone continue the engineering."
- **STL of a printable part** is the "make this real" deliverable. It is the format a slicer ingests to produce a 3D print. This is the right format when the question is "can someone manufacture it."

Two STL pitfalls a reviewer probes. First, **resolution**: STL approximates curves with triangles, and the *chord tolerance / angle* setting controls how finely. Export too coarse and a cylinder looks like a hexagonal prism; export absurdly fine and the file is gigabytes for no benefit. The competent setting is "fine enough that the facets are invisible at the print's layer height" — for a hobby FDM print, a chord tolerance around 0.05mm. Second, **units**: STL carries no guaranteed unit, so a part modeled in millimeters can import as inches and print 25.4× too big. Export from OnShape with units set explicitly and confirm the bounding box on import. A reviewer who asks "what resolution did you export, and how do you know the units survived" wants exactly these two answers.

A third format worth naming (a stretch deliverable): **3MF**, the modern successor to STL, which carries units, color, and metadata that STL drops — if your print toolchain accepts it, it is strictly better than STL for the print handoff.

## 2.7 — The export sanity check: never ship an export you didn't open

The most embarrassing way to fail the handoff is to export a file that is broken — a STEP with a missing part, an STL at the wrong scale or with inverted normals — and never notice because you never opened it. The discipline is simple and absolute: **open every export in a neutral viewer before you call it shipped.**

The sanity check:

1. Export the STEP of the assembly and the STL of the printable part *from the tagged Version*, not from the live state.
2. Open the STEP in a viewer that is *not* OnShape — [3dviewer.net](https://3dviewer.net/) in a browser is free and immediate, or another CAD package if you have one. Confirm: all the parts are present, they are in the right relative positions, and nothing imported as a hollow shell or a degenerate body.
3. Open the STL in your slicer (or the same viewer). Confirm: the bounding box dimensions match what you expect *in millimeters* (this catches the units bug), the mesh is watertight (no holes a slicer would choke on), and the facets are fine enough that curves look curved.
4. If anything is wrong, fix it *before* the export is part of the deliverable. A STEP that opens missing a part, or an STL that imports at 25.4× scale, is a failed handoff even if the OnShape model is perfect.

This is the CAD equivalent of "read the file you wrote before you call it done." The grader opens your exports; if they are broken, the capstone does not pass, regardless of how good the live model is.

## 2.8 — The design review as the gate the deliverable passes through

Step back from the files. Everything above — the Version, the drawing, the exports — exists to pass through one gate: the **design review**, where a senior designer decides whether your deliverable is trustworthy. Lecture 1 covered how the review *runs* and the question bank; here we connect the *shipping artifacts* to the review, because the review is where they earn their keep.

The reviewer reads your packet (§1.2) and probes whether the deliverable is real:

- **"Which Version is this?"** — tests release discipline. The answer is "v1.0, and the drawing, STEP, and STL all came from it." A deliverable where the artifacts came from different states of the Document is internally inconsistent and the reviewer will find the disagreement.
- **"Could a machinist build the slider from this drawing alone, with no other information?"** — tests the drawing package. They will look for a missing dimension, an untoleranced fit, a section view that does not actually section the feature that needs it.
- **"Show me you opened the STL."** — tests the export sanity check. "Here it is in the slicer, bounding box is 84 × 40 × 22 mm, watertight" is the answer; "I exported it" without having opened it is the failure.
- **"What's the revision plan?"** — tests whether you understand that a deliverable lives past v1.0. "I branch for v1.1, the released v1.0 stays frozen for anyone consuming it" is the answer.

The deliverable is not "the model looks good." The deliverable is "a frozen Version, a drawing a machinist can build from, exports that open clean, and a designer who can defend every one of those in the review." The shipping artifacts are how the abstract "I built a mechanism" becomes a concrete "here is the thing, anyone can build it, and I can prove it's the released design."

## 2.9 — A worked review exchange: the release-and-export question

Here is how the shipping conversation sounds in the review, reconstructed and edited.

> **R:** This drawing — is it the same design as the STEP you sent me, or have you edited since?
>
> **Student:** Same design, guaranteed. I tagged Version v1.0 when the mechanism was clean — drags through its range, rebuilds parametrically. The drawing is locked to v1.0, the STEP was exported from v1.0, the STL was exported from v1.0, and the video was recorded against v1.0. I've kept working since, but that's on a `v1.1` branch — the released geometry hasn't moved. So everything you're holding is provably the same frozen design.
>
> **R:** Good. Now this slider drawing — could I hand it to a machine shop and get the part back, with no calls to you?
>
> **Student:** Yes, with one honest caveat. The external geometry is fully dimensioned and there's a section view through the bore because you can't dimension that internal step from outside. The bore-to-pin fit is toleranced — the bore is `⌀6.2 +0.1/−0.0` for a clearance fit on a 6mm pin, about 0.2mm of play, which is what the Revolute joint needs. The caveat is the note: I designed this for FDM, so the holes are 0.3mm oversize for print shrinkage. If a shop machines it instead, that note says ream to nominal. So the drawing is build-ready for *either* process because it says which is which.
>
> **R:** And the STL — did you actually open it, or just export it?
>
> **Student:** Opened it. *(pulls up the slicer)* Here it is in the slicer, not in OnShape. Bounding box is 84 by 40 by 22 millimeters, which matches the model, so the units survived the export. It's watertight — no mesh errors the slicer flags. I exported at a 0.05mm chord tolerance so the pin bore looks round, not faceted. It's print-ready.

That answer wins because it ties every artifact back to one frozen Version, proves the drawing is build-ready *and* names its one honest caveat, and demonstrates the export was actually opened and checked rather than blindly produced. It is release discipline made conversational.

## 2.10 — The deliverable conversation you'll have for the rest of your career

Step fully back from the capstone. The skill you just built — taking a design from "it works on my screen" to "here is a frozen, documented, exportable deliverable anyone can consume" — is one of the highest-value things a CAD professional does, and almost nobody does it well early. The two failure modes are everywhere:

- **The artist who never ships.** Models something beautiful, keeps tweaking it forever, never tags a Version, never produces a drawing, and when asked for "the file" sends whatever the Document happens to contain that day. Their work cannot be built by anyone but them, which means it cannot be built at all in a real shop.
- **The exporter who never checks.** Dumps a STEP and an STL the moment the model looks done, never opens them, and discovers in a meeting (or worse, after the print fails) that the STL was at the wrong scale or the STEP dropped a body. They confused "I clicked export" with "I delivered a working file."

The right posture is the one this lecture has modeled: **freeze the design as a Version, document it so a stranger can build it, export the right format for each consumer, open every export to confirm it's real, and defend the whole package in the review.** A drawing is worth making *because* a machinist can build from it; a STEP is worth exporting *because* another engineer can continue from it; an STL is worth exporting *because* a printer can make it real — and you can say all of that, with the fit tolerances and the export settings as numbers, now. That is what it means to ship a CAD deliverable.

## 2.11 — Building the BOM so it survives a configuration change

The bill of materials is the part of the drawing package students treat as an afterthought and reviewers treat as a tell, because a clean, accurate, balloon-linked BOM proves the assembly is *structured*, not just modeled. OnShape auto-generates the BOM from the assembly, but "auto-generated" does not mean "correct by magic" — it means the BOM is exactly as good as the metadata you put on your parts.

The metadata that flows into the BOM lives on each part: the **part number**, the **part name**, the **description**, and the **material**. If you never set these, your BOM reads "Part 1, Part 2, Part 3" — useless to a downstream reader. Set them deliberately, in each part's Properties, *before* you generate the BOM:

- **Part number** — a real identifier (`CRANK-01`, `ROD-01`), not a default. This is what a balloon points at and what a purchaser orders by.
- **Name and description** — human-readable (`Crank, 12mm radius`, `Connecting rod`).
- **Material** — the BOM's material column and, downstream, the mass calculation. Set it to the real material (PLA, aluminum 6061, etc.).
- **Quantity** — OnShape counts instances automatically; if you have four identical M3 screws, the BOM rolls them into one row with quantity 4. This only works if they are genuinely the *same* part instance, which is one more reason to model a fastener once and insert it four times rather than modeling four near-identical parts.

Now the configuration wrinkle, which is exactly the kind of thing a reviewer probes: **what does your BOM show when the configured part changes size?** If your jaw is configured Small/Medium/Large and the assembly is set to Medium, the BOM should show the Medium jaw — and a well-built BOM carries the *configuration* in the description so the row reads "Jaw, Medium (24mm)" rather than an ambiguous "Jaw." Switch the assembly to Large and the BOM row updates. A BOM that goes stale or ambiguous under a configuration change is the same fragility bug as a feature tree that goes red — it means the documentation does not track the model. The senior move is to confirm, on camera, that flipping the configuration updates both the geometry *and* the BOM row, so the drawing always describes the design it claims to.

The balloons are the BOM's other half. Each balloon on the assembly drawing points at one part and carries its BOM item number, so a reader can go from the picture to the table and back. The discipline: **every unique part gets exactly one balloon, the balloon numbers match the BOM item numbers, and no part is unballooned.** An assembly drawing with parts the BOM does not list, or BOM rows nothing points at, is internally inconsistent — and that inconsistency is precisely what a reviewer scans for first, because it reveals whether you treated the drawing as a real specification or a decoration.

## 2.12 — Section views and auxiliary views: showing what the outside hides

The mini-project requires at least one section view, and there is a reason it is mandatory rather than optional: **a great many of a real part's critical dimensions live inside it, where no external view can reach them.** A hub has a bore; a slider has an internal step; a housing has a wall thickness. You cannot dimension a bore diameter from an outside view — the bore is hidden — so you cut the part open with a section view and dimension the freshly-revealed internal geometry.

A **section view** in an OnShape drawing is made by drawing a *cutting line* across an existing view and projecting the result: OnShape slices the part along that line and shows the cut face with section hatching (the diagonal lines that mean "this is solid material the cut passed through"). The bore, the counterbore, the internal step — all now visible and dimensionable. The convention to respect: the cutting-plane line gets arrows showing the viewing direction and a label (`SECTION A-A`), and the resulting view carries the same label so a reader can connect the cut to the result.

Choose the cut to reveal the feature that needs dimensioning. For the capstone's slider with an internal rail groove, a section *along* the slide axis shows the groove's depth and width — dimensions a machinist needs and an outside view cannot give. Cutting in the wrong place produces a section view that reveals nothing useful, which is a wasted sheet. The reviewer's question — "why did you section here" — wants the answer "because the bore depth and the internal step are the dimensions a machinist can't get any other way, and this cut exposes both."

A cousin worth knowing for the stretch case is the **auxiliary view**: when a part has a face that is *not* parallel to any standard plane (an angled boss, a slanted mounting pad), its true shape and size do not appear in any orthographic view — they are foreshortened. An auxiliary view projects perpendicular to that angled face so its true dimensions appear undistorted. You will not always need one, but if your mechanism has an angled feature and you try to dimension it off a foreshortened standard view, the dimension is wrong; the auxiliary view is the fix. Naming that you *recognized* a foreshortened face and added an auxiliary view (or, honestly, that you avoided angled faces precisely to keep the drawing simple) is a mature drawing-package decision.

## 2.13 — Parasolid, DXF, and the rest of the export menu

STEP and STL cover the two consumers the capstone names — the downstream engineer and the printer — but the OnShape export menu has more, and knowing what each is *for* is the difference between a designer who hands over the right file and one who guesses. A reviewer may ask "what would you export for a laser cutter," and "I'd send a STEP" is a wrong answer that reveals you do not know the menu.

- **Parasolid (`.x_t`)** — OnShape's *native* geometry kernel format (OnShape, SolidWorks, NX, and others all run on Parasolid). It carries exact B-rep solids with the highest fidelity of any neutral-ish format, because there is no kernel-to-kernel translation loss. If the recipient runs a Parasolid-based CAD package, Parasolid beats STEP. STEP is the more *universal* choice; Parasolid is the *higher-fidelity* one. Know both exist and when each wins.
- **DXF / DWG** — *2D* formats. You export a DXF of a flat profile (a sheet-metal flat pattern, a laser-cut or waterjet outline, a gasket) so a 2D fabrication machine can cut it. This is the right answer to "what does the laser cutter want" — a flat 2D outline, not a 3D solid. If your capstone has a flat plate that would be laser-cut rather than printed, a DXF of its profile is the correct export for that part.
- **3MF** — the modern mesh format (named in §2.6) that fixes STL's units-and-metadata gaps; the better print-handoff format when the slicer supports it.
- **IGES (`.igs`)** — an older neutral format, largely superseded by STEP. You will meet it in legacy workflows; default to STEP unless a recipient specifically asks for IGES.
- **PDF** — how you ship the *drawing*, not the model. The drawing PDF is what a machinist prints and marks up at the machine. The capstone's drawing package is delivered as a PDF (or a set of them), generated from the tagged Version.

The principle behind the whole menu: **match the format to what the consumer's tool ingests, and to whether they need editable geometry, exact-but-dumb geometry, a mesh, or a flat 2D profile.** A 3D printer eats a mesh (STL/3MF). A laser cutter eats a 2D profile (DXF). Another CAD engineer eats exact solids (STEP/Parasolid). A machinist at a manual machine eats a drawing (PDF). Hand each the format their tool reads, and the handoff works the first time.

## 2.14 — The release checklist: what "done" actually means

It helps to make "done" concrete, because "the model looks finished" is not a definition anyone can grade. Here is the release checklist the capstone is, in effect, asking you to satisfy — the CAD analog of a deployment checklist. Run it before you tag `v1.0`, and run it again on Saturday as the grader will:

1. **The mechanism is clean.** It drags through its full range, has exactly the intended DOF, no red over-constraint warnings, and zero interferences across the sweep (home, mid, both extremes), with the worst clearance measured.
2. **The parametric rebuild holds.** Changing the key driving variable within its documented range rebuilds the whole assembly with zero red errors and the mechanism still moves. Every configuration of the configured part rebuilds and still articulates.
3. **The feature trees read as build sequences.** Features are renamed with intent, not left as `Sketch 7 / Extrude 4`. A reviewer can read the tree and understand the design.
4. **The drawing package is build-ready.** Assembly drawing with balloons and a BOM whose metadata is real; at least one part drawing with orthographic + section views, full dimensioning, tolerances on the fits, and one GD&T frame; every sheet's title block declaring units, scale, projection, designer, and the revision tied to the Version.
5. **The Version is tagged.** `v1.0` is frozen, and the drawing, STEP, and STL all reference it. Further work is on a branch.
6. **The exports are real.** STEP and STL exported from `v1.0`, and *both opened in a neutral viewer* — STEP shows all parts in place, STL is watertight and at the correct mm bounding box.
7. **The walkthrough is honest.** It names the mechanism, the motion, each mate and its DOF, the mobility-equation count, and a "known limitations" section that states the variable's valid range and any bounded robustness — the self-named risks from Lecture 1, §1.8.

Every item is binary: it passes or it does not. A capstone that satisfies all seven is shippable; one that satisfies six is not yet done, and the missing one is the first thing the reviewer will find. The checklist is not bureaucracy — it is the operational definition of "done" that lets you, and the grader, agree on whether the work is finished without arguing about taste.

## 2.15 — The 5-minute video: the deliverable that travels without you

The last shipping artifact is the one that reaches the widest audience: the 5-minute video walkthrough. The drawing is read by a machinist, the STEP by one engineer, the live model by a reviewer in the room — but the *video* is what a hiring manager watches months later, alone, with no chance to ask you a question. It has to stand on its own.

The structure that works mirrors the review agenda (§ Lecture 1, 1.3), compressed to five minutes:

- **0:00–0:30 — What it is and what it does.** One sentence of purpose, one of the motion. "This is a slider-crank gripper; one 90-degree crank rotation closes the jaw 24 millimeters." Show the assembled mechanism. Do not start with the feature tree; start with the thing moving.
- **0:30–2:00 — Drag the motion.** Grab the input and move it through the full range, narrating the mate at each joint. This is the heart; it is the same drag you rehearsed for the live review (Lecture 1, §1.10).
- **2:00–3:00 — One design decision, in depth.** Pick the most interesting tradeoff — the joint clearance, the Grashof choice, the configuration — and explain it with a number. This is where you show you *understand* the design, not just that it moves.
- **3:00–4:00 — The parametric rebuild.** Change the driving variable on camera, show the clean regen, show the mechanism still moving. This is the proof that reads as engineering rather than sculpting.
- **4:00–5:00 — The deliverable and a known limitation.** Show the drawing and the export briefly, and *name one honest limitation* ("the clearance is only safe for crank radius 10–16mm"). Ending on a self-named limit is the senior note; ending on "and it's perfect" is the junior one.

People read aloud at roughly 150 words a minute, so five minutes is about 750 words — which is *tight*. Script it (Homework Problem 6), read it aloud once to time it, and cut ruthlessly. The most common failure is overrunning by narrating the feature tree click-by-click; the fix is to show the *motion and the decisions*, not the modeling steps. The video is your capstone's ambassador: it is the artifact that gets watched when you are not in the room, so it is worth the half-hour of rehearsal that turns a thirty-take ordeal into one clean recording.

## 2.16 — Sharing the live Document: read-only links and what a reviewer sees

The capstone's most powerful artifact is the *live OnShape Document itself* — a reviewer or hiring manager who can open your actual model, drag it, and inspect the feature tree gets far more signal than any video or PDF. OnShape makes this a first-class action, and using it well is part of shipping.

The mechanics:

- **Share read-only, not edit.** Use the Share dialog to grant **view** (or **can comment**) access, never **edit**, to anyone outside your team. A reviewer should be able to open, orbit, drag the assembly, and read the tree — but not change your geometry. The released `v1.0` Version is immutable regardless, but you also do not want someone editing your working state.
- **Link to the Version, or to the workspace, deliberately.** You can share a link that opens the live workspace (always-current) or a link pinned to the `v1.0` Version (always-the-release). For the portfolio and the review, pin to `v1.0` so the reviewer sees exactly the released design, not whatever you happened to be editing.
- **Public vs unlisted.** On the free plan your Documents are public, which is fine and often desirable for a portfolio — a public link a hiring manager can open with no account is a feature. If you need it unlisted, that requires a paid plan; the capstone does not.

What a reviewer *does* with the link is the reason it matters: they open it, drag the mechanism themselves (the live test you cannot fake), expand the feature tree to judge whether it reads as a build sequence, click into the Mate features to confirm one mate per joint, and switch the Configuration to watch the rebuild. Everything Lecture 1's question bank probes, a reviewer can now check directly. This is why the feature-tree hygiene (§2.14, item 3) and the clean mate scheme (Lecture 1, §1.15) are not cosmetic — when you hand over a live link, the *inside* of your model is on display, not just the rendered outside. A tidy, well-named, cleanly-constrained Document is itself a deliverable.

## 2.17 — Why the shipping discipline outlives the capstone

Two of the failure modes in §2.10 are worth turning into a positive habit you carry forward, because the shipping discipline is the part of CAD that separates a hobbyist from a professional, and it generalizes far past this one mechanism:

1. **Freeze before you hand off.** Any time someone downstream depends on your geometry — a teammate, a print shop, a manufacturer — tag a Version first, so "the file I sent you" is a frozen, nameable thing and not a moving target. This is the single habit that prevents the most expensive class of CAD mistake: a part made to a drawing that no longer matches the model because the model kept changing.
2. **Open every export.** The thirty seconds it takes to open a STEP or an STL in a viewer is the cheapest insurance in engineering. A failed handoff — a part printed at 25.4× scale, a STEP missing a body — costs hours or days downstream and is entirely preventable by the person who exported it actually looking at what they exported.
3. **Document for a stranger, not for yourself.** Your walkthrough, your drawing, your BOM are read by people who were not in your head when you designed. The test is always "could someone who has never spoken to me build this and understand the tradeoffs from what I shipped." If yes, you shipped a deliverable; if no, you shipped a personal project that only you can finish.

These three habits are the through-line from this lecture to a career. The capstone is where you practice them under a deadline with a reviewer watching — which is exactly the pressure that makes them stick. Ship the mechanism the way you would ship a part someone is going to manufacture, because that is the skill the whole course was building toward: not "can you model a thing," but "can you deliver a thing someone else can build and trust."

## 2.18 — The deliverable manifest

It helps to have a single checklist of *what files* ship and *where they came from*, so nothing is missing and everything traces to the frozen Version. Drop this into your Document or repo as a `DELIVERABLES.md` so the reviewer (and future-you) can see the whole package at a glance:

```markdown
# Capstone Deliverables — <Mechanism Name>  ·  Release v1.0

## Source of truth
- OnShape Document: <read-only link, pinned to Version v1.0>
- Frozen Version:    v1.0  (immutable; all artifacts below generated from it)
- Working branch:    v1.1-dev  (further edits live here; v1.0 does not move)

## Drawing package (generated from v1.0)
- [ ] assembly-drawing.pdf   — iso/exploded view, balloons, BOM, envelope dims, title block
- [ ] crank-drawing.pdf       — orthographic + section, full dims, fit tolerances, 1 GD&T frame
- [ ] jaw-drawing.pdf         — configured part; drawing notes the configuration shown

## Neutral-format exports (from v1.0, opened & verified)
- [ ] mechanism.step  — assembly, AP242, mm; opened in 3dviewer.net: all 4 parts present  [PASS]
- [ ] jaw.stl         — printable part, 0.05 mm chord, mm, binary; bbox 30x16x10 mm, watertight  [PASS]

## Narrative artifacts
- [ ] design-walkthrough.md  — motion, DOF budget, mates, robustness, known limitations
- [ ] video.mp4 (or link)    — 5-minute walkthrough: motion + one decision + one live rebuild

## Verification log
- Drag through full range:        PASS (1 DOF, no float, no red warnings)
- Interference sweep (4 positions): PASS (worst clearance 0.9 mm @ full-open)
- Parametric rebuild (#crank):     PASS within [10,16] mm, 0 errors
- Configuration rebuild (3 sizes): PASS (assembly articulates at all 3)
- Exports opened in viewer:        PASS (STEP all parts; STL watertight, correct scale)
```

Two things this manifest enforces. First, **traceability**: every artifact line says it came from `v1.0`, so there is no ambiguity about whether the drawing matches the STEP matches the STL — they all matches the same frozen design. Second, **completeness**: the reviewer (and the grader) can scan the checkboxes and immediately see if anything is missing. A manifest with an unchecked box is a deliverable that is not done; a manifest with every box checked and every artifact tracing to `v1.0` is a release.

The manifest is the last thing you write, on Friday, after the Version is tagged and the exports are verified — and it is the first thing the reviewer reads, because it tells them the shape of the whole package before they dive into any one piece. It is the table of contents for your shipped work, and a clean one signals, before they have opened a single file, that you treated this like a release rather than a homework dump.

## 2.19 — Two quick reference tables you will use all week

To close, here are the two tables you will reach for most while building the drawing package — kept compact so you can glance at them while you work.

**The title block, field by field.** Every drawing sheet carries one; a reviewer scans it first to know whether the drawing is trustworthy. The required fields and what each declares:

| Field | What it declares | Capstone value (example) |
|-------|------------------|--------------------------|
| Title / part name | what the part is | `Crank` |
| Part number | the orderable identifier | `CRANK-01` |
| Material | what it is made of | `PLA` |
| Units | the dimension system | `mm` |
| Scale | drawn-size vs real-size | `2:1` |
| Projection | first- or third-angle | `Third-angle` |
| Drawn by | the designer | `<your name>` |
| Date | when | `2026-06-12` |
| Revision | ties to the Version | `v1.0` |
| Sheet | which of how many | `1 of 1` |

The revision field is the one students forget and reviewers check, because it is the link between the paper in a machinist's hand and the frozen `v1.0` geometry. A drawing with no revision is a drawing nobody can trust to be current.

**Common pin/hole fits for a printed capstone.** The fit you put on a joint decides whether it rotates, slides, or holds fast. For an FDM mechanism, design in extra clearance on top of these nominals because printed holes shrink:

| Joint behavior | Fit class | Hole vs pin (nominal) | FDM adjustment |
|----------------|-----------|------------------------|----------------|
| Rotates freely (Revolute pin) | clearance / running | hole ~0.2 mm larger | +0.2-0.3 mm more |
| Slides (Slider rail) | clearance / sliding | rail slot ~0.2 mm larger | +0.2-0.3 mm more |
| Locates precisely, removable | transition | near-zero gap | +0.1-0.2 mm |
| Presses in, stays put (Fastened) | interference | pin larger than hole | reduce interference; FDM swells |

The rule these tables embody is the same as §2.4: **tolerance the joints that fit, default the rest, and put the process adjustment on the drawing as a note.** A reviewer who asks "what fit is this Revolute and does it survive FDM" wants a row from this table plus the note — a clearance fit with the print adjustment called out, not a bare nominal dimension. These two tables are the working reference behind a drawing package a machinist or a print shop can actually build from on the first try.

## 2.20 — A worked release sequence: Friday, step by step

To make the whole shipping discipline concrete, here is the exact sequence you run on Friday to take the mechanism from "clean on my screen Thursday night" to "released, exported, verified, and defended." It is the operational form of the §2.14 checklist, in the order you actually do it, with the OnShape action named at each step.

1. **Final clean pass (15 min).** Open the Assembly. Drag the mechanism home → both extremes → home, watching the Mate features list for any red flicker. Run **Insert → Interference Detection** at home, mid, and both extremes; record the worst clearance. Switch the configured part through every configuration and drag each. If anything is red or interferes, stop — you are not ready to tag. This is the gate, and it is binary.

2. **Verify the parametric rebuild (10 min).** Open the Variable Studio, change the key driving variable to the top of its documented range, regenerate, confirm zero errors and that the mechanism still moves; set it back. This is the property the reviewer tests hardest, so you confirm it yourself first, with your own hands, before you freeze anything.

3. **Tidy the feature trees (10 min).** Walk each Part Studio's Feature list and the Assembly's Mate list. Rename anything still called `Sketch 7` or `Mate 3` to something a stranger can read (`pivot-hole-sketch`, `crank-to-rod-revolute`). The reviewer reads these on the live link (§2.16); a tidy tree is itself a deliverable.

4. **Tag Version `v1.0` (2 min).** Version graph → **Create version** → `v1.0`, with a one-line description naming the mechanism, the DOF, and the configuration count. The instant you click create, the geometry is frozen forever — everything downstream now references this exact snapshot.

5. **Generate the drawing PDFs from `v1.0` (30 min).** Open each Drawing tab, confirm its views reference `v1.0` (not the live state), confirm the title-block revision reads `v1.0`, and **Export → PDF**. The assembly drawing and the key part drawing(s) are now paper a machinist can build from, provably tied to the frozen design.

6. **Export STEP and STL from `v1.0` (10 min).** STEP of the Assembly (AP242, mm); STL of the printable part (0.05 mm chord, mm, binary). Both from the tagged Version, not the live workspace — if you exported from the workspace and then kept editing, the files would no longer match the drawings.

7. **Open every export in a neutral viewer (10 min).** STEP into [3dviewer.net](https://3dviewer.net/): all parts present, in place, no hollow shells. STL into your slicer: bounding box correct in millimeters, watertight, curves look round. Tick the verification log. An export you have not opened is not shipped.

8. **Write the deliverable manifest (10 min).** Fill in the `DELIVERABLES.md` from §2.18 — every artifact line tracing to `v1.0`, every verification box checked. This is the table of contents the reviewer reads first.

9. **Share the read-only link pinned to `v1.0` (2 min).** Share → **can view**, link pinned to the Version, not the workspace. This is what the reviewer opens to drag the live model themselves.

10. **Deliver the review (the Friday slot).** Run the agenda from Lecture 1 §1.3: context, skeleton walk, drag one motion, failure modes, the live parametric rebuild, the cost/manufacturability questions, the risk list. You have rehearsed the drag (Lecture 1 §1.10); now you perform it.

The whole sequence is about two hours of careful, unhurried work, and the reason it is worth writing out is that the *order* matters: you tag the Version *before* you generate any artifact, so every artifact inherits the frozen geometry; you open every export *before* you call it done, so a broken file never reaches the reviewer; and you tidy the trees *before* you share the live link, so the inside of your model reads as cleanly as the outside. Do it in this order and the deliverable is internally consistent by construction — which is exactly the property the reviewer's "which version is this" question is probing for. A capstone delivered this way passes the shipping gate not because you got lucky, but because the process made it impossible for the artifacts to disagree.

## Summary

Shipping a CAD deliverable is the discipline of turning "it works on my screen" into "here is the released design, anyone can build it, and I can prove it." You tag an immutable **Version** so "the design" means one exact frozen thing, and you generate the drawing, the STEP, and the STL all *from that Version* so they agree. The **drawing package** is a specification, not a picture: an assembly drawing with a balloon-and-BOM, key part drawings with orthographic and section views, full dimensioning, tolerances on the features that *fit*, and at least one GD&T frame controlling the thing plus-minus cannot. You tolerance the joints and default the rest, and for an FDM capstone you design in clearance and note the process. You export **STEP** for the engineer (exact B-rep, assembly structure) and **STL** for the printer (a mesh approximation, watch the resolution and the units), and you **open every export** in a neutral viewer before calling it shipped. The whole package passes through the design review, where a senior designer tests whether it is real — which Version, can a machinist build it, did you open the STL, what's the revision plan. Freeze it, document it, export it, check it, defend it. That is the capstone. That is C12.
