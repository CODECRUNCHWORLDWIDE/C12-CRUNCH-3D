# Lecture 2 — Multiplying Geometry: Linear & Circular Patterns, Mirror, Sweep, and Loft

> **Duration:** ~2 hours of reading + hands-on in OnShape.
> **Outcome:** You can populate a bolt-hole circle with a circular pattern, a vent grille with a linear pattern, and a symmetric part with a mirror — *without re-sketching anything*. You can sweep a profile along a path to make a handle or a pipe, and loft between two dissimilar profiles to make a transition. And you can reason about which of these tools to reach for, and how to keep each one parametric so a single dimension change rebuilds them all.

If you only remember one thing from this lecture, remember this:

> **Define a feature once; let OnShape make the copies.** The moment you find yourself drawing the same circle a second time, or the same vent slot, *stop* — you want a pattern or a mirror. Hand-copied geometry doesn't update when the design changes; a pattern does. One vent slot patterned twelve times is one feature to edit. Twelve hand-drawn slots are twelve bugs waiting to drift out of alignment.

Lecture 1 gave you the references to build on: planes, axes, mate connectors. This lecture gives you the *productivity multipliers* that turn one well-built feature into many. These are the features that make a part look "real" — the grille of holes, the ring of bolts, the swept handle, the lofted spout — and they are exactly where beginners either save hours or create unmaintainable messes, depending on whether they pattern or copy-paste.

---

## 1. The two ideas: pattern the *result*, or pattern the *seed*

Every "make copies" feature in OnShape works the same way conceptually: you pick a **seed** (the thing to copy) and a **rule** (how to place the copies). The seed can be:

- a **feature** (a hole, an extrude, a cut — "pattern feature"),
- a **face/body** (a boss, a solid — "pattern body"), or
- **sketch entities** (copy geometry inside a sketch — "sketch pattern").

For multi-feature parts you almost always want **feature pattern** (or **body pattern**): the copies stay live and parametric, tied to the seed. If you edit the seed hole's diameter, every patterned copy updates. That is the whole point.

> **Don't pattern in the sketch when you mean to pattern the feature.** A beginner trap: sketching twelve circles in one sketch (via sketch pattern) and extruding them all in one Hole feature. It works, but the twelve holes are now welded into a single feature you can't selectively edit, and you've lost the Hole feature's countersink/counterbore intelligence. Prefer: sketch *one* hole, make it a proper Hole feature, then **Circular pattern** that feature. One seed, one rule, full control.

---

## 2. Linear pattern

A **Linear pattern** copies the seed along one or two directions, evenly spaced.

The dialog fields:

- **Pattern type** — Feature / Face / Part.
- **Features to pattern** — pick the seed (e.g. your vent slot cut).
- **Direction 1** — pick an edge, axis, or plane normal that defines the first direction. The arrow shows which way; flip if needed.
- **Distance & instance count** — either "spacing between copies" or "total span" depending on the **Spacing** mode (`Spacing` = gap between each; `Up to` = fit N across a total length). Instance count *includes* the seed.
- **Direction 2** (optional) — a second direction for a 2-D grid.

Concrete walkthrough — a 4 × 3 vent grille of slots:

1. Model **one** slot: sketch a 3 × 12 mm slot (rounded rectangle) on the front face, Remove-extrude it through.
2. **Linear pattern** the slot feature.
3. **Direction 1** = the part's horizontal edge; **Spacing = 8 mm**, **Instances = 4**.
4. Turn on **Direction 2** = the vertical edge; **Spacing = 16 mm**, **Instances = 3**.
5. Green check. You now have 12 slots from one seed sketch.

Change the seed slot's width from 3 to 4 mm, or the spacing from 8 to 6 mm: **every** slot updates. That is twelve edits collapsed into one.

> **Centering a grid.** A 4-wide grid placed from one corner isn't centered on the face. Two clean fixes: (a) build the seed at the center and pattern symmetrically — OnShape's linear pattern has a **"Centered"/symmetric** option that grows the pattern both ways from the seed; or (b) drive the start position with a dimension tied to the face width and instance count so it stays centered when either changes. Centered grids survive resizing; corner-anchored grids drift.

---

## 3. Circular pattern

A **Circular pattern** copies the seed around an axis — the bread-and-butter tool for bolt-hole circles, lug nuts, fan blades, gear teeth blanks, and anything radial.

The dialog fields:

- **Features/faces/parts to pattern** — the seed.
- **Axis** — *the* critical input. Pick a **construction axis** (the named one you built in Lecture 1) or the axis of a cylindrical face. **This is why you built an explicit axis last lecture** — a robust circular pattern spins about a named axis, not a transient inference.
- **Angle & instance count** — either "equal spacing across N instances over an angle" (usually 360° for a full circle) or "angle between each instance."
- **Equal spacing** toggle — on for an evenly distributed ring.

Concrete walkthrough — a 6-bolt flange:

1. Build the centerline **Axis** through the flange's bore (Lecture 1).
2. Sketch **one** bolt hole on a bolt-circle radius (e.g. 45 mm from center), fully defined. Make it a **Hole** feature (clearance for M6).
3. **Circular pattern** the Hole feature.
4. **Axis** = `Bore axis`. **Angle = 360°**, **Instances = 6**, **Equal spacing = on**.
5. Green check. Six holes, evenly spaced, all driven by one seed.

Change the bolt count from 6 to 8: type 8, regenerate, done. Change the bolt-circle radius: edit the *seed* sketch's 45 mm dimension and all eight move outward together. A hand-placed bolt circle cannot do this; a patterned one does it for free.

> **The bolt-circle-diameter (BCD) trick.** Drive the seed hole's radial position with a variable, e.g. `#bcd = 90 mm`, and dimension the seed at `#bcd / 2`. Now BCD is a single named parameter. In Week 5 you'll put `#bcd` and the bolt count in a Configurations table and switch between a 4-bolt and 8-bolt flange from a dropdown. Reference-and-variable discipline this week is what makes configurability trivial later.

---

## 4. Mirror

**Mirror** reflects the seed across a plane or planar face. Use it whenever the part has a plane of symmetry — which is *most* mechanical parts.

The dialog:

- **Pattern type** — Feature / Face / Part.
- **Entities to mirror** — the seed feature(s) or the whole body.
- **Mirror plane** — a plane or planar face to reflect across.

Concrete walkthrough — mirror a bracket arm:

1. Model the left arm of a symmetric bracket: its boss, its hole, its fillet — the whole left half.
2. **Mirror** → type Feature, select all the left-arm features.
3. **Mirror plane** = the **Front** origin plane (the symmetry plane, if you centered the part on the origin in Lecture 1 — *this is why centering matters*).
4. Green check. The right arm appears, a perfect reflection, fully parametric.

Now edit the left arm's hole diameter: the right arm's hole follows. You maintain *half* the part; symmetry maintains the other half for free.

> **Mirror feature vs. mirror body.** Mirroring *features* reflects the construction steps and keeps everything as one continuous solid (good for a part that's symmetric but connected — a bracket). Mirroring the whole *body/part* gives you a separate mirrored solid (good for a true left/right handed *pair* — a left and right door bracket). Pick based on whether you want one symmetric part or two mirror-image parts. For this week's running project, feature mirror inside one part is the common case.

> **The mid-plane reference.** No convenient origin plane on the symmetry line? Build one: **Plane → Mid plane**, selecting the two outer faces (Lecture 1). That mid plane *is* the mirror plane. Symmetric modeling almost always pairs a mid-plane reference with a mirror feature.

---

## 5. Sweep

So far every feature has been a *straight* push (extrude) or a *spin* (revolve). **Sweep** drags a 2-D **profile** along a **path** — a curve that can bend in three dimensions. It's how you model handles, tubes, hoses, rails, gaskets that follow a non-straight outline, and trim that wraps a corner.

The two ingredients:

- A **profile** — a closed sketch (the cross-section). For a round handle, a circle; for a hollow tube, a circle with a smaller circle subtracted, or use a single profile and Shell after.
- A **path** — a continuous sketch or set of edges the profile follows. The path can be in a different plane than the profile.

The crucial reference detail: **the profile should sit on a plane that is perpendicular to the path at the path's start.** This is exactly the **Point–normal plane** from Lecture 1 — build a plane normal to the path at its start point, sketch the profile there, and the sweep starts clean. If the profile plane isn't perpendicular to the path, the sweep either fails or produces a skewed, self-intersecting mess at the start.

Concrete walkthrough — a swept handle for the running project:

1. **Path:** sketch the handle's centerline on the **Front** plane — say two vertical segments joined by a 180° arc (a U-shape), fully defined. This is the path. Finish the sketch.
2. **Profile plane:** the path starts at a point; build a **Plane → Point–normal**, point = the path's start vertex, normal = the path's starting tangent (pick the path edge). The plane is now perpendicular to the path.
3. **Profile:** sketch a Ø8 mm circle on that plane, centered on the path start. Finish.
4. **Sweep:** click **Sweep** → **Profile** = the circle, **Path** = the U-shape. Operation = **New** (or **Add** to fuse it to the part).
5. Green check. A round handle follows the U.

Sweep options worth knowing:

- **Keep profile orientation vs. follow path** — whether the profile twists to stay perpendicular as the path bends (almost always "follow path" / perpendicular, the default) or stays in a fixed orientation.
- **Twist** — spin the profile a number of turns along the path (springs, twisted cables, auger flights).
- **Multiple profiles along the path** — for a sweep whose section changes; this shades into Loft territory.

> **Sweep vs. Extrude.** If the path is straight, you don't need Sweep — Extrude is simpler and faster. Reach for Sweep only when the path bends. A "swept" straight boss is a code smell: someone over-reached for the fancy tool. Use the simplest feature that expresses the intent.

---

## 6. Loft

**Loft** blends between **two or more profiles** on **different planes**, creating a smooth transition surface between them. It's how you model a square-to-round duct transition, a boat hull, a faucet spout, a bottle shoulder, a chisel-to-handle blend — anything where the cross-section *changes shape* from one end to the other.

The ingredients:

- **Two or more profiles**, each a closed sketch, each on its own plane (use **Offset planes** from Lecture 1 to stack them).
- Optionally, **guide curves** that control the path the loft takes between profiles, and **connections** that pin matching points so the loft doesn't twist.

Concrete walkthrough — a square-to-round transition:

1. **Profile 1:** sketch a 40 × 40 mm square on **Top**, centered on the origin. Finish.
2. **Profile 2 plane:** build a **Plane → Offset** from Top, distance 60 mm. Rename `Loft top`.
3. **Profile 2:** sketch a Ø30 mm circle on `Loft top`, centered on the origin. Finish.
4. **Loft:** click **Loft** → add **Profile 1**, then **Profile 2** (order matters — pick them end-to-end). Operation = **New**.
5. Green check. A smooth square-to-round transition rises 60 mm.

Two things that bite beginners:

- **Twist.** If the loft connects the square's corner to a random point on the circle, the transition spirals. Use the **connection points / vertices** controls to pin "this corner of the square ↔ this point on the circle," forcing a clean, untwisted blend. OnShape shows draggable connection dots; align them.
- **Profile alignment.** Both profiles centered on the origin keeps the loft straight and symmetric. Off-center profiles produce a leaning transition (sometimes that's what you want — a cant — but usually it's an accident).

> **Loft vs. Sweep.** Sweep = *same* cross-section dragged along a path. Loft = cross-section that *changes* between profiles. If your section is constant, sweep. If it morphs, loft. Many organic shapes use both: loft the body, sweep the trim.

---

## 7. Choosing the right multiplier — a decision table

| You want… | Reach for… | Key reference it needs |
|-----------|-----------|------------------------|
| N copies in a row or a grid | **Linear pattern** | a direction edge/axis; center it for robustness |
| N copies around a center | **Circular pattern** | a **named construction axis** |
| A reflected, symmetric half | **Mirror** | a symmetry plane (origin plane or **mid plane**) |
| One section along a bent path | **Sweep** | a path sketch + a **point–normal profile plane** |
| A blend between different sections | **Loft** | two+ profiles on **offset planes**, connection points |

Notice the right-hand column: *every* multiplier depends on a reference you learned to build in Lecture 1. That's the through-line of the week — **references first, then multiply off them.** A pattern with no named axis, a sweep with no perpendicular profile plane, a mirror with no symmetry plane: these are the fragile parts that turn red on the first edit.

---

## 8. Keeping multiplied features parametric

The reason to pattern instead of copy is *parametric rebuild*. To keep that promise:

1. **Drive counts and spacings with variables**, not literals. `#vents = 12`, `#bolts = 6`, `#pitch = 8 mm`. Change one number, the whole pattern re-lays-out. In Week 5 these go straight into a Configurations table.
2. **Pattern the smallest correct seed.** Pattern the *Hole feature*, not a sketch full of circles. Pattern *one* fin, not a hand-built stack. The smaller and more semantic the seed, the more control you keep.
3. **Mind pattern-of-pattern order.** You can pattern a pattern (a circular pattern of a linearly-patterned cluster), but the tree gets subtle. Build and name carefully; group the pattern and its seed into a folder.
4. **Watch for instances that fall off the part.** A linear pattern of 6 across a face only 4 wide pushes two copies into empty space — they either fail or float. Tie the instance count or spacing to the face dimension so the pattern *fits* whatever size the face becomes.
5. **Suppress, don't delete, for variants.** Need a version with the vent grille omitted? Don't delete the pattern — *suppress* it (or wire it to a config in Week 5). Deleting destroys the parametric work; suppressing keeps it one click away.

---

## 9. The rebuild test, applied to multiplied features

The Week 2 rebuild test — flex two driving dimensions ±20%, nothing turns red — gets sharper this week because patterns can fail in new ways. When you flex a dimension on a multi-feature part, watch specifically for:

- **A pattern instance landing off the part** (count vs. size mismatch). Fix: tie count/spacing to size.
- **A circular pattern whose axis moved** because it referenced a transient face instead of a named axis. Fix: re-reference to the named construction axis.
- **A swept feature self-intersecting** because its profile is too big for the path's smallest radius (the section can't make the turn). Fix: shrink the profile or open up the path radius — and note the geometric limit in your walkthrough.
- **A loft twisting or collapsing** when a profile resizes past the other. Fix: re-pin connection points; keep profiles concentric.
- **A mirror breaking** because the mirror plane moved relative to the seed. Fix: anchor the symmetry plane to the origin so it never drifts.

A part that survives the ±20% flex *with patterns, a sweep or loft, and a non-default plane all present* is the deliverable bar for this week's mini-project. Build it reference-first and it'll pass; bolt features onto magic numbers and it won't.

---

## 10. A worked example: a finned heat sink

Tying it all together — the kind of part the challenge asks for. Narrate the references and multipliers:

1. **Base:** sketch a 60 × 60 mm square on **Top**, centered on origin; extrude 5 mm. *Origin reference, centered.*
2. **One fin:** sketch a 1.5 × 25 mm tall thin rectangle on the **Front** plane at one edge; extrude it the full 60 mm depth (or symmetric). *One seed fin.*
3. **Fin array:** **Linear pattern** the fin feature, Direction 1 = the base's X edge, `Instances = #fins (= 15)`, `Spacing = #pitch (= 4 mm)`, **centered** so the fin bank stays centered on the base. *One seed → fifteen fins, all parametric.*
4. **Mounting holes:** build the **Axis** of the part (origin Z), sketch one corner hole, **Circular/linear pattern** to four corners — or mirror twice across the two origin planes. *Named axis or symmetry planes.*
5. **Dress-up:** fillet the fin tips and chamfer the base edges (after the patterns, at the tail of the tree). *Dress-up last.*
6. **Mate connector:** place one on the base underside, Z normal, for Week 4. *Persistent reference frame.*

Rebuild test: change `#fins` from 15 to 20 and `#pitch` from 4 to 3 mm. The fin bank re-lays-out, stays centered, nothing red. Change the base from 60 to 70 mm: the centered fin pattern re-centers, the corner holes (if mirrored off the origin) follow. *One model, a family of heat sinks.* That is the standard this week aims for.

---

## 11. Pattern types in depth: feature vs. face vs. body vs. sketch

Every multiplier asks "what am I copying?" The answer changes what stays editable, so choose deliberately.

**Pattern a feature** (the default, and usually correct). You copy a *step in the recipe* — a Hole, an Extrude, a Cut. Each copy re-executes the feature, so changing the seed changes all copies, and the Hole feature keeps its counterbore/clearance intelligence. Pattern features whenever you can.

**Pattern a face.** You copy a *region of an existing solid* (a boss face and the material under it). Useful when the thing you want to multiply isn't cleanly one feature but is one face-set. Slightly less semantic than feature patterning; reach for it when feature patterning can't grab what you want.

**Pattern a part/body.** You copy a *whole solid body*. This is for repeated identical parts within one Part Studio (a tray of identical cells, a panel of identical bosses) and for making a true mirrored *pair* (left/right). The copies are separate bodies, which matters in Week 4 when each becomes its own assembly instance.

**Sketch pattern.** You copy *entities inside a sketch* (circles, lines) before any 3-D feature runs. This is the one to be careful with: it's fine for laying out a grid of *points* that a single Hole feature then consumes, but it's the wrong tool for multiplying finished features, because it welds the copies into the sketch with no per-instance control. Use sketch pattern for point grids; use feature pattern for everything with depth.

The rule of thumb: **pattern at the highest semantic level that captures your intent.** A bolt ring is "six of *this hole feature*," so pattern the feature. A repeated cell is "twelve of *this body*," so pattern the body. Dropping to sketch pattern when you meant feature pattern is the most common over-reach.

---

## 12. Patterning a pattern, and other compound moves

Real parts stack multipliers. A few patterns worth recognizing:

**Pattern of a pattern.** A vent panel might be a *linear* row of slots, *circular*-patterned around a hub — a fan-shaped grille. Build the linear pattern first (the row), then circular-pattern *that pattern* about the hub axis. The tree nests: the circular pattern's seed is the linear pattern's output. It works, but it gets subtle fast — name both patterns clearly and group them into a folder, or future-you won't untangle it.

**Mirror of a pattern.** Build a patterned feature set on one side, then mirror the whole set across the symmetry plane. Cheaper than patterning across the centerline directly, and it reads cleanly: "this bank of ribs, mirrored." Common on symmetric housings.

**Pattern then dress-up, never the reverse.** Always pattern the *raw* feature and apply fillets/chamfers *after*, across all copies at once. If you fillet the seed and then pattern, you multiply the fillet too — usually fine — but if the fillet's geometry depends on neighboring copies (a fillet that blends between adjacent fins), patterning a pre-filleted seed produces gaps or overlaps at the boundaries. Dress-up belongs at the tail of the tree, after the multipliers, where it can see the final shape.

**Suppress for variants, don't delete.** When you need "the same part but without the vent grille," *suppress* the pattern (right-click → Suppress) rather than delete it. Suppression is reversible and, in Week 5, wirable to a configuration. Deleting throws away the parametric work you'd just have to rebuild.

---

## 13. Sweep and loft: the advanced controls you'll actually reach for

The basic sweep and loft get you most of the way. A few controls separate a clean transition from a lumpy one.

**Sweep — follow path vs. keep orientation.** "Follow path" (the default) re-orients the profile to stay perpendicular as the path bends — correct for tubes, handles, and trim. "Keep orientation" holds the profile in a fixed direction, letting it shear relative to the path — niche, for things that must stay vertically aligned regardless of path tilt. When in doubt, follow path.

**Sweep — twist.** A twist value spins the profile a set number of turns along the path. One half-turn makes a Möbius-ish blade; many turns make a coil, an auger, or a coarse thread. Pair twist with a helical path for springs. Watch self-intersection: a fat profile with a tight twist overlaps itself.

**Loft — connection points.** The single most important loft control. The draggable dots tell OnShape which point on profile A maps to which point on profile B. Pin a square's four corners to four evenly-spaced points on the circle above and the blend is symmetric and untwisted. Leave them unpinned and OnShape guesses — often a spiral. Always check and pin connections on any non-trivial loft.

**Loft — guide curves.** A guide curve is a sketched edge that runs *along* the loft (corner-to-edge, up the side) and controls how the section interpolates between profiles — whether the blend bulges out, caves in, or runs straight. Guide curves turn a generic loft into a controlled, fair surface. You don't need them for a simple square-to-round, but they're how you tune a faucet spout or a hull.

**Loft — start/end conditions.** Tangency or curvature conditions at the first/last profile make the loft blend *smoothly* into adjoining faces instead of meeting them at a hard crease. Important for cosmetic/fluid surfaces; optional for structural parts. We touch surfacing lightly; for this week, "normal to profile" or "none" is fine.

---

## 14. Performance, instance counts, and when *not* to pattern

A pattern is parametric, which is a gift — but it's not free, and a few habits keep big parts fast and sane.

**Instance count is regeneration cost.** Every patterned instance is geometry OnShape recomputes on each rebuild. A 6-bolt ring is nothing; a 2-D grid of 40 × 40 = 1,600 instances will make the whole Part Studio sluggish, and every edit upstream pays that cost again. If you genuinely need a thousand identical features (a perforated sheet, a fine mesh), that's often a sign the geometry should be expressed differently — as a texture, a cosmetic thread, a simplified representation, or handled at manufacture rather than modeled instance-by-instance. Model the *intent*, not a brute-force copy of every hole.

**Don't pattern what a single feature can express.** A ring of holes is a circular pattern. But a *continuous* ring slot is just one revolved or swept cut — don't pattern 360 tiny segments to fake a groove. A row of identical teeth on a rack might be a pattern, or might be a single extrude of a repeating sketch profile. Ask whether one feature captures it before you reach for a multiplier.

**Mirror beats pattern-of-two.** For exactly two symmetric copies, a mirror is clearer and cheaper than a 2-instance linear pattern. Reserve patterns for "many"; use mirror for "the other half."

**Suppress heavy patterns while you work.** If a dense pattern slows down editing the rest of the tree, suppress it, do your upstream work, and unsuppress at the end. The pattern's definition is preserved; you just skip recomputing it on every intermediate edit.

The meta-point: a pattern is a tool for *expressing repetition you mean*, not a hammer for every repeated shape. The cleanest multi-feature parts use the fewest features that fully capture the design intent — and each of those features is parametric, named, and ordered to rebuild predictably.

---

## 15. A debugging walkthrough: "my pattern broke when I resized the part"

This is the single most common failure students hit this week, so let's walk a real fix end to end.

**The symptom.** You have a 5-column linear pattern of vent slots on a 120 mm panel. You widen the panel to 90 mm to test a smaller variant. Two slots now hang off the right edge in empty space, the pattern feature goes red, and three features below it inherit the error.

**Step 1 — find the cause, not the symptom.** The red pattern is the *victim*. Drag the **rollback bar** to just before the pattern. The panel and the seed slot are fine; the pattern is the first thing that breaks. So the cause is the pattern's *rule* — it places copies at a fixed 16 mm spacing regardless of panel size, and at 90 mm wide there isn't room for five.

**Step 2 — decide the intended behavior.** What *should* happen when the panel shrinks? Two reasonable intents: (a) keep five slots but tighten the spacing to fit, or (b) keep the spacing and reduce the count. Both are valid; pick one and encode it.

**Step 3 — encode it.** For intent (a): change the pattern from "spacing = 16 mm" to a spacing *derived* from the panel — e.g. drive spacing as `(panelWidth − 2 × #margin) / (#cols − 1)`, with the pattern **centered**. Now five slots always fit, evenly, with a margin, whatever the width. For intent (b): leave spacing fixed but make `#cols` itself a function of width, or simply accept a smaller count for the small variant via a configuration in Week 5.

**Step 4 — re-test the range.** Roll forward, regenerate, and flex the panel 90 → 120 → 150 mm. The slots re-lay-out, stay centered, none fall off, nothing red. *Now* it's robust.

**The lesson, generalized.** A pattern that breaks on resize almost always has a rule tied to a *constant* where it should be tied to the *thing it sits on*. The fix is to express the count or spacing as a function of the host dimension, and center it. This same diagnosis — rollback to find the cause, decide the intent, encode it as a relationship, re-test the range — works for circular patterns drifting off a moved axis, lofts twisting on a resized profile, and sweeps self-intersecting on a tightened path.

---

## 16. The Boolean question: do the copies merge, or stay separate?

Every multiplier quietly asks one more question you should answer on purpose: **when a copy lands on top of existing material, does it fuse, cut, or stand apart?** Patterns and mirrors inherit the operation of their *seed*, and that determines the answer.

- **A patterned Add feature fuses.** If the seed is an Add-extrude boss and the copies overlap each other or the base, OnShape merges them into one continuous solid. A linear-patterned rib bank that overlaps at the roots becomes one welded part — usually what you want for a structural array.
- **A patterned Remove feature cuts.** If the seed is a Remove-extrude (a vent slot, a bolt hole), each copy cuts independently. Overlapping cuts simply union their voids — fine.
- **A patterned New feature makes separate bodies.** If the seed created a *new* standalone body, each copy is its own body. That's correct for a tray of identical-but-separate cells (each becomes its own assembly instance in Week 4), and wrong if you meant one fused part. If you got separate bodies and wanted one solid, change the seed (or the pattern) to **Add**, or add a **Boolean → Union** at the tail of the tree.

The trap is patterning a **New**-bodied seed when you wanted a single fused solid, then being surprised in Week 4 that your "one part" shows up as fifteen instances. Decide up front: *one solid* (seed = Add, or Union after) versus *many bodies* (seed = New). Check the part list (the bodies panel) after any pattern to confirm you got the body count you intended — this 5-second check saves a confusing Week 4.

---

## 17. Recap

You should now be able to:

- Build a **linear pattern** (1-D and 2-D grids), keeping it **centered** so it survives resizing.
- Build a **circular pattern** about a **named construction axis**, driving count and BCD with variables.
- **Mirror** features (or bodies) across an origin or **mid plane**, maintaining symmetric parts from a single half.
- **Sweep** a profile along a bent path, starting the profile on a **point–normal plane**.
- **Loft** between two profiles on **offset planes**, pinning connection points to avoid twist.
- Pick the right multiplier for the job, keep it parametric with variables, and pass the rebuild test with patterns, a sweep/loft, and a non-default plane all in play.

You now have every tool the mini-project needs: references (Lecture 1) and the multipliers that ride on them (Lecture 2). Next, the exercises drill each one in isolation; the challenge combines them; the mini-project promotes your running part to a real multi-feature part.

---

## References

- *Linear pattern* — OnShape Help: <https://cad.onshape.com/help/Content/linearpattern.htm>
- *Circular pattern* — OnShape Help: <https://cad.onshape.com/help/Content/circularpattern.htm>
- *Mirror* — OnShape Help: <https://cad.onshape.com/help/Content/mirror.htm>
- *Sweep* — OnShape Help: <https://cad.onshape.com/help/Content/sweep.htm>
- *Loft* — OnShape Help: <https://cad.onshape.com/help/Content/loft.htm>
- *OnShape Learning Center — Patterning and Symmetry* (free, account required): <https://learn.onshape.com/learn/learning-path/cad>
- *Designing with design intent* — OnShape technical briefs: <https://www.onshape.com/en/resource-center>
