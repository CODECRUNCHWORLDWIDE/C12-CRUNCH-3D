# Lecture 1 — OnShape Tour: Documents, Workspaces, the Feature Tree, and Cloud Versioning

> **Duration:** ~2 hours of reading + hands-on.
> **Outcome:** You can describe what a Document, a Part Studio, and an Assembly are without confusing them, create a Document from a blank workspace, navigate the window and the Feature tree, set units, and explain how OnShape's cloud auto-save and Versions graph work.

If you only remember one thing from this lecture, remember this:

> **A Document is the cloud container. A Part Studio is where you model. An Assembly is where you connect parts.** They live *inside* one Document, they are easily confused, and conflating them is the single most common beginner mistake in OnShape. We will not help anyone make it.

---

## 1. The three things people call "a model"

Open OnShape, ask three people "where's the model?", and you'll get three answers — all correct, because they're pointing at different layers.

| Layer | Example | What it is |
|-------|---------|-----------|
| **Document** | "My Bracket Project" | The cloud container. Holds Part Studios, Assemblies, drawings, imported files, and the **entire history** of all of them. The closest thing OnShape has to a "file" — but it is not a file on your disk; it lives in OnShape's cloud. |
| **Part Studio** | "Part Studio 1" | The environment where you draw sketches and build 3D geometry. One Part Studio can contain several solid *parts*. This is where you spend Week 1 through Week 3. |
| **Assembly** | "Assembly 1" | The environment where you insert finished parts and connect them with **mates** so they fit together and move. We get here in Week 4. |

A Document is shown as **tabs along the bottom** of the OnShape window — exactly like sheet tabs in a spreadsheet. Each tab is a Part Studio, an Assembly, a drawing, or an imported file. When you create a brand-new Document, OnShape gives you one empty **Part Studio** tab to start, and that is where this week happens.

> **Why this matters now.** People who think "the Document is the part" get confused the first time they put two parts in one Part Studio, or the first time they need an Assembly. Build the mental model correctly on day one: **Document = container, Part Studio = modeling, Assembly = mating.**

There is no "Save" button anywhere in OnShape. This unnerves people coming from desktop CAD. OnShape **auto-saves every change to the cloud continuously**, and the full edit history is recorded. We'll come back to what that means for versioning in §10.

---

## 2. Creating your first Document

From the OnShape **Documents** page (the dashboard you land on after signing in):

1. Click the blue **Create** button (top-left) → **Document**.
2. Name it something real — `C12-W1-Onboarding`, not `Untitled`. Names are searchable; future-you will thank present-you.
3. Click **OK**.

OnShape opens the Document with a single empty Part Studio tab. You're now looking at the modeling window. Take a breath and learn the room before you draw anything.

---

## 3. The OnShape window, region by region

```
┌──────────────────────────────────────────────────────────────────────┐
│  Document name · menu bar · share · versions                          │  top bar
├───────────────┬──────────────────────────────────────────────────────┤
│               │                                          ┌──────────┐ │
│  Feature      │                                          │ view cube│ │
│  tree         │            graphics area                 └──────────┘ │
│  (history)    │         (where geometry appears)                      │
│               │                                                       │
│  Origin       │              ·origin·                                 │
│  Top plane    │                                                       │
│  Front plane  │                                                       │
│  Right plane  │                                                       │
├───────────────┴──────────────────────────────────────────────────────┤
│  ▣ Sketch  ⬚ Extrude  ⟳ Revolve  …  feature toolbar  …               │  bottom toolbar
├──────────────────────────────────────────────────────────────────────┤
│  Part Studio 1 │ + (add tab)                                          │  document tabs
└──────────────────────────────────────────────────────────────────────┘
```

The five regions you must know by name:

- **Feature tree** (left panel). The ordered, top-to-bottom list of everything you've done in this Part Studio. At the top, before you've drawn anything, it already contains the **Origin** and the three default planes: **Top**, **Front**, **Right**. Every feature you add — sketches, extrudes, fillets — appends to this list in order. This ordering *is* your design intent; Week 3 is largely about controlling it.
- **Graphics area** (center). The 3D viewport where geometry appears. The **origin** — the (0,0,0) point — sits in the middle by default.
- **View cube** (top-right corner of the graphics area). A little cube you click to snap to standard views (Top, Front, Right, isometric). Clicking a corner gives you an isometric view; clicking a face looks straight at that face.
- **Feature toolbar** (bottom strip). The icons that create features: **Sketch**, **Extrude**, **Revolve**, **Fillet**, and so on. This week we live almost entirely on the leftmost icon, **Sketch**.
- **Document tabs** (very bottom). One tab per Part Studio / Assembly / drawing.

There's also a **top menu bar** (Document name, the share button, and — important for §10 — the **Versions and history** button, which looks like a little branching-graph clock icon).

---

## 4. Mouse navigation — learn this before you draw

CAD is a spatial tool. If you can't fluidly rotate, pan, and zoom, everything else is misery. OnShape's default 3-button-mouse scheme:

| Action | How |
|--------|-----|
| **Rotate** (orbit) | **Right-click drag** in empty space |
| **Pan** | **Middle-click (scroll-wheel) drag**, or **Ctrl + right-drag** |
| **Zoom** | **Scroll wheel** (zooms toward the cursor) |
| **Zoom to fit** | Press **`f`**, or double-click the scroll wheel in empty space |
| **View normal to** a face/plane | Select the face/plane, then press **`n`** (looks straight down at it) |
| **Standard views** | Click the **view cube** faces and corners, or press **`Shift`+ number keys** |

> **Trackpad survival.** If you're on a laptop trackpad with no real mouse, OnShape has a touch-friendly mode, but you will fight it. Borrow, buy, or scavenge a three-button mouse before Tuesday. This is not optional advice; it's the difference between enjoying this course and resenting it.

Practice now: rotate the empty scene with right-drag, watch the three planes tilt, press **`f`** to recenter, and click an isometric corner on the view cube. Do it ten times. Build the reflex before there's geometry to fuss over.

---

## 5. The three default planes and the origin

Before you draw anything, expand the top of the Feature tree. You'll see, under the Origin:

- **Top** plane — horizontal, like looking down at a tabletop.
- **Front** plane — vertical, facing you.
- **Right** plane — vertical, facing left/right.

They all intersect at the **origin**, the (0,0,0) point. These three planes are your starting canvases. To begin a sketch, you click the **Sketch** tool and then click one of these planes (or, later, a flat face of an existing part).

> **Anchor to the origin — always.** The single most important habit in Week 1: your *first* sketch in any Part Studio should be tied to the origin, so the geometry can never float off into space. The cleanest way is to draw a center-point rectangle or circle *starting from the origin point itself* — OnShape snaps to it and adds a coincident constraint automatically. We drill this in Exercise 1. A sketch that isn't anchored to the origin is the #1 cause of "why did my whole part jump when I edited it?"

Which plane should you sketch on? Convention, and the one we follow in C12:

- **Top plane** for parts that are naturally "lying flat" — plates, gaskets, the flat washer and name plate in this week's mini-project.
- **Front plane** for parts you think of as standing up and looking at from the front — a bracket profile, a revolve profile for a bottle (Week 2).
- **Right plane** for profiles seen from the side.

There is no wrong answer that can't be fixed, but choosing the natural plane up front keeps your model intuitive when you open it six weeks later.

---

## 6. Entering and leaving a sketch

Click the **Sketch** icon (bottom toolbar, far left), then click the **Top** plane in the graphics area. Three things happen:

1. OnShape **orients the view normal** to that plane (you're now looking straight at it).
2. A new **Sketch** feature appears in the Feature tree (named "Sketch 1").
3. The **sketch toolbar** appears, full of 2D tools: line, rectangle, circle, arc, slot, dimension, the constraint icons.

You are now *inside* a sketch. Everything you draw belongs to this sketch feature. When you're done, click the green **✓ checkmark** (top-right of the graphics area) to **accept and exit** the sketch, or the **✗** to discard it. Exiting drops you back into the Part Studio with your sketch recorded as a feature.

To **re-edit** a sketch later: double-click it in the Feature tree (or right-click → Edit). You can always go back. Nothing is ever destroyed; this is parametric CAD.

> **Sketch geometry vs construction geometry.** Inside a sketch, you can toggle any entity to **construction** (the keyboard shortcut is **`q`**, or use the construction toggle in the sketch toolbar). Construction lines are reference-only — dashed, and they never become part of a 3D feature. You use them for centerlines, bolt-circle radii, and symmetry axes. We use construction geometry heavily in Exercise 3 and the challenge.

---

## 7. The Feature tree as a history

The Feature tree is **not** a static list of "things in the scene." It is an **ordered recipe**, executed top to bottom every time the model rebuilds. This is the heart of parametric CAD and the thing that makes it different from "drawing" software.

- Each feature is computed **using the result of the features above it**. Sketch 1 → Extrude 1 (uses Sketch 1) → Fillet 1 (uses Extrude 1's edges), and so on.
- There's a **rollback bar** at the very bottom of the tree. Drag it up and the model rebuilds *as it was* at that earlier point — every feature below the bar is temporarily suppressed. This lets you insert a feature *in the middle* of the history.
- You can **rename** any feature (double-click its name) and **reorder** features (drag them) as long as you don't break a dependency.

This week your tree will be short — usually just one or two sketches. But start the habit now: **rename your sketches** to something meaningful ("Master profile," not "Sketch 1"). In Week 3 a tree with 25 features named `Sketch 1 … Sketch 12` is unreadable; a tree with named features is documentation.

---

## 8. Setting units and precision

Before you dimension anything, set the Document's default unit. OnShape supports mixed units (you can type `1 in` in a millimeter document and it converts), but you want a sensible default.

- Open the **document menu** (the menu under the Document name, top-left) → **Workspace units**, *or* click the **gear / units indicator** at the bottom-right status bar.
- Set **Length unit** to **millimeter** (the C12 default — most of the world's mechanical CAD is metric) or **inch** if your drawings are imperial.
- Set **default precision** (decimal places shown on dimensions) — 2 or 3 places is plenty this week.

When you place a dimension, you can always type the unit inline to override: typing **`25.4 mm`** or **`1 in`** both produce a one-inch dimension regardless of the document default. OnShape parses the unit you type.

> **Pick a unit and stick with it.** Mixing units silently across a project is how parts end up 25× too big. For C12 we standardize on **millimeters** unless a drawing is explicitly in inches. The challenge drawing this week is metric.

---

## 9. Parts, the Parts list, and the difference from the Feature tree

As you build 3D geometry (Week 2 onward), the solid bodies you create show up in a **Parts list** at the top of the Feature tree, *separate* from the feature history below it. Don't confuse them:

- The **Feature tree** is the *recipe* (the ordered steps).
- The **Parts list** is the *result* (the solid bodies that exist right now).

This week you produce **zero parts** — just sketches — so your Parts list stays empty. That's expected and correct. We don't extrude until Week 2. The whole point of Week 1 is that the discipline lives in the sketch, before any solid exists.

---

## 10. Cloud versioning — auto-save, history, and named Versions

OnShape has no Save button because it saves *constantly*. Every edit streams to the cloud and is recorded. That has two big consequences you need to understand.

### Auto-save and the live workspace

The Part Studio you're editing is a **workspace** (the default one is called **Main**). Every change is live and saved. If your browser crashes, you reopen the Document and you're exactly where you left off — nothing lost, nothing to recover.

### The Versions and history graph

Click the **Versions and history** icon in the top bar (the little graph/clock). You'll see a **vertical graph** of the Document's life: the live **Main** workspace at the top, and below it any **named Versions** you've created, plus an automatic, fine-grained **history** of every edit.

- **History** is automatic and continuous — OnShape logs every operation. You can scrub back through it and even restore an earlier state.
- A **Version** is something *you* create deliberately: a named, **immutable snapshot** ("v1 — master sketch complete"). Versions are the stable points you share, branch from, or reference from a drawing.

### Why you create a Version

1. **Sharing a stable point.** When you hand work off, you share a *Version*, not the live workspace — so your collaborator sees a frozen, known-good state even while you keep editing Main.
2. **Branching.** You can create a **branch** off a Version to try a redesign without disturbing Main, then **merge** it back. This is Git-style version control, built into CAD. We use it lightly this week and heavily by Week 6.
3. **References.** Drawings and inserted parts can reference a specific Version, so an upstream change doesn't silently break downstream consumers.

**To create a Version:** open Versions and history → **Create version** → name it. For this week's mini-project, you'll create a Version named something like `w1-master-sketch` once your master sketch is fully defined. That's your deliverable's stable tag.

> **Versions are immutable; the workspace is live.** Internalize this split. You edit in the live Main workspace; you *freeze* a Version when you reach a milestone. It's exactly the workspace-vs-commit distinction from Git, applied to a 3D model.

### Sharing

The blue **Share** button (top bar) lets you share a Document (or a specific Version) with another OnShape user by email, or generate a link. For C12 homework you'll share your Document read-only with your reviewer, or export a screenshot — both are covered in the homework instructions.

---

## 11. Branches, merges, and collaboration (a preview)

OnShape's versioning isn't just a linear backup — it's genuinely Git-style. From any **Version**, you can create a **branch**: an independent line of edits that diverges from Main. You redesign on the branch, leave Main untouched, and when you're happy you **merge** the branch back. OnShape walks you through any conflicts (two people changed the same feature) much the way a code merge tool does.

You won't *need* branching in Week 1 — your work is a single sketch on a single workspace — but it's worth seeing the shape of it now, because it's the reason OnShape can claim "version control for CAD":

- **Main** is your live, default workspace. Edits stream here continuously.
- A **Version** is a frozen, named point in Main's history (immutable).
- A **branch** starts from a Version and lets you experiment in parallel.
- A **merge** brings a branch's changes back into Main.

Two more collaboration facts to file away:

- **Real-time co-editing.** Multiple people can be *in the same Document at the same time*, and you'll see their cursors and selections live — like a Google Doc for CAD. There's no "check out / check in" lock dance.
- **Followers.** You can "follow" another editor's viewport to watch what they're doing — handy for instructor demos and pair-modeling.

We lean on branching lightly when teams form in Week 4 and heavily for the capstone in Week 6. For now, just know that the **Version** you create at the end of each assignment is the stable point everything else (branches, shares, drawings) hangs off of.

---

## 12. The Documents dashboard and staying organized

Step back out to the **Documents** dashboard (the page you land on after sign-in). This is your home base across the whole course, and a little organization now saves real pain by Week 6 when you have a dozen Documents.

- **Search.** The search bar matches Document *names* — another reason to name things like `C12-W1-Ex1-Plate` rather than `Untitled (3)`.
- **Labels and folders.** You can apply labels and group Documents. Make a `C12` label now and tag every course Document with it; you'll filter to just your coursework instantly.
- **Recently opened** vs **My Documents** vs **Shared with me** vs **Public.** The left rail filters by ownership. Work you create lives in **My Documents**; Documents a classmate shares with you appear under **Shared with me**.
- **Owned vs shared.** When you share a Document, *you* still own it; the recipient gets the access level you granted (view / comment / edit). Sharing does not duplicate the Document — there's one cloud copy, and everyone with access sees the same live data.

> **Make a copy to experiment.** If you want to hack on a *public* Document (or a classmate's shared one) without disturbing it, use **Make a copy** — that forks an independent Document you own. The original is untouched. This is the safe way to take apart someone else's model and see how it's built, which is one of the best ways to learn this week.

---

## 13. The keyboard shortcuts worth learning today

You can drive all of Week 1 from the toolbar, but a handful of shortcuts pay for themselves within an hour. Learn these six now:

| Key | Action |
|-----|--------|
| `f` | Zoom to fit (recenter the whole model) |
| `n` | View **normal to** the selected face/plane (look straight at it) |
| `s` | Open the **shortcut toolbar** (a radial menu of common tools at the cursor) |
| `q` | Toggle selected sketch geometry to/from **construction** |
| `l` | Line tool (inside a sketch) |
| `c` | Circle tool (inside a sketch) |
| `d` | Dimension tool (inside a sketch) |

The full list lives at the keyboard-shortcuts help page (see References). Don't try to memorize all of them — `f`, `n`, and `q` alone will noticeably speed you up this week, and the rest accrete naturally as you model.

> **`s` is the secret weapon.** Pressing `s` inside a sketch pops a small, customizable radial of your most-used tools right at the cursor, so you stop traveling to the toolbar for every line and circle. Set it up once with the tools from Lecture 2 and your sketching speed roughly doubles.

---

## 14. Reading and editing the Feature tree like a pro

We touched the Feature tree in §7, but it rewards a closer look because it is the spine of every Part Studio you'll build for six weeks. Five operations you should be able to do without thinking:

1. **Rename** — double-click a feature's name. Do this *as you go*, not at the end. `Master profile`, `Outer bore`, `Mounting holes` — names are free documentation, and a 25-feature tree of `Sketch 1 … Sketch 12` is unreadable by Week 3.
2. **Roll back** — drag the rollback bar (bottom of the tree) up to an earlier point. The model rebuilds *as it was*, suppressing everything below the bar. This lets you insert a feature in the *middle* of the history rather than always at the end — crucial when you realize step 3 should have come before step 7.
3. **Reorder** — drag a feature up or down. OnShape lets you, *unless* it would break a dependency (you can't move a feature above the geometry it was built on). A red error tells you when you've crossed a dependency.
4. **Suppress** — temporarily disable a feature without deleting it (right-click → Suppress). Great for testing "what does the part look like without this?" The feature greys out; un-suppress to bring it back.
5. **Edit** — double-click any feature to reopen its dialog (or, for a sketch, re-enter the sketch). Nothing in OnShape is write-once; every feature is editable forever. This is the defining property of *parametric* CAD.

> **The tree *is* the design intent.** The order of features encodes which geometry depends on which. A well-ordered, well-named tree is the difference between a model a colleague can confidently edit and one they're afraid to touch. We grade the mini-project partly on tree hygiene starting in Week 3 — build the habit now, even though this week your tree is just one or two sketches.

There's also a **search box** at the top of the tree (handy once trees get long) and small **status icons** beside each feature: a clean feature is silent; a feature with a problem shows a warning (⚠) or error (✕) icon you can hover for the message. A sketch that isn't fully defined shows a small indicator too — another way to catch leftover blue before it bites you.

---

## 15. Comments, the part list color chips, and other small UI affordances

A few smaller pieces of the window that you'll meet this week and shouldn't be mystified by:

- **Comments.** OnShape has a built-in comment thread per Document (the speech-bubble icon). You can pin a comment to a specific feature or face. For coursework, this is where a reviewer leaves feedback *attached to the geometry it's about* — far better than a separate email.
- **The selection filter.** When you're trying to click an edge but keep grabbing a face, the selection-filter controls let you restrict what's selectable (only edges, only faces, only sketch entities). You rarely need it in Week 1, but know it exists for when a busy sketch fights your clicks.
- **Measure.** Select any geometry and OnShape shows quick measurements (length, distance, angle) in the lower-right. This is a *reference* readout, not a dimension — it doesn't change anything, it just tells you the current value. Useful for sanity-checking a sketch ("is that edge really 80 mm?") without adding a driven dimension.
- **Undo / redo.** Standard `Ctrl/Cmd+Z` and `Ctrl/Cmd+Y`. Because everything auto-saves, undo works across the live session normally; for going further back, you use the history graph (§10) rather than mashing undo.
- **The display / view-settings menu.** Toggles for the grid, shaded vs wireframe, section views (Week 5), and — importantly this week — **Show constraints** and **Show dimensions** inside a sketch.

None of these are deep, but knowing they're there means you won't waste time hunting. The OnShape window is dense; spend a few minutes hovering over icons to see their tooltips before Tuesday.

---

## 16. A word on what's *not* in Week 1

- **No extrudes, revolves, or any 3D.** That's Week 2. This week is sketches only. If you find yourself wanting to extrude, resist — the discipline is to make the *sketch* perfect first.
- **No Assemblies, no mates.** That's Week 4.
- **No drawings, dimensions sheets, or GD&T frames.** That's Week 5. (We *use* dimensions inside sketches this week, but we don't produce a drawing document.)
- **No FeatureScript** (OnShape's scripting language). C12 is a modeling course, not a programming course — there is no code anywhere in it. If you're curious, FeatureScript exists, but we never touch it.

Week 1 is the Document, the Part Studio, the sketch environment, and the constraint discipline. By Friday you can create a Document, navigate it fluidly, and produce a fully-defined master sketch — without referring to a tutorial.

---

## 12. Common first-day mistakes (and the fix)

| Mistake | Symptom | Fix |
|---------|---------|-----|
| Sketch not anchored to the origin | The whole sketch drags freely; geometry "floats" | Tie the first point to the origin (coincident). Redraw the anchor or add a coincident constraint to the origin. |
| Leaving a sketch under-defined | Lines stay **blue**; geometry shifts on edit | Add constraints/dimensions until everything is **black**. The status bar says "Fully defined." |
| Confusing the Document with the part | "Where did my other part go?" | Remember: a Part Studio can hold many parts; the Document holds many tabs. Check your tabs. |
| Drawing in the wrong plane | The part is oriented sideways later | Pick Top/Front/Right intentionally per §5. You can edit a sketch's plane, but choose well up front. |
| Hunting for a Save button | "I don't trust that it saved" | There isn't one. It's saved. Trust the cloud; verify with Versions and history. |
| Wrong / mixed units | Parts 25× too big or small | Set the workspace unit (§8) before dimensioning. Type the unit inline when in doubt. |

---

## 13. Recap

You should now be able to:

- State what a **Document**, a **Part Studio**, and an **Assembly** are without conflating them.
- Create a Document, name it, and find the empty Part Studio tab.
- Identify the **Feature tree**, **graphics area**, **view cube**, **feature toolbar**, and **document tabs** by name.
- Rotate, pan, zoom, and "view normal to" a plane with a three-button mouse.
- Name the three default planes and explain why every first sketch should anchor to the **origin**.
- Enter and exit a sketch, and toggle **construction** geometry.
- Read the Feature tree as an ordered history with a rollback bar.
- Set the workspace **units** and precision.
- Explain OnShape's **auto-save**, the **history** graph, and why you create a named, immutable **Version** at a milestone.

Next up: the actual craft of sketching — degrees of freedom, every geometric constraint, driving dimensions, and how to make a sketch turn black. Continue to [Lecture 2 — Sketching with Intent](./02-sketching-with-intent-constraints-and-dimensions.md).

---

## References

- *Onshape Fundamentals: CAD (Learning Center path)*: <https://learn.onshape.com/learn/learning-path/onshape-fundamentals-cad>
- *Documents (Help)*: <https://cad.onshape.com/help/Content/documents.htm>
- *Part Studios (Help)*: <https://cad.onshape.com/help/Content/partstudios.htm>
- *Feature list (Help)*: <https://cad.onshape.com/help/Content/featurelist.htm>
- *Planes (Help)*: <https://cad.onshape.com/help/Content/plane.htm>
- *Versions and history (Help)*: <https://cad.onshape.com/help/Content/version_manager.htm>
- *Keyboard shortcuts (Help)*: <https://cad.onshape.com/help/Content/keyboard-shortcuts.htm>
