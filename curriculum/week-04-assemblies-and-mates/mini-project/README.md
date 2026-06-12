# Mini-Project — From a Multi-Feature Part to an Articulating Assembly

> Take the **multi-feature part** you delivered in Week 3 and promote it into a **working, multi-part assembly**: model one or two mating components for it, insert everything into an Assembly, and join the parts with the right mates so **at least one joint articulates**. Validate it with the C12 drag test and interference detection. Deliver the assembly plus a walkthrough listing every mate and the degree of freedom it controls.

This is the fourth installment of the **running project** that grows every week of C12. Week 1 gave it a master sketch. Week 2 made it a solid part. Week 3 made it multi-feature (planes, patterns, references). **This week it stops being a single part and becomes a mechanism that moves.** Week 5 will dimension and configure it; Week 6 ships it as part of the capstone. Each week builds on the last *artifact*, not from scratch — so do this well; you'll mate this assembly again in two weeks.

**Estimated time:** ~8.5 hours (split across Thursday through Sunday in the suggested schedule).

---

## Starting point (compounds on Week 3)

You should already have, from Week 3:

- An OnShape Document with your running part as a **multi-feature solid** — built with at least one non-default plane, at least one patterned or mirrored feature set, a clean and renamed feature tree, and a written walkthrough of the design-intent ordering.
- The part **rebuilds clean** when you change a key driving dimension (the Week 2/3 rebuild test).

If your Week 3 part is thin — single feature, no patterns, messy tree — **fix it first.** This week mates a *new* component to it, and a sloppy host part makes mating miserable (no clean faces to grab, no mate connectors, surprise geometry). Re-open it, rename its features, and make sure it has at least one clean mounting feature (a hole, a boss, a flat face) where a second part can attach.

> **If you're joining C12 at Week 4** and have no Week 3 part: spend the first hour modeling a simple multi-feature host part — a **bracket** (flat plate, ~80 × 50 × 6 mm, with a patterned set of Ø5.5 mm mounting holes and one Ø8 mm pivot hole) is ideal, because it gives you an obvious place to mate a moving component. The rest of this brief assumes a host part with at least one pivot or rail feature exists.

---

## What you will deliver

A single OnShape **Assembly** containing your Week 3 host part plus **one or two new mating components**, joined so that:

1. The host part (or a frame) is **Fixed** as the assembly's ground.
2. **At least one joint articulates** — a Revolute, Slider, or Cylindrical mate that gives a moving component **exactly the intended degree(s) of freedom**.
3. At least one part is **Fastened** (rigidly attached) — e.g., a cover, a bracket, or a fastener.
4. At least one fastener is pulled from the **Standard Content library** (correctly sized to its hole).
5. The assembly passes the **C12 drag test**: the moving part moves through its full range and **0 interferences** are detected at the extremes and across the sweep.
6. Every instance and every mate is **renamed meaningfully**.

Plus a created **Version** of the Document, a shared public link, and a **mate walkthrough** (below).

---

## Pick your articulating component

Choose the moving component that best fits the running part you've been building. A few patterns that work well:

| If your host part is… | Add a moving component that… | Articulating mate |
|---|---|---|
| A bracket / mounting plate | a **swinging arm** on a pivot pin | Revolute |
| A box / housing | a **hinged lid** | Revolute (with 0–110° limit) |
| A rail / channel | a **sliding carriage** | Slider (with travel limits) |
| A frame with a bore | a **rotating shaft / spindle** | Cylindrical or Revolute |
| A base with a column | a **telescoping or sliding stage** | Slider or Cylindrical |

You need **one** real articulating joint at minimum. A second component (fastened — a cover, a cap, a bracket) plus a **library fastener** rounds the assembly into something that reads as a real product. Don't over-scope; one good moving joint validated correctly beats five sloppy ones.

---

## Rules

- **You may** use any mate covered this week (Fastened, Revolute, Slider, Cylindrical, Planar, Ball, Pin-Slot), mate connectors (implicit or explicit), the Standard Content library, sub-assemblies, Replicate, interference detection, and Measure.
- **You may NOT** use Week 5 features yet — **no Configurations, no Variable Studio, no drawings.** Those arrive next week and you'll add them then. (If a part *screams* to be configured, note it in your walkthrough as a "Week 5 improvement" — don't add it yet.)
- **Units: millimeter**, length precision 2–3 decimals, angles in degrees.
- **Exactly one ground.** Fix the host part or frame; mate everything else relative to it.
- **Every mate renamed.** A Mate features list of `Fastened 1 / Revolute 2 / Slider 3` is an automatic deduction.
- **At least one articulating joint** that drag-tests to the intended DOF.
- The Week 3 host part should still **rebuild clean** — don't break it while mating.

---

## Acceptance criteria

- [ ] A new **Assembly** tab in your running Document containing the Week 3 host part plus **at least one new mating component** you modeled this week.
- [ ] **Exactly one part is Fixed** (the ground/frame).
- [ ] **At least one articulating mate** (Revolute / Slider / Cylindrical) gives a moving component the **intended DOF and only that** — verified by drag test. State the DOF explicitly.
- [ ] **At least one Fastened mate** rigidly attaching a component or fastener.
- [ ] **At least one Standard Content fastener** inserted and correctly sized to its hole (e.g., M5 cap screw in a Ø5.5 mm clearance hole).
- [ ] Where the design calls for it, the articulating mate has **limits** (a hinge that stops, a drawer that can't fall out).
- [ ] **Interference detection** run at **both extremes of motion and across the sweep** returns **0 interferences** (or only a documented intentional fit).
- [ ] Every instance and mate is **renamed**.
- [ ] The Week 3 host part **still rebuilds clean** (change one of its driving dimensions, confirm no errors, then revert).
- [ ] A created **Version** of the Document and a shared **public link**.
- [ ] A **mate walkthrough** delivered (spec below).
- [ ] The assembly passes the C12 drag test:
  ```
  Drag test · <N> DOF · moves freely through full range · 0 interferences
  ```

---

## Suggested order of operations

Build incrementally; don't try to mate everything at once.

### Phase 1 — Prep the host part (~0.5h)

1. Open your Week 3 Document. Confirm the host part rebuilds clean and its feature tree is renamed.
2. Identify (or add) the **mounting feature** the moving component will attach to — a pivot hole, a rail face, a bore. If it's missing, add it now in the Part Studio (a Ø8 mm pivot hole, say), and confirm a clean rebuild.
3. **Optional but recommended:** add an **explicit mate connector** in the Part Studio at the pivot/rail, oriented so its Z is the joint axis. This is the design-intent move from Lecture 1 — it makes mating in the next phase snap together.
4. Create a **Version** named `pre-assembly` so you can roll back.

### Phase 2 — Model the moving component (~2h)

1. In a new Part Studio, model the component that will articulate (arm, lid, carriage, shaft). Keep it a clean parametric part — fully-defined sketches, renamed features (you've done this for three weeks).
2. Give it the **matching joint feature**: a bore that fits the host's pivot pin, a rail that mates the host's channel, etc. Size the fit with running clearance (e.g., bore Ø0.2 mm larger than the pin).
3. Add an explicit mate connector at the joint axis here too, so both parts carry their intent.
4. Model any pin/axle the joint needs (or plan to use a library shoulder screw as the pivot).

### Phase 3 — Assemble & ground (~1h)

1. New **Assembly** tab; rename it (e.g., `Project-Assembly-W4`).
2. **Insert** the host part; accept **Fix** (it's the ground).
3. Insert the moving component and any pin/axle.
4. **Fasten** the pin/axle to the host (if your joint uses a separate pin). Confirm it's locked.

### Phase 4 — The articulating mate (~1h)

1. Apply the **articulating mate** (Revolute / Slider / Cylindrical) between the moving component and the host (or pin).
2. **Predict the DOF, then drag-test.** Confirm the part moves exactly as intended — only swings, only slides, etc.
3. Add **limits** if the joint needs stops. Rename the mate.

### Phase 5 — Fastened component + library fastener (~1h)

1. Model or reuse a second component to **Fasten** (a cover, cap, or bracket), or simply add a **Standard Content fastener** as the fastened element.
2. Pull an appropriately-sized bolt/screw from the **Standard Content library**, size its hole, and **Fasten** it.
3. Rename everything.

### Phase 6 — Validate (~1.5h)

1. **Drag test:** ground doesn't move; moving part moves through its full range; locked parts stay locked.
2. **Interference detection** at both motion extremes and a couple of mid-poses — drive it to zero (fix geometry or tighten limits as needed).
3. **Measure** a key clearance (the swinging gap, the slide runout) to confirm it stays positive through the motion.
4. Re-confirm the **host part rebuilds clean** (change a host driving dimension, check, revert).

### Phase 7 — Walkthrough, version, share (~1.5h)

1. Write the **mate walkthrough** (below).
2. Create a **Version** named `week-04-assembly`.
3. Copy a **public share link** and confirm the assembly drag-tests and interference-checks clean on a fresh open.

---

## The mate walkthrough (required deliverable)

A Markdown file `mate-walkthrough.md` (or a text panel in the Document) that another student could read to understand your assembly cold. It must include:

1. **One paragraph** describing the assembly: what the mechanism is and what it does when it moves.
2. **A mate table** — one row per mate, in this exact shape:

   | Mate name | Type | Parts connected | DOF left | What it controls |
   |-----------|------|-----------------|---------:|------------------|
   | Frame ground | Fixed | Host part → Origin | 0 | grounds the assembly |
   | Arm pivot | Revolute | Arm → Pivot pin | 1 | arm swings 0–95° |
   | … | … | … | … | … |

3. **A DOF summary:** total assembly DOF and which part(s) carry it (e.g., "1 DOF — the arm swings; everything else is fully constrained").
4. **The validation evidence:** that you ran the drag test (state the result line) and interference detection (state the poses checked and the result).
5. **A "Week 5 improvements" note:** one or two things you'd configure or parameterize next week (you're forbidden from doing it now, but plan it).

---

## Example walkthrough excerpt

> **Mechanism:** a bracket-mounted swing arm. The bracket (Week 3 part) is the fixed frame. A shoulder screw pivots a flat arm that swings 0–95° to clear a panel. A library M5 cap screw fastens a cover plate to the bracket.
>
> | Mate name | Type | Parts connected | DOF left | What it controls |
> |-----------|------|-----------------|---------:|------------------|
> | Bracket ground | Fixed | Bracket → Origin | 0 | grounds the assembly |
> | Pivot screw | Fastened | Shoulder screw → Bracket | 0 | the arm's axle |
> | Arm swing | Revolute | Arm → Pivot screw | 1 | arm swings, limited 0–95° |
> | Cover bolt | Fastened | M5 cap screw → Bracket | 0 | retains the cover plate |
>
> **DOF summary:** 1 DOF total — only the arm moves (swing). Everything else is fully constrained.
> **Validation:** Drag test · 1 DOF · swings 0–95° · 0 interferences. Interference checked at 0°, 50°, 95° → zero. Min arm-to-panel gap measured at 95° = 1.4 mm.
> **Week 5 improvements:** configure the arm length (short/long variants) and the bracket bolt pattern via a Configurations table.

---

## Rubric

| Criterion | Weight | What "great" looks like |
|----------|-------:|-------------------------|
| Articulation correct | 25% | At least one joint moves with **exactly** the intended DOF; drag test confirms it; mate type matches the real joint |
| Mate choices & DOF reasoning | 20% | Right mate for each joint; the walkthrough's DOF table is accurate; nothing over- or under-constrained |
| Interference-free motion | 15% | Zero interference at both extremes and across the sweep; any intentional fit documented |
| Standard Content & fastening | 10% | A correctly-sized library fastener, holes sized to it; at least one clean Fastened mate |
| Reuses & preserves Week 3 part | 10% | Host part is genuinely the Week 3 part; it still rebuilds clean; not re-modeled from scratch |
| Naming & organization | 10% | Every instance and mate renamed; tidy instance list; sub-assembly used if it helps |
| Walkthrough quality | 10% | Someone unfamiliar can understand the mechanism and its DOF in <5 minutes |

---

## Stretch (optional)

- Encapsulate your moving joint in a **sub-assembly** and insert it into the parent, making it **flexible** — proving you can build the mechanism as a reusable unit (sets up the capstone).
- Add a **second articulating joint** (e.g., the arm carries a sliding stage) and re-validate the combined DOF.
- **Replicate** a bolt pattern around the cover so all fasteners are identical and correct in one operation.
- Add a **mate value sweep** and capture three screenshots (closed / mid / open) for your walkthrough.
- Add a **Ball** or **Pin-Slot** mate somewhere it genuinely belongs and explain the DOF it leaves.

---

## What this prepares you for

- **Week 5** dimensions and *configures* the key part of this assembly — you'll add a Variable Studio and a Configurations table to drive it into size variants, then produce a drawing package with a BOM. The library fastener you inserted this week already shows up in that BOM.
- **Week 6 (capstone)** is an original multi-part mechanism of 3+ parts that articulates via mates, includes a configured part, and ships a full drawing package. Every skill you used this week — grounding, the right mate, limits, sub-assemblies, interference validation — is exactly what the capstone is graded on. By Week 6 your reflex should be: "what's the ground, what moves, what mate gives it the DOF it needs, does it clear through the full range."

---

## Submission

When done:

1. Create a **Version** named `week-04-assembly` and copy a **public share link**.
2. Make sure `mate-walkthrough.md` (or the Document text panel) includes the mate table, DOF summary, and validation evidence.
3. Confirm the assembly **drag-tests to the intended DOF** and reports **0 interferences** on a fresh open of the shared link.
4. Post the public link in your cohort tracker. You built something that moves — show it.
