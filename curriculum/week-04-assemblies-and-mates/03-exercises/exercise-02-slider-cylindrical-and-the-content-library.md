# Exercise 2 — Slider, Cylindrical, and a Library Bolt

**Goal:** Add three more tools to your mate vocabulary. You'll build a **drawer** that slides (Slider, with travel limits), a **shaft** that both spins and slides (Cylindrical), and pull a correctly-sized **bolt from the Standard Content library** and fasten it into a hole you size to match it. Three small assemblies, three mate types, one library insert.

**Estimated time:** 50 minutes.

Work in the same Document `C12-W4-Assemblies`. Add Part Studios as needed and three Assembly tabs: `Ex2-Drawer`, `Ex2-Shaft`, `Ex2-Bolt`.

---

## Part A — The drawer (Slider, with limits)

### A1 — Model the parts

In a Part Studio **`Cabinet`**:

1. Sketch a **120 mm × 120 mm** square on the Top plane; extrude **100 mm**.
2. **Shell** it to **4 mm** walls, removing the **top face and the front face** (an open-front box). This is the cabinet carcass.

In a Part Studio **`Drawer`**:

1. The drawer must fit the cabinet's inside opening with running clearance. Cabinet inside width = 120 − 2×4 = **112 mm**. Make the drawer box **111 mm × 111 mm** outer (0.5 mm per side clearance).
2. Sketch **111 × 111 mm**, extrude **95 mm**, shell to **4 mm** removing the **top face** (an open-top tray).
3. Rename the part **`Drawer`**.

### A2 — Assemble and mate

1. New Assembly **`Ex2-Drawer`**. Insert **`Cabinet`**; accept **Fix**.
2. Insert **`Drawer`** and position it roughly inside the opening.
3. Click **Slider**.
4. On the `Drawer`, pick a connector on its **bottom face** oriented so **Z points along the in/out (depth) direction**. If the implicit connector's Z isn't along depth, pick a connector on a side face whose Z runs front-to-back, or place an explicit connector. (Tip: hover the front edge midpoint — its connector usually points along depth.)
5. Pick the matching connector on the `Cabinet`'s inner floor along the same axis.
6. **Predict:** Slider leaves **1 translational DOF** along that axis. Green check. Rename the mate **`Drawer travel`**.

### A3 — Limits and drag test

1. Edit `Drawer travel` → **Limits**: min **0 mm** (closed, flush) to max **80 mm** (pulled open). The drawer can't fall out.
2. **Drag** the drawer: it slides 0–80 mm along depth and **does nothing else** — no sideways drift, no tilt.
3. If it slides sideways instead of in/out, your connector's Z is wrong — edit the mate and re-pick or flip.

```
Drag test · 1 DOF · slides 0–80 mm · 0 interferences
```

---

## Part B — The shaft (Cylindrical)

### B1 — Model the parts

In a Part Studio **`Sleeve`**:

1. Sketch **Ø20 mm** outer, **Ø10.2 mm** inner concentric circles on the Top plane; extrude **40 mm**. A tube (plain bearing).

In a Part Studio **`Shaft`**:

1. Sketch **Ø10 mm** on the Top plane; extrude **80 mm**. Chamfer both ends 0.5 mm.
2. Rename **`Shaft`**.

### B2 — Assemble and mate

1. New Assembly **`Ex2-Shaft`**. Insert **`Sleeve`**; **Fix** it.
2. Insert **`Shaft`** near the bore.
3. Click **Cylindrical**.
4. Pick the connector on the **`Shaft` axis** (its cylindrical face) and the connector on the **`Sleeve` bore axis**.
5. **Predict:** Cylindrical leaves **2 DOF** — 1 rotation **and** 1 translation, both about/along the shared axis. Green check. Rename **`Shaft slip-and-spin`**.

### B3 — Drag test

Drag the `Shaft`:

- It should both **spin** about its axis and **slide** along its length through the sleeve. Try rotating it, then sliding it — both must work.
- If it only spins (won't slide), you used Revolute. If it only slides (won't spin), you used Slider. Cylindrical does **both**.

```
Drag test · 2 DOF · spins and slides along axis · 0 interferences
```

> Optionally add a Slider/translation **limit** so the shaft can't slide entirely out of the sleeve. Cylindrical mates expose a limit for the translation component.

---

## Part C — A bolt from the Standard Content library

### C1 — Model a bracket with a correctly-sized hole

You'll fasten an **M5 socket-head cap screw**, so size the hole to it.

In a Part Studio **`Bracket`**:

1. Sketch a **50 mm × 30 mm** plate, extrude **6 mm**.
2. Use the **Hole** feature to place one hole. Choose a **clearance hole for M5**: standard M5 clearance is **Ø5.5 mm**. Place it centered, 15 mm from one end. (If you add a counterbore, size it for the M5 cap-screw head — the Hole feature can size to the fastener standard directly.)
3. Rename **`Bracket`**.

### C2 — Insert and fasten the library bolt

1. New Assembly **`Ex2-Bolt`**. Insert **`Bracket`**; **Fix** it.
2. Click **Insert** → switch to the **Standard content** tab.
3. Choose **ISO / metric → Screws → ISO 4762 socket head cap screw** (or the nearest socket-head cap screw your library lists).
4. **Configure** it: size **M5**, length **16 mm**. Insert the instance.
5. Click **Fastened**. Pick the connector on the **screw's axis** and the connector on the **bracket hole's axis**. The screw seats into the hole.
6. If the head is on the wrong side (screw pointing up out of the hole instead of down through it), **Flip** the screw's connector axis.
7. Green check. Rename **`M5 cap screw`**.

### C3 — Confirm sizing

1. The screw shank (Ø5.0 mm) should sit inside the Ø5.5 mm clearance hole with a small gap. Use **Measure** to confirm the hole-to-shank clearance ≈ 0.25 mm radial.
2. Run **Interference detection** — there should be **zero** (the clearance hole means the shank doesn't bind on the bracket).

```
Drag test · 0 DOF (bolt fastened) · 0 interferences · clearance hole confirmed
```

---

## Acceptance criteria

You can mark this exercise done when:

- [ ] **Drawer:** Slider mate gives 1 DOF along depth, limited to 0–80 mm; no sideways drift; renamed `Drawer travel`.
- [ ] **Shaft:** Cylindrical mate gives 2 DOF — the shaft both spins and slides; renamed; you can articulate why Cylindrical ≠ Revolute ≠ Slider.
- [ ] **Bolt:** an M5 cap screw inserted from the **Standard Content library** (not hand-modeled), configured to M5×16, fastened into a **Ø5.5 mm clearance hole** you sized to it; interference check returns zero.
- [ ] Every mate is renamed meaningfully.
- [ ] You can state the DOF each mate leaves without looking it up.

---

## Stretch

- Add an **M5 hex nut** from the library on the back of the bracket and fasten it; confirm the screw length leaves 1–2 threads protruding (measure).
- **Replicate** the bolt: add three more holes to the bracket as a linear pattern, then Replicate the fastened M5 screw to all four holes in one operation.
- Give the drawer a **library knob screw** as a handle, fastened to its front face.

---

## Hints

<details>
<summary>The drawer slides the wrong direction</summary>

Slider motion follows the picked connector's **Z axis**. Pick a connector whose Z runs front-to-back (along drawer travel). The front-edge midpoint connector usually points along depth; otherwise place an explicit connector pointing the way you want, or flip the one you have.

</details>

<details>
<summary>The shaft won't both spin and slide</summary>

Confirm the mate is **Cylindrical**, not Revolute or Slider. Cylindrical is the only mate that leaves rotation *and* translation on the same axis. Delete and re-pick if needed.

</details>

<details>
<summary>I can't find a socket-head cap screw in the library</summary>

Search the Standard content tab for "cap screw" or "4762" (the ISO number for socket-head cap screws). If your library is configured ANSI-only, switch the standard to ISO/metric, or use the nearest equivalent and size the hole to whatever screw you pick — the workflow is identical.

</details>

---

When all three parts pass their drag tests, move to [Exercise 3 — Sub-assembly + interference check](./exercise-03-subassembly-and-interference-check.md).
