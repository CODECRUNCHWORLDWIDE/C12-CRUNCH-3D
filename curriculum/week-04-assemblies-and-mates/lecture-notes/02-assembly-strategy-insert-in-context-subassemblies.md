# Lecture 2 — Assembly Strategy: Insert vs In-Context, Sub-Assemblies, and the Standard Content Library

> **Duration:** ~1 hour of reading + hands-on.
> **Outcome:** You can choose between bottom-up and top-down (in-context) assembly strategy and justify the choice, design a part against neighboring geometry inside an assembly, group a mechanism into a sub-assembly and decide rigid vs flexible, pull a correctly-sized fastener from the Standard Content library, and validate the result with interference detection and a clearance check.

Lecture 1 taught you *how* mates work. This lecture is about *strategy* — how to organize a real, multi-part assembly so it stays editable, performs well, and validates clean. Anyone can mate two parts. The skill is structuring twenty.

If you remember one thing:

> **Decide your assembly strategy before you insert the first part.** Bottom-up (model everything, then mate) and top-down (model in place against neighbors) are different workflows with different update behavior. Mixing them carelessly is how assemblies become un-editable.

---

## 1. Bottom-up vs top-down

There are two ways to build an assembly, and most real designs use a blend.

### Bottom-up

Model every part **independently** in its own Part Studio (or several Part Studios), then **insert** them into an Assembly and mate them. Each part is self-contained; it knows nothing about its neighbors.

- **Pros:** parts are reusable anywhere; each Part Studio is simple; no hidden cross-part dependencies; easiest to reason about and the easiest to teach. This is what you've effectively been heading toward for three weeks.
- **Cons:** you have to *transfer dimensions by hand* — if the bracket's bolt circle is Ø60 mm, you must remember to make the cover's bolt circle Ø60 mm too. Nothing enforces the match.
- **Use it when:** parts are standalone, dimensions are known up front, or parts will be reused across assemblies (which is most of the time, honestly).

### Top-down (in-context)

Start from the assembly. Create or edit a part **in-context** — inside the assembly, referencing the geometry of parts already there. The mating face of a cover is sketched *on* the housing it bolts to, so it's guaranteed to match.

- **Pros:** geometry that must match is *derived*, not copied — change the housing's bolt circle and the cover's follows. Great for tightly-coupled parts (mating faces, conformal covers, parts that share a seam).
- **Cons:** creates **cross-part dependencies**; the in-context part now depends on the assembly state at the moment you referenced it; updates need management (more below); harder for a newcomer to untangle.
- **Use it when:** two parts share a boundary that must stay matched, or you're laying out a mechanism where the parts' sizes depend on each other.

### The honest answer

Real designs are **mostly bottom-up with a few in-context relationships** where coupling genuinely helps. Don't make everything in-context "to be safe" — you'll build a web of dependencies you can't see. Use in-context surgically, for the boundaries that must match, and keep everything else bottom-up and reusable.

---

## 2. In-context design, concretely

Here's how in-context actually works in OnShape and the one behavior that trips everyone up.

1. In the Assembly, with your parts positioned, choose to **edit in context** (right-click an instance → *Edit in context*, or create a new Part Studio in context).
2. OnShape captures an **in-context reference** — a snapshot of the surrounding assembly geometry at that moment. You sketch and model against it: project a neighboring part's edge, sketch on its face, offset from its surface.
3. The new/edited geometry now **depends** on that captured context.

**The behavior to understand:** the in-context reference is a *snapshot*, not a live link by default. If you move the neighboring parts later, your in-context geometry does **not** silently follow — it stays tied to the captured snapshot until you **update the context**. OnShape flags when a context is out of date and lets you refresh it. This is deliberate: it prevents your part from thrashing every time you nudge the assembly. But it means "I changed the housing and the cover didn't update" is usually "you haven't updated the context yet," not a bug.

> **Rule of thumb:** in-context is powerful for matched boundaries, but each in-context reference is a dependency you're signing up to maintain. Keep them few, name them, and know that you must **update the context** after you change the parts they reference.

### A concrete in-context case: a snap-fit cover

To make the snapshot behavior tangible, walk a real one. You have a `Housing` (an open-top box) modeled bottom-up. You need a `Cover` whose outer wall sits exactly inside the housing's lip with a 0.2 mm gap all around — the kind of fit you cannot eyeball and don't want to re-type if the housing changes.

1. In the Assembly, insert and **Fix** the `Housing`.
2. **Create a new Part Studio in context** of the assembly. OnShape snapshots the housing's geometry into that Part Studio.
3. **Project** the housing's inner lip edge onto a sketch and **offset it inward 0.2 mm**. Extrude that as the cover wall. The cover's footprint is now *derived* from the housing — not a number you copied.
4. Finish the cover (top face, snap tabs) and exit. It mates into the housing perfectly because its boundary *came from* the housing.

Now the payoff and the trap together: widen the housing by 5 mm. The cover does **not** resize yet — its context is a snapshot from step 2. OnShape marks the context **out of date**. Right-click → **Update context**, and the projected edge re-derives, the 0.2 mm offset re-applies, and the cover grows to match. That manual refresh is the whole deal with in-context: derived, but on your command, never silently.

> **The senior move:** use in-context for the *one boundary that must match* (here, the cover-to-lip fit) and keep the rest of the cover defined by its own dimensions. Don't derive the whole part from the assembly — derive only the coupled edge. That keeps the dependency small and the update cheap.

---

## 3. Sub-assemblies

When an assembly grows past a handful of parts, you group related parts into **sub-assemblies**. A sub-assembly is itself an Assembly tab; you insert it into a parent assembly as a **single instance**, exactly like inserting a part.

Why bother:

- **Reuse:** a caster wheel built as a sub-assembly (wheel + axle + fork, internally mated) can be inserted four times under a cart. Build the joint once, place it four times.
- **Organization:** the parent assembly's instance list shows one "Caster" node instead of twelve loose parts. Big assemblies stay readable.
- **Performance:** OnShape can treat a sub-assembly as one rigid unit, which is cheaper to solve than re-solving its internal mates every drag.
- **Encapsulation of mechanism:** a mechanism (a gripper, a linkage) belongs in its own sub-assembly so its internal motion is self-contained and testable.

### Rigid vs flexible sub-assemblies

By default, an inserted sub-assembly is **rigid**: its internal mates are *frozen*, and it behaves as one solid body in the parent. The caster's wheel won't spin while it's just a rigid sub-assembly instance — the parent sees a single locked unit.

Toggle a specific instance to **flexible** (right-click the sub-assembly instance → *Make flexible*) and its internal DOF come alive **for that instance**: now the caster's wheel can roll and its fork can swivel inside the parent. Insert the same sub-assembly twice and you can make one flexible and one rigid independently.

- **Rigid (default):** faster, simpler; use when you only need the sub-assembly *placed*, not *moving*, in this context.
- **Flexible:** use when the sub-assembly's internal motion matters in the parent — a wheel that must roll, a linkage that must actuate.

> **Mechanism = sub-assembly + flexible.** If your Week 6 capstone gripper is a sub-assembly, you'll insert it and make it flexible so its jaws move in the full assembly. Build the habit now.

---

## 4. The Standard Content library — never model a bolt

You will need fasteners — bolts, screws, nuts, washers. **Do not model them by hand.** Modeling threads, hex heads, and washer chamfers is slow, error-prone, and pointless when OnShape ships a parametric library of off-the-shelf parts.

The **Standard Content library** is built into the Insert panel:

1. In the Assembly, click **Insert**.
2. Switch to the **Standard content** tab (or search the library).
3. Choose a standard — **ANSI** (inch) or **ISO/DIN** (metric) — and a category: *Bolts*, *Screws*, *Nuts*, *Washers*.
4. Pick the fastener (e.g., *ISO 4762 socket head cap screw*), then **configure** it: size (M3, M4, M5…), length, thread.
5. Insert the instance and **Fastened**-mate it into your tapped hole or counterbore. Its axis connector is right on the screw axis — pick it and the matching hole connector.

The inserted fastener is a real, dimensioned part: it shows up in your **Bill of Materials** (Week 5), it's the correct size for interference checks, and if you change the configured size it updates everywhere.

> **Match the hole to the bolt, not the other way around.** If you're using M5 socket-head screws, your clearance holes should be Ø5.5 mm (clearance) and your counterbores sized for the M5 head. Pick the fastener first; size the holes to it. (Standard clearance for M5 is ~5.5 mm; OnShape's Hole feature can size to a fastener standard directly.)

### Why this matters beyond convenience

Library fasteners are **configurations** in action (Week 5's topic, previewed here): one part definition, many sizes, selected from a table. When you grasp that an M3 and an M6 cap screw are the *same configured part* at two settings, you're ready for the configurations lecture. For now: use the library, size it right, mate it, move on.

---

## 5. Replicate — placing many of the same part

Need eight identical bolts around a flange? Mate **one** correctly, then use **Replicate**: select the mated fastener and a pattern of seed faces/holes (e.g., the eight holes of the bolt circle), and OnShape copies the part-and-its-mate to every one. It's the assembly analog of the Week 3 pattern feature — define the relationship once, multiply it.

This keeps you honest: you mate one bolt *properly* (right connector, right size), then replicate, so all eight are identical and correct. Manually inserting and mating eight bolts is how you end up with one that's subtly wrong.

---

## 6. Inserting from other Documents — and what "linked" means

So far we've inserted parts that live in the *same* Document. Real projects span many Documents: a shared library of brackets here, a vendor's motor model there, your fasteners from Standard Content. OnShape lets you insert a part or sub-assembly from **any Document you can access** through the same **Insert** panel — switch the source from "Current document" to "Other documents" and search.

The crucial behavior: a part inserted from another Document is **linked to a specific version of that source Document**, not to its live, in-progress state. This is deliberate and it's a feature, not a limitation:

- **You insert from a Version (or the latest).** OnShape records *which* version of the source you pulled. If the source Document keeps changing, your assembly doesn't silently churn underneath you.
- **You update on your terms.** When the source publishes a newer version, OnShape flags that an update is available; you choose when to pull it. This is the same "snapshot you refresh deliberately" philosophy as in-context references.
- **Why it matters:** imagine a shared `Fasteners` Document used by forty assemblies. If editing one bolt instantly mutated all forty assemblies, chaos. Versioned linking means each assembly pins a known-good version and upgrades intentionally.

> **Practical rule for C12:** for the mini-project and capstone, keep your running project in **one Document** with multiple Part Studios and Assembly tabs — simpler, no cross-Document version juggling. Reach for cross-Document inserts only when you genuinely reuse a part across projects (your own bracket library, say). When you do, **insert from a Version**, not the workspace, so your assembly is reproducible.

This ties back to Week 1's cloud-versioning lecture: OnShape's whole model is *immutable versions you reference deliberately*. Inserting a linked part is that idea applied to assemblies.

---

## 7. A decision framework: which strategy, which mate

When you sit down in front of an empty Assembly tab, run this checklist. It collapses the whole week into a procedure:

1. **What's the ground?** Identify the one part that doesn't move in real life — the frame, the housing, the base — and plan to **Fix** it first. (If two things are both "fixed," one is still the ground and the other is Fastened to it.)
2. **What moves, and how?** For each moving part, name its **real-world joint** (hinge? drawer? shaft? ball joint?). The joint name picks the mate: hinge→Revolute, drawer→Slider, spinning-and-sliding shaft→Cylindrical, ball joint→Ball, pin-in-slot→Pin-Slot. The DOF count follows automatically.
3. **Does any boundary have to match?** If two parts share a mating face that must stay coincident as sizes change, that's a candidate for **in-context** design. Otherwise stay **bottom-up** and reusable. Default to bottom-up; reach for in-context only for genuine shared boundaries.
4. **Is anything a repeated unit?** A wheel used four times, a hinge used twice — build it once as a **sub-assembly** and insert it, flexible if it must move.
5. **Are there fasteners?** Pull them from **Standard Content**, size the holes to them, and **Replicate** across patterns.
6. **Validate.** Drag-test the DOF, run **interference** at the extremes of motion, **Measure** critical clearances.

Run those six questions and the assembly almost builds itself. The mistakes happen when people skip step 1 (nothing grounded), guess at step 2 (wrong mate, wrong DOF), or skip step 6 (ship something that interferes). The exercises, challenge, and mini-project this week are all this checklist applied.

### A worked decision: the laptop-hinge example

Say you're modeling a laptop. Walk the checklist:

1. **Ground:** the base (keyboard deck) is the world — **Fix** it.
2. **Moves:** the lid is a hinge → **Revolute** about the hinge axis, 1 DOF, with a **0–130°** limit (a laptop lid's real range).
3. **Matching boundary:** the lid's hinge cylinder must align with the base's hinge cylinder — that axis is shared, but the parts are otherwise independent, so **bottom-up** is fine; you don't need in-context here.
4. **Repeated unit:** if there are two hinge barrels, the hinge mechanism could be a **sub-assembly** placed twice.
5. **Fasteners:** the screws holding the hinge to each half come from **Standard Content**, replicated around their hole patterns.
6. **Validate:** drag the lid 0–130°, confirm 1 DOF, run **interference** at closed (0°) and open (130°) — confirm the lid doesn't clip the base — and **Measure** the screen-to-deck gap when closed.

Same procedure scales from a two-part hinge to the Week 6 capstone. Internalize the checklist now.

---

## 8. Validation: interference detection

"It looks assembled" is not "it works." Two solids can **occupy the same space** — overlap, pass through each other — and the renderer won't necklace it for you. Real parts can't interpenetrate; an interference means your design is physically impossible. So you check.

**Interference detection** (Assembly toolbar → *Interference*, or the Insert/inspect area depending on your toolbar layout):

1. Run it across the whole assembly (or a selected set of parts).
2. OnShape lists every pair of parts that overlap and the **volume** of overlap.
3. Click an entry to highlight the clashing region in the graphics area.

What to do with results:

- **Static interference** (parts overlap even at rest): a modeling error. A hole that's too small for its pin, a bracket sized wrong, a bolt longer than its hole is deep. Fix the part geometry.
- **Motion interference** (parts clash only somewhere in the range of motion): drag the mechanism through its **full range** and re-check. A hinge that's fine at 0° but slams into the frame at 120° needs a **mate limit** (Lecture 1) or a geometry change.

> **The C12 standard:** an assembly that's supposed to move passes only when it moves through its **full intended range with zero interferences**. Run interference at the extremes of motion, not just the rest pose.

A note on **intended contact:** some "interferences" are by design — an interference fit (a press-fit pin) deliberately overlaps slightly. OnShape will report it; you note it as intentional. Most interferences in student work are *not* intentional — they're mistakes. Treat every reported interference as guilty until you've explained it.

---

## 9. Validation: clearance and the Measure tool

Interference catches overlaps (negative clearance). You also want to confirm **positive clearance** where parts must *not* touch: the gap between a swinging lid and its frame, the runout around a spinning shaft.

Use the **Measure** tool: select two faces/edges across two parts and read the minimum distance. Pose the assembly at the tight point of its motion (set a mate value, e.g., lid at 5°) and measure the gap. If the design calls for ≥1 mm clearance and you measure 0.3 mm, tighten the geometry.

Measure also reads **angles** (the current hinge angle), **distances** (drawer travel), and assembly-level dimensions — your go-to for "is this actually the size I think it is."

---

## 10. The drag test, formalized

Lecture 1 introduced dragging as the truth-teller for DOF. As your final validation each time you finish mating, run the **C12 drag test** deliberately:

1. **Ground check:** drag the part you fixed. It should not move. (If it does, you didn't Fix it.)
2. **DOF check:** drag each part that should move. Confirm it moves in **exactly** the intended way — a hinge only swings, a drawer only slides — and that parts which should be locked stay locked.
3. **Range check:** push each moving part to both extremes of its range. Confirm limits stop it where they should.
4. **Interference check:** with the mechanism dragged to its tightest pose, run interference detection. Expect zero (or only documented intentional fits).

```
Drag test · 1 DOF · moves freely through full range · 0 interferences
```

That line is the bar. An assembly that earns it is done. One that doesn't, isn't — no matter how good the render looks.

---

## 11. A worked example: a drawer in a cabinet (strategy view)

To see strategy and validation together, here's a drawer — built bottom-up with one in-context boundary:

1. **Bottom-up parts:** model the `Cabinet` (an open box) and the `Drawer` (a smaller box) in separate Part Studios with known sizes.
2. **In-context boundary:** the drawer's outside width must match the cabinet's inside width minus a running clearance. Rather than copy the number, edit the drawer **in-context**: project the cabinet's inner faces and offset inward 0.5 mm per side. Now if the cabinet grows, update the context and the drawer follows.
3. **Insert & ground:** insert both; **Fix** the `Cabinet`.
4. **Slider mate:** mate `Drawer` to `Cabinet` with a **Slider** along the in/out axis. One translational DOF.
5. **Limits:** Slider limits 0 mm (closed) to 250 mm (open) so the drawer can't fall out.
6. **Library:** pull an **M4 knob screw** from Standard Content and **Fastened**-mate it to the drawer front as a handle.
7. **Validate:** drag the drawer through 0–250 mm; run interference at the closed pose (should be zero — the 0.5 mm clearance keeps the box off the cabinet walls); Measure the side gap to confirm ≥0.4 mm.

```
Drag test · 1 DOF · slides 0–250 mm · 0 interferences
```

Notice the blend: *bottom-up* for the two boxes, *one in-context* relationship for the boundary that must match, a *library* fastener for the handle, *limits* and *interference* for validation. That's how real assemblies are built.

---

## 12. Performance and hygiene for bigger assemblies

A few habits keep large assemblies fast and editable:

- **Sub-assemble aggressively.** Twenty loose parts is a mess; five sub-assemblies of four parts each is navigable.
- **Keep sub-assemblies rigid unless they need to move.** Flexible sub-assemblies cost solver time; only flex the ones whose internal motion matters in this context.
- **Fix exactly one ground, mate outward.** A clear grounded reference makes the whole DOF picture legible.
- **Name everything** — instances, mates, sub-assemblies, mate connectors. `Revolute 7` between `Part Studio 1 <3>` and `Part Studio 2 <1>` is unmaintainable; `Lid hinge` between `Lid` and `Pin` is self-documenting.
- **Replicate instead of hand-placing repeats**, so identical parts are genuinely identical.
- **Version before big edits.** OnShape's versioning (Week 1) lets you branch the Document; create a Version before a risky re-mate so you can roll back.

---

## 13. Mate relations — coordinating motion across joints

Everything so far has been about *positioning* parts and *removing* DOF. But a real mechanism often needs two joints to move **together** in a defined relationship — a gear train, a lead screw, a rack-and-pinion. That's not a mate; it's a **mate relation**. You met these briefly in Lecture 1; here's why they belong in the *strategy* conversation.

A mate relation does not remove a degree of freedom on its own. It **links** the DOF of one mate to the DOF of another:

- **Gear relation.** Couples two **Revolute** mates so they rotate at a fixed **ratio**. A 2:1 gear relation means shaft A turns twice for every turn of shaft B. You do *not* model meshing teeth and let contact drive the motion — that's slow and fragile in CAD. You model two gear blanks, give each its own Revolute, then add a Gear relation with the right ratio (and pick the rotation sense — same or opposite). Drive one; the other follows exactly.
- **Screw relation.** Couples a **rotation** to a **translation** — turn the screw, the nut advances. A lead-screw stage: one Revolute (the screw spinning) and one Slider (the nut/stage translating), tied by a Screw relation with a defined **pitch** (mm of travel per revolution).
- **Rack-and-pinion relation.** Couples a **Revolute** (the pinion) to a **Slider** (the rack): the pinion turns, the rack slides, at a ratio set by the pinion's pitch radius.

The strategic point: **a mate relation lets one input drive a whole train.** Drive the crank; the gear relation spins the output gear; the screw relation advances the stage. This is how the Week 6 capstone gear-train or scissor-lift comes alive from a single driven DOF instead of you dragging every part by hand.

> **When to reach for a relation vs more mates:** if two parts must move in a *fixed proportion* (gears, screws, racks), that's a **relation**. If a part just needs *its own* freedom (a hinge, a drawer), that's a **mate**. Don't try to fake a gear ratio by hand-positioning — add the Gear relation and let the solver hold the ratio exactly through the whole range.

You won't need relations for this week's exercises or the four-bar challenge (a four-bar is pure revolutes, no ratio coupling). But knowing they exist — and that they *link* DOF rather than *remove* it — completes the mate-system picture and sets up the capstone.

---

## 14. Assembly patterns, Replicate, and when to use which

Section 5 introduced **Replicate** for fasteners. Step back and see the full toolkit for placing repeats, because choosing the right one keeps a big assembly clean.

OnShape gives you three ways to put many copies of a mated part into an assembly:

1. **Replicate** — select a mated instance plus a set of seed entities (the eight holes of a bolt circle) and OnShape copies the part *and its mate* to each. Best for fasteners and any part whose placement is defined by existing seed geometry (holes, faces). The copies are independent instances that inherit the original's mate relationship.
2. **Assembly linear/circular pattern** — like the Part Studio patterns from Week 3, but at the assembly level: pick an instance and a direction/axis/count, and OnShape arrays it. Best when the spacing is a clean linear or angular step (a row of identical drawer slides, a ring of identical spokes) rather than tied to specific seed holes.
3. **Mate the first, copy-paste the rest** — the *wrong* default. Hand-placing repeats is how one of them ends up subtly mis-mated, off by a flip, or the wrong size. Avoid it.

The decision is simple: **is the repeat defined by existing seed geometry (holes, faces)?** Use **Replicate**. **Is it a regular linear/angular step?** Use an **assembly pattern**. Either way, you mate **one** instance *correctly* and let OnShape propagate it — so every copy is identical by construction, not by careful hand-work.

> **Why this is a strategy decision, not a convenience.** In a twenty-fastener flange, the difference between "Replicate one correct M5 screw" and "insert and mate twenty screws by hand" is the difference between an assembly that's trivially correct and one where you'll spend an afternoon hunting the one screw that's 0.5 mm proud or flipped. Propagate from a single correct source; never multiply by hand.

This is the assembly-level echo of Week 3's lesson: define the relationship **once**, multiply it parametrically. Patterns in the Part Studio multiply *geometry*; Replicate and assembly patterns multiply *mated instances*. Same discipline, one level up.

### The strategy cheat sheet

Pin this somewhere. It collapses the whole lecture into a lookup you can run while staring at an empty Assembly tab:

| You need to… | Reach for | Why |
|---|---|---|
| Make two parts whose **boundary must match** | **In-context** (derive the coupled edge only) | Change one, update context, the other follows |
| Reuse a **mechanism** several times | **Sub-assembly**, made **flexible** where it must move | Build the joint once, place it many times |
| Place **many fasteners** on existing holes | **Replicate** from one correct mated screw | Every copy identical by construction |
| Array a part on a **regular step** | **Assembly linear/circular pattern** | Spacing is parametric, not hand-typed |
| Pull an **off-the-shelf bolt/nut/washer** | **Standard Content library**, size the hole to it | Never hand-model fasteners |
| Couple two joints in a **fixed ratio** (gears, lead screw) | **Mate relation** (gear / screw / rack-and-pinion) | One input drives the whole train |
| Reuse a part **across projects** | **Insert from a Version** of another Document | Pinned, reproducible, you upgrade on your terms |
| Confirm parts **don't overlap** through motion | **Interference detection** at the extremes + sweep | "Looks assembled" is not "works" |
| Confirm a **gap stays positive** | **Measure** at the tightest pose | Clearance is a number, not a vibe |

Notice the through-line: in every row you do the careful thing **once** (one in-context edge, one correct screw, one sub-assembly joint) and let OnShape propagate or validate it. That single habit — *define once, propagate parametrically, validate deliberately* — is the entire difference between an assembly that scales to the capstone and one that collapses under its own twenty hand-placed parts.

---

## 15. Recap

You should now be able to:

- Choose **bottom-up vs top-down (in-context)** and justify it; explain that most real assemblies blend the two.
- Design a part **in-context** against neighbor geometry and explain that the reference is a snapshot you must **update the context** to refresh.
- Build a **sub-assembly**, insert it, and choose **rigid (default) vs flexible** based on whether its internal motion matters in the parent.
- Pull a correctly-sized fastener from the **Standard Content library**, size the mating holes to it, and **Replicate** it around a pattern.
- Validate with **interference detection** (run at the extremes of motion) and **Measure** for clearances, and finish every assembly with the **C12 drag test**.

That's the strategy half of the week. Now go build things that move — the exercises start with a hinge and a shaft, the challenge is a working 4-bar linkage, and the mini-project turns your running part into an articulating mechanism.

Back to the [week overview](../README.md), or jump to the [exercises](../exercises/README.md).

---

## References

- *Assemblies overview* — OnShape Help: <https://cad.onshape.com/help/Content/assembly.htm>
- *In-context design* — OnShape Help: <https://cad.onshape.com/help/Content/incontext.htm>
- *Sub-assemblies & flexible assemblies* — OnShape Help: <https://cad.onshape.com/help/Content/assembly.htm>
- *Standard content* — OnShape Help: <https://cad.onshape.com/help/Content/standardcontent.htm>
- *Replicate* — OnShape Help: <https://cad.onshape.com/help/Content/replicate.htm>
- *Interference detection* — OnShape Help: <https://cad.onshape.com/help/Content/interferencedetection.htm>
- *Measure* — OnShape Help: <https://cad.onshape.com/help/Content/measure.htm>
