# Challenge 1 — Shelled Bottle or Cup from a Photo

**Time estimate:** ~120 minutes.

**You build this in:** a new Part Studio named `Challenge-Bottle` in your `C12-Week2` Document (or a fresh Document `C12-Week2-Challenge`), units = mm.

> **This is a CAD modeling challenge, not code.** You reverse-engineer a real object into a robust, shelled, revolved OnShape part.

---

## Problem statement

Pick a real bottle, cup, mug, vase, or jar from your kitchen. Photograph it from the side, dead-on, with a ruler or a known-size object (a credit card is 85.6 mm wide; a standard pop can is ⌀66 mm) in frame for scale. Then **model it in OnShape** as a single revolved, shelled part:

1. **Revolve** the body from a single fully-defined half-section sketched against the centerline axis.
2. **Shell** it to a **uniform wall thickness** with the top (mouth) open.
3. **Fillet** the base — both the outer base edge and, if the object has one, the inner base radius — using the correct fillet-vs-shell ordering.
4. **Reproduce the target** so a stranger could glance at your photo and your model side by side and say "yes, that's the same object."

Your model does not need to be dimensionally perfect — you're working from a photo, not a CAD file. It needs to be **proportionally faithful**, **uniformly walled**, and **robust to edits**.

---

## Required dimensions to capture from the real object

Measure (caliper ideal, ruler fine) and write these into your sketch as driving dimensions:

| Measurement | How to take it |
|-------------|----------------|
| Overall height | Base to mouth rim |
| Max body diameter | Widest point of the body |
| Neck / mouth diameter | The opening |
| Base diameter | The footprint where it sits |
| One intermediate diameter | At a shoulder or waist, to capture the curve |
| Wall thickness (estimate) | Look at the rim; typical glass 2–4 mm, plastic 1–2 mm |

Use **arcs and tangent constraints** (not a polyline of straight segments) for the curved shoulder and body — a bottle's profile is smooth, and tangency between arcs is what makes it look real instead of faceted.

---

## Suggested order of operations

### Phase 1 — Scale and trace (~30 min)

1. Optionally **import the photo** as a reference: in a sketch, use **Insert image** (right-click in a sketch → *Insert image*, or the image tool) and scale it using your known reference object so 1 mm in the photo = 1 mm in OnShape. This lets you trace directly over it.
2. Start a sketch on the **Front** plane. Draw the **vertical construction-line axis** from the origin.
3. Trace the **right half** of the silhouette with lines (straight sections), **arcs** (curved shoulder/body), and **tangent** constraints between them. Keep the whole profile to the right of the axis.
4. Add your measured **driving dimensions**. Drive the sketch to **fully defined (black)**. This is the hardest part — budget time for it.

### Phase 2 — Revolve solid (~10 min)

5. `Shift+R`, **New**, **Full**, axis = the construction line. You now have a **solid** body in the rough shape of the bottle. Rename `Body`.

### Phase 3 — Fillet the base, correctly ordered (~20 min)

6. Decide: do you want the base round carried through to the *inside* after shelling? For most bottles, **yes** — fillet the outer base edge **before** shelling so the inside base is also rounded.
7. Fillet the **outer base edge** (radius to match the photo, e.g. 3–8 mm). Rename `Base fillet`. Keep this **above** the shell in the feature list.

### Phase 4 — Shell to a uniform wall (~20 min)

8. **Shell**, remove the **top mouth face**, thickness = your measured wall (e.g. 2.5 mm). Rename `Wall`.
9. **Verify uniformity:** `right-click a face → Section view` through the axis. The wall must read constant everywhere. If it breaks through at a tight shoulder, your wall is thicker than the local radius allows — reduce thickness or soften the shoulder arc.

### Phase 5 — Detail + verify (~20 min)

10. Add any remaining detail the object has: a **chamfered or filleted mouth rim** (after the shell — surface-only), a slight **neck taper**, a punt (the dimple in a wine-bottle base — a small revolve-remove). Rename each.
11. Run the **rebuild test** (below).

---

## Acceptance criteria

- [ ] A single revolved, shelled part in `Challenge-Bottle`.
- [ ] The body is made from **one Full revolve** of a **fully-defined** half-section that uses at least one **tangent arc**.
- [ ] The half-section lies **entirely on one side of the axis** and the axis is **construction geometry**.
- [ ] The part is **shelled to a uniform wall**, top open, and you have a **section-view screenshot** proving the wall is uniform with no breakthrough.
- [ ] The **base is filleted**, with the fillet ordered **before** the shell so the inside base is also rounded.
- [ ] Every feature is **renamed**; the feature list is short and ordered base → fillet → shell → surface detail.
- [ ] **Rebuild test passes:** with the part open, edit the **overall height by ±20%** and the **wall thickness by ±1 mm**; **no feature turns red**, the wall stays uniform, the base stays filleted.
- [ ] A short write-up (in a text note or the Document's notes) covering: the object you chose, the six measurements, your chosen wall thickness, and **why your fillet is before the shell**.

---

## Stretch

- Model the bottle's **screw-cap thread** cosmetically (a helix sweep) — you'll learn Sweep formally in Week 3, but try it; thread profiles are a great Sweep test case.
- Add a **handle** (for a mug) as a separate swept body and Boolean-Add it. Note where it must blend (fillet) into the body.
- Make the part a **family** in spirit: identify the *one* driving variable (height, or a scale factor) that, when changed, gives you a small/medium/large version that still looks right. (Formal Configurations are Week 5 — here, just prove one variable scales it cleanly.)
- Reproduce the **base punt** as a partial revolve-remove and confirm it doesn't break the uniform wall.

---

## Hints

<details>
<summary>My traced profile won't go fully defined</summary>

Curved profiles are the hardest to define. Two tricks: (1) make adjacent arcs **tangent** to each other and to the straight sections — each tangency removes a degree of freedom; (2) dimension arc **radii** and the **endpoints' distances from the axis**. If something is still blue, drag it — whatever moves is what's unconstrained.

</details>

<details>
<summary>The shell broke through the wall at the shoulder</summary>

The local radius of curvature at the shoulder is smaller than your wall thickness, so the inner offset self-intersects. Either reduce the wall thickness, or open up (increase the radius of) the tight shoulder arc. This is a real manufacturing constraint, not just a CAD quirk — a too-thick wall on a tight curve can't be molded either.

</details>

<details>
<summary>Should the base fillet be before or after the shell?</summary>

If you want the **inside** of the base rounded (almost always, for a bottle), fillet **before** the shell — the shell then offsets the rounded base inward, rounding both surfaces. Fillet **after** the shell only rounds the outer skin, and a base fillet bigger than the wall will turn red. Before-the-shell is the right answer here.

</details>

---

## Submission

1. In OnShape, **Versions and history → Create version**, name it `Challenge submission`.
2. Share the Document link (free-plan documents are public) and paste it in your cohort tracker under Week 2 Challenge.
3. Attach your **photo** and your **section-view screenshot** so a reviewer can compare fidelity and verify the uniform wall.

## Why this matters

Reverse-engineering a real object from a photo is one of the most common professional CAD tasks: a client hands you a competitor's part, a legacy component with no drawings, or a hand-made prototype, and says "make this in CAD, parametric, so we can iterate." Everything in this challenge — tracing a smooth profile, revolving it, shelling to a uniform wall, ordering the base fillet correctly, and proving it survives edits — is exactly that job in miniature.
