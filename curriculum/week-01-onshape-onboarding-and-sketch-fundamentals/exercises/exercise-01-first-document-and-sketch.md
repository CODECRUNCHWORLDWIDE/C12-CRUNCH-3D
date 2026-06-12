# Exercise 1 — First Document and Sketch

**Goal:** Create a real OnShape Document from a blank workspace, set its units, navigate the window, then draw and **fully define** a simple flat plate with two holes. By the end you'll change a driving dimension and watch the geometry rebuild parametrically. No 3D — just the sketch.

**Estimated time:** 35 minutes.

---

## Setup

You need a free OnShape account and a browser. Sign in at <https://cad.onshape.com/>. A three-button mouse is strongly recommended (see the README). Nothing to install.

---

## Step 1 — Create and name the Document

1. From the Documents dashboard, click **Create** → **Document**.
2. Name it **`C12-W1-Ex1-Plate`**. (Real names are searchable; never leave it `Untitled`.)
3. Click **OK**.

OnShape opens with one empty **Part Studio** tab. You're looking at the modeling window: Feature tree on the left (showing Origin, Top, Front, Right), the graphics area in the center, the view cube top-right, the feature toolbar at the bottom.

---

## Step 2 — Set the units

1. Bottom-right status bar: click the **units indicator** (or use the document menu → **Workspace units**).
2. Set **Length unit** to **millimeter**.
3. Set **default precision** to **2** decimal places.
4. Confirm.

Everything you dimension now defaults to millimeters. You can still type `1 in` inline anywhere to override.

---

## Step 3 — Practice navigation (60 seconds, do it anyway)

Before drawing, build the reflex:

- **Right-drag** in empty space → the planes orbit. Do it a few times.
- **Scroll** → zoom toward the cursor.
- **Middle-drag** (scroll-wheel press) → pan.
- Press **`f`** → zoom to fit / recenter.
- Click an **isometric corner** of the view cube → standard 3/4 view.

---

## Step 4 — Start a sketch on the Top plane

1. Click the **Sketch** icon (bottom toolbar, far left).
2. In the graphics area (or the Feature tree), click the **Top** plane.

OnShape orients the view normal to the Top plane (you're looking straight down at it), adds **Sketch 1** to the Feature tree, and shows the sketch toolbar. You're now *inside* a sketch.

---

## Step 5 — Draw the plate outline (center-point rectangle)

We'll center the plate on the origin so it's symmetric and anchored.

1. Pick the **center-point rectangle** tool.
2. Click **the origin** as the center point. (OnShape snaps to it and shows a coincident glyph — accept it.)
3. Move out and click to place a corner, making a rough rectangle. Don't worry about exact size yet.

You now have a rectangle, centered on the origin, with its sides already **horizontal/vertical** (the rectangle tool added those constraints) and its center coincident with the origin. Most of it is **blue** — the width and height are still free.

---

## Step 6 — Dimension the plate

1. Pick the **Dimension** tool (`d`).
2. Click the **top** horizontal edge → move the cursor up → click to place the dimension → type **`80 mm`**, Enter. The width locks.
3. Click a **side** vertical edge → click to place → type **`50 mm`**, Enter. The height locks.

The rectangle should now be **black** — fully defined. (Centered on origin = both center DOF gone; two dimensions = width and height gone; rectangle tool handled the rest.) Check the status bar: **"Fully defined."**

> If it's still blue somewhere, run the drag test: try to drag a corner. Whatever moves still has a free DOF — usually it means the center didn't actually snap to the origin. Add a **coincident** from the rectangle's center to the origin to fix it.

---

## Step 7 — Add two mounting holes

1. Pick the **center-point circle** tool (`c`).
2. Draw a circle in the **left half** of the plate. Then a second circle in the **right half**. Rough sizes; both blue.
3. Make the two holes the **same size:** select both circles, apply the **equal** constraint. Now they share a radius — dimension *one* and both follow.
4. **Dimension hole diameter:** Dimension tool → click one circle → type **`8 mm`**. Because of `equal`, both holes are now ⌀8.

The holes still float left-right and up-down — they're blue. Lock them:

5. **Vertical placement:** dimension from the bottom edge to a hole center → type **`25 mm`** (centers them vertically on the 50 mm height). Apply to one hole; for the other, you can dimension it too, or use a constraint in step 7.
6. **Center the holes vertically with a constraint instead of a second dimension:** select both hole centers and the horizontal centerline of the plate and apply **midpoint** / **horizontal** alignment, *or* dimension the second hole's vertical position `25 mm` as well. Either works; the constraint approach uses fewer numbers.
7. **Horizontal placement:** dimension each hole center from the nearest vertical edge → type **`15 mm`** for each. (Or: make them **symmetric** about the plate's vertical centerline — draw a construction centerline through the origin, select both holes + the centerline, apply **symmetric**, then dimension only one hole's horizontal position.)

When every circle is **black**, you're fully defined. Status bar: **"Fully defined."**

---

## Step 8 — The parametric payoff

This is the moment the whole course is about.

1. **Double-click** the `80 mm` width dimension → change it to **`120 mm`** → Enter. The plate grows; if you used the symmetric approach, both holes reposition automatically.
2. Double-click the `8 mm` hole diameter → change to **`10 mm`** → Enter. *Both* holes resize together (thanks to the `equal` constraint).
3. Change them back to `80` and `8`.

You just edited a model by changing numbers, and the geometry rebuilt itself. That's parametric CAD. Sit with it for a second — this is why we constrain instead of just drawing.

---

## Step 9 — Exit and create a Version

1. Click the green **✓** to exit the sketch.
2. **Rename** the sketch in the Feature tree: double-click "Sketch 1" → call it **`Plate master sketch`**.
3. Open **Versions and history** (top bar) → **Create version** → name it **`ex1-plate-defined`**.

You've created an immutable snapshot of your fully-defined plate.

---

## Acceptance criteria

You can mark this exercise done when:

- [ ] You have a Document named `C12-W1-Ex1-Plate` with millimeter units.
- [ ] The plate sketch is **fully defined** — all geometry **black**, status bar says "Fully defined."
- [ ] Both holes are **⌀8 mm** and tied together with an **equal** constraint (changing one changes both).
- [ ] The sketch is anchored to the **origin** (the plate is centered on it).
- [ ] You changed the width to 120 mm, saw the geometry rebuild, and changed it back.
- [ ] The sketch is renamed to something meaningful, not "Sketch 1."
- [ ] You created a named **Version**.
- [ ] You can explain, in your own words, why "fully defined" matters and what the **drag test** tells you.

---

## Stretch

- Re-do the hole placement using **symmetric** about a construction centerline so you dimension only *one* hole's horizontal position and the other mirrors. Count how many dimensions you saved.
- Add a third hole at the exact **center** of the plate (coincident with the origin), ⌀5, made equal to... no — keep it independent. Notice it's fully defined with *zero* dimensions because it's pinned to the origin.
- Turn on **Show constraints** and screenshot the decorated sketch. Identify every glyph.

---

## Hints

<details>
<summary>My sketch won't go fully defined — something is still blue</summary>

Run the drag test: grab a blue point and drag. Whatever moves has a free DOF. Most common culprits this week: (1) the rectangle center never actually snapped to the origin — add a coincident; (2) a hole's vertical *or* horizontal position is dimensioned but not both; (3) you drew an extra stray point or line somewhere — look for an orphaned blue dot.
</details>

<details>
<summary>OnShape keeps adding a constraint I don't want while I draw</summary>

That's constraint **inferencing**. The glyph (a small dash, parallel mark, or tangent symbol) shows what it's about to add. To avoid it, move the cursor until the glyph disappears before clicking, then add the constraint you *do* want deliberately afterward.
</details>

<details>
<summary>I can't tell a driving dimension from a driven one</summary>

Driving dimensions are normal text and *control* geometry. Driven (reference) dimensions appear in parentheses/grey and only *report* a value. If OnShape ever asks "make this driven?", it's because the measurement is already locked by your constraints — usually a good sign.
</details>

---

When this feels comfortable, move to [Exercise 2 — Constraint drills](exercise-02-constraint-drills.md).
