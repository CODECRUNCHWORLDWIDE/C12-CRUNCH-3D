# Lecture 1 — The Mate System and Degrees of Freedom

> **Duration:** ~2 hours of reading + hands-on.
> **Outcome:** You can describe the six degrees of freedom of a rigid body, predict exactly which DOF each OnShape mate removes and leaves, place and re-orient mate connectors, and build a hinge that swings and a shaft that spins — knowing *before* you click the green check what the assembly will do.

If you remember one thing from this lecture, remember this:

> **A mate is not glue. A mate is a constraint on motion.** You don't "attach" parts in an assembly — you *remove degrees of freedom* from them, one mate at a time, until exactly the motion you want survives. "Assembled" is the wrong mental model; "constrained to N degrees of freedom" is the right one.

---

## 1. Six degrees of freedom

Drop a single part into a brand-new Assembly tab. It is a **free rigid body**. In 3D space, a free rigid body can move in exactly **six independent ways**:

- **Three translations** — slide along X, slide along Y, slide along Z.
- **Three rotations** — spin about X, spin about Y, spin about Z.

That's it. Any motion of a rigid body, no matter how complicated it looks, is some combination of those six. We call them the **six degrees of freedom (DOF)**.

```
        Z (up)
        │   ↻ rotate about Z (yaw)
        │
        │
        └────────── X
       /     ↻ rotate about X (roll)
      /
     Y    ↻ rotate about Y (pitch)

Translations: along X, along Y, along Z   (3)
Rotations:    about X, about Y, about Z    (3)
                                    Total = 6 DOF
```

When you insert a part into an OnShape Assembly it has all 6 DOF — grab it and drag and it floats anywhere, tumbling freely. Your job as an assembly engineer is to **subtract** DOF with mates until the count is what your design needs:

- A bracket bolted solid to a frame should have **0 DOF**.
- A door hinge should have **1 DOF** (it swings about one axis).
- A drawer should have **1 DOF** (it slides along one axis).
- A ball-and-socket joint should have **3 DOF** (it rotates freely, doesn't translate).

> **The whole week in one sentence:** choosing a mate is choosing which of the six degrees of freedom to keep.

### Fully-, under-, and over-constrained

Three states, and you want to recognize each on sight:

- **Fully constrained:** every DOF you intended to remove is removed; the remaining DOF are exactly the motion you want. A 0-DOF part won't move when dragged. A 1-DOF hinge moves only in its swing. This is the goal.
- **Under-constrained:** the part still has DOF you didn't want. Drag it and it wobbles in a direction it shouldn't. Usually a missing mate or a mate that left too much freedom.
- **Over-constrained:** you've applied conflicting mates that fight each other (e.g., two fastened mates pulling a part to two different places). OnShape will warn you, and the assembly may fail to solve or "snap" oddly. Over-constraint is the assembly version of an over-dimensioned sketch.

OnShape doesn't paint parts black the way it does fully-defined sketches, so you confirm constraint state by **dragging**. The drag test is your truth: grab a part, pull it, and watch what moves.

---

## 2. The Assembly tab vs the Part Studio

You've lived in Part Studios for three weeks. The Assembly tab is a different world; the differences matter.

| | **Part Studio** | **Assembly** |
|---|---|---|
| What it holds | Features that build geometry (sketches, extrudes, fillets) | **Instances** of parts/sub-assemblies, positioned by **mates** |
| Left-panel list | Feature tree (ordered, top-to-bottom) | **Instance list** + **Mate features** list |
| How things relate | Features reference earlier features | Mates constrain instances to each other |
| Motion | None — geometry is static | Parts move according to remaining DOF |
| Edit a part | Edit the feature directly | Open the part's Part Studio, or edit **in-context** |

Two ways to get parts into an assembly:

1. **Insert** (the part icon, top-left of the Assembly toolbar) — opens a panel listing parts in the current Document and lets you search other Documents and the Standard Content library. Click a part, click in the graphics area to drop an **instance**.
2. **Derive / in-context** — design a part inside the assembly against neighboring geometry. That's Lecture 2's topic.

The first part you insert lands at the assembly origin and OnShape offers to **Fix** it. Usually you want that — read on.

---

## 3. Every assembly needs a ground

Here is a rule with no exceptions: **every assembly needs at least one fixed reference.** If nothing is grounded, the whole assembly floats as one free body, and "drag a part" drags everything. Worse, mates have nothing absolute to resolve against.

Two ways to ground a part:

- **Fix** — right-click the instance → **Fix**, or accept the prompt when you insert the first part. A fixed part is locked to the assembly origin with 0 DOF. A small anchor icon appears on it.
- **Fastened mate to the origin** — a Fastened mate between the part's mate connector and the assembly's **Origin** mate connector. Functionally similar to Fix, but it's an explicit, editable mate in your Mate features list, and you can offset it.

**Convention for C12:** pick the part that represents "the world" — the base, the frame, the housing — and **Fix** it first. Everything else mates relative to it. A hinge has a fixed leaf and a swinging leaf; a drawer has a fixed cabinet and a sliding box. Fix the thing that doesn't move in real life.

If you forget to ground anything, the symptom is unmistakable: you drag one part and the entire assembly slides around together like it's on ice. That means: nothing is fixed. Go fix the base.

---

## 4. Mate connectors — the heart of the system

This is the concept that separates people who *fight* OnShape assemblies from people who *fly* through them. **Mates don't connect faces to faces. Mates connect mate connectors to mate connectors.**

A **mate connector** is a small coordinate frame — an **origin point** plus an **X, Y, and Z axis** (a "triad") — that lives on a part. When you apply a mate, you pick two mate connectors, and the mate aligns or constrains them according to its type. A Fastened mate, for instance, makes the two connectors coincident and co-aligned: same origin, same axes.

### Implicit connectors

You rarely have to create connectors by hand, because OnShape **offers implicit ones** as you hover. Move your cursor over a part during a mate and OnShape suggests connectors at natural locations:

- **The center of a circular edge or cylindrical face** — origin at the center, Z along the axis. This is the one you'll use most: hover a bolt hole or a pin and OnShape hands you a connector right on the axis.
- **A flat face** — origin at the point you hover, Z normal to the face.
- **A vertex** — origin at the vertex.
- **A midpoint of a straight edge**, the center of a rectangular face, etc.

Hover, watch the triad snap to these locations, click to pick. Most mates this week are "pick the connector on the hole of part A, pick the connector on the pin of part B."

### Explicit connectors

Sometimes the implicit options aren't where you want them, or you want a connector that's reusable and design-intent-bearing. Then you create an **explicit mate connector**:

- In the **Assembly**, use the **Mate connector** tool to add one to a part.
- Better — in the **Part Studio**, add a mate connector as a feature, so it travels with the part and is available the instant the part is inserted. This is how senior modelers make parts "snap together": they build the connectors that define how the part is meant to mate. (You met mate connectors briefly in Week 3 as reference geometry; this is where they pay off.)

### Re-orienting a connector

When you pick a connector, a small panel lets you adjust it without leaving the mate:

- **Flip primary axis** — reverse Z (turns a part 180°; the #1 fix when an inserted part faces backwards).
- **Re-align / pick a secondary** — set which way X points, to control rotational alignment.
- **Offset** — slide the connector along its axes by a distance; the basis for offset mates (e.g., two faces parallel but 5 mm apart).

> **Debugging tip:** if a mate snaps the part to a position that's *almost* right but flipped or rotated 90°, you don't need to delete the mate. Edit it and use **Flip** / re-align on one of the connectors. Ninety percent of "the mate went weird" problems are a connector pointing the wrong way.

---

## 5. The mate types — what each removes and leaves

Here is the table to internalize. Memorize the right two columns. (Ball and Pin-Slot get a fuller treatment in Lecture 1's sibling drills and the exercises; the table lists all seven plus the relations for completeness.)

| Mate | DOF left | Motion it allows | Real-world example |
|------|---------:|------------------|--------------------|
| **Fastened** | 0 | none — rigidly locked | a bolted bracket; a pressed-in bushing |
| **Revolute** | 1 (rotation) | spins about one axis | a door hinge; a wheel on an axle (with the axle fixed) |
| **Slider** | 1 (translation) | slides along one axis | a drawer; a linear rail; a piston in a guide |
| **Cylindrical** | 2 (1 rot + 1 trans, same axis) | spins *and* slides along one axis | a shaft in a sleeve bearing; a telescoping tube |
| **Planar** | 3 (2 trans + 1 rot in a plane) | slides anywhere in a plane and spins in it | a hockey puck on ice; a part lying on a table |
| **Ball** | 3 (rotations) | rotates freely, can't translate | a ball-and-socket joint; a camera ball head |
| **Pin-Slot** | 2 (1 rot + 1 trans, decoupled) | rotates *and* translates, independently | a pin riding in a slotted link |
| *Parallel (relation)* | — | keeps two connectors' axes parallel | aligning faces |
| *Tangent (relation)* | — | keeps a face tangent to another | a cam follower riding a cam |

The pattern: **Fastened** removes everything; every other mate leaves precisely the DOF its real-world analog has. If you can name the real-world joint, you can pick the mate.

### Fastened (0 DOF)

The workhorse. Use it any time two parts move together as one rigid body: a bolt fastened into a tapped hole, a label fastened to a panel, a base fastened to the origin. Pick a connector on each part; OnShape makes them coincident and co-aligned. If the part lands rotated wrong, flip or re-align a connector — don't delete the mate.

A clean Fastened workflow:

1. Click **Fastened** in the mate toolbar.
2. Hover the bolt-hole circle on part A — OnShape offers a connector on its axis. Click it.
3. Hover the matching hole on part B — click its connector.
4. The parts snap coincident. If the bolt is upside-down, click **Flip primary axis** on one connector.
5. Green check.

### Revolute (1 rotational DOF) — the hinge

Leaves exactly one rotation about the connectors' shared Z axis; removes all translations and the other two rotations. This is your hinge, your wheel, your knob.

1. Click **Revolute**.
2. Pick a connector on the **axis of rotation** of part A — typically the center of the hinge knuckle's cylindrical hole (its Z is the swing axis).
3. Pick the matching connector on part B.
4. The parts align on a common axis; everything is locked **except** rotation about it.
5. Green check, then **drag** part B — it should swing about the axis and nothing else.

If your hinge slides along the axis when you drag it (instead of only swinging), you picked the wrong mate (probably Cylindrical) — Revolute does not allow that slide.

### Slider (1 translational DOF) — the drawer

Leaves exactly one translation along the connectors' shared axis; removes the other two translations and all three rotations. Drawers, rails, pistons.

1. Click **Slider**.
2. Pick a connector on part A whose **Z axis points along the slide direction**. A face whose normal is along the rail works, or an explicit connector you placed pointing down the rail.
3. Pick the matching connector on part B.
4. Drag part B — it slides along the axis and only along it.

A common gotcha: the slide happens along the connector's **Z axis**, so if the drawer slides sideways instead of in/out, your connector's Z is pointing the wrong way. Flip or re-pick.

### Cylindrical (1 rotation + 1 translation, same axis) — the shaft

Leaves two DOF, but coupled to one axis: the part can both **spin about** and **slide along** that axis. A shaft in a plain bearing, a telescoping leg. It's "Revolute plus Slider on the same axis."

1. Click **Cylindrical**.
2. Pick the connector on the shaft's axis (center of its cylindrical face).
3. Pick the connector on the bore it rides in.
4. Drag — the shaft both rotates and translates along its length.

If you want a shaft to spin but **not** slide, that's Revolute, not Cylindrical. If you want it to slide but not spin (a keyed shaft), that's Slider. Cylindrical is specifically "both."

---

## 6. The other three mates: Planar, Ball, Pin-Slot

The four above (Fastened, Revolute, Slider, Cylindrical) cover the vast majority of mechanisms, and they're all you need for this week's exercises and the four-bar challenge. But three more mates round out the system, and you'll meet them in the capstone — so know what each leaves.

### Planar (3 DOF: 2 translations + 1 rotation in a plane)

Constrains a part to a **plane**: it can slide anywhere *within* that plane (two translational DOF) and spin *in* the plane (one rotational DOF), but it can't lift off the plane or tip. The real-world analog is a **hockey puck on ice** or a part lying flat on a table you can slide and spin but not pick up.

1. Click **Planar**.
2. Pick a connector on the part whose **Z is normal to the constraining plane** (a flat face's connector works — its Z points off the face).
3. Pick the connector on the surface it rides on.
4. Drag — the part slides in two directions and spins, but stays in the plane.

Use Planar when a part must stay coplanar with a surface but is otherwise free to shuffle around — a base plate dropped on a workbench, a magnet on a fridge, a part being positioned before other mates lock it down.

### Ball (3 DOF: 3 rotations, 0 translations)

A **ball-and-socket** joint: the part can rotate freely about all three axes but can't translate at all. The connectors' **origins stay coincident** while the orientations are free. The analog is a **camera ball head**, a trailer hitch ball, a human shoulder (roughly).

1. Click **Ball**.
2. Pick a connector at the **center of the ball** on the part.
3. Pick the connector at the **center of the socket**.
4. Drag — the part pivots in every rotational direction about the shared center, but the center point doesn't move.

Ball is exactly the *opposite* split from Slider: Slider keeps one translation and kills all rotation; Ball keeps all rotation and kills all translation.

### Pin-Slot (2 DOF: 1 rotation + 1 translation, **decoupled**)

Pin-Slot looks like Cylindrical at a glance — one rotation, one translation — but the two are **independent**, not tied to the same axis. The picture is a **pin riding in a slotted link**: the pin can slide *along* the slot (translation) and the link can rotate *about* the pin (rotation), and those two motions are decoupled. It's the mate for cam-and-slot mechanisms, oscillating linkages, and Geneva-style drives.

1. Click **Pin-Slot**.
2. Pick the connector for the **rotation axis** (the pin's axis) and the connector defining the **slide direction** (along the slot).
3. Drag — the part both rotates about the pin and translates along the slot, the two motions independent.

> **Cylindrical vs Pin-Slot — the distinction that trips people up:** Cylindrical's rotation and translation are *about the same axis* (a shaft spinning as it slides down its own length). Pin-Slot's rotation and translation are *about different things* (rotate about the pin, slide along the slot) and are decoupled. Same DOF *count* (2), different *coupling*.

---

## 7. Mate relations: gear, screw, tangent, and the lightweight ones

Mates set absolute constraints between parts. **Mate relations** instead *link* the motion of two existing mates — they don't remove DOF on their own, they tie one DOF to another. You won't need these this week, but recognize them:

- **Gear relation** — couples two revolute mates so they rotate together at a defined **ratio** (a 2:1 gear pair spins one shaft twice per turn of the other). This is how you make a real gear train turn in the assembly without modeling tooth contact.
- **Screw relation** — couples a rotation to a translation (turn the screw, the nut advances). A lead-screw drive.
- **Rack-and-pinion relation** — couples a revolute to a slider (gear turns, rack slides).
- **Tangent / Parallel** — lightweight relations that keep a face tangent to another (a cam follower riding a cam) or two axes parallel.

The key idea: a **mate** constrains *where a part can be*; a **relation** constrains *how two motions relate*. Gear and screw relations are how the Week 6 capstone gear-train or lead-screw mechanisms come alive.

---

## 8. Mate limits — stopping motion realistically

A real hinge doesn't swing 360°; a real drawer can't fall out of the cabinet. After you create a Revolute or Slider mate, edit it and enable **Limits**:

- **Revolute limits:** a **minimum** and **maximum** angle, e.g., min 0°, max 110°. The part now stops at those angles when dragged — like a laptop lid.
- **Slider limits:** a minimum and maximum distance, e.g., 0 mm (closed) to 250 mm (fully open) — the drawer can't slide past either stop.

Limits make a mechanism *feel* real and prevent the drag test from sending parts to absurd positions. They also matter for interference: a hinge that's allowed to swing through its own frame will report interference; clamp the limit and the collision goes away.

You can also set a fixed **mate value** (a current angle/offset) to pose the assembly — e.g., set the hinge to 90° to take a screenshot of the open position — without removing the DOF.

---

## 9. A worked example: a two-leaf hinge

Let's build the canonical revolute case end to end. (Exercise 1 walks the clicks in detail; this is the mental model.)

You have two parts: a **fixed leaf** (`Leaf-A`) and a **swinging leaf** (`Leaf-B`), each with a cylindrical **knuckle** that shares a common pin axis, plus a separate **pin** part.

1. **Insert** `Leaf-A`, `Leaf-B`, and `Pin`. Three free bodies, 18 DOF total.
2. **Fix** `Leaf-A`. It's the world. (18 → 12 DOF remaining across the other two parts.)
3. **Fastened** `Pin` into `Leaf-A`'s knuckle — pick the pin's axis connector and the knuckle hole's axis connector; flip if needed so the pin sits centered. (Pin now 0 DOF; 12 → 6.)
4. **Revolute** `Leaf-B` to `Pin` — pick `Leaf-B`'s knuckle-hole connector and `Pin`'s axis connector. `Leaf-B` aligns on the pin axis with one rotation left. (6 → 1.)
5. **Drag** `Leaf-B`. It swings about the pin and nothing else.

```
Result: Drag test · 1 DOF · swings freely · 0 interferences
```

6. (Optional) Edit the Revolute mate → **Limits** → min 0°, max 110°. Drag again; it now stops like a real lid.

Notice the bookkeeping: we started with 18 DOF and walked it down to 1 deliberately. When you can narrate an assembly that way — "this mate takes it from 6 to 1" — you understand the mate system.

---

## 10. Reading the Mate features list

The left panel's **Mate features** list is your assembly's "feature tree." Each mate shows its type icon, its name, and the two entities it connects. Habits of people who don't get lost in big assemblies:

- **Rename every mate.** `Revolute 1` tells the next person nothing. `Lid swing` tells them everything. (A list of `Fastened 1 / Revolute 2 / Slider 3` is, in C12, an automatic deduction on the mini-project — same rule as renaming features in a Part Studio.)
- **Click a mate to highlight what it connects.** The two parts and the connectors light up. This is how you reverse-engineer someone else's (or last-week's-you's) assembly.
- **Order doesn't drive geometry the way Part Studio features do**, but grounding-then-mating is still the sane order: fix the base, then build outward.
- **Suppress a mate to test a theory.** Right-click → Suppress temporarily removes a mate's constraint so you can see what it was holding.

---

## 11. Common failure modes and how to read them

| Symptom | Likely cause | Fix |
|---|---|---|
| Whole assembly slides together when you drag one part | Nothing is grounded | **Fix** the base part |
| Part you expected to move is frozen | Over-constrained / wrong mate (e.g., Fastened where you wanted Revolute) | Check the mate type; delete the extra mate |
| Part wobbles in a direction it shouldn't | Under-constrained | Add the missing mate or pick a mate that removes more DOF |
| Part snaps in flipped or rotated 90° | Mate connector axis pointing wrong way | Edit mate → **Flip** / re-align a connector |
| OnShape warns "over-constrained" | Conflicting mates fighting | Suppress mates one at a time to find the conflict; remove the redundant one |
| Hinge swings *through* the frame | No mate limit; or interference not yet checked | Add Revolute limits; run interference detection |
| Inserted part is absurdly large/small | Source part modeled in different units | Check the source Document's units |

The diagnostic discipline is always the same: **drag, observe, compare to intended DOF.** If what moves doesn't match what should move, the mate count is wrong somewhere.

---

## 12. Why mate connectors are design intent

Here's the senior-engineer move that pays off all the way to the capstone: **build your mate connectors in the Part Studio, where they describe how the part is meant to assemble.**

When you model a bracket, drop an explicit mate connector at the center of each mounting hole, oriented so Z points along the bolt axis. Now when that bracket is inserted into any assembly, those connectors are right there — the part *tells* the assembler "mate me here, this way." You stop hunting for implicit connectors and the assembly snaps together like LEGO.

This is exactly the design-intent thinking from Week 3, carried into assemblies. A part with thoughtful connectors is a part that assembles itself. A part with no connectors makes every assembler re-derive your intent by hovering around hoping the right implicit connector appears. Be the first kind of modeler.

---

## 13. Recap

You should now be able to:

- State the **six degrees of freedom** and explain that a mate **removes** DOF rather than gluing parts.
- Recognize **fully-, under-, and over-constrained** assemblies by drag-testing.
- Explain why every assembly needs a **fixed/grounded** part and how to **Fix** one.
- Describe a **mate connector** (origin + triad), use implicit connectors, create explicit ones, and **flip/re-align/offset** them.
- Predict the DOF left by **Fastened (0), Revolute (1), Slider (1), Cylindrical (2)** and pick the right one by naming the real-world joint.
- Add **mate limits** to stop a hinge or drawer realistically.
- Read the **Mate features** list, rename mates, and diagnose the common failure modes.

Next up: how to *organize* a real assembly — bottom-up vs top-down, in-context design, sub-assemblies, and the Standard Content library. Continue to [Lecture 2 — Assembly Strategy](./02-assembly-strategy-insert-in-context-subassemblies.md).

---

## References

- *Mates* — OnShape Help: <https://cad.onshape.com/help/Content/mate.htm>
- *Mate connectors* — OnShape Help: <https://cad.onshape.com/help/Content/mateconnector.htm>
- *Assemblies overview* — OnShape Help: <https://cad.onshape.com/help/Content/assembly.htm>
- *Revolute mate* — OnShape Help: <https://cad.onshape.com/help/Content/revolute_mate.htm>
- *Slider mate* — OnShape Help: <https://cad.onshape.com/help/Content/slider_mate.htm>
- *Cylindrical mate* — OnShape Help: <https://cad.onshape.com/help/Content/cylindrical_mate.htm>
- *Degrees of freedom (Kutzbach criterion)* — background: <https://en.wikipedia.org/wiki/Chebychev%E2%80%93Gr%C3%BCbler%E2%80%93Kutzbach_criterion>
