# Mini-Project — The Full Capstone: An Original Multi-Part Mechanism & Drawing Package

> Bring every prior week's compounding skill — fully-defined sketches (Week 01), solid parts from extrudes and revolves (Week 02), multi-feature parts on construction geometry (Week 03), articulating assemblies with real mates (Week 04), and parametric drawings with GD&T and Configurations (Week 05) — into one deliverable: an **original multi-part mechanism that moves**, of 3+ parts, that articulates via mates, includes at least one configured part, and ships with a complete drawing package (assembly drawing + key part drawings + BOM), STEP/STL exports, and a written design walkthrough. Then defend it in a live design review.

This is the capstone. It is not a new feature to learn; it is the **synthesis** of six weeks of compounding work into one mechanism you can design, build, prove, document, and ship on demand. By the SYLLABUS note, the mini-projects compound — by Week 04 you were turning your Week 03 part into an assembly, and by Week 05 you were configuring and drawing it. Week 06 is where the compounding pays off. If you kept your sketches fully defined, your feature trees clean, and your mates non-redundant every week, this week is design plus assembly plus documentation. If you took shortcuts, this is where you pay for them.

**Estimated time:** ~12.5 hours of the week's schedule (Monday through Saturday mini-project blocks), on top of the exercises and the live review.

---

## What you build

You design and model an original mechanism, assemble it so it articulates, configure one part into a family, document it as a drawing package, and export it. The exercises walk the mechanics; this brief is the whole deliverable wired together.

### The mechanism (pick one or design your own)

A mechanism of **3 or more parts** with one driven degree of freedom:

- **A gripper** (slider-crank or parallel-jaw) — one crank rotation closes a jaw.
- **A scissor lift** — one input extends/collapses a stacked-link platform.
- **A four-bar linkage** — a crank-rocker or parallel-motion arm.
- **A gear train** — meshing gears coupled by a Gear mate, with a defined ratio.
- **A hinged enclosure with a stay** — a lid held open by a linkage.

The worked example across the exercises is the slider-crank gripper; substitute your own and the structure is identical.

### The OnShape Document structure

```
C12-Capstone-<mechanism>/   (one OnShape Document)
├── Skeleton            (Part Studio: kinematic skeleton sketch + DOF budget)  -- Ex 1
├── frame               (Part Studio: grounded frame, mate connectors placed)
├── crank               (Part Studio: input link, mate connector on pivot)
├── connecting-rod      (Part Studio: transmits motion, connectors both ends)
├── jaw  [CONFIGURED]   (Part Studio: configured Small/Medium/Large family)   -- Ex 3
├── Mechanism           (Assembly: grounded + Revolute x3 + Slider, articulates) -- Ex 2
├── Assembly-Drawing    (Drawing: iso/exploded view, balloons, BOM)
├── Jaw-Drawing         (Drawing: orthographic + section, dimensions, tol, GD&T)
└── [Version v1.0]      (immutable release; STEP + STL exported from it)        -- Ex 3
```

### The deliverable files (in your portfolio repo or linked from the Document)

```
capstone/
├── design-walkthrough.md   # the written narrative (motion, mates, DOF budget, tradeoffs)
├── dof-budget.md           # the mobility-equation calculation (Ex 1)
├── interference-report.md  # the four-position sweep results (Ex 2)
├── Mechanism.step          # STEP export of the assembly (from v1.0)
├── jaw.stl                 # STL export of a printable part (from v1.0)
├── Assembly-Drawing.pdf     # the assembly drawing with balloons + BOM
├── Part-Drawing.pdf        # the key part drawing with section + GD&T
└── video-link.md           # link to the 5-minute walkthrough
```

The key parametric pattern is that the **motion is driven by a small set of variables**, so one edit changes the whole mechanism consistently. Put the link lengths and the joint sizes in a Variable Studio:

```
#crank      = 12 mm     // crank radius -> sets the jaw stroke
#rod        = 40 mm     // connecting rod length
#jaw        = 30 mm     // jaw link length
#jaw_width  = 24 mm     // CONFIGURED: Small 18 / Medium 24 / Large 30
#pin_dia    = 6 mm      // joint pin nominal -> holes are #pin_dia + 0.3 for FDM clearance
```

Every sketch dimension that defines the motion references one of these variables, never a raw number. That is what makes the mechanism rebuild when the reviewer changes a value.

---

## The motion you must demonstrate

One input, traced through every joint. This is the drag-one-motion walk from Lecture 1 §1.5, and it is what your 5-minute video shows:

1. **Input.** You grab the crank and rotate it about its Revolute mate (the ground pivot). The crank is the only thing you touch.
2. **Transmission.** The connecting rod, pinned to the crank by a Revolute and to the slider by a second Revolute, transmits the rotation.
3. **Conversion.** The slider rides its Slider mate along the frame rail, converting the rod's swing into straight-line travel.
4. **Output.** The jaw, carried by the slider, closes (or opens) — the output motion.
5. **Range.** You drive it from one extreme to the other and state the numbers: input range (e.g., 90° of crank), output range (e.g., 24 mm of jaw stroke).
6. **Clearance.** At the tightest position you run Interference Detection (zero) and Measure the worst gap (a real number ≥ 0.4 mm).
7. **Robustness.** You change a driving variable (e.g., `#crank` from 12 to 15) and the whole assembly rebuilds clean and still moves.

---

## Rules

- **You may** reuse every skill and habit from Weeks 01–05 — fully-defined sketches, clean feature trees, placed mate connectors, variables, configurations. That is the point — this is synthesis, not a rewrite of fundamentals.
- **You may NOT** leave any part under-defined or any sketch with floating geometry. A blue (under-defined) sketch in a capstone part is the equivalent of a leaked resource — it makes the model fragile and it fails the rebuild gate.
- **Ground exactly one part.** One Fixed part, everything else positioned by mates. Two grounded parts over-constrain; zero means the parts float.
- **Drive the motion from variables.** The link lengths and joint sizes live in a Variable Studio; every motion-defining dimension references them. No magic numbers in motion-critical sketches.
- **Design for your process.** If you will 3D-print it, size the Revolute holes oversize for FDM shrinkage and note it on the drawing; if you will machine it, tolerance for the fit you want.
- **Rebuild discipline:** at the end of every working session this week, change a driving variable and switch through every Configuration, and confirm the clean regen before you stop. The brittle reference is the expensive bug; catch it daily.

---

## Acceptance criteria

The rubric maps each box to a deliverable. This is the same bar as `challenges/challenge-01`, restated for the build.

### Design & motion (25%)

- [ ] A kinematic skeleton (Exercise 1) and a DOF budget computing to mobility = 1.
- [ ] The assembled mechanism articulates through its full range, dragged from one input, with exactly the intended DOF.
- [ ] The range of motion is stated in real units (input range, output range).

### Parts & feature trees (15%)

- [ ] 3+ parts, each fully defined, with a feature tree that reads top-to-bottom like a build sequence (features renamed with intent).
- [ ] Mate connectors placed deliberately at every joint, not inferred from edges.

### Assembly & DOF (20%)

- [ ] Exactly one grounded part; the rest positioned by mates; no red over-constraint warnings.
- [ ] Zero interferences at home, mid-travel, and both extremes (Exercise 2 sweep), worst clearance recorded as a measured number.

### Parametric robustness (15%)

- [ ] At least one part configured (≥ 2 configurations); the assembly rebuilds and still articulates in every configuration.
- [ ] Changing a key driving variable rebuilds the whole assembly with zero red errors and the mechanism still moves.

### Documentation (15%)

- [ ] An assembly drawing with balloons and a BOM, plus the overall envelope dimensions.
- [ ] A key part drawing with orthographic + at least one section view, full dimensioning, tolerances on the fits, and at least one GD&T frame.

### Release & delivery (10%)

- [ ] An immutable `v1.0` Version; STEP (assembly) + STL (printable part) exported from it, both opened clean in a neutral viewer at correct scale.
- [ ] A 5-minute video tracing the motion and showing one live rebuild; a written design walkthrough; the live design review delivered.

---

## Suggested order of work

- **Monday.** Scope the mechanism and build the kinematic skeleton (Exercise 1). Compute the DOF budget. Do not model a single solid until the skeleton drags through its full range without binding.
- **Tuesday.** Model each part as a clean parametric Part Studio, placing a mate connector at every joint. Drive motion dimensions from the Variable Studio. Rename features with intent.
- **Wednesday.** Assemble and mate (Exercise 2). Ground one part, add the Revolutes and the Slider, drag through the full range, run the four-position interference sweep, and fix whatever binds.
- **Thursday.** Configure the jaw into a family and prove the assembly rebuilds across all configurations (Exercise 3). Build the drawing package — assembly drawing with BOM, key part drawing with a section view and a GD&T frame.
- **Friday.** Tag `v1.0`. Export STEP + STL and sanity-check them in a neutral viewer. Record the 5-minute video. Deliver the live design review and capture the risk list.
- **Saturday.** Mock review, portfolio polish, and a final clean drag → rebuild → configuration-sweep cycle as the reviewer will run it.

---

## What "done" looks like

A reviewer opens your live OnShape Document at Version `v1.0`, drags your mechanism through its full range of motion and watches it articulate with no interference, changes a driving variable and watches the whole assembly rebuild with zero red errors and keep moving, switches through every jaw configuration and confirms each one still works, reads your assembly drawing and your part drawing and agrees a machinist could build the part, opens your STEP and your STL in a neutral viewer and finds them complete and correctly scaled, then watches your 5-minute video and reads your design walkthrough and finds the tradeoffs honest. Every one of those steps passes without you touching the keyboard to fix something. That is the capstone. That is C12.
