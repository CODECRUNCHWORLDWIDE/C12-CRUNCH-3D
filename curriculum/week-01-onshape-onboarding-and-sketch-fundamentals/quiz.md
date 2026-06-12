# Week 1 — Quiz

Ten questions on Documents, the Part Studio, constraints, dimensions, and fully-defined sketches. Take it with your lecture notes closed. Aim for 9/10 before moving to Week 2. Answer key at the bottom — don't peek.

---

**Q1.** Which best describes the relationship between a Document, a Part Studio, and an Assembly in OnShape?

- A) They are three names for the same thing, shown in different tabs for convenience.
- B) The Document is the cloud container; a Part Studio is where you model geometry/sketches; an Assembly is where you connect finished parts with mates. Part Studios and Assemblies live *inside* a Document.
- C) A Part Studio contains Documents, and an Assembly contains Part Studios.
- D) The Assembly is the cloud container; Documents and Part Studios are exported from it.

---

**Q2.** You draw a single line in a sketch and nothing else. You can drag both of its endpoints freely around the plane. How many degrees of freedom does this line have, and what color is it?

- A) 0 DOF; black.
- B) 2 DOF; black.
- C) 4 DOF; blue.
- D) 4 DOF; red.

---

**Q3.** A sketch entity is showing **blue**. What does that mean, and what should you do?

- A) It's fully defined; leave it alone.
- B) It's over-defined; delete a constraint.
- C) It's under-defined (free DOF remain); add constraints/dimensions until it's black.
- D) It's construction geometry; toggle it back to normal.

---

**Q4.** You want a rectangle to *stay square* no matter how you later resize it, using the **fewest** dimensions. What's the best approach?

- A) Dimension all four sides to the same value.
- B) Dimension the width and the height to the same value.
- C) Apply an **equal** constraint between one width and one height line, then dimension **one** side.
- D) Apply a **Fix** constraint to all four corners.

---

**Q5.** What is the difference between a **driving** dimension and a **driven** (reference) dimension?

- A) There is no difference; the terms are interchangeable.
- B) A driving dimension controls the geometry (change the number, the geometry moves); a driven dimension only reports a measurement and does not control anything.
- C) A driven dimension controls the geometry; a driving dimension only reports a value.
- D) Driving dimensions are for circles; driven dimensions are for lines.

---

**Q6.** You try to add a dimension and OnShape asks whether you want to make it a **driven** (reference) dimension instead. What is this usually telling you?

- A) Your sketch has a bug and must be deleted.
- B) The measurement you're dimensioning is already determined by existing constraints/dimensions, so adding it as a driving dimension would over-define the sketch.
- C) You're not allowed to dimension that type of entity.
- D) The document units are wrong.

---

**Q7.** You have two circles and you want them to always share the same center point. Which constraint should you use?

- A) Equal
- B) Tangent
- C) Concentric
- D) Coincident between their two radii

---

**Q8.** Which of these is the **single most important** habit for the *first* sketch in a Part Studio, to keep the geometry from floating away when you edit it later?

- A) Use the largest possible dimensions.
- B) Anchor the sketch to the **origin** (e.g., a coincident constraint to the origin point).
- C) Turn every entity into construction geometry.
- D) Apply a **Fix** constraint to every entity.

---

**Q9.** You enable **Show constraints** and notice your "square" is actually held square by two separate `40 mm` and `40 mm` dimensions rather than an `equal` constraint. Why is the constraint-based version preferred?

- A) It isn't — two dimensions are always better.
- B) The `equal` constraint encodes the *intent* ("these are equal") so the squareness survives edits and you maintain one number instead of keeping two in sync; it's more robust and uses fewer dimensions.
- C) `equal` makes the sketch render faster.
- D) Dimensions are not allowed on squares.

---

**Q10.** In OnShape, when do build artifacts — er, when is your work **saved**, and what is a **Version**?

- A) You must click Save after every change; a Version is an auto-backup.
- B) OnShape **auto-saves continuously** to the cloud (there is no Save button); a **Version** is a named, **immutable snapshot** you create deliberately at a milestone to share, branch from, or reference.
- C) Work is saved only when you close the browser; a Version is the current live workspace.
- D) Nothing is saved until you export a file; a Version is an exported STEP file.

---

## Answer key

<details>
<summary>Click to reveal answers</summary>

1. **B** — Document = cloud container; Part Studio = modeling environment (sketches + 3D geometry); Assembly = mating environment. The latter two live inside a Document. This is the foundational mental model from Lecture 1.
2. **C** — A free line segment has **4 DOF** (two endpoints × two coordinates, or equivalently position + length + angle) and is **blue** because it's under-defined and draggable.
3. **C** — Blue = under-defined; free degrees of freedom remain and the entity can be dragged. Add constraints/dimensions until it turns black (fully defined). (Over-defined is red/yellow; construction is grey/dashed.)
4. **C** — An `equal` constraint between a width and a height line ties them together, so a single dimension on one side fully sizes the square *and* it can never accidentally become a non-square rectangle. One dimension beats two, and the squareness is encoded as intent.
5. **B** — A driving dimension *controls* geometry; a driven (reference) dimension only *reports* a measurement (shown in parentheses/grey) and controls nothing.
6. **B** — The prompt means the measurement is already locked by your existing constraints/dimensions. Forcing a second driving dimension would over-define (conflict). Accept it as driven to *display* the value, or cancel — usually it's a sign your constraints are doing their job.
7. **C** — **Concentric** forces two circles/arcs to share a center (removes 2 DOF). `Equal` makes radii match (not centers); `tangent` makes them touch smoothly; there's no such thing as "coincident between two radii."
8. **B** — Anchor the first sketch to the **origin**. Without it, the whole sketch can be dragged as a unit and "floats," which is the #1 cause of geometry shifting on later edits. `Fix` is a blunt crutch, not the right tool.
9. **B** — The `equal` constraint encodes the relationship as design intent: it survives edits, keeps the part square automatically, lets you maintain one number instead of two, and reduces the dimension count. This is the core lesson of the week.
10. **B** — OnShape auto-saves to the cloud continuously; there is no Save button. A **Version** is a named, immutable snapshot you create on purpose at a milestone, used for sharing, branching, and referencing. (There is no manual save, no "live workspace as a version," and exporting a file is unrelated to saving.)

</details>

---

If you scored under 7, re-read the lectures for the questions you missed — especially the difference between constraints and dimensions, which underpins the whole course. If you scored 9 or 10, you're ready for the [homework](./homework.md).
