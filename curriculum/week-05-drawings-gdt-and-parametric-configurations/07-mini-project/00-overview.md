# Mini-Project — Parameterize & Document the Assembly's Key Part

> Take the **multi-part assembly you built in Week 4**, pick its most important component, turn that part into a **configured family** with Variables and a Configurations table (at least two size/variant options), then produce a **manufacturing drawing** of it with views, dimensions, a title block, and a BOM — and ship the **PDF**.

This is the fifth step of the running C12 project, and it is the one that turns your model into something the world outside your OnShape account can use. Through Weeks 1–4 you went sketch → solid part → multi-feature part → working assembly. This week you don't add a mechanism feature — you make the design **parametric and documented**: a part that resizes itself from a dropdown, and a drawing that a shop could manufacture from.

**Estimated time:** ~8.5 hours (split across Thursday, Friday, Saturday in the suggested schedule).

---

## How this builds on prior weeks

| Week | What you delivered | How Week 5 uses it |
|-----:|--------------------|--------------------|
| 1 | A fully-defined master sketch | The sketch you'll now drive with `#variables` instead of literals |
| 2 | A finished solid part with holes & dress-up | The body you'll section and tolerance in the drawing |
| 3 | A multi-feature part (planes, patterns) | The feature tree you'll configure (a pattern is great to suppress per config) |
| 4 | A multi-part **assembly** with working mates | The assembly the **BOM** comes from; the *key part* is the one you'll configure |

If you skipped or want to redo earlier weeks, you can substitute any multi-feature part you own — but the assembly context is what makes the BOM meaningful, so have at least your Week 4 assembly open.

---

## What you will deliver

1. **A configured key part** — the most important component of your Week 4 assembly, rebuilt **variable-first** and exposing a **Configurations table** with **at least two** size/variant options, each switchable from a dropdown and carrying its own part number.
2. **A drawing of that part** — orthographic views, at least the dimensions a shop needs, a filled title block, and (because the part lives in an assembly) a **BOM** generated from that assembly with the configured part in it.
3. **An exported PDF** of the drawing.
4. **A written walkthrough** (`walkthrough.md`) explaining the configuration logic: what variable drives what, why you chose those variants, and how the drawing stays associative across them.

By the end you'll have a part that produces a family of real SKUs and a sheet a fabricator could make any of them from.

---

## Rules

- **You may** use any OnShape feature, the Standard Content library (for fasteners in the BOM), and your own parts from prior weeks.
- **You must** drive the configured part's key dimensions from **variables/equations** — no hard-coded magic numbers in the configured dimensions. (Non-configured cosmetic dimensions can stay literal, but the *driving* dimensions must be variables.)
- **You must NOT** override any drawing dimension by hand. Every dimension reads from the model. An overridden dimension is an automatic fail of the "associativity" criterion.
- **You must** use the **clean configuration pattern**: drive a single configuration variable (or a small number) with equations expanding it, rather than a wide table of unrelated dimension columns, *if* your part's variants are related by size. (A genuinely unrelated option — e.g., with/without tabs — gets its own column; that's fine.)
- Units: keep the document consistent (mm or in — match whatever your prior weeks used). Projection: third-angle unless your sheet template is ISO.

---

## Acceptance criteria

- [ ] The **key part** is rebuilt **variable-first**: its driving dimensions reference `#variables` (Variable feature or Variable Studio), with at least one **equation** relating two of them.
- [ ] A **Configurations table** with **≥ 2** variants, each:
  - driving at least one dimension (directly or via the driving variable), and
  - stamping its own **Part Number** property.
- [ ] **Every** configuration rebuilds with **no feature-tree errors** — you cycled through all of them and confirmed.
- [ ] A **Drawing** of the configured part with:
  - front + top + right ortho views (third-angle, aligned) and an iso for readability,
  - at least one **section** view if the part has an internal feature (wall thickness / bore dimensioned on the section),
  - the part **fully dimensioned and not over-dimensioned**, all **associative**,
  - a **filled title block** driven from part properties, and a visible **general tolerance block**.
- [ ] A **BOM** generated from your Week 4 **assembly**, appearing on the drawing (or on an assembly sheet in the same document), with the configured part as a line item carrying its configured part number. Parts **balloon** to BOM item numbers on at least one assembly view.
- [ ] **Zero overridden dimensions** anywhere in the drawing; **no out-of-date views**.
- [ ] An exported **PDF** of the drawing committed to your project folder (and/or linked).
- [ ] A **`walkthrough.md`** that includes:
  - one paragraph naming the part and why it's the assembly's key component,
  - the **configuration logic**: each variable, what it drives, the equations between them, and what each variant changes,
  - a statement that every configuration rebuilds clean and every dimension is associative (with how you verified),
  - a "Things I learned" section with at least 3 specific items.

---

## Suggested order of operations

Build incrementally — don't try to configure and document at once.

### Phase 1 — Pick and audit the key part (~0.5h)

1. Open your Week 4 assembly. Decide which component is the **key part** — usually the one that defines the assembly's function or the one most likely to come in sizes (the base plate, the arm, the body).
2. Open that part's Part Studio. Audit the feature tree: rename features meaningfully, confirm zero errors. Set part properties (part number, description, material) if not already set.

### Phase 2 — Make it variable-first (~1.5h)

1. Add a **Variable feature** (or Variable Studio tab) near the top of the tree. Define the part's driving dimensions as variables (e.g., `#length`, `#width`, `#thickness`, `#bore`).
2. Add at least one **equation** that encodes design intent (e.g., `#hole_offset = #width / 2` to keep a hole centered, or `#bore = #od - 2 * #wall`).
3. Open each sketch/driving feature and replace the literal numbers with `#name` references. Confirm the part still rebuilds identically.
4. Sanity test: change one variable, watch the part resize correctly, change it back. **Commit / save a named version**: `Key part driven by variables`.

### Phase 3 — Configure it (~1.5h)

1. Open the **Configurations panel**. Add a **configuration input** — a list (`Compact` / `Standard` / `Wide`) or a configuration variable.
2. Configure the **driving variable(s)** per variant. Keep it to the cleanest set of columns (ideally one driving variable + the part number).
3. Configure the **Part Number** property per variant.
4. If a variant adds/removes a feature (e.g., extra mounting tabs), configure that feature's **suppression**.
5. **Cycle through every configuration** and confirm each rebuilds clean. Fix any size that errors (clamp a dimension with `min`/`max`, or tighten the variable's range). Save a version: `Configured part family`.

### Phase 4 — Verify in the assembly (~0.5h)

1. Back in the Week 4 assembly, confirm the configured part still **mates correctly**. If you swap its configuration in the assembly, the mates should hold (you designed mate connectors on common geometry).
2. Set the assembly's instance of the part to whichever configuration is the "default" for the BOM.

### Phase 5 — Drawing + dimensions (~2h)

1. **Create a drawing** of the configured part (A3/C-size, third-angle).
2. Place front/top/right/iso views; add a **section** if there's an internal feature; turn on centerlines.
3. Dimension associatively and completely. If documenting multiple configurations, set per-view configurations or build a tabulated view.
4. Fill the **title block** from part properties. Confirm the general tolerance block.
5. Save a version: `Part drawing — views & dimensions`.

### Phase 6 — BOM + balloons (~1h)

1. Add an **assembly view** (or a separate assembly sheet) and generate the **BOM** from your Week 4 assembly.
2. Confirm the configured part appears with its configured part number; confirm quantities roll up correctly.
3. **Balloon** the parts on the assembly view so each leader points to a part and shows its BOM item number.
4. Save a version: `BOM + balloons`.

### Phase 7 — Export, walkthrough, polish (~1h)

1. Export the drawing to **PDF**; open it outside OnShape and confirm it renders cleanly with no clipped geometry.
2. Write `walkthrough.md` (see acceptance criteria for required contents).
3. Final check against the acceptance list. Confirm: no out-of-date views, zero overridden dimensions, every config rebuilds.
4. Commit the PDF + walkthrough to your project folder and copy the OnShape document link into your tracker.

---

## Example walkthrough excerpt (shape, not content to copy)

> **Key part:** the *Pivot Arm* (`CC-ARM`). It's the assembly's key component because its length sets the mechanism's reach, and the product ships in two reaches.
>
> **Configuration logic:**
> - `#reach` is the driving configuration variable. `Standard → 80 mm`, `Long → 120 mm`.
> - `#pivot_bore = 8 mm` and `#wall = 4 mm` are common to both variants.
> - Equation: `#tip_x = #reach - 10 mm` keeps the end-hole 10 mm from the tip at any reach.
> - Part numbers: `CC-ARM-080`, `CC-ARM-120`.
> - The mounting-rib pattern is suppressed in `Standard`, present in `Long` (the longer arm needs the stiffener).
>
> **Verification:** cycled both configs — both rebuild clean. The drawing's reach dimension and the BOM part number both track the selected configuration. No overridden dimensions; no out-of-date views.

---

## Rubric

| Criterion | Weight | What "great" looks like |
|-----------|-------:|-------------------------|
| Parameterization | 20% | Driving dimensions are variables; at least one meaningful equation encodes design intent; no magic numbers in driving dims |
| Configuration robustness | 20% | ≥ 2 variants, clean driving input, part numbers configured, **every** config rebuilds with no errors |
| Drawing quality | 20% | Fully dimensioned, not over-dimensioned, associative, sensible third-angle layout, section where needed |
| BOM & assembly link | 15% | BOM generated from the Week 4 assembly, configured part as a line item with its part number, balloons present |
| Title block, tolerance & export | 10% | Title block from properties, tolerance block present, clean PDF that opens outside OnShape |
| Walkthrough | 15% | Clear configuration logic, verification statement, ≥ 3 specific "things I learned" |

---

## Stretch (optional)

- Add a **second configuration axis** (a boolean option) so your part family becomes a grid, and document the matrix in the walkthrough.
- Build a **tabulated drawing** (one view, a dimension table across all variants).
- Add a basic **GD&T frame** (datums + a position tolerance on the part's mounting holes) so the drawing is not just dimensioned but toleranced — this is exactly the Week 5 challenge, folded into the project.
- Export each configuration as its own **STEP AP242** file and confirm the geometry differs between SKUs.
- Add a `ledger`-style sanity note: pick one variant, hand the PDF to a peer, and have them confirm they could make it without asking you anything. Note what they got stuck on.

---

## What this prepares you for

- **Week 6 (Capstone)** ships a *complete drawing package* — assembly drawing, key-part drawings, BOM, exports. Everything you did here is the rehearsal: the configured part, the associative drawing, the BOM all reappear at capstone scale.
- The configure-then-document reflex — *"a part isn't done until it has a drawing and a configuration table"* — is the working habit of every mechanical engineer who ships product. By Week 6 your reflex should be: model → assemble → configure → draw → export.

---

## Resources

- *OnShape Help — Drawings*: <https://onshape-public.document360.io/docs/drawings>
- *OnShape Help — Configurations*: <https://onshape-public.document360.io/docs/configurations>
- *OnShape Help — Variables*: <https://onshape-public.document360.io/docs/variable>
- *OnShape Help — Bill of Materials*: <https://onshape-public.document360.io/docs/bill-of-materials>
- *OnShape Help — Export (PDF/STEP/STL)*: <https://onshape-public.document360.io/docs/export>

---

## Submission

When done:

1. Make your OnShape document shareable (public link or view access) and copy the link.
2. Commit the exported **PDF** and **`walkthrough.md`** to your project folder.
3. Confirm: every configuration rebuilds clean, every dimension is associative, no out-of-date views, the BOM shows the configured part.
4. Post the document link + PDF in your cohort tracker, naming the key part and its variants. You shipped a product, not a model — show it.
