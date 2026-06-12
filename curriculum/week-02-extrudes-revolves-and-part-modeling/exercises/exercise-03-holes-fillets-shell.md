# Exercise 3 — Holes, Fillets, and a Shell

**Goal:** Take a solid block, drill manufacturing-correct counterbored mounting holes off a stable points sketch, fillet the structural corners, and shell the whole thing to a uniform wall — making the right **feature-order decision** between fillet and shell. This is the full dress-up toolkit on one part, and it's a direct rehearsal for the mini-project.

**Estimated time:** 50 minutes.

**You build this in:** a Part Studio named `Ex3-Enclosure` in your `C12-Week2` Document, units = mm.

> **This is a CAD modeling task, not code.** Build it by hand in OnShape. The ordering of the last two steps (fillet vs shell) is the heart of the exercise — read §5 and §6 carefully before you click.

---

## What you're making

The base of a small electronics enclosure: a 90 × 60 × 28 mm rounded box, hollowed to a 2.5 mm wall with the **top open**, four internal **boss posts** with **M3 tapped** holes for the lid screws, and **filleted outer corners** that are carried correctly through the wall.

Target dimensions:

| Feature | Value |
|---------|-------|
| Body | **90 mm × 60 mm × 28 mm** |
| Corner radius (plan view) | **6 mm** rounded rectangle |
| Boss posts | **⌀8 mm**, inset **10 mm** from each corner, full inside height |
| Mount holes | **M3 tapped**, blind, **8 mm** deep, centered in each boss |
| Wall thickness (shell) | **2.5 mm**, top face removed |
| Outer vertical corner fillet | **5 mm** |
| Top rim edge break | **0.5 mm** chamfer |

---

## Step 1 — The body (New extrude from a rounded rectangle)

1. Open `Ex3-Enclosure`. Sketch on the **Top** plane.
2. Draw a **center-point rectangle** at the origin, **90 × 60 mm**. Add a **fillet** (sketch fillet, or the corner-round tool) of **6 mm** to all four corners — or model corners sharp and fillet in 3D later (we'll do an outer 3D fillet in Step 5 regardless; either is fine, but a sketched rounded rectangle is cleaner). Fully define — **black**.
3. `Shift+E`. Operation **New**. End condition **Blind**, **28 mm** up. Green check.
4. **Rename** `Body`.

---

## Step 2 — The boss posts (Add extrude, Up to next)

The posts run from the floor up the inside. We build them as solid columns *before* shelling, so the shell carves around them and leaves them solid.

1. Sketch on the **top face** of the body. Draw **four ⌀8 mm circles**, each inset **10 mm** in X and **10 mm** in Y from a corner (use symmetric constraints about both origin planes so all four move together if you edit one — pro move). Fully define.
2. `Shift+E`. Operation **Add**. End condition **Blind**, **28 mm down** so the posts run the full inside height to the floor (arrow pointing **down into** the body). Green check.

   > Cleaner alternative: end condition **Up to face**, pick the bottom inside face — but that face doesn't exist until after the shell, so for now Blind to the floor depth is correct. We'll revisit "build posts up to a face" in Week 3.
3. **Rename** `Bosses`. You now have four solid posts fused into the solid block (you can't see them yet — they're inside the solid).

---

## Step 3 — The mount holes (Hole feature, M3 tapped)

1. Sketch **four points** on the **top face**, each **concentric** with a boss circle (constrain each point coincident with a boss center, or *Use* the boss top edges and pick centers). Fully define. Close the sketch.
2. Invoke the **Hole** feature. Type **Simple**, with **tapped** enabled. **Standard ISO metric**, size **M3**. End condition **Blind**, depth **8 mm**.
3. Pick the four points. Confirm the holes drill **down into** the bosses. Green check.
4. **Rename** `M3 mounts`. These are the lid-screw holes; the lid (a future part) will bolt down into them.

---

## Step 4 — Fillet the structural corners (BEFORE the shell)

This is the deliberate ordering choice. We want the outer corner rounds to be **carried through the wall** so the inside corner is also nicely rounded after shelling. Therefore the fillet goes **before** the shell.

1. `Shift+F` (Fillet). Select the **four outer vertical edges** of the body. (If you used a sketched rounded rectangle in Step 1, those corners are already round — instead select the **top and bottom horizontal outer edges** to round them, radius **3 mm**, and skip the vertical ones.)
2. Radius **5 mm** (vertical edges) or **3 mm** (horizontal edges). Green check.
3. **Rename** `Outer corner fillet`.

> **Why before the shell?** A fillet on the solid, then shelled, gives a uniform-thickness wall that follows the round on both the outside and the inside. Fillet *after* shelling a 2.5 mm wall with a 5 mm radius would exceed the wall → zero-thickness → red. Order is design intent.

---

## Step 5 — Shell it (top face removed)

1. Invoke **Shell**. 
2. **Faces to remove:** click the **top face** (the open mouth of the enclosure). 
3. **Thickness:** **2.5 mm**, direction **inward** (keeps the 90 × 60 outer footprint).
4. Green check. The block is now a 2.5 mm-walled open box — and the four bosses survive as **solid posts** inside it (because they were solid before the shell carved the cavity around them). Orbit and look inside; or `right-click a side face → Section view` to inspect the wall thickness and posts.
5. **Rename** `Shell`.

---

## Step 6 — Break the top rim (chamfer, AFTER the shell)

A tiny edge break on the rim — this one is purely cosmetic/surface, so it goes **after** the shell.

1. Invoke **Chamfer**. Select the **top rim edges** (the thin 2.5 mm rim now exposed). Mode **Equal distance**, **0.5 mm**.
2. Green check. **Rename** `Rim break`.

> **Why after the shell?** This chamfer lives only on the surface of the finished wall — it doesn't need to be carried through anything. Surface-only dress-up goes last. Contrast with Step 4's fillet, which had to be carried through the wall and therefore went first.

---

## Step 7 — The rebuild test

1. Edit `Shell` and change thickness **2.5 → 3.5 mm**. Regenerate. Posts still solid, holes still present, fillets fine (3.5 mm wall < 5 mm fillet room). **No red features.**
2. Now push it: change shell thickness to **6 mm**. Regenerate. This likely turns `Shell` or `Outer corner fillet` **red** because a 6 mm wall fights the 5 mm fillet / boss spacing. **Diagnose it:** roll back, read the error, and either reduce the thickness or note exactly which feature breaks and why. Then **set it back to 2.5 mm.** Watching it break and fixing it *is* the exercise.
3. Edit `Body` height **28 → 36 mm**. Regenerate. Posts (Blind to floor depth) — check they still reach the floor; if you used a fixed 28 mm post depth, they now fall 8 mm short, which is a *real* design bug. Fix it by tying the post depth to the body height (or note it as the reason "Up to face" beats Blind here — a Week 3 fix). Restore to 28 mm.

---

## Expected outcome

- A 90 × 60 × 28 mm rounded enclosure base, shelled to a **uniform 2.5 mm wall** with the **top open**, four solid **boss posts** carrying **M3 tapped** holes, **filleted outer corners** carried through the wall, and a **0.5 mm rim chamfer**.
- Feature list: `Body`, `Bosses`, `M3 mounts`, `Outer corner fillet`, `Shell`, `Rim break` — all renamed, in that order.
- The fillet is **before** the shell (carried through the wall); the rim chamfer is **after** (surface-only).
- You have observed at least one feature go red under an aggressive edit and either fixed it or explained exactly why it broke.

---

## Acceptance criteria

- [ ] Counterbored or tapped **holes placed off a fully-defined points sketch** (not free-floating).
- [ ] At least one **fillet** and the **shell**, with the ordering justified (which is before/after and why).
- [ ] The shell has the **correct face removed** and a **uniform wall thickness**.
- [ ] All sketches black; every feature renamed.
- [ ] You triggered a red feature with an aggressive edit and can explain the cause.

---

## Hints

<details>
<summary>The bosses disappeared after I shelled</summary>

Either the bosses were added *after* the shell (so the shell didn't know to leave them solid), or their height didn't reach into the body. Make sure the `Bosses` feature is **above** `Shell` in the feature list and that the posts actually intersect the body. Drag features to reorder if needed.

</details>

<details>
<summary>Shell turned red: "thickness too large"</summary>

Your wall thickness is larger than some feature it must carve (often the gap between two bosses, or a fillet). Reduce the thickness, increase the boss spacing, or use a **per-face thickness** override. This is the normal shell failure — diagnosing it is the skill.

</details>

<details>
<summary>I can't tell if my wall is actually uniform</summary>

`Right-click a face → Section view`, pick a plane through the part, and look at the cut. The wall should read a constant 2.5 mm everywhere. Turn the section view off when done (the same menu).

</details>

---

You've now exercised the entire single-body modeling toolkit. Take these reflexes into the [challenge](../challenges/challenge-01-shelled-bottle.md) and the [mini-project](../mini-project/README.md).
