# Week 4 Homework

Six practice problems that revisit the week's topics. The full set should take about **6 hours** in total. Work in your Week 4 Document (`C12-W4-Assemblies`) so each problem produces an Assembly tab or a written note you can point to later. Create a **Version** when you finish each substantial one.

Each problem includes:

- A short **problem statement**.
- **Acceptance criteria** so you know when you're done.
- A **hint** if you get stuck.
- An **estimated time**.

A grading **rubric** is at the bottom.

---

## Problem 1 — DOF audit of a free body

**Problem statement.** Without modeling anything new, write a short note `notes/dof-audit.md` that, for each of the following real-world joints, states **how many degrees of freedom it leaves** and **which OnShape mate** produces it:

1. A door on its hinges.
2. A desk drawer on its rails.
3. A bolt fastened into a tapped hole.
4. A camera on a ball head (the ball, not the pan-tilt).
5. A drill bit in a chuck that lets it spin and plunge.
6. A hockey puck sliding on ice.
7. A pin riding loosely in a slotted link.

Then state the **starting** DOF of a single free rigid body and explain in one sentence what "fully constrained" means.

**Acceptance criteria.**

- File `notes/dof-audit.md` exists with all seven joints (DOF count + mate name) and the free-body + fully-constrained sentences.
- Each mate name is correct (Revolute, Slider, Fastened, Ball, Cylindrical, Planar, Pin-Slot).

**Hint.** Map each joint to its real-world analog from the Lecture 1 table. A free rigid body starts at 6 DOF. "Fully constrained" means every DOF you intended to remove is removed and only the intended motion survives.

**Estimated time.** 20 minutes.

---

## Problem 2 — A revolute hinge with a real limit

**Problem statement.** In a new Assembly `HW2-Hinge`, model (or reuse Exercise 1's parts) a two-part hinge and mate it so the moving leaf swings on a **Revolute**. Add **limits** of **0° to 95°**. Then drag-test and confirm the leaf stops exactly at both ends.

**Acceptance criteria.**

- A Revolute mate with a 0–95° limit, renamed meaningfully.
- Drag test shows the leaf swings and stops at 0° and 95° — `Drag test · 1 DOF · swings 0–95° · 0 interferences`.
- One Fixed ground part.
- Committed as a Version `hw2-hinge`.

**Hint.** Edit the Revolute mate → enable Limits → set min 0°, max 95°. If the leaf swings the "wrong way" past your intended zero, flip a mate connector so 0° is the closed position you want.

**Estimated time.** 45 minutes.

---

## Problem 3 — A sliding stage with travel limits

**Problem statement.** In an Assembly `HW3-Slider`, model a **base rail** and a **carriage** that rides it. Mate the carriage with a **Slider** along the rail. Add travel **limits** so the carriage moves a defined distance (e.g., 0–60 mm) and **cannot leave the rail**. Confirm with a drag test, then **Measure** the carriage's travel at both limit poses to verify it matches your limits.

**Acceptance criteria.**

- A Slider mate (1 translational DOF) with 0–60 mm (or your chosen) limits, renamed.
- The carriage slides only along the rail axis — no sideways drift, no tilt.
- A Measure reading at each limit pose confirming the travel distance.
- `Drag test · 1 DOF · slides 0–60 mm · 0 interferences`.
- Committed as a Version `hw3-slider`.

**Hint.** Slider follows the picked connector's **Z axis** — make sure Z runs along the rail. Use the Measure tool between a carriage face and a rail datum at each end to read the travel.

**Estimated time.** 45 minutes.

---

## Problem 4 — Standard Content fastener, sized right

**Problem statement.** In an Assembly `HW4-Fastener`, model a plate with **one hole sized for an M6 cap screw** using the **Hole feature** (M6 clearance ≈ Ø6.6 mm). Insert an **M6 socket-head cap screw** from the **Standard Content library**, configure it (M6 × 20 mm), and **Fasten** it into the hole. Add an **M6 hex nut** from the library on the back and fasten it. Run **interference detection** and **Measure** the thread protrusion past the nut.

**Acceptance criteria.**

- An M6 clearance hole (~Ø6.6 mm) made with the Hole feature.
- An M6 cap screw and M6 hex nut, **both from the Standard Content library** (not hand-modeled), correctly configured and fastened.
- Interference detection returns **0** (clearance hole means no bind).
- A Measure reading of how many mm of thread protrude past the nut.
- Committed as a Version `hw4-fastener`.

**Hint.** Pick the fastener first, size the hole to it. M6 standard clearance is ~6.6 mm. The Hole feature can size directly to a fastener standard. Protrusion = screw length − (plate thickness + nut thickness).

**Estimated time.** 1 hour.

---

## Problem 5 — Sub-assembly, rigid vs flexible

**Problem statement.** Take any 2-part articulating mechanism you've built this week (the hinge or the slider). Rebuild it as a **sub-assembly**, then insert it into a **parent** assembly `HW5-Parent` where a base part is Fixed. **First confirm the joint does NOT move while the sub-assembly is rigid**, then **make it flexible** and confirm the joint **now moves**. Write a two-sentence note on when you'd want rigid vs flexible in a real design.

**Acceptance criteria.**

- A named sub-assembly containing the articulating joint.
- A parent assembly with a Fixed base and the sub-assembly inserted as one instance.
- Documented (a screenshot or note) that the joint is **frozen when rigid** and **moves when flexible**.
- A two-sentence rigid-vs-flexible note.
- Committed as a Version `hw5-subassembly`.

**Hint.** Insert the sub-assembly, try to drag the moving part (it won't move — rigid by default), then right-click the sub-assembly instance → **Make flexible**, and drag again. Use rigid when you only need the unit *placed*; flexible when its internal motion matters in this context.

**Estimated time.** 1 hour.

---

## Problem 6 — Mate-walkthrough reflection

**Problem statement.** Write a 300–400 word note at `notes/week-04-reflection.md` answering:

1. Which mate type took the longest to "click" for you, and what finally made it make sense?
2. Describe one assembly this week that you **over-constrained** or **under-constrained** by accident. How did you diagnose it (what did the drag test show), and how did you fix it?
3. In your own words, explain to a Week-1 student why "it looks assembled" is not the same as "it works," referencing the drag test and interference detection.
4. What's one thing about assemblies you'd want to learn next that this week didn't cover (e.g., gear/screw mate relations, mate connector scripting, large-assembly performance)?

**Acceptance criteria.**

- File exists, 300–400 words, each numbered question addressed in its own paragraph.
- Committed as part of your Week 4 Version.

**Hint.** This is for *you*. Be honest about what confused you — the over/under-constraint story is the most valuable one to write down, because you'll hit it again in the capstone.

**Estimated time.** 30 minutes.

---

## Time budget recap

| Problem | Estimated time |
|--------:|--------------:|
| 1 | 20 min |
| 2 | 45 min |
| 3 | 45 min |
| 4 | 1 h 0 min |
| 5 | 1 h 0 min |
| 6 | 30 min |
| **Total** | **~4 h 20 min** |

(The remaining ~1.5 h of the 6-hour budget is review, versioning, and cleanup.)

---

## Grading rubric

Each problem is scored out of its weight; the homework totals 100 points.

| Problem | Points | What earns full marks |
|--------:|-------:|-----------------------|
| 1 — DOF audit | 15 | All seven joints correct (DOF + mate); free-body and fully-constrained explained correctly |
| 2 — Revolute + limit | 15 | 1-DOF swing, 0–95° limit holds at both ends, ground fixed, mate renamed |
| 3 — Slider + limit | 15 | 1-DOF slide, limits hold, Measure confirms travel, no sideways drift, renamed |
| 4 — Library fastener | 20 | Hole sized to fastener; M6 screw + nut **from the library**; interference zero; protrusion measured |
| 5 — Sub-assembly rigid/flexible | 20 | Demonstrated frozen-when-rigid and moving-when-flexible; rigid-vs-flexible reasoning correct |
| 6 — Reflection | 15 | 300–400 words, all four questions addressed, honest over/under-constraint story |
| **Total** | **100** | |

**Bands:** 90–100 excellent · 75–89 solid · 60–74 passing · <60 revisit the lectures and resubmit.

Common deductions:
- Any mate left as `Revolute 1` / `Slider 2` instead of a meaningful name: **−2 each**.
- A moving joint that drag-tests to the wrong DOF (over/under-constrained) and wasn't caught: **−5**.
- A hand-modeled bolt in Problem 4 instead of a Standard Content insert: **−10** (the whole point is the library).
- Interference present and undocumented in any moving assembly: **−5**.

When you've finished all six and versioned your Document, push on to the [mini-project](./07-mini-project/00-overview.md) if you haven't already started it.
