# Lecture 2 — Sketching with Intent: Geometric Constraints, Dimensions, and Fully-Defined Sketches

> **Duration:** ~2 hours of reading + hands-on.
> **Outcome:** You can read the color state of a sketch, apply every common geometric constraint and explain which degrees of freedom it removes, add driving dimensions, tell a driving dimension from a driven one, and fully-define a profile using the *minimum* number of dimensions.

If you only remember one thing from this lecture, remember this:

> **Constrain first, dimension last, and stop the moment everything turns black.** Geometry should be locked by *relationships* (parallel, equal, concentric, symmetric) wherever possible and pinned by *numbers* only where a real dimension actually matters. A sketch held together by constraints rebuilds robustly when an upstream value changes; a sketch held together by dimensions alone is brittle and over-specified.

This lecture covers the whole craft of 2D sketching. Everything you build in the next five weeks starts here, so we go deep.

---

## 1. The mental model: degrees of freedom

A 2D sketch entity can *move*. The number of independent ways it can move is its **degrees of freedom (DOF)**.

- A free **point** in 2D has **2 DOF**: it can move in x and in y.
- A free **line segment** has **4 DOF**: 2 for each endpoint. (Equivalently: position, length, and angle.)
- A free **circle** has **3 DOF**: 2 for its center, 1 for its radius.
- A free **arc** has **4 DOF**: center (2), radius (1), and... well, the endpoints add the sweep — practically, treat it as "more than a circle."

**Sketching is the act of removing degrees of freedom** until none remain. You remove them two ways:

1. **Geometric constraints** — *relationships* with no number (this line is horizontal; these two are equal; this point sits on the origin).
2. **Dimensions** — *numbers* (this line is 40 mm; this angle is 30°).

When **every DOF is removed**, the sketch is **fully defined**: all geometry turns **black** and OnShape's status bar reads "Fully defined." When DOF remain, geometry is **blue** and you can literally **drag it around** with the mouse — that's the test. When you over-specify (two facts that fight, like "this line is 40 mm" *and* "this line is 50 mm"), geometry turns **red/yellow** and OnShape flags a conflict.

> **The drag test.** Want to know if a sketch is under-defined? Try to drag a line or point with the cursor. If it moves, it's under-defined and that endpoint still has free DOF. If nothing moves anywhere, you're fully defined. This is the fastest sanity check in CAD; use it constantly.

---

## 2. Reading sketch color — the traffic light

OnShape color-codes sketch state. Learn to read it on sight:

| Color | Meaning | What to do |
|-------|---------|-----------|
| **Blue** | Under-defined — this entity still has free DOF and can be dragged. | Add constraints/dimensions until it's black. |
| **Black** | Fully defined — fully locked, no remaining DOF. | Done. Leave it alone. |
| **Red / yellow** | Over-defined or conflicting — too many constraints/dimensions fight each other. | Remove the redundant one. Don't add `!`-style overrides; *fix the cause*. |
| **Grey / dashed** | Construction geometry — reference-only, never becomes part of a 3D feature. | Use for centerlines and symmetry axes; doesn't need to be defined to count. |

Your **Week-1 goal in every sketch**: drive the blue out. The whole geometry should be black before you exit the sketch. A single overlooked blue endpoint is the most common cause of a part silently shifting two weeks later when someone edits an upstream dimension.

---

## 3. Drawing the entities

Inside a sketch, the sketch toolbar gives you the drawing tools. The set you need this week:

- **Line** (`l`) — click start, click end; keep clicking to chain segments. Press `Esc` or double-click to stop. While dragging, OnShape shows **inference glyphs** (see §5) — a small horizontal/vertical dash, a parallel mark — telling you a constraint it's about to add.
- **Corner rectangle** — click one corner, click the opposite corner. Adds two horizontal + two vertical constraints for you automatically.
- **Center-point rectangle** — click the center, then a corner. Symmetric about the center; great when you want the rectangle centered on the origin.
- **Center-point circle** (`c`) — click center, click to set radius.
- **Three-point arc** — click two endpoints and a point on the arc.
- **Tangent arc** — start it from the endpoint of an existing line/arc and it auto-creates a tangent constraint to that entity. The backbone of slots, fill’d profiles, and lever shapes.
- **Slot** — a purpose-built tool that draws two parallel lines capped by two semicircular arcs, pre-constrained. A huge time-saver versus building one by hand.
- **Point** — a standalone construction/reference point.

> **Let the tools do constraint work for you.** A corner rectangle arrives with four constraints already applied. A tangent arc arrives tangent. The slot tool arrives nearly fully constrained. Using the *right* tool means OnShape adds the obvious constraints automatically and you add fewer by hand. Drawing a rectangle as four separate lines and then manually constraining it is the mark of someone fighting the software.

---

## 4. The geometric constraints, one by one

This is the core vocabulary of CAD. Each constraint removes some DOF *without a number*. Select one or two entities (or a point), then click the constraint icon (or use the keyboard shortcut). Here's every constraint you use this week, what it does, and the DOF it removes.

### Coincident
Forces a point to lie on another point, a line, or a curve. The workhorse. Selecting two endpoints and applying coincident *snaps them together* (removes 2 DOF — they become one point). Selecting a point and a line forces the point *onto* the line (removes 1 DOF). **Anchoring your first point to the origin is a coincident constraint.**

### Horizontal / Vertical
Forces a line to be horizontal (or vertical) in the sketch plane. Removes 1 DOF (the line's angle). Corner rectangles get these for free. Apply to a lone slanted line to straighten it.

### Parallel
Forces two lines to share a direction. Removes 1 DOF. Use it when two edges must stay parallel even as the part resizes — instead of dimensioning both angles.

### Perpendicular
Forces two lines to meet at 90°. Removes 1 DOF. Cleaner than dimensioning a 90° angle (and a perpendicular *constraint* survives a resize; a 90° *dimension* is just a number that could be edited).

### Tangent
Forces a line and an arc/circle (or two arcs) to meet smoothly — no kink. Removes 1 DOF. Essential for slots, rounded lever ends, and any profile where a flat must blend into a curve. Tangent-arc tool adds this automatically.

### Equal
Forces two lines to the same length, or two circles/arcs to the same radius. Removes 1 DOF. **This is the constraint that lets you dimension *once* and apply *everywhere*.** Four mounting holes the same size? Make them `equal` and dimension one. Resize that one and all four follow.

### Concentric
Forces two circles/arcs (or a circle and an arc) to share a center. Removes 2 DOF. The natural way to build a bolt-head counterbore, a washer (inner + outer circle share a center), or a hub.

### Midpoint
Forces a point to sit at the midpoint of a line. Removes the DOF that a free point-on-line would have along the line. Great for centering one feature on an edge.

### Symmetric
Forces two entities (two points, two lines) to mirror across a **centerline** (a construction line). Removes DOF *and* encodes symmetry as design intent. Build a symmetric profile by drawing half, then applying symmetric across a construction centerline — when you resize, both halves move together. This is *the* senior move for symmetric parts.

### Fix
Pins an entity in place absolutely. Use **sparingly** — it removes all of that entity's DOF but it's a blunt instrument that hides design intent. Prefer constraining *to the origin* over `Fix`. A sketch full of `Fix` constraints is a code smell; it usually means someone gave up on real relationships.

> **Constraint priority order (the C12 house style):**
> 1. Anchor to the **origin** (coincident).
> 2. Apply **geometric relationships** (horizontal/vertical, parallel, perpendicular, tangent, equal, concentric, symmetric, midpoint).
> 3. Add **driving dimensions** for the few measurements that actually matter — last, and as few as possible.
>
> If you find yourself adding a dimension that a constraint could express (a "90°" dimension instead of perpendicular; equal lengths dimensioned twice instead of an `equal` constraint), stop and use the constraint. Constraints survive edits; redundant dimensions create brittleness and conflicts.

---

## 5. Constraint inferencing — the glyphs while you draw

As you draw, OnShape constantly *infers* constraints and shows tiny **glyphs**: a horizontal dash when a line is about to snap horizontal, a parallel mark when it lines up with another line, an `×` at a coincident snap, a tangent symbol near a curve. If you click while a glyph is showing, OnShape **adds that constraint** for you.

This is enormously powerful and occasionally annoying. Two things to know:

- **To accept** an inferred constraint, just click while the glyph shows. Free constraints, fewer to add by hand.
- **To suppress** an inference you *don't* want (it keeps snapping horizontal but you want a slight angle), hold the inference-disable modifier (drag a little further so the glyph drops, or use the override) and place the point where you actually want it, then constrain it deliberately.

> **Watch the glyphs.** Beginners ignore the glyphs and then wonder why their sketch already has constraints they didn't add. Read them as you draw — they're OnShape telling you what relationships it's building. Half of "fully defining" a sketch happens automatically through inferencing if you're paying attention.

---

## 6. Dimensions: driving vs driven

The **Dimension tool** (`d`) adds numeric dimensions. It's "smart": click a line and it offers a length; click two parallel lines and it offers the distance between them; click a circle and it offers a diameter (⌀); click an arc and it offers a radius (R); click two lines at an angle and it offers the angle.

There are two kinds of dimension, and the difference is everything:

### Driving dimension
A driving dimension **controls** geometry. Type `40 mm` and the line *becomes* 40 mm; change it later and the geometry *moves*. Driving dimensions remove DOF — each one you add turns more of the sketch black. These are what you place to fully-define a sketch. Shown in normal text.

### Driven (reference) dimension
A driven dimension **reports** a measurement but does **not** control it. If you try to add a dimension that *would* over-define the sketch (you've already locked that measurement another way), OnShape asks whether you want it as a **driven** (reference) dimension instead. Driven dimensions are shown in **parentheses / grey**. They're useful for *displaying* a value you care about without re-specifying it.

> **The over-definition prompt is your friend.** When OnShape pops up "this dimension would over-define the sketch — make it driven?", it's telling you the measurement is *already* determined by your constraints. That's usually a *good sign* — it means your constraints are doing the work. Either accept the driven dimension (to display it) or cancel and delete a redundant constraint. Never force a second driving dimension onto an already-locked measurement; that's how you get a red conflict.

### Dimension types you'll use this week

- **Linear** — distance between two points/lines, horizontal or vertical or aligned.
- **Aligned** — distance measured along a slanted line's direction.
- **Radial (R)** — radius of an arc/circle.
- **Diameter (⌀)** — diameter of a circle (use this for holes — manufacturers think in hole *diameter*, not radius).
- **Angular** — the angle between two lines.

To **edit** a dimension, double-click it and type a new value. The geometry updates *parametrically* — this is the whole magic of CAD. Drag a `40 mm` to `60 mm` and watch every dependent feature rebuild. We make you do exactly this in Exercise 1 so the parametric behavior lands viscerally.

---

## 7. Minimum-dimension thinking — the heart of the week

A square plate, 50 mm × 50 mm, with the bottom-left corner at the origin. How many dimensions does it need?

**Naive answer:** four — top, bottom, left, right.

**Better answer:** two — one width, one height. (The corner rectangle already constrained the four lines horizontal/vertical and coincident at the corners, and you anchored one corner to the origin.)

**Best answer for a *square*:** **one.** Apply an `equal` constraint between an adjacent width and height line, anchor a corner to the origin, then dimension *one* side `50 mm`. The `equal` constraint propagates it. Now changing that single `50` resizes the whole square, and it can *never* become a non-square rectangle by accident — the squareness is *encoded as intent*, not maintained by you typing two equal numbers.

That's the lesson of the whole week: **constraints encode intent; dimensions specify values.** Reach for an `equal`, a `symmetric`, a `concentric` *before* you reach for a second number. The challenge this week is explicitly graded on using the *minimum* number of dimensions — because a profile built that way is the one that survives being edited by someone else.

> **A quick test for "too many dimensions."** Before adding a dimension, ask: "Is this measurement already determined by a relationship I could express as a constraint?" If yes, use the constraint. If the value genuinely matters and isn't implied by any relationship (the bolt-hole spacing on a real bracket, the overall length the customer specified), dimension it. Those are *real* dimensions. The squareness of a square is not.

---

## 8. Worked example: a fully-defined washer profile

Let's fully-define the master sketch for a flat washer-style part — a small disk with a centered hole — leaning on constraints. (This is essentially the mini-project deliverable, walked through.)

1. **Sketch on the Top plane.** Enter a sketch.
2. **Outer circle.** Use center-point circle. Click *the origin* as the center — OnShape snaps and adds a **coincident** to the origin automatically. Click out to set a rough radius. The circle is blue (its radius is still free; its center is locked to the origin = 2 DOF gone, 1 remains).
3. **Inner circle.** Draw a second, smaller center-point circle. Start it at the origin again → **coincident** to origin. *Or* draw it loosely and apply a **concentric** constraint between the two circles (removes 2 DOF). Either way both circles now share the origin as center.
4. **Dimension the outer ⌀.** Dimension tool → click the outer circle → type `30 mm`. The outer circle goes black.
5. **Dimension the inner ⌀.** Dimension tool → click the inner circle → type `12 mm`. The inner circle goes black.
6. **Done.** Status bar: **Fully defined.** Total dimensions used: **two** (the two diameters). Total constraints: two coincident-to-origin (or one coincident + one concentric). The hole can *never* drift off-center because concentricity is a constraint, not a number you maintain.

Now double-click the `30 mm` and change it to `40 mm`. The outer circle grows; the hole stays centered. Change `12` to `8`; the hole shrinks, still centered. *That* is parametric design — and it works robustly because the relationship (concentric) is encoded, not re-typed.

---

## 9. Worked example: a slotted lever (tangent arcs + equal)

A flat lever: a long body with a rounded end at each side, a pivot hole at one end, and a slot near the other. The constraint logic:

1. Draw a **construction centerline** from the origin horizontally (toggle construction with `q`). This is your symmetry/alignment axis.
2. Place a **concentric** pair of circles at the origin for the **pivot** — outer body radius and the pivot hole. Dimension both ⌀.
3. At the far end, use the **slot tool** — it arrives nearly fully constrained (two parallel lines, two equal end-arcs, tangent). Center the slot on the construction centerline with a **midpoint** or **symmetric** constraint so it stays aligned when the lever lengthens.
4. The body's straight edges: make them **tangent** to the end arcs (no kink) and **parallel** to each other. Constrain the body's width with an `equal` to the end-arc diameters if it should match.
5. Dimension only: the pivot ⌀, the slot length and width, the slot's radius (or let the equal-arcs handle it), and the **center-to-center distance** from the pivot to the slot. That distance is the one *real* dimension that defines the lever's reach — everything else is relationships.

The result fully defines with a handful of dimensions and a lot of tangent/equal/symmetric constraints. Resize the center-to-center distance and the whole lever stretches cleanly. This is Exercise 3.

---

## 10. Common sketching mistakes (and the fix)

| Mistake | Symptom | Fix |
|---------|---------|-----|
| Sketch left blue | Lines drag; part shifts on later edits | Run the drag test; add constraints/dimensions until black. |
| Over-dimensioning | Red/yellow conflict, or OnShape forces "driven" | Replace redundant dimensions with constraints (`equal`, `perpendicular`). |
| Forgetting to anchor to origin | Whole sketch floats and drags as a unit | Add a coincident from a sketch point to the origin. |
| Drawing a rectangle as 4 lines | Lots of manual constraining, easy to miss one | Use the rectangle tool; it constrains itself. |
| Fighting the inference glyphs | Constraints you "didn't add" appear | Read the glyphs as you draw; accept or suppress deliberately. |
| Over-using `Fix` | Sketch is "defined" but rebuilds badly | Replace `Fix` with real relationships (origin coincident, symmetric). |
| Dimensioning hole radius not diameter | Manufacturer confusion | Dimension holes by **diameter (⌀)** — that's how drills and tooling are specified. |
| Tangent arc with a kink | The arc meets the line at an angle | Apply a **tangent** constraint (or use the tangent-arc tool from the line endpoint). |

---

## 11. The "show constraints" habit

Turn on **Show constraints** (the display filter in the sketch view) and OnShape decorates the sketch with every constraint glyph — little parallel marks, tangent symbols, coincident dots. Learning to *read* a constraint-decorated sketch is a senior skill. When you pick up someone else's model (or your own, six weeks later), the glyphs tell you *why* the geometry is shaped the way it is. Start the habit this week: before you exit a sketch, toggle constraints on and *look* at what's holding your geometry together. If a relationship you expected isn't there, the geometry is being held by a dimension that should have been a constraint.

---

## 12. Construction geometry — the scaffolding that defines real geometry

A surprising amount of robust sketching is done with **construction geometry** — lines, circles, and points that exist only as references and never become part of a 3D feature. Toggle any entity to construction with `q` (it goes dashed/grey). You'll use construction geometry constantly:

- **Symmetry axes.** A construction centerline through the origin is the anchor for every `symmetric` constraint. Drawing half a profile and mirroring intent across a construction centerline is the cleanest way to build any symmetric part.
- **Bolt-circle radii.** A construction circle concentric with a hub gives you a curve to place pattern holes on. The holes sit on the construction circle; the construction circle never extrudes.
- **Alignment spines.** The lever in Exercise 3 rides a horizontal construction centerline. The slot, the boss, and the body all reference that spine, so the whole part stays collinear when it stretches.
- **Reference points.** A construction point at a computed location (a midpoint, an intersection) gives you something to constrain *to* that isn't real edge geometry.

> **Construction geometry doesn't need to be "fully defined" to be useful, but a fully-defined sketch still requires its construction entities to be locked** if real geometry depends on them. A floating construction centerline drags your "symmetric" geometry with it. Anchor your construction lines to the origin just like real ones.

The mental shift: *construction geometry is part of your design intent, not clutter.* A profile with a thoughtful construction skeleton is far more robust than one where every entity is "real" and pinned by numbers. Senior CAD users' sketches are often half construction geometry.

---

## 13. Sketch relations vs feature-level operations — a boundary to respect

A point of confusion worth heading off now: some shaping operations belong **inside** the sketch, and some belong to **features** that act *on* a sketch. This week you live entirely on the sketch side, but knowing the boundary prevents reaching for the wrong tool.

**Inside the sketch (this week's world):**
- **Sketch fillet / sketch chamfer** — round or bevel a *corner of 2D sketch geometry*. You use sketch fillets on the gasket challenge's corners. They live in the sketch and add tangent constraints automatically.
- **Trim / extend** — clean up where sketch entities overlap or fall short, so you end with one tidy closed loop.
- **Mirror (within a sketch)** — copy entities across a construction line, with the copies constrained symmetric to the originals.
- **Offset** — create a parallel copy of a curve at a fixed distance (great for a constant-width frame or a gasket land).

**Feature-level (Week 2 and later — *not* this week):**
- **3D fillet / chamfer** — rounds the *edges of a solid*, after extruding. Different tool, different stage.
- **Extrude / Revolve / Sweep / Loft** — turn a sketch into a solid.
- **Pattern / Mirror (of features)** — replicate whole 3D features.

> **The rule of thumb:** if it shapes *2D geometry on a plane*, it's a sketch operation and it's fair game this week. If it shapes *a 3D solid*, it's a feature and it waits for Week 2. The same word ("fillet," "mirror") shows up in both worlds — pay attention to *which* one a tutorial means.

---

## 14. Why we spend a whole week before extruding

It's tempting to rush past sketching to "the fun part" — making 3D shapes. Resist. Here's the payoff math, made concrete:

- **A robust sketch makes every later feature trivial.** Extrude a fully-defined profile and the solid inherits its precision. Extrude a sloppy, blue profile and the solid wobbles, and every downstream fillet and hole inherits the wobble.
- **Edits propagate predictably — or catastrophically.** When a colleague changes the overall width in Week 5, a constraint-driven sketch rebuilds cleanly and the whole assembly follows. A dimension-soup sketch throws conflicts, and you spend an afternoon hunting which of 18 dimensions now fights which.
- **Fully-defined is a *contract*.** "Fully defined" means *there is exactly one solution* to your sketch — no ambiguity about where anything sits. Under-defined means the geometry has freedom you didn't intend, and the next person (or the next rebuild) may resolve that freedom differently than you assumed. CAD bugs are almost always under-definition you didn't notice.
- **The discipline transfers to every CAD tool.** SolidWorks, Fusion 360, Inventor, Creo — all of them are sketch-then-feature parametric modelers with the exact same constraint vocabulary. The week you spend here is a skill you keep for your whole engineering career, not an OnShape quirk.

So: constrain first, dimension last, drive out every blue line, and only *then* think about 3D. We start extruding in Week 2 — and your Week-1 master sketch is the first thing we extrude.

---

## 15. Worked example: counting degrees of freedom out loud

The fastest way to internalize "fully defined" is to do the DOF bookkeeping out loud once. Take the simplest real profile — a rectangle with one centered hole — and count.

**The rectangle (drawn with the corner-rectangle tool, one corner at the origin):**

- Four line segments would be 16 DOF if fully free.
- The rectangle tool added: two **horizontal** constraints, two **vertical** constraints, and four **coincident** constraints at the corners (the lines share endpoints). That collapses the four lines into a connected loop with the corners as the only free points.
- A free rectangle anchored nowhere has effectively 4 remaining DOF: x-position, y-position, width, height.
- **Anchor** one corner to the **origin** with a coincident → removes 2 (x and y position). 2 DOF left: width and height.
- **Dimension** the width → removes 1. **Dimension** the height → removes 1. **0 DOF left.** Black. Fully defined.

So a rectangle needs exactly **2 dimensions** once it's anchored — not four. Every extra number you'd add (a second width, a redundant corner position) would *over*-define it and trigger the conflict warning.

**Adding a centered hole:**

- A free circle has 3 DOF: center-x, center-y, radius.
- **Coincident** the center to the origin (or **concentric** with the rectangle's center construction point) → removes 2. 1 DOF left: radius.
- **Dimension** the diameter → removes 1. **0 DOF.** Black.

So the hole needs exactly **1 dimension** once it's centered. Total for the whole "rectangle + centered hole": **3 dimensions** (width, height, hole ⌀), plus the constraints that anchor and center everything. If you find yourself adding a fourth or fifth dimension, *stop* — you've duplicated something a constraint already locked.

> **Do this counting once, deliberately, on your Exercise 1 plate.** After that it becomes intuition: "this entity is still blue, so it has a free DOF; what relationship or number removes it?" That single question, asked over and over, is the entire craft of fully-defining a sketch.

---

## 16. The cost of getting it wrong, in concrete terms

Two failure modes, two real costs:

**Under-defined (left blue).** You extrude a blue profile in Week 2. It looks fine. In Week 5 a teammate edits an upstream dimension, the under-defined geometry resolves to a *different* position than you assumed, and a mounting hole now sits 3 mm off where the drawing says. Nothing errored — the model just silently produced the wrong part. This is the insidious one: under-definition doesn't crash, it *lies*. The fix costs you a re-model and, in a real shop, possibly a scrapped machined part.

**Over-defined (red/yellow).** You add one dimension too many. OnShape immediately turns the conflicting entities red and refuses to accept the sketch cleanly. This one is *loud* — you can't miss it — and the fix is to delete the redundant constraint or dimension. Annoying but cheap, because the software caught it for you at sketch time.

Given the choice, **over-definition is the lesser evil** because it fails loudly and immediately. But the real target is neither: **exactly defined**, every DOF removed once and only once. That's what "fully defined · 0 conflicts" means, and it's the contract every C12 sketch must meet before it earns an extrude.

---

## 17. A glance at what's *not* in this lecture

- **3D fillets, chamfers, shells.** Solid dress-up features — Week 2.
- **Patterns and mirrors of features.** We mirror *sketch* entities this week; mirroring *features* is Week 3.
- **Variables and equations** (driving a dimension by a named variable or a formula). Powerful, but Week 5's topic. This week every dimension is a literal number.
- **Configurations** (one model, many sizes from a table). Week 5.

This lecture is the complete 2D-sketching vocabulary. Everything here recurs in every later week; nothing here becomes obsolete.

---

## 16. Recap

You should now be able to:

- Explain **degrees of freedom** and run the **drag test** to find under-defined geometry.
- Read sketch **color**: blue (under-defined), black (fully defined), red/yellow (conflict), grey (construction).
- Draw lines, rectangles, circles, arcs, and slots with the right tool so constraints come for free.
- Apply **coincident, horizontal/vertical, parallel, perpendicular, tangent, equal, concentric, midpoint, symmetric**, and `fix` — and say which DOF each removes.
- Read and accept/suppress **constraint inference glyphs** while drawing.
- Add **driving** dimensions, recognize **driven** (reference) dimensions, and handle the over-definition prompt correctly.
- **Fully define** a profile with the **minimum** number of dimensions by encoding intent as constraints.

Next, do the exercises — three numbered sketching drills, each ending in a fully-defined, all-black sketch.

---

## References

- *Sketch constraints (Help)*: <https://cad.onshape.com/help/Content/Primary/Tutorials/sketch_constraints.htm>
- *Sketching (Help)*: <https://cad.onshape.com/help/Content/sketch.htm>
- *Dimension tool (Help)*: <https://cad.onshape.com/help/Content/dimensiontool.htm>
- *Introduction to Sketching (Learning Center)*: <https://learn.onshape.com/courses/introduction-to-sketching>
- *Onshape Fundamentals: CAD (Learning Center path)*: <https://learn.onshape.com/learn/learning-path/onshape-fundamentals-cad>
- *Parametric design (background)*: <https://en.wikipedia.org/wiki/Parametric_design>
