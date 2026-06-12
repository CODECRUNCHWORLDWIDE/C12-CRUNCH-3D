# Week 06 — Quiz

Twelve questions. This is the last quiz of the course; it mixes capstone-week material (mechanism design, the drawing package, releases and exports) with the synthesis questions a design reviewer or interviewer actually asks. Take it with your notes closed. Aim for 10/12. Answer key at the bottom — don't peek.

---

**Q1.** In a design review, what is the *output* of the meeting — the thing that means the review succeeded?

- A) A photorealistic render of the mechanism.
- B) A prioritized risk list, each item tagged accept / fix-now / fix-later, with owners.
- C) Sign-off that the design is perfect.
- D) A recording of the presentation.

---

**Q2.** A reviewer asks "how many degrees of freedom does this mechanism have?" For a single-input slider-crank gripper, which is the *most defensible* answer?

- A) "It moves, so probably a few."
- B) "One driven DOF — I rotate the crank and everything follows; the mobility equation gives M = 3(4−1) − 2(4) = 1."
- C) "Zero, it's a solid assembly."
- D) "As many as there are parts."

---

**Q3.** You claim "it never interferes." A reviewer asks how you know. Which check is *correct*?

- A) "It looks fine when I orbit it at the home position."
- B) Interference Detection run at home, mid-travel, and *both* extremes, with the worst clearance measured as a number.
- C) The render came out clean.
- D) Nobody complained.

---

**Q4.** Why do most mechanisms fail at the *extremes* of travel rather than the middle?

- A) OnShape only checks the middle.
- B) At the extremes, links swing closest to the frame, the slider can run off the rail end, or the jaws fully close — the tightest geometry occurs at the ends, not the comfortable home pose.
- C) Parts are weakest at the ends.
- D) The mate connectors expire at the extremes.

---

**Q5.** In an assembly, how many parts should be **grounded (Fixed)**, and why?

- A) All of them, for stability.
- B) Exactly one — everything else is positioned by mates relative to it; two over-constrains, zero means the parts float.
- C) Zero — let everything float and drag into place.
- D) Two, one at each end.

---

**Q6.** You place a Revolute mate *and* a Cylindrical mate at the same pin joint. What is the likely result?

- A) Nothing; redundancy is harmless.
- B) An over-constrained joint — the redundant mate fights the other when you move, and OnShape flags it red; use one mate per joint.
- C) The joint becomes stronger.
- D) The joint gains an extra degree of freedom.

---

**Q7.** Why drive a mechanism's link lengths from a **Variable Studio** instead of typing raw numbers into each sketch?

- A) Variables render faster.
- B) One edit changes the motion consistently everywhere, and you cannot accidentally change a length in one sketch and forget the matching dimension in another — which is what makes the assembly rebuild cleanly.
- C) Raw numbers are not allowed in OnShape.
- D) Variables are required for export.

---

**Q8.** A drawing dimensions a 6mm pin going into a hole, but puts **no tolerance** on either. Why is that a defect?

- A) It isn't; nominal dimensions are enough.
- B) Without a tolerance nobody knows whether the pin slides (clearance fit) or jams (interference) — made exactly 6mm into exactly 6mm, it won't go in; the fit is undefined.
- C) Tolerances are only for assembly drawings.
- D) The drawing will not print.

---

**Q9.** You tag Version `v1.0`, then keep editing the mechanism. The released **drawing** and **STEP** were generated from `v1.0`. What guarantees they still agree with each other?

- A) Nothing — they drift as you edit.
- B) Because a Version is immutable: `v1.0` is a frozen snapshot, so the drawing, the STEP, and the STL all reference the *same* geometry even as the live Document moves on (you branch for v1.1).
- C) OnShape auto-syncs them to the latest edit.
- D) You re-export after every edit.

---

**Q10.** A teammate needs to continue the *engineering* of your mechanism in a different CAD package. Which export do you hand them, and why?

- A) STL — it's the smallest file.
- B) STEP — it carries exact B-rep geometry and the assembly structure, so they get precise, continuable geometry (STL is a faceted mesh with no structure).
- C) A screenshot.
- D) The OnShape link only.

---

**Q11.** You export an **STL** of a printable part. Which two checks catch the most common export bugs?

- A) File size and color.
- B) The **bounding box in millimeters** (catches a units error where the part imports 25.4× too big) and **watertightness** (a non-manifold mesh won't slice).
- C) The filename and the date.
- D) Whether it opens in OnShape.

---

**Q12.** Your mechanism rebuilds cleanly when you set `#crank = 12`, but throws a red error at `#crank = 20`. What is the right thing to put in your design walkthrough?

- A) Claim it works for any value and hope nobody checks.
- B) Document the **valid range** of the variable (e.g., 10–16 mm), and explain that past 16 the rod sweeps into the frame and Interference Detection goes red — an honest bounded-robustness statement.
- C) Delete the variable so it can't be changed.
- D) Nothing; rebuild errors are normal.

---
---

## Answer key

**Q1 — B.** The deliverable of a review is a prioritized, owned risk list. Renders and recordings are inputs, not outputs; "it's perfect" is never a real outcome. (Lecture 1, §1.3, §1.12.)

**Q2 — B.** Naming the DOF *and* backing it with the mobility equation reads as someone who designed the motion; "it just moves" reads as someone who got lucky. (Lecture 1, §1.4, §1.7; Exercise 1.)

**Q3 — B.** "It never interferes" must be proven with Interference Detection at multiple positions — especially the extremes — with the worst clearance measured. Eyeballing the home pose is not a check. (Lecture 1, §1.4; Exercise 2, Step 7.)

**Q4 — B.** The tightest geometry occurs at the ends of travel — links closest to the frame, slider at the rail end, jaws fully closed — which is exactly why you sweep the extremes, not just the home position. (Lecture 1, §1.1, §1.11; Exercise 2.)

**Q5 — B.** Exactly one grounded part; everything else positioned by mates. Two over-constrains, zero leaves the parts floating. (Lecture 1, §1.8; Exercise 2, Step 2.)

**Q6 — B.** Two mates at one joint over-constrain it; they agree at the home pose but fight when you move, and OnShape flags it red. One mate per joint. (Lecture 1, §1.4; Exercise 2, Step 6.)

**Q7 — B.** A Variable Studio makes one edit change the motion consistently and removes the "changed it in one sketch, forgot the other" class of bug — which is precisely what makes the assembly rebuild cleanly under a change. (Lecture 1, §1.9; mini-project.)

**Q8 — B.** A pin and hole at the same nominal will not assemble; the tolerance is what declares clearance vs interference, i.e., whether the joint slides or jams. Tolerance the fits. (Lecture 2, §2.4.)

**Q9 — B.** A Version is immutable. Generating the drawing, STEP, and STL from the same frozen `v1.0` is what keeps them consistent; you branch for further work so the release does not move under the artifacts. (Lecture 2, §2.1, §2.2.)

**Q10 — B.** STEP carries exact geometry and assembly structure for a downstream engineer; STL is a faceted mesh for a printer with no structure or history. Match the format to the consumer. (Lecture 2, §2.6.)

**Q11 — B.** The bounding box in mm catches the silent units bug (a 25.4× scale error), and watertightness catches a non-manifold mesh that won't slice. Always open the export and check both. (Lecture 2, §2.6, §2.7; Exercise 3, Step 8.)

**Q12 — B.** Honest bounded robustness: document the valid range and explain what breaks past it. Overclaiming "any value works" fails the moment the reviewer picks a value outside the safe envelope. (Lecture 1, §1.11; mini-project.)

---

*Score 10+/12 and you're ready for the live review. Below that, re-read the lecture section cited next to each one you missed before Friday.*
