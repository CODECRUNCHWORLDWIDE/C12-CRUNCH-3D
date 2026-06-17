# Mini-Project — From Master Sketch to Finished Solid Part

> Take the fully-defined master sketch you delivered in Week 1 and promote it into a **finished, manufacturable solid part**: extrude (or revolve) it to real thickness, add at least one mounting hole, dress it up with fillets and chamfers, and — the part that matters most — prove it **rebuilds cleanly** when you change its driving dimensions. Deliver the part plus a step-by-step modeling walkthrough.

This is the second installment of the **running project** that grows every week of C12. Week 1 gave it a master sketch. This week it becomes a 3D part. Week 3 makes it multi-feature (planes, patterns). Week 4 mates it into an assembly. Week 5 dimensions and configures it. Week 6 ships it as part of the capstone. Each week builds on the last *artifact*, not from scratch — so do this well; you'll live with this part for five more weeks.

**Estimated time:** ~12 hours (split across Thursday through Sunday in the suggested schedule).

---

## Starting point (compounds on Week 1)

You should already have, from Week 1:

- An OnShape Document containing a **fully-defined master sketch** of your chosen part — a name plate, a flat washer-style part, a bracket profile, or whatever flat part you committed to.
- A short written note explaining every constraint and dimension and why the sketch is fully defined.

If your Week 1 sketch is thin or under-defined, **fix it first.** A 3D part is only as good as the sketch under it. Re-open it, drive it black, and make sure the dimensions you'll want to edit (overall size, hole positions) are real driving dimensions, not accidents of where you clicked.

> **If you're joining C12 at Week 2** and have no Week 1 sketch: spend the first hour creating one. Sketch a flat part — a 100 × 60 mm name plate, or a 4-bolt mounting bracket profile — on the Top plane, fully defined, before continuing. The rest of this brief assumes that sketch exists.

---

## What you will deliver

A single OnShape Part Studio containing **one finished solid part** that:

1. Is built **from your Week 1 master sketch** (extrude it, or revolve it if your part is rotationally symmetric).
2. Has a real **thickness / depth** appropriate to the part (a name plate ~3–5 mm; a bracket ~6–10 mm).
3. Has **at least one mounting hole**, placed with the **Hole feature** (simple/clearance or counterbore), located off a stable points sketch.
4. Has **fillets and/or chamfers** applied for manufacturability — at minimum, break the sharp edges; ideally fillet a structural corner.
5. **Rebuilds clean** under the C12 rebuild test (see Acceptance Criteria).
6. Ships with a **step-by-step modeling walkthrough** that another student could follow to reproduce your part.

Plus a created **Version** of the Document, and a shared public link.

---

## Rules

- **You may** use any OnShape Part Studio feature covered in Weeks 1–2: Sketch, Extrude (all operations and end conditions), Revolve, Hole, Fillet, Chamfer, Shell, Draft, Boolean.
- **You may NOT** use features from later weeks yet — **no patterns, no mirror, no sweep/loft, no construction planes beyond the origin planes, no assemblies/mates.** Those arrive in Week 3–4 and you'll add them then. Keep this week's part to single-body, origin-plane modeling. (If your part *screams* for a mirror, note it in your walkthrough as a "Week 3 improvement" — don't add it yet.)
- **Single body.** One solid part this week.
- **Units: millimeter.** Length precision 2–3 decimals.
- **Every feature renamed.** A feature list of `Extrude 1 / Fillet 2` is an automatic deduction.
- **Every driving sketch fully defined (black).**

---

## Acceptance criteria

- [ ] A Part Studio (in your running-project Document) named clearly, e.g. `Part-v2-solid`.
- [ ] The part is built **from your Week 1 master sketch** — the sketch is visibly the base feature's profile, not a fresh redraw. (Reuse the sketch; edit it if needed, but it traces to Week 1.)
- [ ] The part has a real **thickness/depth** via an Extrude or Revolve with a deliberately-chosen **end condition** (and you can say why you chose it).
- [ ] **At least one mounting hole** via the **Hole feature**, located off a **fully-defined points sketch** (not a free-floating circle).
- [ ] **At least two dress-up features** total (e.g. one fillet + one chamfer, or two fillets) applied for manufacturability, ordered **after** the shape features.
- [ ] If the part should be hollow (an enclosure, a cup-like part), it is **shelled to a uniform wall**; if it's a solid plate-type part, shelling is optional.
- [ ] **Every feature is renamed** meaningfully; the feature list is short and ordered base → add → remove/hole → (shell) → dress-up.
- [ ] **Every driving sketch is fully defined (black).**
- [ ] **The rebuild test passes** (this is graded heavily — see below).
- [ ] A created **Version** named `Week 2 mini-project` and a shared public link.
- [ ] A **walkthrough** (in the Document notes, or a separate Markdown/PDF) that includes everything in the "Walkthrough requirements" section below.

### The rebuild test (mandatory, heavily weighted)

1. Identify your part's **two most important driving dimensions** (e.g. overall length and thickness, or outer diameter and bore).
2. With the part open, **edit each by roughly ±20%** and regenerate.
3. **No feature may turn red.** The part must stay manufacturable — no zero-thickness walls, no holes that miss material, no fillets that vanish, no features floating in space.
4. **Document this** in your walkthrough: state which two dimensions you tested, the values you tried, and a one-line confirmation that the part rebuilt clean. If something *did* break and you fixed it, describe the fix — that's worth more than a part that never broke.

---

## Suggested order of operations

### Phase 1 — Prep the sketch (~1h)

1. Open your Week 1 Document. Create a **new Part Studio** for the v2 solid (keep the original sketch intact for reference, or branch the Document — `Versions and history → Create version`, then branch).
2. Bring in / re-create the master sketch on the Top (or Front, for a revolve) plane. **Drive it fully defined.**
3. Make sure the dimensions you'll want to flex (overall size, hole pitch) are clean **driving dimensions**.
4. Create a Version: `Sketch ready for solid`.

### Phase 2 — The base solid (~2h)

5. **Extrude** (or **Revolve**) the master sketch to real thickness. Choose the end condition deliberately — **Symmetric** if the part should straddle a center plane, **Blind** if the thickness is the design value. Rename the feature.
6. Orbit it. Does it look like a real part? Adjust the thickness until it does.

### Phase 3 — Holes (~2h)

7. Sketch your **mounting-hole points**, fully defined relative to the part's edges. (If your part has multiple holes in a pattern, place them by hand this week — patterns are Week 3.)
8. Use the **Hole feature**: pick simple/clearance for a bolt that passes through, or counterbore for a flush cap screw. Pick a real size (M3/M4/M5). Through all (or blind, deliberately). Rename.

### Phase 4 — Dress-up (~2h)

9. **Fillet** the structural corners (internal corners especially) and **chamfer** the lead-in edges / break the sharp ones. Apply these **last** in the feature list (except any fillet you deliberately want carried through a shell). Rename each.
10. If your part is hollow, **Shell** it now (before the surface-only dress-up, after any carried-through fillets).

### Phase 5 — Rebuild test + repair (~2h)

11. Run the rebuild test. Flex your two driving dimensions ±20%. 
12. If anything turns red: **roll back, find the feature just below the bar, fix the reference or relax the dimension, roll forward.** Make the part robust. This phase is where the grade is won.
13. Re-tidy: rename anything unnamed, delete dead sketches, confirm every sketch is black.

### Phase 6 — Walkthrough + version + share (~3h)

14. Write the walkthrough (requirements below).
15. **Versions and history → Create version**, name it `Week 2 mini-project`.
16. Share the public link. Paste it and the walkthrough into your cohort tracker.

---

## Walkthrough requirements

Your written walkthrough must let another student reproduce your part with no other context. Include:

1. **One paragraph** describing the part and what it's for.
2. **A numbered feature-by-feature build sequence** — for each feature: its name, the operation/end condition, the key dimensions, and *why* you chose that approach (e.g. "Through all so the hole survives a thickness change").
3. **The two driving dimensions you flexed** in the rebuild test, the values you tried, and confirmation the part rebuilt clean (or the bug you found and fixed).
4. **One thing you'd do differently** now that you've built it — and one thing you're saving for Week 3 (a mirror, a pattern, a feature on a non-default plane).
5. **The public OnShape link** to the versioned Document.

---

## Example: what "done" looks like

Suppose your Week 1 part was a **rectangular equipment name plate**, 100 × 40 mm, with four corner mounting-hole positions in the sketch. A strong Week 2 deliverable:

- `Plate body` — Extrude the plate profile, **Blind 4 mm** (the engraved-plate thickness is the design value, so Blind is right). 
- `Mount points` — a points sketch, four positions 6 mm in from each corner, fully defined.
- `M4 clearance` — Hole feature, M4 normal clearance, **Through all** (survives a thickness change).
- `Corner fillets` — 3 mm fillet on the four outer vertical edges (handling, looks finished).
- `Edge break` — 0.5 mm chamfer on the top face perimeter (deburr).

Rebuild test: length **100 → 120 mm** and thickness **4 → 5 mm** — holes still through, fillets fine, plate still flat. Zero red features. Walkthrough explains each choice. Version created, link shared. **That's a full-marks mini-project.**

---

## Rubric

| Criterion | Weight | What "great" looks like |
|----------|-------:|-------------------------|
| Built from Week 1 sketch | 10% | The base feature visibly traces to the Week 1 master sketch, edited but not redrawn from scratch |
| Correct solid + end condition | 20% | Extrude/Revolve with a *deliberately chosen* end condition, justified in the walkthrough |
| Hole feature done right | 15% | Real fastener size, located off a fully-defined points sketch, sensible Through/Blind choice |
| Dress-up for manufacturability | 15% | At least two fillets/chamfers, ordered correctly (last; carried-through fillets before shell) |
| **Rebuild robustness** | **25%** | Passes the ±20% rebuild test on two driving dimensions with zero red features; bugs found are diagnosed and fixed |
| Feature-list quality | 10% | Short, ordered, every feature renamed, every sketch black |
| Walkthrough quality | 5% | A stranger could reproduce the part from it; design choices are explained, not just listed |

---

## What this prepares you for

- **Week 3** promotes this exact part to a *multi-feature* part: you'll add a pattern or mirror and at least one feature on a non-default plane, and audit the feature tree for design-intent ordering. The cleaner your tree is now, the easier that is.
- **Week 4** mates this part into an assembly with one or two companion parts you'll model. A part that's centered on the origin (symmetric extrude!) mates far more easily.
- **Week 5** dimensions and *configures* this part — variables and a configuration table to spin it into a family of sizes. A part that already passes the rebuild test configures cleanly; a fragile one fights you.
- **Week 6** folds it into the capstone mechanism.

Build it to last. You'll thank yourself in five weeks.

---

## Submission

1. **Versions and history → Create version**, named `Week 2 mini-project`.
2. Confirm the part **rebuilds clean** on the versioned copy (open the version, flex the two driving dimensions, no red).
3. Share the public Document link.
4. Post the link **and** the walkthrough in your cohort tracker under Week 2 mini-project. You did real engineering; show it.
