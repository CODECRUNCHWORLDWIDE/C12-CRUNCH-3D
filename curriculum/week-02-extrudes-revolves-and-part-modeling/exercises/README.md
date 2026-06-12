# Week 2 — Exercises

Short, focused modeling drills. Each one should take 30–50 minutes. Do them in order; later ones assume the skills from earlier ones. Every exercise is a precise, numbered OnShape walkthrough — follow the steps, hit the dimensions, and verify the expected outcome.

These are **CAD tasks, not code.** You build them by hand in an OnShape Part Studio. There is nothing to compile and nothing to type into a terminal. The deliverable for each is a Part Studio in your OnShape Document, plus the short verification at the end of the file.

## Index

1. **[Exercise 1 — Extrude and pocket a bracket](exercise-01-extrude-and-pocket-a-bracket.md)** — guided: New extrude a base, Add a boss, Remove a pocket and a through-hole; prove it rebuilds. (~40 min)
2. **[Exercise 2 — Revolve a control knob](exercise-02-revolve-a-knob.md)** — modeling task: sketch a half-section and revolve it 360° into a stepped, chamfered knob; add a flat with a partial cut. (~45 min)
3. **[Exercise 3 — Holes, fillets, and a shell](exercise-03-holes-fillets-shell.md)** — modeling task: place counterbored holes, fillet structural corners, and shell an enclosure base to a uniform wall. (~50 min)

## Set up your Document once

Before Exercise 1, do this once:

1. In OnShape, **Create → Document**, name it `C12-Week2-<yourhandle>`.
2. Confirm units: top bar `⚙ → Workspace units → Millimeter`, length precision 2–3 decimals.
3. You'll create a **new Part Studio tab per exercise** (right-click the tab bar → *Create Part Studio*, or `+` → Part Studio). Name them `Ex1-Bracket`, `Ex2-Knob`, `Ex3-Enclosure`.

Keeping all three in one Document makes them easy to share for review — paste the single Document link in your tracker.

## How to work the exercises

- Read the whole walkthrough first, then build it. Skim, don't memorize.
- **Drive every sketch to fully defined (black) before you extrude or revolve.** A blue (under-defined) sketch makes a fragile feature. This is the Week 1 discipline carried forward; we hold the line on it.
- **Rename every feature** as you create it. `Extrude 1` is a defect; `Base plate` is a part.
- Hit the dimensions given. They're chosen so the rebuild test works and so your part matches the expected screenshot description.
- After each exercise, run the **rebuild test**: change the one or two driving dimensions named at the end by ±20% and confirm no feature turns red. If something breaks, fix it before moving on — that *is* the skill.
- If you get stuck for more than 10 minutes, peek at the hints at the bottom of each file.

## Completion checklist

You're done with the week's exercises when you can tick every box:

- [ ] **Ex1:** A single-body bracket with a base, an added boss, a blind pocket, and a Through-all hole. All four operations (New, Add, Remove + Through all) used. Rebuilds clean when the base thickness changes.
- [ ] **Ex2:** A revolved knob from a fully-defined half-section, axis on the centerline, with a chamfer and a partial-cut flat. Rebuilds clean when the overall height changes.
- [ ] **Ex3:** An enclosure base with at least two counterbored (or tapped) holes placed off a points sketch, filleted outer corners, and a uniform-thickness shell with the correct face removed. Rebuilds clean when wall thickness changes.
- [ ] Every feature in all three Part Studios is **renamed** meaningfully.
- [ ] All three sketches that drive the parts are **fully defined (black)**.
- [ ] You can explain, in one sentence each, why you chose Through all vs Blind, where the revolve axis is, and why your shell happens after (or before) your fillets.

There are no solution files checked in. The course is open source — solutions live in forks and shared OnShape public links. After you finish, search the cohort tracker for others' `C12-Week2` Documents to compare feature lists.
