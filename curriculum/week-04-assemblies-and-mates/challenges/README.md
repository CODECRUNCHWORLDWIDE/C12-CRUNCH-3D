# Week 4 — Challenges

The exercises drill one mate at a time. **The challenge makes them work together.** It takes 60–120 minutes and produces a real, moving mechanism you can show off — a working four-bar linkage with **exactly one degree of freedom** and zero interference through its full sweep.

## Index

1. **[Challenge 1 — A working 4-bar linkage](challenge-01-four-bar-linkage.md)** — model four links, mate them into a closed loop with four revolute joints, and prove the whole mechanism has exactly **1 DOF** and never self-collides as it cycles. (~90 min)

## How it's assessed

The challenge is **pass/strong-pass**, judged on a moving deliverable, not a render:

- **Pass:** the linkage closes the loop, has exactly **1 DOF** (drive one link, all the others follow predictably), and reports **0 interferences** at several poses across its range. Mates and parts are renamed.
- **Strong pass:** all of the above, plus a **driving mate value** you can sweep to animate the full cycle, a documented DOF calculation (Kutzbach), and a deliberate choice of which link is the crank vs the rocker, explained in a short write-up.

The hard part isn't any single mate — they're all revolutes you already know. The hard part is the **closed loop**: four revolute joints around a four-bar loop is the textbook 1-DOF mechanism, but it's easy to accidentally over-constrain it (lock it solid) or under-constrain it (leave it floppy). Getting it to exactly 1 DOF is the whole point, and it teaches you to *count* degrees of freedom in a real mechanism rather than guess.

Challenges are optional — you can pass the week without them. But the four-bar linkage is the canonical articulating mechanism, and the loop-closure intuition you build here is exactly what the **Week 6 capstone** (an original multi-part mechanism) demands. Do this one.
