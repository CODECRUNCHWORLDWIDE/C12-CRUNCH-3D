# Challenge 1 — Deliver the original multi-part mechanism, live

> **Estimated time:** the capstone (the bulk of the week's 12.5 mini-project hours, plus the Friday delivery slot). **This is the assessed capstone.** No solution is provided — only acceptance criteria, because in a real shop nobody hands you the answer key.

You will deliver an **original multi-part mechanism that moves** — designed, modeled, assembled, configured, drawn, and exported with every skill you have compounded since Week 01 — **live, in your own OnShape Document**, end to end. "Live" is the operative word. The reviewer does not read your render and award points. The reviewer opens your live document, drags the mechanism through its full range of motion, changes a driving variable to force a rebuild, reads your drawings, opens your exports, and runs the design review. If any of those steps fails, the capstone does not pass, regardless of how good the writeup is.

This challenge is harder than the mini-project brief in two specific ways: (1) it must **articulate through its full range of motion without interference, live, in front of the reviewer**, and (2) it must **rebuild cleanly on demand** — the reviewer changes a key driving variable (or switches a Configuration) and the whole assembly regenerates with zero red errors and still moves.

## The mechanism

An original mechanism of **3 or more parts** that articulates via mates. Pick one (or design your own in the same spirit):

- **A parallel-jaw or slider-crank gripper** — one crank rotation closes a jaw (the worked example throughout the exercises).
- **A scissor lift** — one input collapses or extends a stacked-link platform.
- **A four-bar linkage** — a crank-rocker or a parallel-motion mechanism (e.g., a desk-lamp arm that keeps the head level).
- **A simple gear train** — two or more meshing gears coupled by a Gear mate relation, with a defined ratio.
- **A hinged enclosure with a stay** — a lid that opens and is held at an angle by a linkage.

Whatever you choose, it must have a clear **input**, a clear **output motion**, and a degrees-of-freedom budget that comes out to one driven DOF.

## Acceptance criteria (the reviewer checks every one of these)

### Live motion

- [ ] **The mechanism articulates through its full range of motion**, dragged live in the Assembly, with the intended degrees of freedom (verified: one input drives everything; nothing floats; no red over-constraint warnings).
- [ ] **Zero interferences** at home, at mid-travel, and at *both* extremes of travel — demonstrated with Interference Detection live, with the worst-case clearance stated as a measured number.
- [ ] The range of motion is stated in real units (input range in degrees or mm, output range in mm).

### Live parametric rebuild

- [ ] **Changing a key driving variable rebuilds the whole assembly with zero red errors** and the mechanism still moves. The reviewer picks the variable and the value (within your documented valid range).
- [ ] **At least one part is configured** (≥ 2 configurations via a Configurations table), and the assembly rebuilds and still articulates in every configuration.

### Drawing package

- [ ] **An assembly drawing** with an isometric or exploded view, **balloons**, and an auto-generated **BOM** (item, part, quantity, description), plus the overall envelope dimensions.
- [ ] **At least one key part drawing**: orthographic views, **at least one section view**, full dimensioning, **tolerances on the dimensions that fit** (the pin/hole joints), and **at least one GD&T frame** (a position or flatness control referencing a datum).
- [ ] Every sheet has a title block declaring units, scale, projection convention, designer, and the **version/revision** (tied to `v1.0`).

### Release & exports

- [ ] **An immutable `v1.0` Version** tagged; the drawing, STEP, and STL all generated from *that* Version.
- [ ] **A STEP** of the assembly (exact geometry + assembly structure, mm) that opens clean in a neutral viewer with all parts present.
- [ ] **An STL** of a printable part (appropriate chord tolerance, mm, watertight) that opens at the correct bounding-box scale in a neutral viewer.

### Delivery artifacts

- [ ] **A 5-minute video walkthrough** (link in the document or repo) tracing the motion through the mechanism and showing one live parametric rebuild.
- [ ] **A written design walkthrough** naming the mechanism, the motion, each mate and the DOF it controls, the mobility-equation DOF budget, and the tradeoffs / known limitations.
- [ ] **Live design review delivered** (Friday slot): you present, you drag the motion, you change a variable on camera, you answer the senior-designer questions, and you capture the risk list.

## How you are graded

This challenge maps to the **Capstone delivery** line of the assessment, plus the **mock review** and the **drawing-package** components. The single hardest gate is the **live parametric rebuild**: a model you cannot edit and regenerate on demand is not a parametric mechanism, and it does not pass. Build the rebuild discipline in from day one — every working session this week, change a driving variable and confirm the clean regen across every Configuration before you stop. The reviewer will, and a mechanism that only holds together at the one set of dimensions you happened to model is a fragile shape, not a design.

## What "open-ended" means here

There is no single right mechanism, and no single right architecture for the one you pick. Within the spec, you make and defend choices: which mechanism, which mates implement which joints, what to parameterize versus hard-code, the fit tolerances on the joints, the print orientation, the configuration family. The challenge is not to match a reference solution; it is to make defensible choices, prove them by dragging the mechanism and rebuilding it under a variable change, and explain the tradeoffs in the review. The known-limitations section of your walkthrough and the self-named risks (Lecture 1, §1.8) are where you demonstrate that you understand the choices you made — which is, in the end, the entire point of the course.
