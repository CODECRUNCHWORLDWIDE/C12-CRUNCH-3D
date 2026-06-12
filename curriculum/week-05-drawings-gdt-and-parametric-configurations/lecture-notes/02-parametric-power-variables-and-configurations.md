# Lecture 2 — Parametric Power: Variables, Equations & Configurations

> **Duration:** ~2 hours of reading + hands-on in OnShape.
> **Outcome:** You can define named variables in a Variable Studio, reference them in sketches and features with `#name` and equations, and configure one part into a family of sizes with a Configurations table — switching variants from a dropdown.

If you only remember one thing from this lecture, remember this:

> **A great parametric model isn't a shape — it's a recipe.** Hard-code `40` into a sketch and you've built one part. Define `#width = 40 mm` and reference `#width` everywhere it matters, and you've built every part of that family at once. Configurations are the dropdown that lets a teammate pick one without ever opening your sketches. The goal of this lecture is to stop drawing *a* part and start defining *a part that knows how to resize itself*.

---

## 1. Two ways to make a model flexible

Everything you've modeled so far is *already* parametric in the loose sense: change a dimension, the feature rebuilds. But "change a dimension by hand" doesn't scale. This week adds two real mechanisms:

| Mechanism | What it is | Use it when… |
|-----------|-----------|--------------|
| **Variables** | Named values (`#width`, `#thickness`) with units, referenced by sketches/features and related by equations | One number drives many dimensions, or several dimensions are related by a formula |
| **Configurations** | A table of named variants that switch dimensions, suppress features, or swap values from a dropdown | You want *one* model to produce a *family* of parts (sizes, options) without copy-pasting documents |

They compose: a Configurations table almost always drives a **configuration variable**, and that variable feeds the same `#name` machinery as a Variable Studio. Learn variables first; configurations sit on top of them.

---

## 2. Variables: `#name` and where they live

A **variable** is a named value with a unit. `#wall = 3 mm`. Once defined, you type `#wall` anywhere OnShape accepts a dimension — in a sketch dimension box, in an Extrude depth, in a pattern spacing — and the feature uses the variable's value. Change the variable in one place; every feature that referenced it rebuilds.

There are two homes for variables, and choosing the right one matters:

### a) The Variable feature (in a Part Studio)

The simplest: in a Part Studio, add a **Variable** feature from the toolbar (the `#` icon). It defines one variable, sits in the feature tree, and is in scope for every feature *below it in the tree*. Order matters — a feature above the Variable feature can't see it. Put your variables at (or near) the **top** of the tree so everything downstream can reference them.

```
Feature tree
├── #wall = 3 mm            ← Variable feature, near the top
├── #height = 50 mm
├── #bolt_dia = 6 mm
├── Sketch 1   (uses #height)
├── Extrude 1  (depth = #wall)
└── Hole 1     (diameter = #bolt_dia)
```

### b) The Variable Studio (document-wide)

A **Variable Studio** is its own tab (like a Part Studio or Drawing). Variables defined there are in scope across the *entire document* — every Part Studio and Assembly can reference them. This is the right home when several parts in one document must share a value (a common wall thickness, a fastener size used everywhere, a clearance gap). Define it once in the Variable Studio; reference `#clearance` in three different Part Studios; change it once and all three rebuild.

> **Rule of thumb.** A value used by one part → a Variable feature in that Part Studio. A value shared across parts in the document → the Variable Studio. The mini-project this week wants you to use at least the Variable feature; the Variable Studio is a natural step up for the multi-part case.

### Units on variables — don't fight them

Variables are **unit-aware**. `#wall = 3 mm` is a length; `#angle = 30 deg` is an angle; `#count = 6` is a unitless number. OnShape enforces dimensional consistency: you can add two lengths, multiply a length by a number, but you *cannot* add a length to an angle — it'll error, and that error is protecting you from a class of bug. When you reference `#wall` in an Extrude depth, OnShape knows it's a length and accepts it; reference `#count` in a circular pattern's instance count and it knows it's a unitless integer.

---

## 3. Equations: relating one variable to another

The power move is **equations between variables**. A variable's value can be a formula referencing other variables:

```
#width      = 60 mm
#height     = 40 mm
#wall       = 3 mm
#bore       = #width - 2 * #wall      → 54 mm, auto-computed
#hole_x     = #width / 2              → 30 mm, always centered
#fillet_r   = #wall / 2               → 1.5 mm, scales with the wall
```

Now `#bore`, `#hole_x`, and `#fillet_r` are *derived*. Change `#width` to 80 and `#bore` becomes 74, the hole stays centered, and nothing breaks — because you encoded the *relationship*, not the *number*. This is **design intent as math.** A reader who opens your model and sees `#bore = #width - 2 * #wall` understands *why* the bore is that size; a reader who sees `54` learns nothing and will break it the moment they edit the width.

You can use the standard operators (`+ - * /`), parentheses, and functions OnShape's FeatureScript exposes for expressions (`sqrt`, `sin`, `cos`, `tan`, `floor`, `ceil`, `round`, `abs`, `pi`, `min`, `max`). Angles inside trig functions need to be angle-typed: `sin(#angle)` where `#angle = 30 deg` works.

> **Worked example — a vent grille that auto-spaces.** Suppose a cover plate is `#plate_w` wide and you want `#n_slots` slots evenly spaced with a `#margin` on each end:
> ```
> #plate_w   = 120 mm
> #n_slots   = 7
> #margin    = 10 mm
> #pitch     = (#plate_w - 2 * #margin) / (#n_slots - 1)   → 16.67 mm
> ```
> Reference `#pitch` as the spacing in a linear pattern and `#n_slots` as its count. Now change `#n_slots` to 9 and the slots re-space themselves to still fit with the same margins. You designed the *rule*, not the layout.

---

## 4. Configurations: one model, a family of parts

Variables make a model flexible. **Configurations** make that flexibility *pickable from a dropdown* without anyone editing the model. A configured Part Studio publishes a set of named variants; downstream — in assemblies, in drawings, in the Standard Content sense — a consumer just selects "the 60 mm one" from a list.

### Configuration inputs

A configuration starts with one or more **configuration inputs**, defined in the **Configurations panel** (the toolbar button that looks like a small table). There are three kinds:

1. **Configuration list** — a dropdown of named options: `Small`, `Medium`, `Large`. Each option is a label; the table behind it decides what each label *means*.
2. **Configuration variable** — a numeric input with a name and units (e.g., `length`, default 60 mm, range 40–100). The consumer types or picks a number; it drives dimensions like a variable.
3. **Configuration checkbox (boolean)** — a true/false toggle, typically used to **suppress** a feature: "with mounting tabs" on/off.

### The configuration table

Once you have an input, OnShape shows a **configuration table** — rows are the configurations (the options of your list), columns are the things each configuration controls. You add a column by clicking a dimension, a feature's suppression state, or a part property and choosing "Configure." Then you fill the grid:

| Configuration | Body Length (`Sketch1.length`) | Bore (`Hole1.diameter`) | Mounting Tabs (`TabPattern` suppress) | Part Number |
|---------------|-------------------------------:|------------------------:|:--------------------------------------|-------------|
| **Small**     | 40 mm                          | 4 mm                    | Suppressed                            | CC-BRKT-S   |
| **Medium**    | 60 mm                          | 6 mm                    | Unsuppressed                          | CC-BRKT-M   |
| **Large**     | 90 mm                          | 8 mm                    | Unsuppressed                          | CC-BRKT-L   |

Now selecting `Large` from the configurations dropdown sets the body to 90 mm, the bore to 8 mm, keeps the tabs, and stamps the part number `CC-BRKT-L`. Three parts, one model, one feature tree. Add a fourth row and you've added a fourth size in ten seconds.

### What a configuration column can control

- **A dimension** — the headline use. Any sketch dimension or feature parameter (extrude depth, hole diameter, fillet radius, pattern count).
- **A feature's suppression** — turn a whole feature (or a pattern) on/off per configuration. This is how "with tabs / without tabs" works.
- **A configuration variable** — drive a `#variable` per configuration, which then propagates through all your equations. This is the cleanest pattern: configure *one* driving variable, let your equations do the rest.
- **A part property** — most importantly the **part number** and **description**, so each configuration carries its own ID into the BOM and title block.
- **A boolean / Boolean feature, an appearance, a sketch's geometry** — yes, but keep it simple this week.

> **The clean pattern: configure a variable, not a pile of dimensions.** Instead of putting five dimension columns in the table, define one configuration variable (`#size`) and write your model's dimensions as equations of `#size` (`#body = #size`, `#bore = #size * 0.1`, `#fillet = #size * 0.03`). Then the table has *one* column. Add a size by adding one number. This is the difference between a configuration table a stranger can extend and one only you can maintain.

---

## 4b. A closer look at the three configuration input types

The input type you choose shapes how a consumer interacts with your part. Pick deliberately.

### Configuration list — named, curated options

A **list** input gives a fixed dropdown: `Small`, `Medium`, `Large`. The consumer can pick *only* those options — there's no "type 53 mm" escape hatch. Use a list when:

- The variants are a **curated catalog** (you sell exactly these three sizes, not arbitrary ones).
- Each option changes **several** things at once (dimensions *and* suppression *and* part number), so a single label needs to map to a whole row of the table.
- You want the BOM and downstream consumers to reference a clean, finite set of SKUs.

The list is the workhorse for a product family. Its weakness: adding a value means editing the table; a consumer can't invent a size you didn't author.

### Configuration variable — a numeric input with a range

A **configuration variable** exposes a number (with units, a default, and an optional min/max range): `length`, default `60 mm`, range `40–100`. The consumer types or slides to any value in range, and it drives the model like a variable. Use it when:

- The dimension is **continuous** — any value in a range is valid (a custom-length standoff cut to order).
- You don't want to enumerate every option (you can't list every length from 40 to 100).

Its strength is flexibility; its risk is that a consumer can pick a value you never tested. **Always set a sensible min/max** so they can't drive the part to an invalid size — the range is your guardrail, the same way a variable equation's `min`/`max` clamp is.

### Configuration checkbox (boolean) — a feature on/off toggle

A **checkbox** is a true/false input, almost always wired to **suppress** a feature: `Mounting tabs`, `Knurled grip`, `Counterbore`. Checked → the feature is present; unchecked → suppressed. Use it for **optional features** that are independent of size. Combine a list (size) with a checkbox (option) and your configuration table becomes a 2-D grid: three sizes × two tab options = six effective variants from two simple inputs. That multiplication is the power of composing inputs.

> **Composability is the design lever.** Two well-chosen inputs (a size list + an options checkbox) describe a whole product matrix more cleanly than one giant list of every combination. Authoring `Small-NoTabs`, `Small-Tabs`, `Medium-NoTabs`, … by hand is the copy-paste anti-pattern in disguise. Let the inputs multiply.

---

## 5. Configured parts in assemblies and drawings

A configured part doesn't stay trapped in its Part Studio:

- **In an Assembly:** when you insert a configured part, the Insert dialog shows the configuration dropdown — you pick which variant to place. You can even insert the *same* part twice in two different configurations (a Small and a Large in one assembly). Mates attach to whichever configuration's geometry is present; design your mate connectors on geometry that exists in *all* configurations so a mate doesn't break when someone switches variants.

- **In a Drawing:** a base view of a configured part has a configuration property — set it, and the view shows that variant. The killer feature: **one drawing sheet can document multiple configurations**, each in its own view with its own dimensions and its own title-block part number. Or a **tabulated drawing**: one view with a table of dimensions, one column per configuration (`A`, `B`, `C` dims down the side, `Small/Med/Large` across the top). That's how a real catalog part is drawn — one sheet, a whole product line.

> **The interlock to design for.** A configuration that suppresses a feature can break anything downstream that referenced it — a mate, a dimension on a drawing, a child feature. Before you ship a configuration table, **switch through every configuration** and confirm each rebuilds with no errors and the drawing's views don't go red. A configuration that errors in one variant is the parametric equivalent of a flaky test: it'll pass for you and fail for whoever picks the variant you didn't check.

---

## 6. Variables vs configurations — when to reach for which

They overlap, so be deliberate:

- Use a **variable** when one number drives many dimensions but you only ever want *one* value at a time, set by editing the model. (A house wall thickness; a global clearance.)
- Use a **configuration** when you want to *publish multiple finished variants* that a consumer picks without editing — sizes in a catalog, options on a product, a fastener family.
- Use **both** when a configuration drives a configuration variable that your equations expand into the whole part — the recommended pattern for any real part family.

A simple decision: *"Do I want a teammate to pick this from a dropdown without opening my sketches?"* Yes → configuration. *"Is this just a value I want to keep DRY across my own features?"* → variable.

---

## 6b. Naming, units, and the readability of a parametric model

A parametric model is read by other people (and by future-you). The difference between a model a stranger can extend and one only you can maintain is mostly **naming and intent**, not cleverness.

- **Name variables for meaning, not geometry.** `#wall`, `#bore`, `#bolt_dia`, `#reach` tell a reader *what the number is for*. `#d1`, `#x`, `#len2` tell them nothing — they're the magic numbers of the parametric world. A teammate who opens `#bore = #od - 2*#wall` understands the design; one who opens `#d3 = #d1 - 2*#d2` has to reverse-engineer it.
- **Keep units honest.** Define every variable with its real unit (`mm`, `deg`, unitless). Don't store an angle as a unitless number "because it's easier" — you lose OnShape's dimensional checking, which catches a whole class of "I added a length to an angle" bugs before they corrupt the model.
- **Order the tree so variables are visible.** Variables (Variable feature) belong at or near the **top** of the feature tree so every downstream feature is in scope. A variable buried halfway down can only be seen by features below it — a confusing source of "why won't this dimension accept `#wall`?" errors.
- **Comment the non-obvious equation.** Most equations are self-documenting once named well. For the rare tricky one (a trig layout, a clamped value), drop a note in the part or the walkthrough explaining the intent. The equation captures the *what*; a one-line note captures the *why*.
- **One driver, many derived.** The hallmark of a clean parametric model is a small set of **driving** variables a human edits, and a larger set of **derived** variables computed from them by equations. If every dimension is independently editable, you don't have a parametric model — you have a pile of numbers that happen to render a shape.

> **The litmus test.** Hand your model to a peer and ask them to "make it 30% bigger." If they can do it by changing **one** driving variable (or picking one configuration), you built a recipe. If they have to hunt through sketches editing literals, you built a shape. Week 5's whole point is to build recipes.

---

## 7. Common failure modes (and the fixes)

- **A configuration errors on one variant only.** A dimension went negative or a feature lost its reference at an extreme size. Fix: add an equation guard (e.g., `#bore = max(#size - 2*#wall, 1 mm)`) or tighten the configuration variable's allowed range so it can't reach an invalid value.
- **A mate breaks when you switch configurations.** The mate connector lived on geometry that one configuration suppresses. Fix: attach mate connectors to geometry common to all configurations (an implicit mate connector on a face that always exists), or define an explicit mate connector that all configs keep.
- **The drawing dimension goes red after a config switch.** The dimensioned edge disappeared in that variant. Fix: dimension to geometry present in all configurations, or make a separate view per configuration.
- **You hard-coded a number you meant to derive.** A dimension didn't update with `#size` because someone typed `40` instead of `#body`. Fix: open the sketch/feature and replace the literal with the variable reference. (This is the CAD version of a magic number — hunt them down.)
- **Over-configuring.** Twelve dimension columns where one driving variable would do. Refactor to a single configuration variable + equations.

---

## 8. A worked end-to-end: the three-size spacer

Let's tie it together with the part you'll build in Exercise 3. A round standoff spacer that comes in three lengths.

1. **Variables.** In the Part Studio, add a Variable feature: `#od = 12 mm`, `#id = 6 mm`, `#length = 20 mm`. Build the spacer as a revolve (or extrude of an annulus) whose outer diameter is `#od`, bore is `#id`, height is `#length`. Every dimension references a `#name` — *zero* hard-coded numbers in the sketches.
2. **Configuration input.** Open the Configurations panel, add a **configuration list** named `Size` with options `Short`, `Standard`, `Tall`.
3. **Configure the driving variable.** Add a column for `#length` (Configure the Variable feature's value). Fill it: `Short → 12 mm`, `Standard → 20 mm`, `Tall → 35 mm`. Leave `#od` and `#id` the same across all three (a spacer family shares its bore and OD; only length changes).
4. **Configure the part number.** Add a Part Number column: `CC-SPACER-12`, `CC-SPACER-20`, `CC-SPACER-35`.
5. **Verify.** Switch the dropdown through all three. Each rebuilds clean; the part number updates; the bore and OD stay put.
6. **Document.** Create a drawing. Put three base views, one per configuration, side by side — or one tabulated view with a `LENGTH` row across `Short/Standard/Tall`. The title block reads the configured part number for whichever view you set. Export PDF.

That's a product line — one feature tree, three SKUs, one drawing sheet. The same recipe scales from a spacer to the mounting-bracket family you'll configure in the mini-project.

---

## 9. Expressions in depth: the functions that make models smart

Most of your equations are arithmetic — `#width / 2`, `#od - 2*#wall`. But OnShape's expression language (it's FeatureScript under the hood, though you never write a line of code) gives you functions that turn brittle layouts into robust ones. You type these straight into any dimension or variable field.

**The functions worth knowing this week:**

| Function | Does | A real use |
|----------|------|-----------|
| `max(a, b)` / `min(a, b)` | The larger / smaller of two | Clamp a derived value so it never goes invalid: `#bore = max(#size - 2*#wall, 1 mm)` |
| `floor(x)` / `ceil(x)` | Round down / up to an integer | Compute a whole number of slots that fits: `#n = floor(#plate_w / #pitch)` |
| `round(x)` | Round to nearest integer | Snap a count to a sensible whole number |
| `abs(x)` | Magnitude | Guard against a negative coming out of a subtraction |
| `sqrt(x)` | Square root | Diagonal of a plate: `sqrt(#w^2 + #h^2)` |
| `sin/cos/tan(θ)` | Trig (θ must be angle-typed) | Lay out a feature at an angle: `#x = #r * cos(#angle)` |
| `pi` | The constant π | Circumference-driven layouts: `#pitch = pi * #pcd / #n_holes` |

**Why the clamp matters more than it looks.** The single most common reason a configuration "works for me but errors for them" is a derived value going negative or zero at an extreme. Consider `#bore = #od - 2*#wall`. At `#od = 12, #wall = 3` the bore is 6 — fine. But put `#od` on a configuration variable a consumer can set to 5, and the bore becomes `-1` — an impossible negative diameter, and the feature fails. Wrap it: `#bore = max(#od - 2*#wall, 0.5 mm)`. Now the worst case is a tiny-but-valid bore instead of a hard error. **Defensive equations are to parametric CAD what input validation is to software** — you're guarding against the value you didn't anticipate.

**A worked angular layout — the bolt circle.** Suppose you want `#n` bolt holes evenly spaced on a pitch-circle diameter `#pcd`, and you want the *chord* distance between adjacent holes for a clearance check:

```
#n      = 6
#pcd    = 80 mm
#angle  = 360 deg / #n                  → 60 deg between holes
#chord  = 2 * (#pcd / 2) * sin(#angle / 2)   → 40 mm between adjacent hole centers
```

Drive a circular pattern's count with `#n` and its angle with `360 deg / #n`. Change `#n` to 8 and the pattern re-spaces to 45° steps and the chord recomputes — no re-sketching, no manual angle math. The model carries the trigonometry so you don't.

> **The discipline.** Every time you're about to type a literal number into a sketch or feature, ask: *"Is this number derived from another number in the model?"* If yes, write the equation, not the result. The first time `#width` changes and everything that depends on it updates correctly, you'll understand why we're strict about this. A model full of equations is a model that survives a redesign; a model full of literals is one you rebuild from scratch every time the spec moves.

---

## 10. Configuration governance: keeping a part family maintainable

A configured part is a tiny database, and like any database it rots without discipline. As a family grows past three rows, the following practices separate a catalog a team can maintain from a tangle one person guards:

- **One driving input, derived everything.** Re-stating the headline rule because it's the whole game: a maintainable family has *one* configuration input (a size list or a configuration variable) and a model whose dimensions are *equations* of it. The table stays one or two columns wide no matter how many sizes you add. The moment your table is eight dimension columns wide, you've encoded the same relationships eight times and they *will* drift.

- **Part numbers are configured, never typed downstream.** Each configuration carries its own part number as a configured part property. The BOM and title block read it automatically. If someone types the part number into the title block by hand "just for the Large," you've reintroduced the duplication bug across the very system configurations exist to prevent.

- **Name configurations like a human would order them.** `Short / Standard / Tall`, `M3 / M4 / M5`, `100mm / 150mm / 200mm` — names a consumer recognizes. `Config1 / Config2 / Config3` is the `#d3` of the configuration world: technically valid, humanly useless.

- **Test every variant before you ship.** Cycle the dropdown through *every* configuration and confirm: no rebuild errors, no red drawing views, no broken mates, part number updates, mass recomputes sanely. A family is only as correct as its worst-tested variant. This is the parametric equivalent of running the full test suite, not just the one case you were working on.

- **Document the configuration logic.** In your walkthrough (every mini-project asks for one), state plainly: *what is the driving input, what does each configuration change, and what stays constant across the family.* A reader who knows "only `#length` varies; bore and OD are shared" can extend your family safely. A reader who has to infer it from the table will eventually add a row that violates an invariant you never wrote down.

> **The catalog mindset.** Real manufacturers ship configured CAD so a customer can drop "the M4×20, knurled" straight into their own assembly from a web catalog (this is literally how McMaster-Carr, Misumi, and OnShape's own Standard Content work — every fastener you pulled in Week 4 is a configured part). When you build a configured family, you're building that same artifact at small scale: a part that a stranger picks from a dropdown and gets right every time, without ever opening your sketches. Build it to that standard even when the only stranger is future-you.

---

## 11. How this connects to the rest of the course

This week's two halves aren't separate skills — they're the two outputs that make a model *shippable*, and they feed directly into the capstone:

- **The drawing package** (Lecture 1) is the *communication* deliverable. Week 6's capstone requires a complete drawing set — assembly drawing, key part drawings, BOM — and it's graded on exactly the associativity, dimensioning, and title-block discipline you learned in Lecture 1.
- **Configurations** (this lecture) are the *parametric robustness* deliverable. The capstone explicitly requires at least one configured part and tests "change a key driving variable and confirm the whole assembly rebuilds cleanly." That test is the litmus test from §6b, applied to a multi-part mechanism.

So Week 5 is not a detour from modeling — it's the week your models stop being private files and become products: documented so they can be made, parameterized so they can be a family. Carry both habits — *associative documentation* and *one-driver parametric design* — into the capstone and every model you build after this course.

---

## 11b. A second worked example: a configured mounting bracket

The spacer in §8 changes exactly one dimension, which makes it the perfect first family but a thin example of *equations*. Let's do a richer one — a mounting bracket whose whole geometry scales from a single driver — because it's close to what the mini-project asks of you.

**The design.** An L-bracket: a vertical mounting face with two bolt holes, a horizontal foot with two more, a fillet at the inside corner, and a wall thickness. We want it in three "duty" sizes — `Light`, `Standard`, `Heavy` — where *bigger duty means a thicker, taller bracket with proportionally larger bolts and fillets*. That's a family related by a single scale factor, not by one independent dimension — exactly the case equations exist for.

**Step 1 — one driver, the rest derived.** Add a Variable feature at the top of the tree:

```
#duty       = 1.0                          ← the single driving number (a unitless scale)
#height     = 60 mm * #duty                ← vertical face height scales with duty
#thickness  = 4 mm * #duty                 ← wall thickness scales with duty
#bolt_dia   = 6 mm * #duty                 ← bolts get bigger on heavier brackets
#fillet_r   = #thickness                   ← inside fillet equals wall thickness (a real rule)
#hole_inset = max(1.5 * #bolt_dia, 8 mm)   ← keep holes a safe distance from the edge, clamped
```

Every dimension in the sketches and features references one of these. The only number a human ever edits is `#duty`. Notice `#fillet_r = #thickness` — that's not arbitrary; a fillet equal to the wall thickness is a standard manufacturable rule, and encoding it means the fillet can never become wrong relative to the wall. Notice the clamp on `#hole_inset` — at small duty the `1.5 * #bolt_dia` rule would put holes dangerously close to the edge, so `max(..., 8 mm)` enforces a floor.

**Step 2 — configure the driver.** Open the Configurations panel, add a **configuration list** `Duty` with `Light / Standard / Heavy`, and add **one** column that configures `#duty`:

| Configuration | `#duty` | Part Number |
|---------------|--------:|-------------|
| **Light**     | 0.75    | CC-BRKT-L   |
| **Standard**  | 1.0     | CC-BRKT-S   |
| **Heavy**     | 1.5     | CC-BRKT-H   |

That's the entire table — one driving column plus the part number. Every other dimension (height, thickness, bolt diameter, fillet, hole inset) recomputes from `#duty` through the equations. Want a fourth size? Add one row with one number. *That* is the maintainability payoff: the relationships live in the equations, not smeared across a dozen configured dimensions you'd have to keep consistent by hand.

**Step 3 — verify the extremes.** Cycle `Light → Standard → Heavy`. At `Light` (`#duty = 0.75`) the thickness is 3 mm and the bolt is 4.5 mm — confirm the `#hole_inset` clamp kicked in (1.5 × 4.5 = 6.75 mm < 8 mm, so it floors at 8 mm) and the holes aren't crowding the edge. At `Heavy` confirm nothing self-intersects (a big fillet on a short flange can, if you didn't scale the flange too). The clamp and the proportional scaling are exactly what stop a "works at Standard, breaks at Light" bug.

Contrast this with the naive approach — six independent dimension columns (`height`, `thickness`, `bolt`, `fillet`, `inset`, all hand-entered per row). It would *render* the same three brackets, but the relationships (`fillet = thickness`, `inset ≥ 1.5×bolt`) would be implicit and unenforced. The day someone adds a row and types a fillet that's bigger than the wall, the part fails — and nothing in the table told them the rule. **Equations make the invariants of your design executable.** That's the difference between a family a stranger can extend safely and one that's a minefield.

---

## 12. Recap

You should now be able to:

- Define **variables** as a Variable feature (Part Studio scope) or in a **Variable Studio** (document scope), with units.
- Reference variables with `#name` in sketches and features, and relate them with **equations** so derived values track their drivers.
- Add **configuration inputs** (list, configuration variable, checkbox) and fill a **configuration table** that drives dimensions, suppresses features, and stamps part numbers.
- Use the clean pattern: **configure one driving variable**, expand it with equations, keep the table to one column.
- Place configured parts in **assemblies** (including the same part in two configs) and document multiple configurations on **one drawing**.
- Choose **variables vs configurations** deliberately, and diagnose the common failure modes (config-specific errors, broken mates, red drawing dimensions, hard-coded magic numbers, over-configuring).

Next: prove it. Continue to the [exercises](../exercises/README.md), then the [mini-project](../mini-project/README.md) where you parameterize your assembly's key part into a family and ship its drawing.

---

## References

- *OnShape Help — Configurations*: <https://onshape-public.document360.io/docs/configurations>
- *OnShape Help — Variables / Variable Studio*: <https://onshape-public.document360.io/docs/variable>
- *OnShape Help — Configuration variable*: <https://onshape-public.document360.io/docs/configuration-inputs>
- *OnShape Learning Center — Configurations learning path*: <https://learn.onshape.com/learn/learning-paths>
- *OnShape Help — equations and expressions*: <https://onshape-public.document360.io/docs/expressions>
