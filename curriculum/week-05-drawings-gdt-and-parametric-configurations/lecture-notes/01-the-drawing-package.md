# Lecture 1 — The Drawing Package: Views, Dimensions, Title Blocks, BOM & GD&T

> **Duration:** ~2 hours of reading + hands-on in OnShape.
> **Outcome:** You can create a Drawing from a part, place orthographic and section views, dimension them associatively, fill a title block, generate a BOM from an assembly, and read and place a basic GD&T feature control frame.

If you only remember one thing from this lecture, remember this:

> **A model says what the part *is*. A drawing says what the part is *allowed to be*.** The model is one exact set of numbers. A real part is never exactly those numbers — it's machined to a tolerance. The drawing is the contract that says how far from nominal the shop may wander and still ship you a good part. That contract is what GD&T writes down precisely.

---

## 1. Three document types, one source of truth

Up to now you have lived in two OnShape tab types:

| Tab type | What it holds | What you've done with it |
|----------|---------------|--------------------------|
| **Part Studio** | Sketches and features that build one or more solid bodies | Weeks 1–3: sketched, extruded, revolved, patterned |
| **Assembly** | Instances of parts joined by mates | Week 4: inserted parts, added revolute/slider/cylindrical mates |
| **Drawing** | 2D documentation: views, dimensions, notes, title block, BOM | **This week** |

A **Drawing** is a third, distinct tab type. You create it from a Part Studio, a single part, or an Assembly, and it *references* that source. The relationship is **associative**: the views in the drawing are projections of the live model, and when the model changes, OnShape marks the affected views "out of date" and offers to update them. A dimension you place on a view by clicking two edges reads its value *from the model* — change the model, the dimension follows.

This is the single most important mental model of the week. The drawing is not a picture you drew; it's a *live window* onto the model with annotations layered on top. Break that link — by typing a number into a dimension instead of letting OnShape measure it — and you've created a lie that will ship to a machinist. We'll come back to this repeatedly.

> **Where Drawings live.** In OnShape a Drawing is a tab inside the same Document as your Part Studios and Assemblies. Right-click the tab bar at the bottom → **Create drawing**, or right-click a part/assembly → **Create drawing of [name]**. The new tab opens onto a sheet with a template and an empty insertion cursor waiting for your first view.

---

## 2. Creating a drawing: template, sheet size, projection angle

When you create a drawing, OnShape asks three things before you place anything. Get them right now; changing them later is annoying.

**1. Template / sheet size.** A template defines the sheet border and the title block layout. OnShape ships ANSI (inch: A, B, C, D, E) and ISO (metric: A4, A3, A2, A1, A0) templates, in landscape and portrait. Rule of thumb:

- **A-size (8.5×11 in) / A4 (210×297 mm)** — a single small part, a few views.
- **B-size (11×17 in) / A3** — a part with a section and several details, or a small assembly with a BOM.
- **C-size / A2 and up** — large assemblies, dense dimensioning.

Pick the smallest sheet your part reads cleanly on. A part crammed onto A4 at scale 4:1 is worse than the same part on A3 at 1:1.

**2. Scale.** The sheet scale (e.g. `1:1`, `2:1`, `1:2`) sets the default for every base view. You can override per-view later. `1:1` means one drawing unit equals one real unit; `2:1` means the drawing is twice life size (good for small parts); `1:2` is half size (good for big parts).

**3. Projection angle — third vs first.** This is the one beginners get wrong and shops *hate*. There are two conventions for arranging projected views:

- **Third-angle projection** (North America, the OnShape ANSI default): the top view sits *above* the front view, the right view sits to the *right*. The view you see is "as if the object were in a glass box and you unfolded the faces toward you."
- **First-angle projection** (Europe/ISO, the default on ISO templates): the top view sits *below*, the right view sits to the *left*. Mirror image arrangement.

A part dimensioned in third-angle and read by a shop expecting first-angle gets made backwards. The title block carries a little symbol (a truncated cone, two views) declaring which convention the sheet uses — that symbol is not decoration, it's a safety interlock. For this course we use **third-angle** unless a metric/ISO exercise says otherwise. Know that the other exists.

---

## 3. The base view and projected views

Your first action on a fresh sheet is to place a **base view**. OnShape drops a dialog: choose the source (Part Studio / part / assembly), choose the **view orientation** (Front, Top, Right, Iso — or a named view you saved in the Part Studio), and the **scale**. Click to place it.

The base view is your anchor. Every other orthographic view is *projected* from it. Drag from the base view:

- Drag **up** → top view. Drag **down** → bottom view.
- Drag **right** → right view. Drag **left** → left view.
- Drag **diagonally** → isometric view (no projection lines; it's a pictorial).

The projected views stay aligned with the base view and share its scale by default. Move the base view and the projected views follow. This alignment is automatic and enforced — you can't accidentally slide the top view sideways out of alignment with the front. That's a feature, not a limitation; aligned views are how a reader's eye walks from one view to the next.

**View properties you'll set on day one** (right-click a view → Properties, or the view's context toolbar):

- **Scale** — per-view override of the sheet scale.
- **Hidden lines** — show/hide edges behind the part. On for a part with internal features you're not sectioning; off for a clean exterior view.
- **Tangent edges** — the soft lines where a fillet blends into a flat face. Convention: show them "with font" (as thin/phantom lines) or hide them. Hidden is cleaner; shown helps a reader see the fillets.
- **Centerlines / center marks** — auto-add centerlines to holes and cylinders. Turn these on; a hole without a center mark reads as ambiguous.

> **A clean starter layout.** For a typical bracket: Front view as the base (the most informative silhouette), Top projected above it, Right projected to its right, and an Iso in a corner for human readability. Three orthos + one iso is the bread-and-butter layout. Add sections and details only where the three orthos can't tell the whole story.

---

## 4. Section views: showing the inside

An orthographic view with hidden lines on can show internal features, but a part with several internal pockets becomes a spaghetti of dashed lines that nobody can read. The fix is a **section view**: an imaginary cut through the part, drawn as if you sawed it open and looked at the freshly-cut face.

To create one in OnShape: select **Section view**, click to define the **cutting-plane line** across an existing view (usually straight through the centerline of the feature you want to expose), then drag to place the resulting section. OnShape draws the cut face with **hatching** (diagonal section lines) and labels the section with letters — `SECTION A-A` — matching the cutting-plane line you drew.

Types you should know:

- **Full section** — the cutting plane goes all the way through. The default and most common.
- **Half section** — half the view is sectioned, half is left as an exterior view. Good for a symmetric part where you want to show inside and outside in one view.
- **Offset / aligned section** — the cutting plane jogs to pass through features that don't all lie on one straight line (e.g., a bolt circle). The aligned section rotates angled features into the plane.
- **Broken-out section** — a small local cut (a "scoop") to expose one internal feature without sectioning the whole view.

**When to section vs when to add another ortho:** if the feature is on an *outside* face, add the ortho that faces it. If the feature is *buried inside* (a counterbore, an internal boss, a cored wall), section it. A wall thickness is almost always communicated with a section — you cannot dimension a wall you can't see.

**Detail views** are the companion tool: a circular zoom-in of a small region, drawn at a larger scale (e.g., `DETAIL B — SCALE 4:1`) so you can dimension a tiny chamfer or a thread relief that's illegible at the sheet scale. Use a detail view whenever a feature is too small to dimension cleanly in the parent view.

---

## 5. Dimensioning: associative is the whole game

Now the part of the lecture that separates a real drawing from a screenshot.

You dimension a view by selecting geometry (an edge, two edges, a vertex, a circle) and placing a dimension. OnShape's dimension tool is context-sensitive: pick one line → length; pick two parallel lines → distance between; pick a circle → diameter; pick an arc → radius; pick two lines that meet → angle. Drag to place the dimension line and text.

The number OnShape writes is **read from the model**. This is an **associative dimension**. If you go back to the Part Studio and change the slot length from 40 mm to 50 mm, the drawing view updates and *the dimension now reads 50*. You did not touch the drawing. That is the entire point of model-based drawings, and it's why we don't let you type numbers.

> **The cardinal sin: overriding a dimension.** OnShape *will* let you double-click a dimension and type a different value to display. Don't. An **overridden dimension** shows whatever you typed regardless of the model. It's how a drawing comes to say "50 mm" over a part that's actually 40 mm — and that part gets made wrong, on your name in the title block. OnShape renders overridden dimensions in a distinct color (and flags them) precisely because they're dangerous. The only legitimate use is rare and deliberate (e.g., a not-to-scale note), and you annotate it explicitly. For this course: **zero overridden dimensions.** Treat one like a compiler error.

**Dimensioning schemes** — how you *organize* dimensions matters as much as their values:

- **Chain dimensioning** — each dimension starts where the last ended. Tolerances *stack*: five chained ±0.1 dimensions can accumulate ±0.5 of error at the far end. Use sparingly.
- **Baseline dimensioning** — every dimension is measured from one common edge (the datum). Tolerances don't stack because every feature references the same origin. Preferred when location precision matters.
- **Ordinate dimensioning** — like baseline but drawn as a tidy set of numbers from a 0,0 origin, no dimension lines. Great for a plate full of holes.

**What to dimension:** every feature a machinist needs to make the part, *and no more*. Don't dimension the same thing twice (that's an over-defined, contradiction-prone drawing). Don't dimension a feature you created by a derived relationship (a mirrored hole is located by symmetry, not by re-dimensioning). A good drawing is *fully* dimensioned and *not over*-dimensioned — the same discipline you learned for sketches in Week 1, now applied to documentation.

---

## 6. The title block: what a shop reads first

Every template has a **title block** in the lower-right corner. A machinist reads it *before* they look at a single view. Fill these fields — they come from the model's **part properties**, so set them on the part, not by typing into the block:

| Field | What it carries | Where it comes from |
|-------|-----------------|---------------------|
| **Part number** | The unique ID for this part (e.g., `CC-BRKT-001`) | Part property → Part number |
| **Title / description** | Human name ("Mounting Bracket") | Part property → Description |
| **Revision** | Which rev of the part this drawing documents (`A`, `B`, `C`…) | Part property / drawing property |
| **Material** | What it's made of (6061-T6 aluminum, ABS, …) | Part property → Material |
| **Finish** | Surface treatment (anodize, bead-blast, as-machined) | Note / property |
| **Scale** | The sheet scale | Sheet setting |
| **Units** | mm or in | Drawing property |
| **Sheet x of y** | Which sheet in a multi-sheet set | Sheet setting |
| **Drawn by / date** | Who made the drawing and when | Drawing property |
| **Tolerance block** | The "unless otherwise specified" general tolerance | Template note |

The reason to drive the title block from **part properties** rather than typing is the same as associativity: set the part number once on the part, and it flows to the title block *and* the BOM *and* the configured variants. Type it by hand in three places and you'll have three different numbers within a week.

### The general tolerance block

Buried in the title block (or just above it) is a small note like:

```
UNLESS OTHERWISE SPECIFIED:
DIMENSIONS ARE IN MILLIMETERS
.X   = ±0.5
.XX  = ±0.25
.XXX = ±0.1
ANGLES = ±0.5°
```

This is load-bearing. It means: *any dimension on this drawing with no explicit tolerance inherits these defaults based on how many decimal places it has.* A dimension written `40` gets ±0.5; `40.00` gets ±0.25. So **the number of decimal places you write is itself a tolerance decision.** Write `12.000` only if you really need ±0.1; otherwise you're asking the shop for precision (and cost) you don't need. New drafters over-decimal everything and quietly triple the machining bill.

---

## 7. Bill of Materials and balloons (from an assembly)

When the drawing documents an **Assembly**, you can auto-generate a **Bill of Materials (BOM)** — the table that lists every part, its quantity, and its identifying properties. Insert it from the drawing toolbar; OnShape walks the assembly's part instances and rolls them up:

| Item | Qty | Part Number | Description | Material |
|-----:|----:|-------------|-------------|----------|
| 1 | 1 | CC-BASE-001 | Base Plate | 6061-T6 |
| 2 | 1 | CC-ARM-002 | Pivot Arm | 6061-T6 |
| 3 | 2 | CC-PIN-003 | Shoulder Pin | 303 SS |
| 4 | 4 | MCM-91290A115 | M3×10 SHCS | — (library) |

Two parts that are *the same part* roll up into one row with `Qty = 2`. The columns are configurable — add/remove/reorder them, and pull any part property in as a column. **Item numbers** are assigned by the BOM and are what the balloons reference.

**Balloons** are the little numbered circles you place on the assembly view, each leader pointing at one part and showing its BOM item number. Auto-balloon places one per part; or place them by hand for control. The reader cross-references: balloon `3` on the view → row `3` in the BOM → "Shoulder Pin, qty 2." BOM + balloons is how an assembly drawing tells someone what to order and where each piece goes.

> **This is where Weeks 4 and 5 join.** The assembly you built in Week 4 already has the part instances. This week that assembly *becomes documentable*: its mates define the geometry, its part properties feed the BOM, and the drawing tab turns it into something a stockroom can fulfill.

### Part properties: the single source of truth

Both the title block and the BOM read the same underlying data: **part properties**. A part in OnShape carries properties — Part number, Description, Material, Revision, and any custom fields your company defines — and they live *on the part*, in the Part Studio, not on the drawing. This matters because:

- Set the **part number** once on the part. It flows to the title block of every drawing of that part, every BOM row that part appears in, and every configured variant (each config can override it). Type it three times by hand and you'll have three different numbers within a week — a classic data-integrity bug, just in CAD instead of a database.
- Assign **Material** from OnShape's material library (not as free text) and you get not just a title-block string but a density, which OnShape uses to compute the part's **mass** — another property you can surface in the BOM or a note.
- **Revision** is the one field people forget to bump. When you change a released part, the revision goes `A → B`, and *the drawing's revision must match*. A drawing showing rev A geometry but labeled rev B is the documentation equivalent of a stale cache.

The discipline here is exactly the associativity discipline from dimensions: **one source of truth, referenced everywhere, never duplicated.** A drawing that hand-types data that exists on the part is the same anti-pattern as a dimension typed by hand to match the model — it works until the model changes, then it lies.

---

## 8. Reading a drawing top to bottom (the muscle worth building)

Before you place a single GD&T frame, you should be able to *read* a drawing the way a shop does. The reading order is not random:

1. **Title block first.** Part number (what am I making?), revision (which version?), material (what stock?), scale (how big is it really?), units (mm or inch?), projection symbol (third- or first-angle?). A machinist who skips this and dives into views makes the wrong thing in the wrong material at the wrong scale.
2. **The general tolerance note.** "Unless otherwise specified, ±0.25." This sets the default precision for every un-toleranced number, so the machinist now knows how tight the *unmarked* dimensions are before reading any of them.
3. **The views, front first.** The front view is the most informative silhouette; the eye then walks to the top (above) and right (beside) to build the 3D picture. Sections and details get read where their cutting-plane lines and circles point.
4. **The dimensions and FCFs.** Now the actual numbers and tolerances — read against the reference frame the datums establish.
5. **The notes.** "Break all sharp edges," "anodize black," "deburr" — the finishing instructions that aren't dimensions.

When you *make* a drawing, you're laying this trail for a reader you'll never meet. A good sheet reads in this order without the reader having to hunt. A bad sheet scatters dimensions across views, hides the section label, and leaves the material blank — and generates a phone call (or a scrapped part) instead of a finished job.

---

## 9. GD&T basics: the grammar of "how exact"

A plus/minus tolerance on a dimension answers "how big," but it's clumsy for answering "how *located*," "how *flat*," or "how *square*." That's what **Geometric Dimensioning and Tolerancing (GD&T)** is for. We cover only the basics — enough to read a real drawing and place three controls correctly. The full standard (ASME Y14.5) is a career's worth.

### Datums: the reference frame

A **datum** is a theoretically perfect reference — a plane, an axis, or a point — that you measure everything else from. You label them `A`, `B`, `C` with a **datum feature symbol** (a boxed letter on a leader touching the surface). The order matters: `A` is the *primary* datum (the surface the part sits on, removing 3 degrees of freedom), `B` the *secondary* (an edge that aligns it, removing 2 more), `C` the *tertiary* (removing the last 1). Together `A|B|C` form the **Datum Reference Frame (DRF)** that fully locks the part in space, exactly the way mates locked degrees of freedom in Week 4 — the mental model transfers directly.

### The feature control frame (FCF)

A geometric tolerance is written in a boxed **feature control frame**, read left to right:

```
┌─────┬────────┬───┬───┬───┐
│  ⌖  │ ⌀0.2 Ⓜ │ A │ B │ C │
└─────┴────────┴───┴───┴───┘
   │       │       └───┴───┴── datum references (measured from A, then B, then C)
   │       └── tolerance: a 0.2 diameter zone, at Maximum Material Condition
   └── the characteristic symbol: ⌖ = position
```

Read it as a sentence: *"the position of this feature's axis must lie within a 0.2 mm diameter cylindrical tolerance zone, located by basic dimensions from datums A, B, and C, with the bonus tolerance allowed at maximum material condition."* The Ⓜ (MMC modifier) is a bonus-tolerance rule for holes — as the hole drills bigger than its smallest allowed size, you earn extra position tolerance — but you only need to *recognize* it this week, not master it.

### Basic dimensions

A **basic dimension** is a boxed number — `[40]` — that is *theoretically exact* and carries **no tolerance of its own**. It establishes the true location; the tolerance comes from the FCF that references it. So you don't write `40 ±0.1` *and* a position tolerance; you write a basic `[40]` to say where the hole's true center is, then a position FCF to say how far the actual center may stray. Mixing the two (a toleranced location *and* a position FCF) double-defines the feature — the GD&T equivalent of an over-dimensioned sketch.

### The three controls you'll actually place this week

1. **Flatness** (`▱`) — a *form* control on a single surface. "This face must lie between two parallel planes 0.1 apart." It references **no datum** (a surface's flatness is measured against itself). Place it on the FCF attached to a face. Use it on a sealing surface or a precision mounting face.

2. **Perpendicularity** (`⊥`) — an *orientation* control. "This face/axis must be square to datum A within 0.1." References one datum. Use it where a boss must stand square to a base.

3. **Position** (`⌖`) — a *location* control, the workhorse of GD&T. "This hole's axis must lie within a ⌀0.2 zone at its basic location from A|B|C." References the DRF. Use it on every located hole that mates with something — position is what guarantees your bolt pattern will actually line up with the part it bolts to.

In OnShape you place these from the drawing's annotation toolbar: add the **datum feature symbols** first (A, B, C on their surfaces), then add a **geometric tolerance** FCF and pick the characteristic, the tolerance value, and the datum references from a dialog. OnShape renders the standard symbols for you. Place a **basic dimension** by selecting an ordinary dimension and toggling it to *basic* (it gets boxed and loses its tolerance).

> **Why a hobbyist should still learn this.** Even if you're 3D-printing in your bedroom, GD&T teaches you to *think in tolerances*: which surface is the reference, which features must be precise, and which can be sloppy. That thinking makes you design parts that actually assemble. And the moment you send a part to a real machine shop or a fabrication service, the GD&T frame is the difference between "made to print" and "made wrong, and it's on your drawing."

---

## 10. Export: the right file for the right reader

A finished drawing isn't done until it leaves OnShape in a format the reader can use. Match the format to the audience:

| You're handing it to… | Give them… | Why |
|-----------------------|-----------|-----|
| A machinist / fabricator | **Drawing → PDF** | A human-readable, dimensioned, toleranced sheet. The PDF *is* the manufacturing instruction. |
| A laser/waterjet/CNC cutter (flat parts) | **DXF/DWG** of the flat profile | Vector geometry their machine reads directly. |
| A CAM programmer / another CAD tool | **Part → STEP (AP242)** | Neutral solid-model exchange. AP242 can even carry the dimensions and tolerances (PMI) with the geometry. |
| A 3D printer / slicer | **Part → STL** (or 3MF) | A triangle mesh. No dimensions, no tolerances — the slicer only needs the surface. **Never** hand a machinist an STL. |
| Someone who'll re-edit it in CAD | **Native OnShape link** or STEP | A link keeps full feature history; STEP keeps geometry but loses the feature tree. |

Export the drawing from the Drawing tab (top-right → Export → PDF/DXF). Export the model from the Part Studio/Assembly (right-click the tab or part → Export → STEP/STL). When you export STEP, prefer **AP242** over AP203/AP214 if PMI matters; when you export STL, set a resolution fine enough that curves don't facet visibly but not so fine the file balloons.

---

## 11. Revisions and the discipline of "released"

A drawing isn't a one-shot artifact; it lives across the life of the part. Two concepts close the loop:

- **Versions.** OnShape's document history lets you name a **version** ("V1 — drawing complete") — an immutable snapshot you can always return to or branch from. Before you export a PDF that goes to a shop, *create a named version*. Then if someone asks "what did we send them in March?" you have the exact frozen state, not a model that has drifted three edits since.
- **Revisions.** A **revision** (rev A, B, C…) is the *released* identity of the part/drawing — the thing the rest of the world references. When you change a released part, you bump the revision, update the drawing's revision block, and re-release. The revision and the version are different: a version is internal history; a revision is the public, controlled identity. The drawing's revision must always match the geometry it shows.

This is the CAD analogue of version control: versions are commits, a named version is a tag, and a revision is a published release. You won't run a full release workflow this week, but understand that a drawing PDF without a version behind it is an untracked artifact — fine for practice, dangerous for production.

---

## 12. Tolerances in depth: plus/minus, limits, and fits

GD&T is the *geometric* layer, but most numbers on a drawing still carry a plain **size tolerance**. You owe it to yourself to know the three notations and the one concept (fits) that turns a tolerance into a working joint.

**The three notations for the same thing.** A 10 mm shaft that may vary ±0.05 can be written three ways, and all three are identical in meaning:

| Notation | Looks like | When to prefer it |
|----------|-----------|-------------------|
| **Bilateral plus/minus** | `10 ±0.05` | The default. Symmetric, easy to read, nominal is obvious. |
| **Unilateral plus/minus** | `10 +0.10 / −0.00` | When the part must never go *under* (or *over*) nominal — e.g., a clearance hole you'll never want tighter. |
| **Limit dimension** | `10.05 / 9.95` | Inspection-friendly: the gauge reads the two numbers directly with no arithmetic. |

In OnShape you set this on the dimension's properties panel: pick the tolerance *type* (None / Symmetric / Deviation / Limits / Basic), then type the values. The dimension on the sheet re-renders in the chosen notation. A `±0` half (the `−0.00` above) is a real, deliberate choice — it says "this direction has zero slack" and the shop will price it accordingly.

**Fits: tolerances that have to work together.** A shaft and the hole it rides in are toleranced *as a pair*. The relationship between the two tolerance ranges is the **fit**, and there are three families:

- **Clearance fit** — the hole is always bigger than the shaft; the part slides or rotates freely. (A pin in a pivot, a bolt in a clearance hole.)
- **Transition fit** — the ranges overlap; you might get a slight clearance or a slight interference depending on where each part lands. (A locating dowel you want snug but removable.)
- **Interference (press) fit** — the shaft is always bigger than the hole; you press or shrink them together and they don't come apart. (A bearing pressed into a housing, a bushing into a bore.)

ISO codes these as letter-number pairs: `H7/g6` is a common running clearance fit, `H7/k6` a transition (locational) fit, `H7/p6` a light press fit. The capital letter is the hole, lowercase the shaft; the number is the tolerance grade (smaller = tighter). You don't need to memorize the table — OnShape and every fit calculator will give you the actual ±values for a given size and fit code — but you must understand that **a hole and its mating shaft are designed together**, and that picking a fit is a design decision with cost and function on both sides. Choose `H7/p6` when you meant `H7/g6` and your "removable" pin becomes a permanent one.

This is exactly the Week 4 lesson in another key: a mate defines *how parts move*; a fit defines *how tightly they touch*. Both are about the relationship between parts, not a single part in isolation.

---

## 13. A drawing checklist (and the mistakes that flunk a review)

Before you call a drawing done, run it against this list. Every item maps to a real failure mode that gets drawings kicked back in a design review:

- [ ] **Every view is up to date.** No "out of date" banner. If the model changed, click *Update views*.
- [ ] **No overridden dimensions.** Scan for the override color. Every number is read from the model.
- [ ] **No dangling dimensions.** Nothing struck-through or pointing at deleted geometry.
- [ ] **Fully dimensioned, not over-dimensioned.** Every feature a shop must make is dimensioned exactly once. No dimension contradicts another.
- [ ] **Title block complete.** Part number, description, material, revision, scale, units, projection symbol, drawn-by — none left as `DEFAULT`.
- [ ] **Projection symbol matches reality.** Third-angle symbol on a third-angle layout.
- [ ] **Section labels resolve.** Every `SECTION A-A` has a matching cutting-plane line; every `DETAIL B` has a matching circle.
- [ ] **Centerlines and center marks** on all holes and cylinders.
- [ ] **GD&T frames reference declared datums.** If an FCF cites datum B, datum B's feature symbol is actually on the sheet.
- [ ] **Basic dimensions are boxed and untoleranced**, and you didn't *also* plus/minus tolerance a position-controlled feature.
- [ ] **BOM resolved** (assembly drawings): every part has an item number, quantities roll up correctly, no `<unresolved>` rows, balloons match BOM items.
- [ ] **Notes present**: "break sharp edges," finish, and any "unless otherwise specified" general note.

The classic review-killers, in rough order of how often they show up:

1. **An overridden dimension** that makes the sheet disagree with the model. Instant fail — the drawing is now a lie.
2. **A missing or wrong projection symbol**, so the part gets made mirrored.
3. **A blank material field**, so the shop calls to ask (best case) or guesses (worst case).
4. **An over-dimensioned feature** — two dimensions that can't both be honored, so the part is uninspectable.
5. **An un-updated view** showing last week's geometry next to this week's dimensions.

None of these are subtle once you know to look. The checklist exists because under deadline pressure everyone forgets one, and the cost of a missed item is a scrapped part or a blown lead time — not a recompile.

---

## 14. Recap

You should now be able to:

- Explain that a Drawing is a third document type that *references* a Part Studio or Assembly, and that views and dimensions are **associative** to the model.
- Create a drawing with the right sheet size, scale, and **third-angle** projection, and place a base view with projected ortho and iso views.
- Add **section** and **detail** views and say when each beats another orthographic.
- Dimension associatively and *never* override a dimension; choose baseline over chain when location precision matters.
- Fill a **title block** from part properties and read the general **tolerance block** (decimal places = tolerance).
- Generate a **BOM** from an assembly and **balloon** the parts.
- Read a **feature control frame**, identify **datums A/B/C**, recognize a **basic dimension**, and place **flatness**, **perpendicularity**, and **position** controls.
- Export the right format — PDF/DXF for the drawing, STEP/STL for the model — for each audience.

Next up: making the part itself flexible. Continue to [Lecture 2 — Parametric Power: Variables, Equations & Configurations](./02-parametric-power-variables-and-configurations.md).

---

## References

- *OnShape Help — Drawings*: <https://onshape-public.document360.io/docs/drawings>
- *OnShape Help — Bill of Materials*: <https://onshape-public.document360.io/docs/bill-of-materials>
- *OnShape Help — Part properties*: <https://onshape-public.document360.io/docs/part-properties>
- *OnShape Help — Export*: <https://onshape-public.document360.io/docs/export>
- *GD&T Basics — feature control frames & datums*: <https://www.gdandtbasics.com/>
- *ASME Y14.5 overview*: <https://www.asme.org/codes-standards/find-codes-standards/y14-5-dimensioning-tolerancing>
