# Lecture 2 — Revolves, Holes, and Dress-Up Features: Fillet, Chamfer, Shell, Draft

> **Duration:** ~2 hours of reading + hands-on.
> **Outcome:** You can revolve a profile a full 360° or a partial angle around the correct axis to make turned parts; place manufacturing-correct holes with the dedicated Hole feature; and apply fillets, chamfers, shells, and draft in an order that keeps the part rebuildable and manufacturable.

If you remember one thing from this lecture, remember this:

> **Extrude and Revolve make the *shape*. Hole, Fillet, Chamfer, Shell, and Draft make the part *manufacturable*.** A block with a sketched-circle cut "looks like" it has a hole; a part with a *Hole feature*, a chamfered edge, a filleted base, and a shelled interior is something a shop can actually make. Dress-up features carry intent the raw shape does not.

---

## 1. Revolve: spin a profile around an axis

Extrude pushes a profile in a straight line. **Revolve** spins it around an axis. Anything rotationally symmetric — a knob, a pulley, a shaft, a wheel, a bottle, a bushing, a turned table leg — is fastest to model as a revolve, because you draw only *half the cross-section* and let the spin do the rest.

Press `Shift+R` (or the Revolve toolbar icon). The dialog mirrors Extrude:

| Field | What it controls |
|-------|------------------|
| **Operation type** | New / Add / Remove / Intersect — same four verbs as Extrude. |
| **Sketch region to revolve** | The profile (the half cross-section). |
| **Revolve axis** | The line the profile spins around. |
| **Revolve type** | Full (360°) / One direction (angle) / Symmetric (angle split both ways). |
| **Angle** | The sweep, when not full. |

### The one rule you cannot break

**The profile must not cross the axis.** The cross-section sits entirely on one side of the axis line. If your profile straddles the axis, the revolve self-intersects and OnShape errors. Think of it physically: you're spinning a flat shape; if part of it is on the far side of the spin line, the two halves collide. Draw the half-section to one side, put the axis on the centerline, spin.

### Choosing the axis

The axis can be:

- **A sketch line** drawn as part of (or as construction geometry in) the same sketch — the most common choice. Draw a vertical construction line on the centerline and revolve around it.
- **A linear edge** of existing geometry.
- **A Mate connector / origin axis** (the Y axis, say) — clean when your profile is already centered on an origin plane.

> **Pro habit:** sketch the profile against an **origin plane** with the **axis on an origin axis**. Then the turned part is automatically centered on the origin, which makes Week 4 assembly mating trivial. A knob whose axis *is* the Z axis drops into an assembly far more easily than one floating off-origin.

### A worked revolve: a stepped knob

Units: mm. New Part Studio.

1. Sketch on the **Front** plane. Press `n` to face it.
2. Draw a **vertical construction line** from the origin straight up, ~30 mm (this is the axis). 
3. To the *right* of that line, draw the half-section of a knob: a base 18 mm wide and 6 mm tall, stepping in to a 10 mm-wide shaft 14 mm tall, with a small 1 mm chamfer line at the top corner. Dimension every segment; constrain the bottom edge to the origin and the left edge of the profile coincident-but-offset is fine — what matters is the profile is closed, fully defined, and entirely right of the construction line.
4. `Shift+R`. **New**. Revolve axis: pick the construction line. Type: **Full**. Green check.
5. You now have a turned knob — drawn as a 2D half-section, solid in 3D. Rename: `Knob body`.

### Partial revolves

Set the type to **One direction** and an angle (say 270°) and the profile sweeps only part way — leaving a wedge cut out. Useful for cam profiles, partial pulleys, pie-slice brackets, and any part that's *almost* rotationally symmetric. **Symmetric** splits the angle evenly about the sketch plane, the same idea as a symmetric extrude.

### Thin revolves

Like extrude, revolve has a **thin** option: revolve an *open* profile into a thin-walled turned shape — a cone, a funnel, a thin cup — without sketching both walls. A single slanted line, revolved thin, becomes a cone shell. Handy, though for uniform-wall cups we usually revolve solid then **Shell** (below), which is more forgiving to edit.

---

## 2. The Hole feature: why not just cut a circle?

You *can* make a hole by sketching a circle and doing a Remove extrude — and for a plain pin hole that's fine. But for real fastener holes, OnShape's dedicated **Hole feature** is the right tool, and here's why.

A Hole feature is *manufacturing-aware*. It knows the difference between a clearance hole and a tapped hole. It carries **standard sizes** from real tables (ISO metric, ANSI inch). It encodes **counterbore** and **countersink** geometry as parameters, not as hand-drawn steps. And it produces holes the downstream **drawing** (Week 5) can annotate automatically with proper callouts (⌀, depth, thread). A sketched-circle cut carries none of that intent — it's just a round hole-shaped void.

### Opening the Hole dialog

Select one or more flat faces, invoke **Hole** (toolbar, or `Shift`+search). You pick:

| Choice | Options |
|--------|---------|
| **Hole type** | Simple / Counterbore / Countersink (and tapped variants) |
| **Standard** | ISO metric, ANSI, etc. — drives the size tables |
| **Profile / size** | e.g. M4 clearance, M5 tapped, ⌀6.5 |
| **Fit** | Close / Normal / Loose clearance (changes the drilled diameter) |
| **End condition** | Blind (with depth) / Through all / Up to next, etc. |
| **Location** | Sketch points, or on-face placement you constrain |

### Simple, counterbore, countersink — when to use each

- **Simple (clearance) hole:** a plain through-hole sized so a bolt passes through with the right slop. An **M4 normal clearance** hole is ⌀4.5 — bigger than the M4's 4 mm nominal so the bolt slides through. Use for the part the bolt *passes through*.
- **Tapped hole:** threaded so a bolt screws *into* it. An **M4 tapped** hole is drilled to the tap-drill size (⌀3.3 for M4) and threaded. Use for the part the bolt *threads into*. (OnShape models the cosmetic thread; you don't sketch the helix.)
- **Counterbore:** a flat-bottomed larger recess at the top of a hole so a **socket-head cap screw**'s cylindrical head sits flush or below the surface. Specify the screw size and OnShape sizes the bore and depth from the standard.
- **Countersink:** a *conical* recess so a **flat-head screw** sits flush. The cone angle (typically 82° or 90°) comes from the standard.

> **The 60-second decision tree.** Bolt passes *through* this part? → clearance (simple). Bolt threads *into* this part? → tapped. Need the head to sit flush and it's a cap screw? → counterbore. Flush and it's a flat-head? → countersink.

### Locating holes

Two robust patterns:

1. **Place a sketch of points first** (a sketch containing only construction points, fully defined relative to edges), then invoke Hole and pick those points. The points carry the location; the Hole carries the size. Editing one doesn't disturb the other. This is the clean, professional pattern.
2. **Place on a face** and constrain the location in the Hole dialog. Faster for a one-off.

For a **bolt circle** (several holes evenly spaced on a circle), sketch one point, dimension it on the circle, and pattern it (Week 3's circular pattern) — or place a few points by hand this week. We do real patterns next week; for now, place each point and fully define it.

### A worked Hole: counterbore the bracket

Take the bracket from Lecture 1 (base plate, boss, pocket).

1. Sketch a single **point** on the top face, dimensioned 15 mm from the left edge and centered top-to-bottom. Fully define it. Close the sketch.
2. Invoke **Hole**. Type **Counterbore**. Standard **ISO metric**. Size **M4** (a socket-head cap screw). End condition **Through all**. Pick the point. 
3. OnShape drills a ⌀4.5 clearance hole with a counterbore sized for an M4 cap-screw head, all the way through. Green check. Rename: `M4 counterbore`.
4. Rebuild test: thicken the base plate — the Through-all hole and its counterbore stay correct.

---

## 3. Fillet: round the edges

A **Fillet** rounds an edge. On a *convex* (outside) edge it removes material to make a rounded corner; on a *concave* (inside) edge it *adds* material to make a smooth blend. Press `Shift+F`, select edges (or whole faces, or whole bodies), set a radius.

Fillets matter for more than looks:

- **Stress.** Sharp internal corners concentrate stress; a fillet spreads it. The inside corner where a boss meets a plate *wants* a fillet.
- **Manufacturing.** A milled internal corner *cannot* be perfectly sharp — the cutter is round. Modeling the fillet that the tool will leave makes the model honest.
- **Safety / feel.** Rounded outside edges don't cut hands.

### Constant, multiple, variable, full-round

- **Constant radius:** one radius on all selected edges. The default.
- **Multiple radii in one feature:** select different edge sets and give each its own radius — still one feature in the list, which keeps the tree short.
- **Variable radius:** the radius changes along a single edge (e.g. 2 mm at one end, 6 mm at the other). Add radius "points" along the edge.
- **Full round:** replaces a narrow face entirely with a half-round (a rounded rib top), driven by the two side faces rather than a radius number.

### Tangent propagation

When you fillet one edge, OnShape can **propagate** along all edges *tangent* to it, so a fillet follows around a smooth contour without you clicking every segment. Watch the preview: if it grabs too much or too little, toggle tangent propagation in the dialog.

> **The order trap.** *Where* in the feature list a fillet lives changes everything. Fillet an edge, then later cut a hole through that edge, and the fillet may break (lost reference) or look wrong. The rule: **build the shape first, dress it up last.** Fillets and chamfers near the bottom of the feature list. We come back to this in §7.

> **The radius-vs-wall trap.** A fillet radius larger than the material it sits in produces zero-thickness or self-intersecting geometry and turns the feature red. A 5 mm fillet on a 4 mm wall cannot exist. Keep fillet radii sensible relative to nearby wall thickness — a good rule is radius ≤ ~0.8 × the thinnest adjacent wall.

---

## 4. Chamfer: bevel the edges

A **Chamfer** is a *flat* angled cut across an edge — a bevel, not a round. Where a fillet is an arc, a chamfer is a straight 45°-ish slice. Three definition modes:

- **Equal distance:** the chamfer cuts the same distance back on both faces — the classic symmetric 45° break. Specify one distance (e.g. 1 mm). Most common.
- **Two distances:** different setbacks on each face — an asymmetric bevel. Specify both.
- **Distance and angle:** one setback plus an angle — for non-45° bevels.

When do you chamfer vs fillet? **Chamfer** for: lead-ins on a hole or shaft so a bolt/pin starts easily; deburring sharp edges (a "1 × 45°" break is the shop-standard "break all sharp edges"); seating surfaces for countersunk hardware. **Fillet** for: stress relief at internal corners, smooth ergonomic outside edges, cast/molded blends. A good part typically has *chamfers on functional lead-ins and small edge-breaks*, and *fillets at structural corners*.

---

## 5. Shell: hollow it out

**Shell** scoops a solid hollow to a uniform **wall thickness**, optionally leaving selected faces open. This is how a solid revolved cup becomes a *cup* (thin walls, open top), how a solid block becomes an *enclosure* (thin walls, open bottom for the lid).

The dialog:

| Field | What it controls |
|-------|------------------|
| **Faces to remove** | The faces left *open* (the mouth of the cup, the open back of an enclosure). Pick none and you get a sealed hollow shell. |
| **Thickness** | Uniform wall thickness (e.g. 2 mm). |
| **Per-face thickness** | Optional overrides — make one wall thicker than the rest. |
| **Direction** | Shell inward (default, keeps outer dimensions) or outward. |

### A worked shell: a cup

Take the knob revolve from §1 — or better, revolve a tall mug profile:

1. Revolve a solid mug body (a tall ⌀80 × 100 mm cylinder with a domed base, say).
2. Invoke **Shell**. **Faces to remove:** click the *top* face (the mouth). **Thickness:** 3 mm.
3. Green check. The solid is now a 3 mm-walled open cup. Orbit and look inside (`right-click a face → Section view` to peek through the wall).

### The shell-vs-fillet ordering question (important)

Suppose you want a cup with a **rounded base on the inside**. If you **fillet the inside base edge first, then shell**, the shell wraps the fillet and you get a clean uniform-thickness rounded inner corner. If you **shell first, then fillet**, you're filleting a thin-walled edge and can easily exceed the wall thickness (zero-thickness error). 

The general principle: **fillets that should be carried through the wall go *before* the shell; fillets that are purely on the outer surface go *after*.** Think about whether you want the round on the solid (before shell) or just on the skin (after shell). This is the single most common ordering decision when shelling, and the challenge this week leans on it.

### Per-face thickness

Real parts often need one thick wall (a boss-mounting face) and thin walls elsewhere. Add a **per-face thickness override** in the Shell dialog: select the face, give it its own thickness. One shell feature, non-uniform walls. Cleaner than two features.

---

## 6. Draft: the taper that lets a part release

**Draft** applies a slight angular taper to faces. Why would you *want* tapered walls? Because **molded and cast parts cannot release from a mold with perfectly vertical walls** — they'd lock in. A degree or two of draft on every wall in the pull direction lets the part pop out. Injection-molded plastic, die-cast metal, and even some 3D-printed parts benefit.

The Draft dialog needs:

- **Neutral plane** (or parting line): the reference where the wall keeps its original size; the taper grows away from it.
- **Pull direction:** the direction the mold opens.
- **Draft angle:** typically **1°–3°** for injection molding; more for deep or textured walls.
- **Faces to draft:** the walls to taper.

You won't draft most coursework parts (we mostly 3D-print, which tolerates vertical walls), but you **must** know what draft is and when it's required, because the moment you design a part to be injection-molded, every external wall needs draft or the tooling won't work. Add draft *after* the main shape, *before or after* fillets depending on whether the rounds should taper too.

---

## 6b. A field guide to choosing the right dress-up feature

When you finish the rough shape of a part, you face a series of small decisions: round this, bevel that, hollow here, taper there. Here is the decision tree the pros run almost without thinking.

**Is this edge an internal corner that will carry load?** → **Fillet** it. Sharp internal corners are stress risers; cracks start there. A generous fillet (radius ≥ ~0.5 × the adjoining wall) spreads the load. The corner where a rib meets a wall, where a boss meets a floor, where a handle meets a body — fillet, always.

**Is this edge a sharp outer edge a hand will touch?** → **Fillet** (for a soft, rounded feel) or **chamfer** (for a crisp, deliberate edge). Consumer products lean fillet; machined tool-and-die parts lean chamfer. Either beats a raw sharp edge that cuts fingers and chips in handling.

**Is this the mouth of a hole or the end of a shaft that something must slide into?** → **Chamfer** it as a lead-in. A `0.5–1 mm × 45°` chamfer at a hole mouth lets a pin or bolt self-center as it enters. Without it, the pin catches on the sharp lip and you fight every assembly.

**Does the part need to be hollow (a housing, a cup, a duct)?** → **Shell** it. Decide the wall thickness from the material and process (injection-molded plastic 1.5–3 mm; FDM 3D print ≥ 2 mm / ≥ 3 perimeters; sheet-metal-like parts to the gauge). Choose which faces stay open.

**Will this part be injection-molded or die-cast?** → **Draft** every face in the pull direction, 1–3°. No draft, no part — the tooling can't release it.

**Is this just a sharp edge nobody cares about, but the shop wants it broken?** → a tiny `0.5 mm` **chamfer** or fillet as a blanket "break all sharp edges." This is so standard that drawings often just write "BREAK ALL SHARP EDGES 0.5 MAX" instead of dimensioning each one (Week 5).

Run that tree on every part and you'll never ship a raw, sharp-edged block again.

---

## 6c. Worked dress-up sequence on the knob

Let's make the dress-up decisions concrete on the Exercise-2 knob (a ⌀40 base flange stepping to a ⌀22 grip, 28 mm tall, with a ⌀6 shaft bore).

1. **Lead-in chamfer at the shaft bore mouth.** The knob presses onto a ⌀6 shaft. Add a `0.75 × 45°` chamfer at the bore opening so it self-centers onto the shaft. (Chamfer, because it's a sliding lead-in.)
2. **Fillet where the grip meets the flange.** That internal step is a stress concentration every time you twist the knob. A 2 mm fillet there spreads the torque. (Fillet, internal load-carrying corner.)
3. **Chamfer the top rim of the grip.** A `1.5 × 45°` break — crisp, deliberate, comfortable, and it removes the molding witness edge. (Chamfer, deliberate outer edge.)
4. **Fillet the bottom outer edge of the flange.** A 1 mm fillet so the flange doesn't scratch the panel it sits against. (Fillet, soft contact edge.)

Notice every choice traces to a *reason* — load, lead-in, feel, contact — not "it looked nicer." That's the difference between a designer and someone pushing the fillet button. And notice all four dress-up features come *after* the shape and bore features in the list, which is the rule we formalize next.

---

## 7. Feature order and design intent (the throughline)

Every feature this week — extrude, revolve, hole, fillet, chamfer, shell, draft — runs in feature-list order. The order is a *design decision*, not an accident. The default professional ordering:

1. **Base feature** (the New extrude/revolve that defines the rough mass).
2. **Add features** (bosses, ribs, pads).
3. **Remove features** (pockets, slots, holes — the Hole feature here).
4. **Shell** (hollow it).
5. **Dress-up** (fillets, chamfers) — *last*, except fillets you deliberately want carried through the shell.
6. **Draft** (if molded) — usually before dress-up so rounds can sit on tapered walls.

> **Why "dress-up last."** Fillets and chamfers reference *edges*. Edges move when you change the shape above them. Put dress-up at the bottom and a shape edit reruns cleanly; put a fillet early and every later cut risks orphaning it. The C12 reflex: model the mass, cut the holes, hollow it, *then* break the edges.

This ordering is also what makes the **rebuild-on-edit test** pass. A part ordered base → add → remove → shell → fillet survives a ±20% dimension change far more reliably than one with fillets scattered through the middle of history.

---

## 8. A complete part, start to finish

Let's put it all together: an enclosure base.

1. **Base (New extrude):** sketch an 80×60 mm rounded-rectangle on Top, extrude **Symmetric? no** — Blind **30 mm** up. Rename `Body`.
2. **Mounting bosses (Add extrude):** sketch four ⌀8 mm circles in the corners on the top face, Add, **Up to next**? — here just Blind to a height; rename `Bosses`. (Better still, *Up to face* a lid plane — but Blind is fine for now.)
3. **Tapped holes (Hole feature):** place four points centered on the bosses, Hole → **M3 tapped**, Blind 10 mm. Rename `M3 mounts`.
4. **Shell:** remove the **top** face, thickness **2.5 mm**. Rename `Shell`. Note the bosses survive as solid posts inside the thin shell — exactly what mounting bosses are for.
5. **Fillet (dress-up, last):** fillet the four outside vertical edges, 3 mm, and break the top rim with a 0.5 mm chamfer. Rename `Edge breaks`.
6. **Rebuild test:** change the body height 30 → 45 mm. Bosses, holes, shell, and fillets all regenerate clean. Change wall thickness 2.5 → 4 mm. Still clean (because 4 mm < the 8 mm boss and < the fillet's room). 

That part — sketched, extruded, bossed, drilled, shelled, filleted, and *proven to rebuild* — is a manufacturable enclosure base. It's also essentially the mini-project shape, so this walkthrough is your warm-up.

---

## 9. Common failures and their fixes

| Symptom | Likely cause | Fix |
|---------|--------------|-----|
| Revolve errors immediately | Profile crosses the axis | Move the profile fully to one side of the axis |
| Revolve makes a weird sliver | Profile not closed, or two regions | Ensure one closed region, fully defined |
| Fillet turns red | Radius ≥ adjacent wall, or referenced edge gone | Shrink the radius; or roll back and re-pick edges |
| Shell turns red | Thickness ≥ thinnest feature it must carve | Reduce thickness, or add per-face override; check feature order vs fillets |
| Hole in wrong spot after edit | Located off a face/edge that moved | Locate holes off a stable sketch of points instead |
| Whole part vanishes after a Remove | Cut consumed the entire body | Check end condition (Through all on a thin part); check merge scope |

The diagnostic loop is always the same (from Lecture 1, §11): **roll back, find the feature just below the bar, edit it, roll forward.**

---

## 9b. Designing holes that match real fasteners

A hole is only useful if a real screw fits it, so a quick reference for the metric sizes you'll use all course. (The Hole feature fills these in automatically when you pick a standard size and fit — but knowing the numbers means you can sanity-check the dialog and read a drawing.)

| Screw | Tap-drill (for a *tapped* hole) | Normal clearance (for a *through* hole) | Counterbore ⌀ for cap-screw head | Cap-screw head ⌀ (approx) |
|-------|-------------------------------:|----------------------------------------:|---------------------------------:|--------------------------:|
| M2    | ⌀1.6 | ⌀2.4 | ⌀4.0 | ⌀3.8 |
| M3    | ⌀2.5 | ⌀3.4 | ⌀6.0 | ⌀5.5 |
| M4    | ⌀3.3 | ⌀4.5 | ⌀8.0 | ⌀7.0 |
| M5    | ⌀4.2 | ⌀5.5 | ⌀10.0 | ⌀8.5 |
| M6    | ⌀5.0 | ⌀6.6 | ⌀11.0 | ⌀10.0 |

Read it as: the part the screw **threads into** gets the **tap-drill** size; the part the screw **passes through** gets the **clearance** size; a **counterbore** is sized so the cap-screw head drops below the surface. The Hole feature knows all of this — your job is to pick *tapped vs clearance* correctly (the §2 decision tree) and let the standard do the arithmetic.

One practical caution: **fit class matters.** "Close" clearance for M4 is ⌀4.3, "Normal" is ⌀4.5, "Loose" is ⌀4.8. Tighter fits locate the part precisely but are less forgiving of misalignment; looser fits assemble easily but let the part shift. For coursework, **Normal** is almost always right. For a part that must locate precisely (a dowel-pinned joint), you'd use a tighter fit — a Week 4 concern.

---

## 10. Recap

You should now be able to:

- **Revolve** a half-section around a sketch line or origin axis, full or partial angle, respecting the "profile must not cross the axis" rule.
- Use the **Hole feature** and choose **simple / counterbore / countersink / tapped** with standard sizes, locating holes off a stable points sketch.
- Apply **Fillet** (constant, multiple, variable, full-round) with tangent propagation, keeping radii sane relative to wall thickness.
- Apply **Chamfer** (equal-distance, two-distance, distance-and-angle) for lead-ins and edge breaks.
- **Shell** to a uniform wall thickness, choosing removed faces, and reason about **shell-vs-fillet ordering**.
- Know what **Draft** is and when a molded part requires it.
- Order features **base → add → remove → shell → dress-up** so the part rebuilds clean.

That's the full toolkit for single-body part modeling. Next week we build geometry *off other geometry* — construction planes, patterns, mirror, sweep, and loft. Bring your mini-project part; we promote it to a multi-feature part in Week 3.

## One-page mental checklist for dress-up and shelling

Tape this next to the extrude checklist from Lecture 1. Before you finish a part:

1. **Holes** — clearance where the bolt *passes through*, tapped where it *threads in*; counterbore/countersink only if the head must sit flush. Located off a *fully-defined points sketch*, not a free circle.
2. **Internal load-carrying corners** — filleted? (Stress relief.)
3. **Sliding lead-ins** (hole mouths, shaft ends) — chamfered?
4. **Sharp outer edges** — broken with a small fillet or chamfer?
5. **Hollow part** — shelled to a uniform wall, correct faces removed, verified in a *section view*?
6. **Fillet-vs-shell order** — fillets that should carry through the wall placed *before* the shell; surface-only dress-up placed *after*?
7. **Molded/cast part** — drafted in the pull direction (1–3°)?
8. **Feature list** — ordered base → add → remove/holes → shell → dress-up, every feature renamed?
9. **Rebuild test** — flexed the two driving dimensions ±20% with *zero red features*?

If every box is ticked, you've shipped a real part — not a 3D doodle.

---

## References

- *Revolve* — OnShape Help: <https://cad.onshape.com/help/Content/revolve.htm>
- *Hole* — OnShape Help: <https://cad.onshape.com/help/Content/hole.htm>
- *Fillet* — OnShape Help: <https://cad.onshape.com/help/Content/fillet.htm>
- *Chamfer* — OnShape Help: <https://cad.onshape.com/help/Content/chamfer.htm>
- *Shell* — OnShape Help: <https://cad.onshape.com/help/Content/shell.htm>
- *Draft* — OnShape Help: <https://cad.onshape.com/help/Content/draft.htm>
- *ISO metric screw thread reference*: <https://en.wikipedia.org/wiki/ISO_metric_screw_thread>
