# Mini-Project — Promote the Running Part to a Multi-Feature Part

> Take the finished single-body solid you delivered in Week 2 and **promote it to a properly multi-feature part**: add a **patterned or mirrored** feature set, add at least one feature built on a **non-default plane**, then **audit your feature tree** — rename every feature meaningfully, reorder for clean design intent, and document the ordering in your walkthrough. The part must still pass the rebuild test, now under the extra stress of patterns and non-default planes.

This is the third installment of the **running project** that grows every week of C12. Week 1 gave it a fully-defined master sketch. Week 2 turned it into a finished solid part (thickness, a mounting hole, fillets/chamfers). **This week it becomes multi-feature** — patterns, mirror, a non-default plane, and a deliberately ordered tree. Week 4 mates it into an assembly. Week 5 dimensions and configures it. Week 6 ships it in the capstone. You build on the last *artifact*, not from scratch — so the cleaner your tree this week, the easier every following week is.

**Estimated time:** ~12.5 hours (split across Thursday through Sunday in the suggested schedule).

---

## Starting point (compounds on Week 2)

You should already have, from Week 2:

- An OnShape Document containing a **finished single-body solid part**, built **from your Week 1 master sketch**, with a real thickness/depth, at least one mounting hole (Hole feature), and fillets/chamfers for manufacturability.
- A part that **passed the Week 2 rebuild test** (flex two driving dimensions ±20%, nothing red).
- A short walkthrough of the modeling steps.

If your Week 2 part is thin, under-defined, or never actually survived the rebuild test, **fix it first.** A multi-feature part is only as robust as the single-body part underneath it. Re-open it, drive every sketch black, confirm the ±20% test still passes, *then* start adding this week's features.

> **If you're joining C12 at Week 3** with no prior part: spend the first ~90 minutes creating a Week-2-grade part. Sketch a flat part on the Top plane (a 100 × 60 mm mounting bracket profile, or a name plate), fully define it, extrude to ~6 mm, add one Hole feature, and break the edges with a fillet/chamfer. The rest of this brief assumes that part exists and rebuilds clean.

---

## What you will deliver

A single OnShape Part Studio (in your running-project Document) containing **one multi-feature solid part** that:

1. Still traces back to your **Week 1 master sketch** as its base profile — it's the *same evolving part*, not a fresh start.
2. Adds **at least one patterned or mirrored feature set** — a bolt-hole circle, a vent grille, a rib array, a symmetric pair of tabs — built from a **single seed** feature and driven by a **variable** count.
3. Adds **at least one feature built on a non-default construction plane** — an offset, angled, point–normal, or mid plane that a real feature sits on.
4. Has a **feature tree audited and renamed** — every feature, plane, axis, and variable named by its job; logical base → references → shape → multiply → dress-up order; folders where they help.
5. **Rebuilds clean** under the C12 rebuild test, now stressed by the new pattern and plane (see Acceptance Criteria).
6. Plants **at least one explicit mate connector** as a persistent, oriented reference frame for Week 4. (Not mated this week — just placed with intent.)
7. Ships with an updated **step-by-step walkthrough** that documents the **design-intent ordering**.

Plus a created **Version** of the Document and a shared public link.

---

## Rules

- **You may** use any Part Studio feature covered in Weeks 1–3: Sketch, Extrude, Revolve, Hole, Fillet, Chamfer, Shell, Draft, Boolean, **Plane** (all types), **Axis**, **Linear/Circular pattern**, **Mirror**, **Sweep**, **Loft**, **Mate connector**.
- **You may NOT** use features from later weeks yet — **no Assemblies/Mates, no Variable Studio configurations table, no drawings.** Those arrive in Weeks 4–5. You *may* declare inline `#variables` (you'll need them); the full Variable Studio + Configurations table is Week 5.
- **Single body.** One connected solid part this week. (Multi-part Part Studios are a Week 4 topic.)
- **Units: millimeter.** Length precision 2–3 decimals.
- **Every feature, plane, axis, and variable renamed.** A tree with `Plane 1 / Pattern 2 / Sweep 1` is an automatic deduction.
- **Every driving sketch fully defined (black).**
- **The new features must be parametric** — counts driven by variables, planes referenced (not magic-numbered), patterns built from single seeds.

---

## Acceptance criteria

- [ ] A Part Studio (in your running-project Document) named clearly, e.g. `Part-v3-multifeature`.
- [ ] The part **traces to your Week 1 master sketch / Week 2 solid** — it's the evolved running part, not a redraw. (Branch the Document or add a new Part Studio that reuses the geometry; the lineage must be visible.)
- [ ] **At least one patterned or mirrored feature set** from a **single seed**, with the count/extent driven by an **inline variable** (e.g. `#bolts`, `#vents`, `#ribs`).
- [ ] If the pattern is **circular**, it spins about a **named construction axis** (not an inferred one).
- [ ] **At least one feature built on a non-default construction plane**, the plane named by its job and referencing stable geometry (origin plane + offset/angle, or a mid plane).
- [ ] **At least one explicit mate connector** placed, with its **primary (Z) axis** oriented for the joint you anticipate in Week 4, and named (e.g. `Hinge MC`, `Mount MC`).
- [ ] **Every driving sketch is fully defined (black).**
- [ ] **Every feature, plane, axis, and variable is renamed** meaningfully; the tree reads top-to-bottom as a sensible recipe (base → reference planes/axes → shape features → patterns/mirror → dress-up → mate connectors); related features **grouped into folders**.
- [ ] **The rebuild test passes** (graded heavily — see below).
- [ ] A created **Version** named `Week 3 mini-project` and a **shared public link**.
- [ ] A **walkthrough** (Document notes or separate Markdown/PDF) covering the "Walkthrough requirements" below, including the **design-intent ordering** discussion.

### The rebuild test (mandatory, heavily weighted)

This week's test extends Week 2's by stressing the new features:

1. Identify the part's **two most important driving dimensions** *plus* **one pattern variable** (e.g. overall length, thickness, and `#bolts`).
2. Flex each: the two dimensions by roughly **±20%**, and the pattern count by **at least ±2 instances** (e.g. `#bolts` 6 → 8 and 6 → 4).
3. Regenerate after each change. **No feature may turn red.** Specifically watch the new failure modes from this week:
   - A **pattern instance falling off** the part (count vs. size mismatch) → tie count/spacing to the size it sits on.
   - A **circular pattern whose axis drifted** because it referenced a face, not a named axis → re-reference to the named axis.
   - A **feature on a non-default plane** floating away because the plane wasn't parametric → drive the plane's offset/angle from a variable or stable geometry.
4. **Document it:** the three things you flexed, the values/counts you tried, and a one-line confirmation it rebuilt clean. If something broke and you fixed it, **describe the fix** — that's worth more than a part that never broke.

---

## Suggested order of operations

Build incrementally. Don't try to add everything at once.

### Phase 1 — Prep & branch (~1h)

1. Open your running-project Document. **Versions and history → Create version** (`Pre-Week-3`), then **branch** so your Week 2 part stays intact.
2. Create a **new Part Studio** for the v3 part (or continue the existing one if your tree is already clean). Confirm units are **millimeter**.
3. Re-open the base geometry and **confirm every existing sketch is black** and the Week 2 rebuild test still passes. Fix anything that drifted.
4. Create a Version: `v3 baseline ready`.

### Phase 2 — Audit & rename the existing tree (~1h)

1. Walk the existing feature tree top to bottom. **Rename every feature** by its job (`Base profile`, `Body extrude`, `Mount hole`, `Edge fillet`). No `Extrude 1` survivors.
2. **Group** related features into folders (`Base`, `Holes`, `Dress-up`).
3. Sanity-check the **order**: shape features before dress-up; nothing referencing geometry that comes after it. Use the **rollback bar** to reorder if needed.
4. Version: `Tree audited`.

### Phase 3 — Add a non-default-plane feature (~2h)

1. Decide what the part needs on a non-default plane — a boss on an offset plane, a stiffener on an angled plane, a mounting pad on a mid plane.
2. Build the **Plane** (offset/angle/mid), driven by a variable or stable reference. **Rename it.**
3. Sketch (fully defined) and build the feature on it. **Rename it.**
4. Run a quick rebuild check: flex the plane's offset/angle; confirm the feature follows. Version: `Non-default-plane feature`.

### Phase 4 — Add the patterned/mirrored feature set (~2.5h)

1. Model **one seed** feature (a hole, a rib, a vent slot, a tab).
2. Choose the multiplier: **circular pattern** (build a named **Axis** first), **linear pattern** (centered), or **mirror** (off an origin/mid plane).
3. Drive the count/extent with an **inline variable** (`#bolts`, `#ribs`, `#vents`).
4. Build the pattern/mirror from the single seed. **Rename it.** Group seed + pattern into a folder.
5. Flex the count once to confirm re-layout. Version: `Pattern/mirror added`.

### Phase 5 — Plant the mate connector(s) (~0.5h)

1. Decide where the part will join something in Week 4 (a hinge, a bolt face, a shaft seat).
2. Place an **explicit Mate connector** there; orient its **Z (primary) axis** for the anticipated joint.
3. **Rename it** (`Hinge MC`, `Mount MC`). Version: `Mate connectors planted`.

### Phase 6 — Full rebuild test (~1.5h)

1. Run the **mandatory rebuild test** above: two dimensions ±20%, one pattern variable ±2.
2. Fix any red features at their **upstream cause** (rollback bar to find it).
3. Re-run until the whole range is clean. Record the values you tested for the walkthrough.
4. Version: `Rebuild test passed`.

### Phase 7 — Walkthrough & ship (~2h)

1. Write the **walkthrough** (see requirements below), including the **design-intent ordering** discussion and the rebuild results.
2. Final tree audit: every feature/plane/axis/variable renamed, foldered, ordered.
3. Create a **Version** named `Week 3 mini-project`. **Share** the Document publicly and copy the link.
4. Confirm a fresh viewer can open it, read the tree, and flex your nominated dimensions.

---

## Walkthrough requirements

Your write-up (it carries real weight in the rubric) must include:

1. **Lineage:** one paragraph confirming this is the evolved Week 1/Week 2 part, and what changed this week.
2. **The non-default plane:** which type, what it references, and why a plane (not a face) was correct there.
3. **The pattern/mirror:** the seed, the multiplier, the axis/plane/direction, and the variable driving it — plus how you kept it centered/on-part.
4. **The mate connector(s):** where placed, which way Z points, and what you expect to mate to it in Week 4.
5. **Design-intent ordering:** walk your feature tree top to bottom and justify the order — why the reference planes/axes come early, why dress-up comes last, and one feature whose position you deliberately chose (and what would break if it moved).
6. **The rebuild test results:** the three things you flexed, the ranges, and the rebuild confirmation (plus any break-and-fix story).
7. **One rejected reference:** a reference you considered and rejected, and why (the dangling-reference reasoning from Lecture 1).

---

## Rubric

| Criterion | Weight | What "great" looks like |
|----------|-------:|-------------------------|
| Required features present | 20% | A real patterned/mirrored set **and** a real non-default-plane feature, both load-bearing |
| Parametric rebuild | 30% | Two dims ±20% **and** a pattern count ±2 rebuild clean; zero red features; break-and-fix documented if any |
| Reference & design intent | 20% | Features ride named planes/axes/variables, not magic numbers/fragile faces; ordering justified |
| Tree hygiene | 10% | Every feature/plane/axis/variable renamed; logical order; folders; reads like a table of contents |
| Mate connector readiness | 10% | At least one explicit, correctly-oriented, named connector ready for Week 4 |
| Walkthrough quality | 10% | Someone unfamiliar can open the model, follow the steps, and flex it from the write-up alone |

A part that looks impressive but turns red on the first edit, or whose tree is a wall of `Pattern 1 / Plane 2`, scores **below** a plain part that flexes cleanly and reads clearly. Robustness and legibility are the craft this week.

---

## What this prepares you for

- **Week 4 (Assemblies & Mates):** the **mate connectors** you planted become the references your mates snap to. A connector with Z pointing along the hinge line makes Week 4's revolute mate trivial; a careless one makes it painful.
- **Week 5 (Configurations):** the **variables** driving your pattern counts and plane offsets go straight into a Configurations table — `#bolts = 4 / 6 / 8` becomes a dropdown. Variable-driven modeling now is configurability later for free.
- **Week 6 (Capstone):** the **clean, foldered, renamed tree** is what lets you (and your reviewers) understand the part months later when it's one component of a moving mechanism.

---

## Resources

- *Planes*: <https://cad.onshape.com/help/Content/planes.htm>
- *Linear pattern*: <https://cad.onshape.com/help/Content/linearpattern.htm>
- *Circular pattern*: <https://cad.onshape.com/help/Content/circularpattern.htm>
- *Mirror*: <https://cad.onshape.com/help/Content/mirror.htm>
- *Mate connectors*: <https://cad.onshape.com/help/Content/mate_connector.htm>
- *Rollback bar & feature history*: <https://cad.onshape.com/help/Content/rollbackbar.htm>

---

## Submission

When done:

1. Create a **Version** named `Week 3 mini-project`.
2. **Share** the Document publicly (or to your cohort) and copy the link.
3. Make sure the walkthrough is attached (Document notes or a Markdown/PDF in your repo/tracker).
4. Confirm on a fresh open that the tree is clean, every sketch is black, and your nominated dimensions flex without red.
5. Post the link in your cohort tracker. You promoted a real part to multi-feature — show it.
