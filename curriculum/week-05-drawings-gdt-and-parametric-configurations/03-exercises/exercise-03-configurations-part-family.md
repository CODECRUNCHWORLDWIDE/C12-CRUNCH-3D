# Exercise 3 — Configurations: One Part, Three Sizes

**Goal:** Turn a single model into a *family* of parts. You'll drive the geometry from a Variable feature, add a Configurations table with three sizes that a teammate can pick from a dropdown, and document all three on one drawing sheet. This is a CAD task — every step is a precise click sequence in OnShape, no code.

**Estimated time:** 50 minutes.

---

## The part you'll configure

A round **standoff spacer** — a cylinder with a through-bore. It's the ideal first configured part: one driving dimension (length) changes, everything else stays.

### Build it variable-first (this is the whole point)

1. New Part Studio.
2. **Add a Variable feature** (the `#` icon) at the top of the tree. Create three:
   - `#od = 12 mm`
   - `#id = 6 mm`
   - `#length = 20 mm`
3. On the Top plane, sketch **two concentric circles** centered on the origin. Dimension the outer to `#od` and the inner to `#id` — type `#od` and `#id` into the dimension boxes, do **not** type numbers. The sketch should fully define (black).
4. **Extrude** the annular region (the ring between the circles) by depth `#length`, Blind, New. Type `#length` as the depth.
5. Confirm: **zero hard-coded numbers** in your sketches or features — every dimension reads a `#variable`. Change `#length` to `30` and watch the part grow; change it back to `20`.

Set part properties: Part number `CC-SPACER-20`, Description `Standoff Spacer`, Material `303 Stainless`.

---

## Step 1 — Add a configuration input

1. Open the **Configurations panel** (the table icon in the Part Studio toolbar).
2. Add a **Configuration list** input. Name it `Size`.
3. Add three options: `Short`, `Standard`, `Tall`.

OnShape now shows a configuration table with three rows (one per option) and a configurations **dropdown** at the top of the Part Studio. Right now all three rows are identical — they don't *do* anything yet.

---

## Step 2 — Configure the driving variable

You'll drive only `#length`; OD and ID stay common across the family (a spacer line shares its bore and OD — only height changes).

1. In the configuration table, add a **column** → choose to **Configure** the `#length` value of your Variable feature. (Click the Variable feature's `#length`, pick "Configure.")
2. Fill the column:
   - `Short` → `12 mm`
   - `Standard` → `20 mm`
   - `Tall` → `35 mm`

Now pick `Tall` from the dropdown. The spacer rebuilds to 35 mm tall. Pick `Short` — it shrinks to 12 mm. One model, three lengths.

> **Why configure the variable, not the extrude:** you *could* configure the Extrude depth directly. But by configuring the **variable**, any future feature that also references `#length` (a counterbore depth, a chamfer setback) follows automatically. Configure the driver, not each consumer. This is the clean pattern from Lecture 2.

---

## Step 3 — Configure the part number (each size gets its own SKU)

1. Add another **column** → Configure the **Part Number** property.
2. Fill it:
   - `Short` → `CC-SPACER-12`
   - `Standard` → `CC-SPACER-20`
   - `Tall` → `CC-SPACER-35`

Now each configuration carries its own identity into any BOM or title block. Switch the dropdown and watch the part number change in the Properties panel.

---

## Step 4 — Verify every configuration rebuilds

This is the step beginners skip and regret. **Cycle through all three** configurations from the dropdown:

- `Short` → rebuilds clean, 12 mm, `CC-SPACER-12`, bore still ⌀6.
- `Standard` → 20 mm, `CC-SPACER-20`.
- `Tall` → 35 mm, `CC-SPACER-35`.

If any configuration shows a **rebuild error** (a red feature), a dimension went invalid at that size. Fix it before moving on — a configuration that errors in a variant you didn't check is a trap for whoever selects it later.

---

## Step 5 — Document all three on one sheet

1. **Create a drawing** of the spacer (A3/C-size, third-angle).
2. Place a **Front** view. In the view's properties, set its **Configuration** to `Short`. Dimension it (OD, ID, length).
3. Place a **second** Front view; set its **Configuration** to `Standard`. Dimension its length (the OD/ID are shared, so you can note "OD, ID per SHORT").
4. Place a **third** Front view; set its **Configuration** to `Tall`.
5. Add a small **note table** or label under each view: `CC-SPACER-12 / -20 / -35`. The OD `⌀12` and ID `⌀6` are common; only the length differs (`12 / 20 / 35`).

You now have one sheet that documents an entire three-SKU product line.

> **Stretch on this step:** instead of three views, make a single **tabulated drawing** — one view with a small table: a `LENGTH` row across `SHORT | STANDARD | TALL` columns. That's how a real catalog part is drawn.

---

## Step 6 — Title block and export

Fill the title block (drawn-by, date, rev `A`). Note that the title-block part number reflects whichever configuration the *primary* view uses — for a multi-config sheet, add a note clarifying the sheet covers the whole family. Export **PDF**.

---

## Acceptance criteria

- [ ] The spacer is built **variable-first**: `#od`, `#id`, `#length` defined in a Variable feature; **zero hard-coded numbers** in sketches/features.
- [ ] A **Configuration list** `Size` with options `Short / Standard / Tall`.
- [ ] A configuration column drives **`#length`** (the driving variable) to `12 / 20 / 35 mm`.
- [ ] A configuration column drives the **Part Number** to `CC-SPACER-12 / -20 / -35`.
- [ ] Switching the dropdown rebuilds all three configurations **with no errors** (you verified each).
- [ ] A drawing documents all three sizes (three views, or one tabulated view), with associative dimensions and **no overridden** values.
- [ ] PDF exported.

---

## Stretch

- Add a **boolean configuration input** `Knurled` (checkbox) that **suppresses/unsuppresses** a knurl pattern feature, giving you a 2-axis family (size × knurled). Watch the table become a grid.
- Add a `Counterbored` checkbox that suppresses a counterbore feature, and confirm the bore depth still works at every length (guard with `#cbore_depth = min(4 mm, #length/2)` so it never exceeds the part).
- Build the **tabulated drawing** version (one view, a dimension table across the three sizes).
- Insert the spacer into an assembly **twice in two different configurations** (a Short and a Tall) and confirm the mate connectors attach in both.

---

## Hints

<details>
<summary>My dimension box won't accept `#length`</summary>

You must define the Variable feature **above** the sketch/feature in the tree, or the `#name` is out of scope. Drag the Variable feature to the top of the feature tree, then re-type `#length` in the dimension box. The autocomplete should offer your variables once they're in scope.

</details>

<details>
<summary>One configuration shows a red rebuild error</summary>

A dimension went invalid at that size — most often a feature that subtracts more than the part has (a bore deeper than the length, a fillet bigger than the wall). Either tighten the configuration value's range or rewrite the offending dimension as an equation that clamps it (e.g., `min(...)`). Never ship a table with a config that errors.

</details>

<details>
<summary>The drawing view won't switch configuration</summary>

Select the **view** (click its border), open its **Properties**, and look for the **Configuration** field — set it to the option you want. It's a per-view property, not a per-sheet one, so each view can show a different configuration.

</details>

---

This was the last exercise. Now apply all three skills together in the [mini-project](../07-mini-project/00-overview.md): parameterize your assembly's key part into a family and ship its full drawing.
