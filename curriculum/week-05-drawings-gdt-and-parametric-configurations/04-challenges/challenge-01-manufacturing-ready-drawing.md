# Challenge 1 — A Manufacturing-Ready, Configured Drawing

**Time estimate:** ~120 minutes.

## Problem statement

Take a part you modeled in an earlier week — your **Week 3 multi-feature part** is the ideal candidate (it has enough features to dimension meaningfully and an internal feature to section). Produce a single, **manufacturing-ready drawing** of it that a competent machine shop could make "to print" with zero follow-up questions, **and** make the part a **configured family** so the same sheet documents at least two metric size variants selectable from a dropdown.

Concretely, the finished sheet must:

1. **Fully and correctly dimension** the part — every feature a machinist needs, nothing measured twice, all dimensions **associative** (zero overrides).
2. Include **at least one section view** that exposes an internal feature, with the internal geometry (bore, wall thickness, pocket depth) dimensioned **on the section**.
3. Carry a complete, correct **GD&T frame**: a datum reference frame (`A`, `B`, `C`), at least one **form** control (flatness or perpendicularity), and at least one **position** control on a located feature, with that feature's location given by **basic** dimensions (not double-defined).
4. Be **parameterized and configured**: the part is driven by variables/equations and exposes a **Configurations table** with **at least two** metric size variants (e.g., a `Compact` and a `Wide`), each with its own **part number**, switchable from a dropdown — and **every configuration rebuilds clean**.
5. Document the configurations: either one drawing with a **per-configuration view** for each size, or a single **tabulated** view with a dimension table across the variants.
6. Have a **filled title block** (driven from part properties) and a visible **general tolerance block**.
7. Export to **PDF** (the manufacturing instruction) and the model to **STEP AP242** (the CAM hand-off).

## Acceptance criteria

- [ ] An OnShape document (shareable as a **public link**) containing the configured Part Studio and the Drawing tab.
- [ ] The Drawing shows **no out-of-date views** and contains **zero overridden dimensions**.
- [ ] The part is **fully dimensioned and not over-dimensioned** — a machinist could make it without guessing or measuring off the screen.
- [ ] At least **one section view** with a labeled cutting plane and internal dimensions placed on the section.
- [ ] A valid **datum reference frame** (`A` primary on the seating surface, `B`, `C` on locating edges), at least one **form** FCF, and at least one **position** FCF referencing the DRF.
- [ ] The located feature's position is given by **basic** dimensions — **no** double definition (basic *and* ± on the same location).
- [ ] A **Configurations table** with **≥ 2** size variants, each driving at least one dimension via a **variable/equation** and stamping its own **part number**; **all** configurations rebuild error-free (you cycled through every one).
- [ ] The configurations are **documented** on the sheet (per-config views or a tabulated table).
- [ ] A **filled title block** (part number/description/material from part properties) and a visible **general tolerance block**.
- [ ] Exported **PDF** of the drawing and **STEP AP242** of the part, both committed/linked alongside the document link.

## Rubric

| Criterion | Weight | What "great" looks like |
|-----------|-------:|-------------------------|
| Drawing completeness & associativity | 25% | Fully dimensioned, not over-dimensioned, every dimension reads from the model; no out-of-date views; clean view layout (third-angle, aligned). |
| Section & manufacturability | 20% | Section exposes the right internal feature; wall thickness and internal depths dimensioned on the section; sheet readable, decimals chosen deliberately (not over-precise). |
| GD&T validity | 20% | DRF in correct primary/secondary/tertiary order; FCFs read as valid sentences; position references the DRF; located feature on basic dims with no double-definition. |
| Configuration robustness | 20% | ≥ 2 variants driven by variables/equations; one clean driving input (not a pile of dimension columns); part numbers configured; **every** config rebuilds; configs documented on the sheet. |
| Title block, tolerance block & export | 15% | Title block driven from properties; general tolerance block present and understood; PDF + STEP AP242 exported and verified to open. |

## Stretch

- Add a **third configuration axis** (a boolean option that suppresses a feature) so the family is a 2D grid — and confirm the drawing handles the suppressed case without a red dimension.
- Add the **MMC modifier** (`Ⓜ`) to your position tolerance and write a one-line note explaining the bonus tolerance it grants.
- Make a **tabulated drawing** (one view, a dimension table across all variants) instead of one-view-per-config, and decide which reads better for a catalog.
- Generate a tiny **BOM** by dropping the configured part into a two-part assembly (the part + a fastener from Standard Content) and balloon it.
- Export each configuration's model as its **own STEP file** and confirm the geometry differs between SKUs.

## Hints

<details>
<summary>How do I keep configurations from breaking my GD&T or my drawing?</summary>

Attach datums and dimension to geometry that exists in **every** configuration. If a feature is suppressed in one variant, anything dimensioned to it goes red in that variant. Dimension to the always-present faces, and reference datums to surfaces no configuration suppresses. Then cycle through all configs *with the drawing tab open* and watch for red.

</details>

<details>
<summary>How many decimal places should my dimensions have?</summary>

Only as many as the tolerance you actually need — the general tolerance block ties decimal places to tolerance. Write `40` (gets the coarse ±) for a non-critical edge; write `40.00` only where you truly need the tighter band. Over-decimaling everything quietly inflates the machining cost. Reserve tight tolerances and FCFs for the features that *mate* with something.

</details>

<details>
<summary>What's the cleanest way to drive two size variants?</summary>

Define one configuration variable (e.g., `#size`) and write your driving dimensions as equations of it (`#width = #size`, `#bore = #size * 0.12`, `#fillet = #size * 0.04`). Then the configuration table has **one** column — the size — and adding a variant is adding one number. Far more maintainable than six dimension columns.

</details>

## Submission

When done:

1. Make your OnShape document **public** (or share a link with view access) and copy the link.
2. Export the drawing to **PDF** and the part to **STEP AP242**; keep both files.
3. Post the **document link + PDF + STEP** in your cohort tracker. State which earlier part you started from and which two (or more) size variants the sheet documents.
4. Confirm, in your own words in the post, that *every* configuration rebuilds clean and *every* dimension is associative. You did real work; show it.

## Why this matters

Fully-toleranced, configured drawings are the actual deliverable of a CAD job — the file that goes to the shop, the catalog, and the quote. A part with no drawing is a hobby; a part with an associative, toleranced, configured drawing is a **product**. The drawing-plus-configuration pattern here reappears immediately in Week 6's capstone, where the whole mechanism ships with a drawing package — and it's the literacy every working mechanical engineer is expected to have on day one.
