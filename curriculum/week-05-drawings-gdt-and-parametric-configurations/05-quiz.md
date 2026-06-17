# Week 5 — Quiz

Ten multiple-choice questions on drawings, GD&T, variables, and configurations. Take it with your lecture notes closed. Aim for 9/10 before moving to the capstone. Answer key at the bottom — don't peek.

---

**Q1.** What does it mean for a drawing dimension to be **associative**?

- A) The dimension is locked and can never change.
- B) The dimension's value is read from the model and updates automatically when the model changes.
- C) The dimension was typed by hand to match the model at the time of drawing.
- D) The dimension only appears on the assembly drawing, not the part drawing.

---

**Q2.** In **third-angle** projection (the ANSI default), where does the **top** view sit relative to the front (base) view?

- A) Below the front view.
- B) To the left of the front view.
- C) Above the front view.
- D) Diagonally, with projection lines.

---

**Q3.** You double-click a dimension on your drawing and type `50` over a value that the model computed as `40`. What have you created?

- A) A basic dimension.
- B) An associative dimension.
- C) An overridden dimension — a value that no longer tracks the model and may ship wrong to a machinist.
- D) A reference (driven) dimension.

---

**Q4.** A part has a counterbore buried inside a boss. Which view best communicates the counterbore depth and the wall thickness around the bore?

- A) An additional orthographic view with hidden lines on.
- B) A section view cutting through the boss's centerline.
- C) An isometric view.
- D) A detail view at the same scale.

---

**Q5.** In a **feature control frame** reading `⌖ | ⌀0.2 | A | B | C`, what does the `A B C` portion mean?

- A) The tolerance applies only to faces labeled A, B, and C.
- B) The feature is located and oriented relative to the datum reference frame — datum A first, then B, then C.
- C) The part has three revisions: A, B, and C.
- D) The position tolerance is ±0.2 in each of three axes.

---

**Q6.** What is a **basic dimension**?

- A) A dimension with the loosest tolerance on the drawing.
- B) A theoretically exact location (boxed, no tolerance of its own); its tolerance comes from a related feature control frame.
- C) A dimension that OnShape places automatically.
- D) The first dimension you place on any view.

---

**Q7.** Which GD&T control is a **form** control that references **no datum**?

- A) Position.
- B) Perpendicularity.
- C) Flatness.
- D) Concentricity.

---

**Q8.** In OnShape, you write `#bore = #od - 2 * #wall` in a Variable feature. Later you change `#wall` from `3 mm` to `4 mm` (with `#od = 30 mm`). What is `#bore` now?

- A) `30 mm` — derived variables don't update.
- B) `24 mm` — it's recomputed from the equation.
- C) `22 mm` — it's recomputed from the equation.
- D) It errors, because variables can't reference other variables.

---

**Q9.** You want one model to produce `Small`, `Medium`, and `Large` versions that a teammate can pick from a dropdown without editing your sketches. Which OnShape feature do you use?

- A) A Variable feature alone.
- B) A separate Part Studio for each size.
- C) A Configurations table with a configuration input.
- D) Three exported STL files.

---

**Q10.** You're handing your finished design to a CNC machine shop so they can program toolpaths and make the part. Which export best fits that audience?

- A) STL — a triangle mesh of the surface.
- B) A PDF of the drawing **and** a STEP (AP242) of the solid model.
- C) A PNG screenshot of the OnShape window.
- D) The raw OnShape feature history as a `.zip`.

---

## Answer key

<details>
<summary>Click to reveal answers</summary>

1. **B** — Associative means the drawing dimension reads from the live model; change the model and the dimension follows. This is the whole point of model-based drawings. (C describes a non-associative, hand-typed value, which is exactly what you avoid.)
2. **C** — Third-angle puts the top view *above* the front. First-angle (ISO) puts it below. Mixing the two gets parts made mirror-imaged, which is why the title block declares the convention.
3. **C** — That's an **overridden** dimension: it displays whatever you typed regardless of the model. It's the cardinal sin of model-based drawing because it lets a sheet say "50" over a part that's actually "40."
4. **B** — A section view cuts the part open so internal features become solid, dimensionable geometry. Hidden lines (A) make a tangle; iso (C) is pictorial only; a detail at the same scale (D) doesn't expose the inside.
5. **B** — `A B C` are the **datum references**: the feature is located/oriented relative to the datum reference frame, A primary, B secondary, C tertiary. The order matters.
6. **B** — A basic dimension is theoretically exact and boxed, carrying **no** tolerance itself; the tolerance comes from the FCF that references it. Pairing a basic location with a position FCF (and *not* also a ± tolerance) is correct GD&T.
7. **C** — **Flatness** is a form control measured against a surface itself, so it needs no datum. Position and perpendicularity both reference datums.
8. **C** — `#bore = 30 - 2*4 = 22 mm`. Derived variables recompute from their equations whenever an input changes — that's the value of encoding the relationship instead of the number.
9. **C** — A **Configurations table** publishes named variants selectable from a dropdown without editing the model. A Variable feature alone (A) gives flexibility but no dropdown of finished variants; separate Part Studios (B) is the copy-paste anti-pattern.
10. **B** — A machinist reads the **PDF drawing** (the manufacturing instruction with dimensions and tolerances) and a CAM programmer ingests the **STEP AP242** solid (which can even carry the PMI). STL (A) has no dimensions and is for printing, never machining.

</details>

---

If you scored under 7, re-read the lectures for the questions you missed. If you scored 9 or 10, you're ready to dive into the [homework](./06-homework.md).
