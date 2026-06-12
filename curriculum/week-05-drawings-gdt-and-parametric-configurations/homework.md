# Week 5 Homework

Six practice problems that revisit the week's topics — drawings, dimensioning, GD&T, variables, and configurations. The full set should take about **6 hours**. Do the work in your OnShape account; for each problem, keep a **public document link** (and a PDF where one is produced) so you can point to it later.

Each problem includes:

- A short **problem statement**.
- **Acceptance criteria** so you know when you're done.
- A **hint** if you get stuck.
- An **estimated time**.

---

## Problem 1 — Drawing-tab vocabulary audit

**Problem statement.** Create a file `notes/week-05-drawing-terms.md` and, in your own words (no copy-paste from the docs), define each of the following and give one concrete example of when you'd use it: (1) Part Studio vs Assembly vs Drawing tab, (2) associative vs overridden dimension, (3) third-angle vs first-angle projection, (4) section view vs detail view, (5) the general tolerance block. Then answer one sentence: *why does driving the title block from part properties beat typing into it?*

**Acceptance criteria.**

- File `notes/week-05-drawing-terms.md` exists with all five definitions, each with an example, plus the one-sentence answer.
- Definitions are in your own words.

**Hint.** If you can't explain "overridden dimension" as a *hazard* (a sheet that lies about the model), re-read Lecture 1 §5. The title-block answer is about a single source of truth flowing to many places.

**Estimated time.** 25 minutes.

---

## Problem 2 — A complete three-view drawing

**Problem statement.** Pick any single part you've modeled (Week 2 or 3 is ideal). Produce a drawing with **front, top, right, and iso** views (third-angle), fully dimensioned and **not over-dimensioned**, with a filled title block driven from part properties. Then prove associativity: change one model dimension, screenshot the drawing updating, and change it back.

**Acceptance criteria.**

- A Drawing tab with the four views, correctly aligned.
- Every feature a machinist needs is dimensioned; nothing is dimensioned twice.
- **Zero overridden dimensions**; no out-of-date views.
- Title block filled (part number/description/material from properties).
- A before/after screenshot pair showing a dimension tracking a model change.
- PDF exported.

**Hint.** Use baseline (not chain) dimensioning for hole locations so tolerances don't stack. Hide tangent edges for a cleaner sheet.

**Estimated time.** 1 hour.

---

## Problem 3 — Section view + wall thickness

**Problem statement.** On a part with an internal feature (a shelled part, a bored boss, a pocket), add a **full section view** through the feature's centerline and dimension the **wall thickness** and the internal depth/diameter **on the section**. Add a one-line note on the sheet explaining why those numbers belong on the section and not the exterior view.

**Acceptance criteria.**

- A labeled section view (`SECTION A-A`) with a cutting-plane line and arrows.
- Wall thickness and at least one internal dimension placed on the section, associative.
- The explanatory note is present.
- PDF exported.

**Hint.** Snap the cutting-plane line to the feature's centerline, or the section will hatch through geometry you wanted open. Wall thickness is `(OD − bore) / 2` — but dimension it directly on the cut, don't just compute it.

**Estimated time.** 45 minutes.

---

## Problem 4 — A GD&T frame you can read

**Problem statement.** On any part with a located hole, build a complete datum reference frame (`A` on the seating surface, `B`, `C` on locating edges), make the hole's location **basic**, and add a **position** feature control frame `⌖ ⌀0.2 | A | B | C`. Separately, add a **flatness** control to datum A's face. Then, in `notes/week-05-gdt.md`, write the two FCFs out as plain-English sentences.

**Acceptance criteria.**

- Datums A/B/C placed in correct primary/secondary/tertiary roles.
- The hole's location is **basic** (boxed), with **no** ± on the same location (no double-definition).
- A position FCF referencing A|B|C and a flatness FCF (no datum) are placed.
- `notes/week-05-gdt.md` translates both frames into sentences.
- PDF exported.

**Hint.** Flatness references no datum — leave its datum boxes empty. Position references the DRF. If OnShape lets you add a position FCF while the location is still ± toleranced, that's the double-definition trap — convert the location to basic first.

**Estimated time.** 1 hour.

---

## Problem 5 — Variable-driven part with equations

**Problem statement.** Model (or rebuild) a simple part **variable-first**: define at least **four** variables, and relate at least **two** of them with an **equation** that encodes design intent (e.g., a centered hole, a wall-derived bore, an auto-spaced pattern). Then change one driving variable to three different values and confirm the part resizes correctly each time with no errors.

**Acceptance criteria.**

- At least four `#variables` defined (Variable feature or Variable Studio).
- At least one equation between variables; zero hard-coded numbers in the driven dimensions.
- The part rebuilds correctly at three different driving values (note them in a short comment in your walkthrough or a `notes` file).
- Public document link.

**Hint.** Good equations: `#hole_x = #width / 2` (centered), `#bore = #od - 2*#wall` (wall-derived), `#pitch = (#plate_w - 2*#margin) / (#n - 1)` (auto-spaced). Pick whichever your part motivates.

**Estimated time.** 1 hour.

---

## Problem 6 — Configure it into a family

**Problem statement.** Take the variable-driven part from Problem 5 and add a **Configurations table** with **at least three** named variants. Drive the configuration through your variable(s), give each variant its own **part number**, and (stretch within the problem) suppress one feature in one variant. Cycle through **every** configuration and confirm each rebuilds clean. Document all variants on a single drawing sheet (per-config views or a tabulated table) and export a PDF.

**Acceptance criteria.**

- A configuration input (list or configuration variable) with **≥ 3** variants.
- Each variant drives a dimension via the variable and stamps its own part number.
- **Every** configuration rebuilds with no errors (verified by cycling through all).
- A single drawing documents all variants; dimensions associative; no overrides.
- PDF exported; public document link.

**Hint.** Use the clean pattern: configure the **driving variable**, not each individual dimension, so the table stays one or two columns. If a small variant errors, clamp the offending dimension with `min`/`max` or tighten the range.

**Estimated time.** 1 hour 15 minutes.

---

## Grading rubric

| Problem | Weight | What earns full marks |
|--------:|-------:|-----------------------|
| 1 | 10% | All five terms defined correctly in your own words, each with an example; title-block answer is about single-source-of-truth |
| 2 | 20% | Four aligned third-angle views, fully but not over-dimensioned, zero overrides, associativity demonstrated, title block from properties, PDF |
| 3 | 15% | Correct section through the centerline, wall thickness + internal dim on the section, associative, note present, PDF |
| 4 | 20% | DRF in correct order, hole location basic (no double-definition), valid position + flatness FCFs, plain-English translations, PDF |
| 5 | 15% | ≥ 4 variables, ≥ 1 meaningful equation, no magic numbers in driven dims, rebuilds at three values |
| 6 | 20% | ≥ 3 variants driven by the variable, part numbers configured, **every** config rebuilds, documented on one sheet, PDF |

**Total: 100%.** Anything below 70% means re-read the relevant lecture and resubmit the weak problems.

---

## Time budget recap

| Problem | Estimated time |
|--------:|--------------:|
| 1 | 25 min |
| 2 | 1 h 0 min |
| 3 | 45 min |
| 4 | 1 h 0 min |
| 5 | 1 h 0 min |
| 6 | 1 h 15 min |
| **Total** | **~5 h 25 min** |

When you've finished all six, make sure your documents are shareable and your PDFs are exported, then open the [mini-project](./mini-project/README.md).
