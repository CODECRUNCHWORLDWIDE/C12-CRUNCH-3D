# Week 06 Homework

This is the last homework of C12, and it is not "more modeling drills" — it is the set of capstone deliverables that are not already covered by the mini-project build itself. Each one is a concrete artifact a hiring manager or a design reviewer will actually read or open. The full set should take about **5 hours** spread across the week. Work in your capstone OnShape Document (and a small portfolio repo or folder for the written artifacts) so each deliverable is a thing you can point to.

Each problem includes a **statement**, **deliverable**, **acceptance criteria**, a **hint**, and an **estimated time**. The rubric at the bottom is how the week is graded.

---

## Problem 1 — The kinematic skeleton + DOF budget diagram

**Statement.** Capture your mechanism's *motion* as a one-page artifact: a kinematic skeleton (links as lines, joints as points/symbols) with the input and output labeled, plus the mobility-equation calculation that proves it has exactly one driven degree of freedom. This is the artifact that proves you designed the motion, not just some parts.

**Deliverable.** `dof-budget.md` containing a Mermaid (or photographed hand-drawn) skeleton and the worked Kutzbach mobility equation.

**Acceptance criteria.**

- [ ] The skeleton shows every link and every joint, with the **input** and the **output motion** labeled.
- [ ] The mobility equation is worked out with real numbers: `M = 3(N − 1) − 2·J1 − J2`, with `N`, `J1`, `J2` stated and the result equal to **1**.
- [ ] If your mechanism is a four-bar linkage, the **Grashof** check (`S + L` vs `P + Q`) is included with the grounded inversion named.
- [ ] The diagram renders cleanly (Mermaid in GitHub, or a legible photo).

**Hint.** Reuse the skeleton you built in Exercise 1 — this is its writeup. The mobility result must match the single free DOF you left in the skeleton sketch (the input). If `M` comes out to 0 or 2, your skeleton has a design problem, not a typo. (Lecture 1, §1.6, §1.7, §1.14.)

**Estimated time.** 45 minutes.

---

## Problem 2 — The design walkthrough

**Statement.** Write `design-walkthrough.md` following the Lecture 1 template (§1.19): what the mechanism is and does, the motion (kinematics), the parts and why each is a separate part, the mates and the DOF each controls, the parametric robustness with the variable's valid range, the manufacturability and fits, and a **known-limitations** section that names your own biggest risks.

**Deliverable.** `design-walkthrough.md`, the written narrative a stranger could read to understand and defend your mechanism.

**Acceptance criteria.**

- [ ] All seven sections of the §1.19 template are present and filled — no `<placeholder>` left behind.
- [ ] The mates table lists every mate by name and the **degree of freedom** it controls.
- [ ] The robustness section states the **valid range** of the key driving variable and what breaks outside it.
- [ ] The fits section gives the pin/hole **clearance as a number** and names the process (FDM clearance note, or the machined fit).
- [ ] The known-limitations section names at least **two** honest self-identified risks (a bounded-robustness limit, a tight clearance, a joint you'd reinforce).

**Hint.** The section reviewers read first is **7 — Known limitations**. A walkthrough that names its tightest measured clearance and its variable's bounded range reads as the work of someone who measured their mechanism; one with no limitations reads as someone who didn't check or is hiding what they found. (Lecture 1, §1.8, §1.19.)

**Estimated time.** 75 minutes.

---

## Problem 3 — The interference sweep report

**Statement.** Write `interference-report.md`: run Interference Detection at home, mid-travel, and *both* extremes of travel, record whether each position interferes and the worst clearance at each (measured, not eyeballed), and identify the single worst position across the whole sweep.

**Deliverable.** `interference-report.md` with the four-position table and a screenshot of the worst position.

**Acceptance criteria.**

- [ ] A table of **four** positions (home, mid, both extremes) with interference yes/no and the measured minimum clearance at each.
- [ ] The single **worst clearance** across the sweep is identified, with the position and the parts that come closest named.
- [ ] The worst clearance is a real number ≥ **0.4 mm** (for an FDM capstone) — or, if smaller, an explicit statement of how you'd fix it.
- [ ] A screenshot or measurement capture of the worst position.

**Hint.** The worst clearance is often *not* at the obvious extreme. For the slider-crank gripper the jaws are tightest at full closure, but the rod-vs-frame clearance is often worst at a different crank angle. Sweep the whole range; the measured minimum is the one that counts. (Lecture 1, §1.11; Exercise 2, Step 7.)

**Estimated time.** 45 minutes.

---

## Problem 4 — The drawing package (assembly + key part)

**Statement.** Produce the drawing package: an **assembly drawing** with an isometric or exploded view, balloons, an auto-generated BOM, and the overall envelope dimensions; plus at least one **key part drawing** with orthographic views, at least one section view, full dimensioning, tolerances on the fits, and one GD&T frame. Export both as PDF from the tagged `v1.0` Version.

**Deliverable.** `Assembly-Drawing.pdf` and `Part-Drawing.pdf` (or one combined multi-sheet PDF), generated from `v1.0`.

**Acceptance criteria.**

- [ ] The assembly drawing has **balloons** linked to a **BOM** (item, part number, quantity, description), and every unique part is ballooned exactly once.
- [ ] The part drawing has at least one **section view** that actually reveals an internal feature (a bore, a step), labeled `SECTION A-A`.
- [ ] The **dimensions that fit** (pin/hole joints) carry tolerances; cosmetic dimensions are left at the block default.
- [ ] At least one **GD&T frame** (position or flatness) referencing a datum, with a one-sentence justification of why that control.
- [ ] Every sheet's title block declares units, scale, projection convention, designer, and the **revision tied to `v1.0`**.

**Hint.** A reviewer's real test is "could a machinist build this part from the drawing alone." Walk your own part drawing as if you'd never seen the model: is any dimension missing? Is the bore dimensioned (you need the section view for that)? Is the fit toleranced? The BOM's part metadata (part number, material) must be set in each part's Properties *before* you generate the BOM, or it reads "Part 1, Part 2." (Lecture 2, §2.3, §2.4, §2.5, §2.11, §2.12.)

**Estimated time.** 75 minutes.

---

## Problem 5 — The release + verified exports

**Statement.** Tag the immutable `v1.0` Version, export a STEP of the assembly and an STL of a printable part *from that Version*, and verify both by opening them in a neutral viewer. Then write a short `DELIVERABLES.md` manifest tying every artifact to `v1.0`.

**Deliverable.** `Mechanism.step`, `jaw.stl` (or your printable part), and a `DELIVERABLES.md` manifest (the §2.18 template) with the verification log filled in.

**Acceptance criteria.**

- [ ] A `v1.0` Version is tagged, and the drawing, STEP, and STL all reference it (further work, if any, is on a branch).
- [ ] The **STEP** opens in a neutral viewer (e.g. 3dviewer.net) with all parts present and in place.
- [ ] The **STL** opens in a slicer/viewer **watertight**, at the correct **bounding box in millimeters** (proving the units survived), with curves looking round (chord tolerance fine enough).
- [ ] `DELIVERABLES.md` lists every artifact tracing to `v1.0`, with the verification log (drag, interference sweep, rebuild, configuration sweep, exports-opened) checked.

**Hint.** Export *from the tagged Version*, not the live workspace — if you export from the workspace and keep editing, the files silently stop matching the drawings. The two STL bugs that fail this problem are the **units error** (imports 25.4× too big) and a **non-manifold mesh** (won't slice); the bounding-box and watertight checks catch both. An export you have not opened is not a deliverable. (Lecture 2, §2.6, §2.7, §2.18, §2.20.)

**Estimated time.** 45 minutes.

---

## Problem 6 — The 5-minute video script + mock-review notes

**Statement.** Two short writing tasks. (a) Write the *script* for your 5-minute video — the drag-one-motion narration from Lecture 1 §1.5, timed, following the §2.15 structure (what it is, drag the motion, one design decision, the live rebuild, one honest limitation). (b) After your mock review, write a half-page retrospective: the two questions you answered well, the one you fumbled, and what you'd say differently.

**Deliverable.** `video-script.md` and `mock-review-retro.md`.

**Acceptance criteria.**

- [ ] The video script is **timed** and stays under 5 minutes read aloud at a normal pace (~750 words).
- [ ] It narrates **one real motion** through the mechanism, naming the **mate at each joint**, and includes one **live parametric rebuild**.
- [ ] It ends on one **honest limitation**, not "and it's perfect."
- [ ] The mock-review retro names **two strengths, one fumble, and a concrete fix** for the fumble.
- [ ] Both are honest — a retro that says "I nailed everything" fails this problem.

**Hint.** People read aloud at ~150 words/minute, so 5 minutes is ~750 words — tight. Read the script out loud once and time it; the most common overrun is narrating the feature tree click-by-click. Show the *motion and the decisions*, not the modeling steps. (Lecture 1, §1.10, §1.13; Lecture 2, §2.15.)

**Estimated time.** 45 minutes.

---

## Rubric

Graded out of 100. This homework is the deliverable scaffolding for the capstone, so the weights mirror the capstone's emphasis.

| Problem | Artifact | Points | What earns full marks |
|---|---|---:|---|
| 1 | `dof-budget.md` | 15 | Labeled skeleton + worked mobility equation = 1; Grashof check if a linkage; renders cleanly. |
| 2 | `design-walkthrough.md` | 25 | All seven sections filled; mates-and-DOF table; variable valid range; fit clearance as a number; two honest limitations. |
| 3 | `interference-report.md` | 15 | Four-position table, worst clearance identified and measured ≥ 0.4 mm, worst-position screenshot. |
| 4 | drawing PDFs | 20 | Balloon-and-BOM assembly drawing; part drawing with section view, toleranced fits, one justified GD&T frame, revision tied to v1.0. |
| 5 | release + exports | 15 | `v1.0` tagged; STEP all parts; STL watertight + correct mm bounding box; manifest traces every artifact to v1.0. |
| 6 | video script + retro | 10 | Timed <5-min script narrating one motion + one live rebuild + one limitation; honest mock-review retro. |

**Passing the week** requires ≥70 on this rubric *and* a capstone that articulates and rebuilds on demand (the mini-project / Challenge 1 gate). The two are scored together; a perfect homework with a mechanism that throws a red error when a driving variable changes does not pass.

**Deductions.** Any sketch or part left **under-defined (blue)** in the released model: −10 and a required fix (a fragile model is the equivalent of a leaked resource). Any **export you ship without opening it** that turns out broken (wrong scale, missing part, non-manifold mesh): −20 and a required fix. A drawing whose **fits carry no tolerance**, or a walkthrough that **omits the known-limitations section**: −10 each. These are the production-shop non-negotiables; the deductions are deliberately harsh because in a real shop they are the difference between a part that assembles and a part that goes in the scrap bin.
