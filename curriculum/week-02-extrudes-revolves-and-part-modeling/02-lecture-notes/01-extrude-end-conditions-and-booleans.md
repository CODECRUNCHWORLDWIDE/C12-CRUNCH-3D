# Lecture 1 — From 2D to 3D: Extrude, End Conditions, and Boolean Solids

> **Duration:** ~2 hours of reading + hands-on.
> **Outcome:** You can extrude a profile as a New, Add, Remove, or Intersect operation; pick the correct end condition (Blind, Symmetric, Through all, Up to face/next/vertex) and explain why; control the merge scope of a Boolean; and read the feature list as a replay engine that rebuilds when you edit a dimension.

If you remember one thing from this lecture, remember this:

> **An extrude is not "make a box." An extrude is a verb that takes a profile, a direction, an end condition, and an operation, and either creates a new solid or modifies an existing one.** Those four inputs — profile, direction, distance/condition, operation — are the whole feature. Master them and you have mastered most of solid modeling.

---

## 1. The feature list is a replay engine

Open a Part Studio. On the left is the **feature list** (sometimes called the feature tree). In Week 1 it held only sketches. This week it fills with features: Extrude 1, Fillet 1, Shell 1.

Here is the single most important idea in parametric CAD, and the reason it beats "mesh modeling" in tools like Blender for engineering work:

**The part you see on screen is not stored as a fixed shape. It is computed by replaying the feature list from top to bottom, every time anything changes.**

When you create:

```
Origin planes (Top, Front, Right)
Sketch 1        ← a rectangle, 80 × 50 mm, on the Top plane
Extrude 1       ← New, Blind, 10 mm, from Sketch 1
```

OnShape does not save "a 80×50×10 block." It saves "draw this rectangle, then push it up 10 mm." When you later open Sketch 1 and change 80 to 120, OnShape **regenerates**: it re-draws the rectangle at 120, then re-runs Extrude 1, and the block is now 120×50×10. Every downstream feature reruns too. This is *regeneration* (also called *rebuild*), and it is why we obsess over building parts that survive edits.

The **rollback bar** is the blue line at the bottom of the feature list. Drag it up and the model rewinds to that point — features below the bar are temporarily suspended. You use it for two things: (1) **diagnosing** where a part broke (roll back until the error disappears; the feature just below the bar is the culprit), and (2) **inserting** a feature in the middle of history (roll back, add the feature, roll forward).

> **Why this matters for design intent.** Because features replay in order, *the order you create them in is part of the design.* A fillet created before a hole behaves differently from a fillet created after it. We will return to this constantly. For now: features run top to bottom, edits propagate downward, and order is meaningful.

---

## 2. The anatomy of the Extrude dialog

Press `Shift+E` (or click the Extrude toolbar icon) with a sketch profile selected. The dialog has these fields. Learn them by name; this is the vocabulary of half of all CAD.

| Field | What it controls |
|-------|------------------|
| **Operation type** | New / Add / Remove / Intersect — what the extrude *does* to the model. |
| **Faces and sketch regions to extrude** | The profile(s). One closed region, several, or even a part face. |
| **Direction** | Which way to push. A flip button reverses it. |
| **End condition** | How far: Blind, Symmetric, Through all, Up to next, Up to face, Up to vertex, Up to part. |
| **Depth** | The distance, when the condition needs one (Blind, Symmetric). |
| **Second end position** | An optional *second* direction/condition, so one extrude grows both ways with different limits. |
| **Draft** | An optional taper applied as you extrude (covered in Lecture 2). |
| **Merge scope** | For Add/Remove: which existing bodies this operation may touch. |

A clean first extrude reads like a sentence: *"**New** body, extrude this **rectangle**, **Blind**, **10 mm**, in the **up** direction."*

---

## 3. The four operation types

This is the conceptual core of the lecture. Every solid feature in OnShape — Extrude, Revolve, Sweep, Loft — offers the same four operations. Learn them once here and they transfer everywhere.

### New

**New** creates a brand-new solid body, independent of anything already in the Part Studio. Your *first* feature in a part is almost always a New extrude (or New revolve). If you extrude a profile that sits in empty space as New, you get a fresh body.

### Add (union)

**Add** fuses the extruded material into an existing body, like welding a boss onto a plate. The result is one body. Use Add when you sketch on top of an existing part face and push up to make a raised feature (a boss, a rib, a mounting pad). The two volumes become one — there is no seam, no internal wall.

### Remove (subtraction)

**Remove** subtracts the extruded volume from an existing body — it *cuts*. This is how you make pockets, slots, through-holes (when you don't use the Hole feature), and windows. The extruded profile defines the shape of the hole; the end condition defines how deep the cut goes.

### Intersect

**Intersect** keeps only the volume where the extrude *overlaps* an existing body and discards everything else. It is the least-used of the four day to day, but it is the elegant answer to certain problems — for example, trimming a tall boss so it conforms to a curved top, or carving a part to the intersection of two profiles (the classic "two-view" carving trick). 

> **The mental test.** Ask: *do I want new material standing alone (New), more material fused on (Add), material taken away (Remove), or only the overlap kept (Intersect)?* That question chooses the operation every time.

---

## 4. End conditions — how far the extrude goes

The operation says *what* the extrude does. The **end condition** says *how far*. Choosing the right one is the difference between a part that survives edits and one that breaks the first time you change a dimension. Here is the full set, with the engineering judgement for each.

### Blind

Go a fixed distance — say 10 mm — in the chosen direction. Simplest, most common, and a perfectly good default when the depth is a real design number you want to control directly.

- **Use when** the depth is itself a meaningful, controlled dimension (a 10 mm plate thickness).
- **Watch out:** a Blind depth is a *number*, not a *relationship*. If a Blind boss must always reach a top face and you later make the part taller, the boss will fall short. That is a job for *Up to face* or *Up to next*.

### Symmetric

Extrude the *same* distance in both directions from the sketch plane. A 10 mm symmetric extrude is 5 mm each way. Invaluable when you sketch on the **Front** or **Right** origin plane and want the part centered on it — which keeps your part symmetric about the origin, which keeps mirroring and assembly mating sane later.

- **Use when** the part should straddle the sketch plane evenly. This is the pro move for symmetric parts: sketch on a center plane, extrude symmetric.

### Through all

Cut or extrude through *everything* in the direction chosen, with no fixed distance. Most useful as a **Remove** condition for through-holes and slots that must pass completely through the part no matter how thick it becomes.

- **Use when** a cut must always pass fully through. Make the bolt-clearance slot *Through all* and it stays a through-slot even if you triple the plate thickness. A Blind cut at "exactly the current thickness" silently becomes a blind pocket the moment you thicken the plate. This is a classic rookie defect.

### Up to next

Stop at the *next* face the extrude encounters in its path. 

- **Use when** you want a boss or cut to stop at the first wall it hits, and you want that to keep working as geometry moves.

### Up to face (Up to surface)

Stop precisely at a face (or plane) you select. The extrude length becomes a *relationship* to that face, not a number — move the face and the extrude follows.

- **Use when** a feature must always meet a specific surface, including a curved or angled one. A boss that must always reach a domed top: extrude *Up to face*, pick the dome. Edit the dome height and the boss tracks it. This is design intent expressed as geometry.

### Up to vertex

Stop at the depth of a selected vertex (point). Niche but handy when a feature's depth is defined by some other point in the model rather than a face.

### Up to part

Stop at a selected solid body. Useful in multi-body Part Studios when you want one body's extrude to terminate at another's surface without picking a specific face.

> **The robustness rule of thumb.** Prefer *relationship* conditions (Up to face / next / part) over *number* conditions (Blind) whenever the feature's real intent is "meet that thing." Use Blind only when the distance is genuinely the design value you want to own. Every "Up to…" condition you choose is one fewer dimension that goes stale when the part changes.

### The second end position

The Extrude dialog has a **Second end position** toggle. Turn it on and the extrude grows in *both* directions with *independent* conditions. Example: a shaft that must run 20 mm one way (Blind) and *Up to face* the other. One feature, two conditions. Cleaner than two separate extrudes, and it keeps the feature list short.

---

## 5. A worked example: base, boss, pocket

Let's build a small bracket so the four operations and the conditions are concrete. Units: millimeters. Follow along in a fresh Part Studio.

**Feature 1 — the base plate (New, Blind).**

1. Sketch on the **Top** plane. Draw a rectangle, corner-to-corner, and dimension it **80 mm × 50 mm**. Add a coincident constraint putting one corner on the origin (or, better, center it on the origin with two symmetric constraints so it straddles the Front and Right planes). Fully define it — black sketch.
2. `Shift+E`. Operation **New**. End condition **Blind**, depth **8 mm**, direction up. Click the green check.
3. You now have an 80×50×8 mm block. Rename the feature `Base plate` (double-click its name in the feature list).

**Feature 2 — a raised boss (Add, Blind).**

1. Click the top face of the base. Press `n` (normal-to) to look straight down at it. Start a new sketch *on that face*.
2. Draw a circle, ⌀30 mm, dimensioned and located 25 mm from the left edge and centered top-to-bottom. Fully define it.
3. `Shift+E`. Operation **Add** (OnShape auto-selects Add because you sketched on an existing body). End condition **Blind**, **6 mm**. Green check.
4. The boss is now fused to the plate — one body. Rename: `Boss`.

**Feature 3 — a pocket (Remove, Blind).**

1. Sketch on the top face again. Draw a rounded-rectangle slot, 40 mm × 16 mm, located in the right half of the plate, fully defined.
2. `Shift+E`. Operation **Remove**. End condition **Blind**, **5 mm** (a blind pocket, not a through-cut). Confirm the direction arrow points *into* the part.
3. Green check. You now have a 5 mm-deep pocket. Rename: `Pocket`.

**Feature 4 — a through-window (Remove, Through all).**

1. Sketch a 12 mm circle near the boss. `Shift+E`, Remove, **Through all**. Green check. A clean through-hole — and because it's Through all, it stays a through-hole if you thicken the base later.

Now do the **rebuild test**: open `Base plate`'s sketch and change the plate from 8 mm... wait, the *thickness* is the extrude depth, so open `Base plate` and change **8 mm → 16 mm**. Regenerate. The boss still adds, the through-window still goes all the way through (because it's Through all), but the **5 mm blind pocket stays 5 mm** — exactly as intended. If you had instead made the through-window a *Blind 8 mm* cut, it would now be a blind pocket. That difference is the whole point of choosing end conditions deliberately.

---

## 6. Boolean solids and the merge scope

Add, Remove, and Intersect are **Boolean operations** — the set algebra of solids: union, difference, intersection. OnShape also exposes a standalone **Boolean** feature (under the toolbar, or `Boolean` in the feature search) that combines *existing* bodies, separate from extrude. Same three verbs.

The subtle field is **merge scope**. When you Add or Remove, OnShape needs to know *which existing bodies* the operation may affect. By default it affects all of them in its path; you can restrict the scope to specific bodies.

- **Why it matters:** in a multi-body Part Studio (you'll model two bodies that later become two parts), a Remove cut that *should* only pierce body A might also clip body B if both are in its path. Set the merge scope to body A only, and B is protected.
- **In single-body parts** (most of this week) merge scope is automatic and you can ignore it. But know the field is there; the day a cut eats a body it shouldn't, merge scope is your fix.

> **Multi-body Part Studios, in one sentence.** OnShape lets one Part Studio hold *several* solid bodies. Each body becomes a separate part you can pull into an Assembly later. The Boolean operations and merge scope are how you keep those bodies correctly separate or correctly fused. We lean on single-body parts this week and reach for multi-body work in Weeks 3–4.

---

## 7. Sketch reuse and "use" geometry

A single sketch can feed *several* features, and one feature can consume *part* of a sketch. If your sketch has two closed regions, the Extrude dialog lets you pick one, the other, or both. This is why disciplined Week 1 sketching pays off now: a clean, fully-defined sketch with well-separated regions extrudes predictably.

You can also extrude *part of a part's face* directly (no sketch) by selecting a planar face — handy for quick bosses. But the robust habit is: **sketch, constrain, then extrude.** A sketch is editable, dimensioned, and rebuildable; a face-selection extrude is more fragile when geometry moves.

The **Use** (project/convert) tool (Week 1) pulls existing edges into a new sketch as reference. When you sketch a boss on a face and want it to share an edge with the face below, *Use* that edge so they stay linked. Just be aware: a *Use*-d edge creates a **reference** to the geometry it came from, and references can break if that geometry is later deleted — the number-one cause of red features. We diagnose exactly that failure on Friday.

---

## 8. Thin extrudes

The Extrude dialog has a **thin** option that extrudes an *open* profile (or offsets a closed one inward/outward) to a wall thickness rather than filling the whole region. A single line extruded "thin" by 2 mm becomes a 2 mm-thick wall. This is occasionally the cleanest way to make a wall, gusset, or sheet-like feature without sketching both sides of it. We mostly shell to get thin walls (Lecture 2), but thin extrude is the right tool when the wall isn't a uniform offset of a closed solid.

---

## 9. Reading the direction arrow (and flipping it)

Every extrude shows a direction arrow in the graphics area. Two habits will save you grief:

1. **Look at the arrow before you click the check.** For a Remove, the arrow must point *into* the material. For an Add boss, it must point *away* from the face, out into space. The flip button (or dragging the arrow) reverses it.
2. **Use the on-screen drag handle** to set Blind depth interactively, then type the exact number in the dialog. Dragging gives you the gross sense; typing gives you the dimension you can defend later.

---

## 9b. The Intersect operation, in practice

Intersect is the operation beginners skip and pros reach for at exactly the right moment. Two concrete uses make it click.

**Use 1 — trim a boss to a curved top.** You have a base body whose top is a dome. You want a rectangular boss that stands proud of the base but whose top conforms *exactly* to the dome. Naively you'd fight with "Up to face." A clean alternative: extrude the boss tall and straight (overshooting the dome), then create a second body that is the dome's volume, and **Intersect**. Only the overlap survives — the boss is automatically trimmed to the dome. One operation, no fragile face reference.

**Use 2 — the two-view carving trick.** Old draftsmen carved a complex shape by cutting it from two directions. In CAD: extrude profile A (the side view) as a tall solid, extrude profile B (the front view) as another tall solid crossing it, and **Intersect** the two. What remains is the solid that satisfies *both* silhouettes — a fast way to model organic shapes like a computer-mouse shell or a hand grip from two orthogonal sketches. Intersect is the operation that makes this a single, robust feature.

The mental signature of Intersect: *"keep only where these two overlap; throw away the rest."* When you catch yourself wishing you could "trim this to the shape of that," Intersect is usually the answer.

---

## 10. Renaming features and why we insist on it

A feature list of `Extrude 1`, `Extrude 2`, `Extrude 3`, `Sketch 4` is unreadable in a week. Double-click each feature and rename it for *what it is*: `Base plate`, `Boss`, `Bolt pocket`, `Drain hole`. 

This is not cosmetic. When a feature turns red, the error references the feature *by name*. When a teammate (or future-you) opens your part to edit it, named features are the difference between five minutes and an hour. C12 grades feature-list readability in the mini-project; start the habit now.

---

## 11. Diagnosing a red feature (preview of Friday)

When OnShape can't compute a feature, it turns **red** and shows an error icon. The most common causes you'll meet this week:

- **Lost reference.** A feature pointed at a face/edge/vertex that a *later edit* deleted or moved out from under it. (E.g., you *Used* an edge, then changed the sketch that owned that edge.)
- **Zero-thickness / self-intersecting geometry.** A fillet radius bigger than the wall it sits on; a shell thicker than the part; a pocket that breaks the body into disconnected pieces unexpectedly.
- **Empty profile.** A Remove that no longer overlaps any material after an edit, so there's nothing to cut.

The fix is always the same workflow: **drag the rollback bar up** until the red clears, look at the feature *just below* the bar, **edit it** to repair the reference or relax the dimension, then roll forward. We'll drill this on Friday; for now, know that red is recoverable and the rollback bar is your scalpel.

---

## 11b. Multi-region sketches and the "what gets extruded" question

A single sketch often contains more than one closed region. A rectangle with a circle inside it has *two* regions: the disc, and the ring (rectangle-minus-circle). When you invoke Extrude on that sketch, OnShape asks which region(s) you mean, and you click the ones you want filled. This is enormously powerful and a little dangerous.

- **Powerful**, because one well-built sketch can drive several features. Sketch a faceplate outline *and* its cutout circles once; extrude the faceplate region as the body, then later Remove the circle regions. The locations stay linked because they share one sketch.
- **Dangerous**, because if you don't watch which region you select, you can fill the wrong area — extruding the disc when you meant the ring. Always glance at the highlighted region before clicking the check.

The discipline: **keep sketches as simple as the feature needs, and name them.** A sketch called `Faceplate outline` extruded by `Faceplate body` reads as intent. A sketch called `Sketch 7` with six regions, three of which feed different features, is a debugging nightmare three weeks later. When in doubt, split into two sketches — sketches are cheap, confusion is expensive.

> **The "sketch once, reference often" tension.** There's a real trade-off here. Sharing one sketch across features keeps locations linked (move a hole in the sketch, every feature that used it moves). But it also couples those features — edit the sketch wrong and several features break at once. The professional default: share a sketch when the features genuinely must stay co-located (a bolt pattern), and separate them when they're independent. You'll develop a feel for this; for Week 2, lean toward *one sketch per feature* and graduate to shared sketches as you get comfortable.

---

## 11c. A note on units, precision, and "nice numbers"

OnShape stores geometry in full precision internally; the **display precision** (decimals shown) is just how many digits the dimension field rounds to. Set it under `⚙ → Workspace units`. Three things to internalize:

1. **Model in the units the part is specified in.** A metric fastener part is modeled in mm. Mixing mm and inch in one part is a recipe for "why is this hole 0.04 mm off" rounding ghosts.
2. **Prefer round, intentful numbers.** A wall of `2.5 mm` is a decision; a wall of `2.4837 mm` is an accident (usually from dragging instead of typing). Type your dimensions.
3. **Tiny gaps and overlaps kill Booleans.** Two faces that are supposed to be coincident but sit `0.001 mm` apart can make an Add fail to merge or a Remove leave a sliver. When a Boolean misbehaves, suspect a near-miss coincidence first — fully-defined sketches (Week 1's discipline) are the cure.

This is why we were so strict about *fully-defined, intentionally-dimensioned* sketches in Week 1. Sloppy sketches don't just look bad; they produce Booleans that fail in ways that are genuinely hard to debug.

---

## 12. The "rebuilds clean" test, formalized

Here is the C12 standard you will be held to all course. After building any part:

1. Identify the part's one or two most important **driving dimensions** (overall length, wall thickness, bolt-circle diameter — whatever a real design change would touch).
2. **Edit each by roughly ±20%** and regenerate.
3. **No feature may turn red.** The part must remain manufacturable (no zero-thickness walls, no features hanging in space).
4. Restore the original values.

A part that passes this is a *parametric model*. A part that fails it is a one-off shape that happens to look right. We build the former.

---

## 12b. Extrude vs the other base features: when *not* to extrude

Extrude is the workhorse, but reaching for it reflexively is a beginner tell. Before you extrude, ask whether the part's *nature* suggests a different base feature:

- **Rotationally symmetric** (knob, pulley, shaft, bottle, wheel, lens)? → **Revolve** (Lecture 2). You draw half the cross-section instead of fighting to extrude-and-cut a round shape.
- **Constant cross-section that follows a path** (a pipe, a handle, a trim molding, a cable channel)? → **Sweep** (Week 3). Extruding can't follow a curved path; sweep can.
- **Cross-section that *changes* along its length** (a boat hull, a transition duct, an ergonomic grip)? → **Loft** (Week 3) between two or more profiles.
- **A genuinely prismatic shape** (a plate, a block, a bracket, a gear blank)? → **Extrude**. This is most parts, which is why extrude feels like the default.

Choosing the right base feature is the single biggest lever on whether your feature list stays short and editable. A round knob built as "extrude a cylinder, then cut six steps and a chamfer with Remove extrudes" might take eight features and break on every edit; the same knob as one Revolve is one feature that rebuilds instantly. We're extrude-only this week by design — but keep the others in your peripheral vision, because half of "modeling skill" is *picking the feature that makes the part trivial.*

---

## 13. Recap

You should now be able to:

- Read the feature list as an ordered replay engine and use the rollback bar.
- Open the Extrude dialog and name every field.
- Choose **New / Add / Remove / Intersect** by asking what you want the material to do.
- Choose an **end condition** by asking whether the limit is a *number* (Blind/Symmetric) or a *relationship* (Up to face/next/part) — and prefer relationships for robustness.
- Use **Through all** for cuts that must always pass through.
- Understand **merge scope** as the control over which bodies a Boolean touches.
- Rename features and run the **rebuild-on-edit** test.

Next up: spinning profiles into turned parts, and the dress-up features that make a part manufacturable. Continue to [Lecture 2 — Revolves, Holes, and Dress-Up Features](./02-revolves-holes-and-dress-up-features.md).

## One-page mental checklist for every extrude

Tape this to your monitor for the week. Before you green-check any Extrude, run it:

1. **Profile** — is the source sketch *fully defined* (black)? Did I select the *right region(s)*?
2. **Operation** — New (standalone) / Add (fuse) / Remove (cut) / Intersect (keep overlap)? Did I pick the one that matches my intent?
3. **Direction** — is the arrow pointing the way I want? (Into the part for a Remove; out for an Add boss.)
4. **End condition** — is this a *number* (Blind/Symmetric) or a *relationship* (Through all / Up to face/next/part)? Did I pick the robust one for what this feature *means*?
5. **Merge scope** — in a multi-body part, am I touching only the bodies I intend to?
6. **Name** — did I rename the feature for *what it is*?

Six questions, five seconds, and you've eliminated 90% of the mistakes that make a part fail the rebuild test.

A last word before Lecture 2: everything here — operation, direction, end condition, merge scope — is the *same vocabulary* you'll use for Revolve, Sweep, and Loft. The dialogs differ in how they generate the shape (push vs spin vs follow-a-path), but they all ask "what operation, how far, on which bodies." Learn it cold on Extrude and the rest of solid modeling is a series of small variations on a pattern you already own.

---

## References

- *Extrude* — OnShape Help: <https://cad.onshape.com/help/Content/extrude.htm>
- *Boolean* — OnShape Help: <https://cad.onshape.com/help/Content/booleanmf.htm>
- *Rollback bar / editing features* — OnShape Help: <https://cad.onshape.com/help/Content/rollbackbar.htm>
- *Introduction to Onshape* (Learning Center path): <https://learn.onshape.com/learn/learning-plan/introduction-to-onshape>
- *Sketching* (Week 1 refresher) — OnShape Help: <https://cad.onshape.com/help/Content/sketching.htm>
- *Introduction to Part Studios* (Learning Center): <https://learn.onshape.com/courses>
