# Lecture 1 — Reference Geometry: Construction Planes, Offset/Angled Planes, Axes, and Mate Connectors

> **Duration:** ~2 hours of reading + hands-on in OnShape.
> **Outcome:** You can create offset, angled, and three-point construction planes; build construction axes; sketch on a non-default plane and on a part face; place and reuse a mate connector as an implicit reference; and explain — out loud — why a feature should reference one piece of geometry rather than another so that edits propagate predictably.

If you only remember one thing from this lecture, remember this:

> **Every feature you build sits on top of geometry that came before it. The geometry you pick as a reference *is* your design intent.** Sketch on a smart reference and the part flexes cleanly when a dimension changes. Sketch on a lazy reference — a random face, a stray edge — and the part turns red the first time someone edits it. References are not a detail; they are the whole game in week 3.

In Weeks 1 and 2 you lived almost entirely on the three origin planes — **Top, Front, Right** — and the faces of the solid you extruded from them. That was on purpose. Real parts cannot live there. A bracket has a face tilted 30°; a heat sink has fins offset 4 mm apart; a flanged elbow has a sketch plane that doesn't exist until you create it. This week you learn to *manufacture geometry to build on*: construction planes, construction axes, and mate connectors. Then in Lecture 2 you learn to multiply features off that geometry with patterns, mirror, sweep, and loft.

---

## 1. The three default planes, revisited

Open any new Part Studio. In the feature tree, before you have done anything, you already have:

- **Top** plane (the XY plane — looking straight down).
- **Front** plane (the XZ plane — looking from the front).
- **Right** plane (the YZ plane — looking from the side).
- An **Origin** point where all three intersect.

These are *default* construction geometry. They are infinite, they have no thickness, they never appear in a manufactured part, and they exist solely to give your first sketch something to live on. You can sketch on any of them, and you have been.

The mental model to adopt now: **default planes are just the first three members of a family.** You are about to add more members to that family — offset planes, angled planes, planes through three points — and they behave identically. A construction plane is a construction plane whether OnShape gave it to you or you built it.

> **Why "Top/Front/Right" and not "XY/XZ/YZ"?** OnShape labels the default planes by the view they represent rather than by their coordinate pair, because most CAD users think in views, not axes. Internally Top *is* XY. When you import or export STEP, or when you read a colleague's SolidWorks part, the same three planes appear under different names. The geometry is identical; only the label differs.

---

## 2. Why you need more than three planes

Here is the concrete problem. You have extruded a rectangular boss. Now you need a rib on top of it, but the top of the boss is 12 mm above the origin and the boss height is a *driving dimension* you intend to change. You have three bad options and one good one:

1. **Sketch on the Top origin plane and extrude up 12 mm to reach the boss.** Bad: the 12 mm is now a magic number duplicated from the boss height. Change the boss to 15 mm and your rib floats 3 mm in the air. Red part, or worse, silently wrong.
2. **Sketch directly on the top *face* of the boss.** Better — the sketch now rides the face, so it moves when the boss height changes. But face references are fragile: if you later add a fillet that consumes that face, or reorder features, the face's internal ID can change and the sketch loses its home ("dangling reference").
3. **Eyeball a plane somewhere near the top.** Never do this. Construction geometry must be *defined*, not placed by feel.
4. **Create an offset construction plane referenced to the Top plane, offset = the boss-height variable.** Good. The plane is parametric, it tracks the variable, and it is a stable, named reference that survives fillets and reordering.

Option 4 is what a senior modeler reaches for. The rest of this lecture teaches you to build references like option 4 deliberately, and to know when option 2 (face sketching) is actually fine — because sometimes it is.

---

## 3. Creating an offset plane

The **Plane** feature lives in the toolbar (the icon is a small angled plane; it sits near the sketch tools). Insert it and OnShape asks for a **Plane type**. The first and most common type is **Offset**.

Concrete walkthrough — build a plane 20 mm above Top:

1. Click the **Plane** tool.
2. Set **Plane type → Offset**.
3. For **Entities**, select the **Top** plane (in the tree or in the graphics area).
4. Enter **Distance = 20 mm**.
5. A flip arrow appears. Click it if the preview offsets *down* instead of up; the offset direction is signed.
6. Green check.

You now have `Plane 1` in your tree. Rename it immediately — double-click it and call it something like `Top + 20`. (Renaming references is not optional in C12; an unnamed `Plane 1 / Plane 2 / Plane 3` tree is an automatic deduction in the mini-project, exactly as unnamed features were in Week 2.)

Sketch on it the same way you sketch on any plane: select the plane, click **Sketch**, and you are drawing on a surface 20 mm above the origin.

> **Make the offset a variable.** If the offset distance relates to another dimension — a boss height, a wall thickness, a clearance — type the variable name instead of a literal: `#bossHeight + 2 mm`. We formally cover the Variable Studio in Week 5, but you can declare a variable inline today with the `#name = value` syntax in any dimension field. A plane offset by `#bossHeight` is the single biggest robustness upgrade you can make this week.

---

## 4. Creating an angled plane

Set **Plane type → Angle** (sometimes shown as "At angle"). This plane pivots about an edge or axis by a specified angle from a reference plane.

Concrete walkthrough — build a plane tilted 30° off Front, hinged about the Right plane's vertical axis... actually, hinged about a real edge is clearer, so:

1. Make sure you have an **edge or axis** to hinge about. The Y axis (the line where Front meets Right) works; so does any straight edge on your part.
2. Click **Plane → type Angle**.
3. For the **first entity**, pick the reference plane you measure the angle *from* (say, **Front**).
4. For the **second entity** (the hinge), pick the edge or axis to rotate about.
5. Enter **Angle = 30°**.
6. Flip if the tilt goes the wrong way.
7. Green check, then rename `Front @ 30`.

Angled planes are how you model anything draft-like, faceted, or deliberately non-orthogonal: the angled face of a wedge bracket, the slanted mounting boss on a housing, the canted vane of an impeller. The angle is a driving dimension — change it and the downstream sketch and feature re-tilt.

---

## 5. Other plane types you will use

The **Plane** feature offers several types beyond Offset and Angle. The ones worth knowing this week:

| Plane type | Define it with | Typical use |
|------------|----------------|-------------|
| **Offset** | a plane + a distance | a sketch surface parallel to an existing one |
| **Angle** | a plane + a hinge axis + an angle | slanted faces, draft references, faceted geometry |
| **Point–normal** | a point + a line/edge (the normal) | a plane perpendicular to a path at a point — *essential for sweep profiles* |
| **Three points** | three vertices | reconstruct a plane through known features (e.g. three holes) |
| **Line–point** | a line + an off-line point | a plane containing an edge and tilted to pass through a point |
| **Mid plane** | two parallel planes/faces | the symmetry plane between two faces — *the natural Mirror reference* |
| **Tangent** | a cylindrical/conical face + a plane or point | a plane that touches a round surface, e.g. to sketch a flat on a shaft |
| **Curve point** | a sketch/edge curve + a parameter | a plane riding along a curve — used with sweeps and helices |

You do not need all of these memorized. You need to know they exist so that when a sketch "has nowhere to live," your reflex is *"which Plane type manufactures the surface I need?"* rather than *"I'll fudge an offset and hope."*

The **Point–normal** and **Mid plane** types earn special attention this week. Point–normal builds the start plane for a sweep profile that must sit *perpendicular to the path*. Mid plane builds the symmetry reference that Mirror needs (Lecture 2). Practice both in the exercises.

---

## 6. Construction axes

A **construction axis** is the 1-D analogue of a construction plane: an infinite reference line, no thickness, never manufactured. You create them with the **Axis** feature (the icon is a dashed line).

Common ways to define an axis:

- **Through a cylindrical/conical face** — instantly gives you the centerline of a hole or boss. This is the single most useful axis in the course: it is what a **Circular pattern** spins around (Lecture 2).
- **Through two points** — a line between two vertices.
- **Intersection of two planes** — the line where two planes cross (the Y axis is Top ∩ Right).
- **Perpendicular to a plane through a point** — a line normal to a face at a chosen point.

Concrete walkthrough — make the centerline axis of a bored hole:

1. Click the **Axis** tool.
2. Pick the **cylindrical face** of the bore.
3. OnShape infers "the axis of this cylinder." Green check.
4. Rename `Bore axis`.

Why bother, when OnShape can often infer an axis on the fly during a Circular pattern? Because an *explicit, named* axis is a stable reference that survives edits, that you can dimension to, and that documents intent. The on-the-fly inferred axis vanishes if the face it was inferred from changes. In a robust part, the rotational features pattern about a **named construction axis**, not a transient inference.

> **Origin axes are free.** Like the three origin planes, OnShape gives you the X, Y, and Z origin axes at the origin. Turn them on in the tree (they're hidden by default). For anything symmetric about the global origin — a flange, a hub — you often don't need to build an axis at all; the origin Z axis is already there.

---

## 7. Sketching on a part face vs. sketching on a construction plane

Both are legal. Both are common. Choosing between them *is* a design-intent decision, and getting it right is most of what separates a robust part from a fragile one.

**Sketch on a construction plane when:**

- The sketch's position is defined by a *dimension* (offset, angle), not by an existing solid surface.
- You want the sketch to survive feature reordering and dress-up (fillets/chamfers) downstream.
- The surface you'd otherwise sketch on doesn't exist yet, or might be consumed later.

**Sketch on a part face when:**

- The sketch genuinely belongs *to* that face — a logo engraved on the front, a boss growing straight out of a wall, a counterbore on a specific surface.
- You *want* the sketch to move when the face moves (the boss should stay on the wall even as the wall thickens).
- The face is stable: a large primary face that won't be split, filleted away, or reordered out from under you.

The classic failure mode is the **dangling reference**: you sketch on a face, then later insert a fillet that rounds that exact face out of existence, and the sketch turns yellow/red with "the face this sketch was on no longer exists." The fix is almost always: *don't sketch on faces that downstream features will eat.* Sketch on the plane that defined the face instead, or move the dress-up feature to after the sketch's feature in the tree.

> **The "use construction planes for structure, faces for detail" rule of thumb.** Structural geometry — the ribs, bosses, and major features that define the part's shape and that you'll want to edit — should reference construction planes and origin geometry, because those are stable. Surface detail — text, small cosmetic cuts, the occasional clearance pocket — can ride a face, because if the face moves you usually *want* the detail to move with it. It's a guideline, not a law, but it'll keep you out of trouble while you build the instinct.

---

## 8. References, the feature tree, and rollback

OnShape is a **history-based parametric modeler**. The feature tree is not a list of parts; it is a *recipe*, executed top to bottom every time the part regenerates. Feature 5 can reference the output of features 1–4 but knows nothing about feature 6. This single fact drives every design-intent decision you'll make.

Two consequences you must internalize this week:

1. **A feature can only reference geometry that exists *above* it in the tree.** You cannot sketch on a plane you haven't created yet. So the *order* in which you build references matters: planes and axes that many features depend on belong early; one-off dress-up belongs late.
2. **The rollback bar lets you "time travel."** Drag the rollback bar (the blue line at the bottom of the tree) up to a point in history, and OnShape regenerates the part *as it was at that step*. Insert a new feature there, and it lands mid-history — letting you add a reference plane *before* the features that should depend on it. This is how you retrofit a clean reference into a part you built in the wrong order.

Concrete example of order mattering: suppose you built `Extrude boss → Fillet edges → (now you want a rib on top)`. If you sketch the rib on the *filleted* top face, the rib references a face that depends on the fillet — change the fillet radius and the rib may shift. Better: roll back **before** the fillet, create an `Offset plane` from Top at the boss height (or sketch on the un-filleted top face), build the rib, then roll forward so the fillet rounds everything at the end. The rib now references stable geometry; the fillet is pure dress-up at the tail of the recipe.

---

## 9. Mate connectors — references that travel into the Assembly

A **mate connector** is a small, fully-defined coordinate frame — an origin point plus an orientation (three axes) — that you can place anywhere on your geometry: on a vertex, the center of a face, the midpoint of an edge, at the origin, or freely on a plane. It looks like a tiny RGB triad in the graphics area.

You will use mate connectors *heavily* in Week 4 to define how parts join in an Assembly (a fastened mate snaps two connectors together; a revolute mate lets one spin about another's Z axis). But they begin life in the **Part Studio**, and that is why they appear in *this* week's lecture on references.

Three things to understand now:

**(a) A mate connector is a reusable, named reference frame.** Once placed, it is a stable handle you can mate to, dimension from, or pattern. Unlike an inferred point that vanishes on edit, an *explicit* mate connector you add as a feature persists and can be renamed.

**(b) Implicit vs. explicit connectors.** In an Assembly, OnShape will *infer* mate connectors on the fly as you hover (the center of that hole, the corner of that face). Those are convenient but transient. An **explicit mate connector**, added in the Part Studio with the **Mate connector** feature, is a deliberate, persistent reference that you control — its origin, its primary axis (Z, which most mates spin or align about), and its secondary axis. For any joint that matters, place an explicit connector now so Week 4's assembly is built on intent, not on whatever face you happened to hover.

**(c) The connector's orientation is the whole point.** A mate connector's **Z axis** is its primary direction — revolute mates rotate about it, slider mates translate along it, fastened mates align it. When you place a connector, *check which way Z points* and reorient it (the connector dialog lets you re-pick the primary axis and flip/rotate it) so that Z means what you want it to mean for the joint. A hinge connector whose Z points along the hinge pin is correct; one whose Z points sideways will make your Week 4 hinge swing about the wrong line.

Concrete walkthrough — place a hinge connector now, ready for Week 4:

1. In the Part Studio, click the **Mate connector** feature (or the connector tool in the toolbar).
2. Hover the **cylindrical face** of the hinge knuckle; OnShape snaps the connector to its **axis and a planar end**. Click to place.
3. In the dialog, confirm the **primary (Z) axis runs along the hinge centerline**. If it points across the part instead, re-select the primary axis or use the **Reorient** controls.
4. Set the **origin** to the end of the knuckle (or its midpoint) — somewhere meaningful and stable.
5. Rename `Hinge MC`.

You don't mate anything this week. You're *planting flags* — named reference frames on the geometry that will become joints — so that when you reach assemblies, the references already say what you mean.

---

## 10. A worked multi-feature build, reference-first

Let's build a small part the right way, narrating every reference choice. The part: a **mounting bracket with an angled gusset and a bolt face offset above the base.** You'll build the full version in the exercises; here we walk the reference decisions.

1. **Base plate.** Sketch a 80 × 50 mm rectangle on **Top**, symmetric about the origin (use the origin point as a constraint anchor so the part is centered — centered parts mirror and pattern cleanly). Extrude 6 mm up. *Reference: origin plane + origin point. Maximally stable.*
2. **Bolt face.** The bolt face must sit 40 mm above the base. Don't sketch on the base's top face and extrude 40 mm (magic number). Instead: create an **Offset plane** from **Top**, distance `#bossHeight = 40 mm`. Sketch the bolt-face rectangle there. *Reference: a parametric offset plane driven by a variable.*
3. **Gusset.** The triangular gusset that braces the bolt face must lie in the part's symmetry plane. Use the **Front** origin plane (which already *is* the symmetry plane, because the part is centered). Sketch the gusset triangle on Front, extrude **symmetric** (mid-plane end condition) so it's centered. *Reference: origin symmetry plane + symmetric extrude. No new geometry needed — the smart move is often to reuse an origin plane.*
4. **Angled stiffener.** A small stiffener sits on a face tilted 30°. Create a **Plane → Angle**, 30° off Top, hinged on the base's back edge. Sketch and extrude the stiffener there. *Reference: an angled construction plane, so the 30° is a driving dimension.*
5. **Hole pattern.** Four mounting holes near the base corners. Sketch *points* (not circles) on the base top face, fully defined to the corners; use the **Hole** feature off those points. *We pattern these in Lecture 2.*
6. **Hinge connector.** Place an explicit **mate connector** on the bolt face, Z normal to the face, ready for whatever bolts on in Week 4.

Now the rebuild test: change `#bossHeight` from 40 to 55. The offset plane rises, the bolt face rises with it, the gusset (on the symmetry plane, extruded symmetric) stretches to meet it, the angled stiffener is unaffected, the holes stay put. **Nothing turns red.** That is the payoff of reference-first modeling. Had you used magic numbers and face-sketches, that single edit would have produced two or three red features.

---

## 11. Diagnosing a broken reference

When you edit a part and features turn yellow or red, OnShape is telling you a reference broke. Read the message; it is specific. The common ones:

| Symptom | What it means | Usual fix |
|---------|---------------|-----------|
| "The entity this sketch is on no longer exists" | The face/plane you sketched on was deleted, consumed by a fillet, or reordered above the sketch. | Re-attach the sketch to a stable plane, or move the consuming feature later in the tree. |
| Sketch goes **under-defined** (blue) after an edit | A constraint referenced geometry that moved or vanished. | Re-add the lost constraint to a stable reference. |
| "Could not regenerate pattern — seed feature failed" | A pattern's seed feature broke; the pattern can't copy a broken thing. | Fix the seed first; patterns are downstream of their seed. |
| A plane turns red after deleting a feature | The plane referenced the deleted feature's geometry. | Re-reference the plane to origin geometry or to an earlier, stable feature. |

The meta-lesson: **a red feature is almost never the problem — it's the *victim*.** The problem is upstream, where a reference it depended on changed. Fix the cause, not the symptom. The rollback bar is your debugger: roll back to just before the first red feature and you'll usually see exactly what changed.

---

## 12. Naming, organizing, and folders

A multi-feature part has a long tree. Discipline keeps it readable:

- **Rename every feature** as you create it, not at the end. `Offset plane → Bolt-face plane`, `Plane 2 → Stiffener plane @30`, `Extrude 1 → Base plate`, `Hole 1 → M5 corner holes`.
- **Use folders.** Right-click features → **Group into folder**. Group `Bolt-face plane + bolt-face sketch + bolt-face extrude` into a `Bolt face` folder. A tree of five labeled folders reads like a table of contents; a flat tree of forty features does not.
- **Name construction geometry by its job**, not its type. `Top + 40` or `Bolt-face plane`, never `Plane 1`. Six months from now (or in a code review tomorrow) the name is the only thing telling the next person *why* that plane exists.

This is not cosmetic. In Week 4, the people mating to your part read your feature names and mate-connector names to understand it. In Week 5, the configuration table references features by name. A disciplined tree this week pays compounding interest for the rest of the course.

---

## 13. A field guide to the Plane dialog, type by type

Beginners freeze at the Plane dialog because there are seven types and the right one isn't obvious. Here is the decision flow, with a concrete trigger for each.

**Offset** — *"I need a surface parallel to one I already have, a fixed distance away."*

- Select: a plane or planar face, plus a distance.
- Trigger: a stacked feature (a boss above a base, a lid above a body, a sketch above a face).
- Robustness move: drive the distance from a variable so it tracks the dimension it's parallel-offset from.

**Angle** — *"I need a surface tilted a set angle from an existing one."*

- Select: a reference plane, a hinge edge/axis, and an angle.
- Trigger: a slanted face, a draft reference, a faceted feature, a canted mounting boss.
- Robustness move: hinge about a *stable* edge (an origin axis or a primary part edge), not a fillet edge that might move.

**Point–normal** — *"I need a surface perpendicular to a direction at a specific point."*

- Select: a point, plus a line/edge that gives the normal direction.
- Trigger: the start of a **sweep** profile (perpendicular to the path), a cut normal to a curved surface at a point.
- Robustness move: use the path's own start vertex and first segment so the plane stays glued to the path if the path edits.

**Three points** — *"I need to reconstruct the plane that passes through three known features."*

- Select: three non-collinear vertices.
- Trigger: re-deriving a plane from three holes, three corners, or three datum targets you already have.
- Robustness caveat: the plane follows those three points — if any moves, the plane re-tilts. That's usually *desired*, but be aware of it.

**Line–point** — *"I need a plane that contains an edge and also passes through an off-edge point."*

- Select: a line/edge and a point not on it.
- Trigger: a plane that must hold a specific edge but tilt to reach a feature elsewhere.

**Mid plane** — *"I need the symmetry plane halfway between two faces."*

- Select: two parallel planes or planar faces.
- Trigger: the mirror reference for a symmetric part, or a sketch that must sit on a part's centerline when no origin plane lands there.
- Robustness move: this is the single best friend of the **Mirror** feature — build it once and mirror everything across it.

**Tangent** — *"I need a flat plane touching a round surface."*

- Select: a cylindrical/conical face, plus a plane or point to orient it.
- Trigger: a flat milled onto a shaft, a sketch on the tangent of a boss, a wrench flat.

**Curve point** — *"I need a plane riding along a curve at a parameter."*

- Select: a curve/edge and a position along it.
- Trigger: helices, features placed along a spline, decorative geometry that follows a path.

If you can match the *trigger* to your situation, the type chooses itself. The mistake to avoid is forcing every problem into Offset because it's the one you know — the wrong plane type is how you end up with a magic number or a fragile reference.

---

## 14. References across Part Studios and the import boundary

Two practical notes that bite people the first time they hit them.

**Derived parts and in-context references.** OnShape lets you *derive* a part from another Part Studio (the **Derived** feature) or reference assembly geometry **in context**. When you do, you create a reference that crosses a boundary — and that reference can go stale if the source changes. This is powerful (it's how Week 4's in-context design works) but it's also a new way to get a dangling reference, now spanning two tabs. The rule is the same as within one Part Studio: reference *stable, named* geometry, and know what each cross-tab reference depends on. We use these deliberately in Week 4; for now, just know they exist and follow the same discipline.

**Imported geometry has no feature tree.** When you import a STEP or Parasolid file, you get a "dumb" solid — a body with faces and edges but *no parametric history*. You can still create construction planes and axes off its faces, and sketch on it, but you cannot edit its original features because there are none to edit. If you find yourself needing to heavily modify imported geometry, the honest move is often to re-model it natively so it's parametric. We touch import/export properly in Week 6; the takeaway now is that references to imported faces are references to fixed geometry, not to a recipe.

---

## 15. Why this all compounds: the running project

This is Week 3 of a six-week build, and the references you create now are load-bearing for everything after:

- **Week 4 (Assemblies & Mates)** snaps mates to the **mate connectors** you plant this week. A connector with Z along the hinge line makes the hinge mate trivial; a careless one makes it painful. The assembly is only as clean as the connectors underneath it.
- **Week 5 (Configurations)** turns the **variables** driving your plane offsets and pattern counts into a dropdown of part sizes. `#bossHeight`, `#bolts`, `#bcd` declared now become configuration columns later — for free, if you used variables; with a painful retrofit, if you used magic numbers.
- **Week 6 (Capstone)** asks you to understand a part months later as one moving component of a mechanism. The **renamed, foldered, deliberately-ordered tree** you build this week is what makes that possible. Nobody — including future-you — can reason about a wall of `Plane 1 / Extrude 2 / Pattern 3`.

The discipline isn't busywork. It's the difference between a part you can edit in Week 6 and a part you have to rebuild from scratch.

---

## 16. Recap

You should now be able to:

- Create **offset** and **angled** construction planes, and pick the right plane *type* (point–normal, mid plane, tangent, three-point) for a given job.
- Create **construction axes**, especially the centerline of a cylindrical face for circular patterns.
- Decide, deliberately, between **sketching on a construction plane** and **sketching on a part face**, and explain the trade-off in terms of robustness.
- Understand the feature tree as a **top-to-bottom recipe**, use the **rollback bar** to insert references mid-history, and diagnose a broken reference by finding its *upstream cause*.
- Place an explicit **mate connector** as a persistent, oriented reference frame, ready for Week 4 assemblies.
- Keep a multi-feature tree **renamed and foldered** so design intent is legible.

Next: multiplying that geometry. Continue to [Lecture 2 — Multiplying Geometry: Linear & Circular Patterns, Mirror, Sweep, and Loft](./02-multiplying-geometry-patterns-mirror-sweep-and-loft.md).

---

## References

- *Planes* — OnShape Help: <https://cad.onshape.com/help/Content/planes.htm>
- *Mate connectors* — OnShape Help: <https://cad.onshape.com/help/Content/mate_connector.htm>
- *Sketching* (sketch planes and on-face sketching) — OnShape Help: <https://cad.onshape.com/help/Content/sketdialog.htm>
- *Construction geometry & axes* — OnShape Help: <https://cad.onshape.com/help/Content/axis.htm>
- *OnShape Learning Center — Fundamentals: Part Studios* (free, account required): <https://learn.onshape.com/learn/learning-path/cad>
- *Rollback bar & feature history* — OnShape Help: <https://cad.onshape.com/help/Content/rollbackbar.htm>
