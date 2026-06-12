# C12 · Crunch 3D: CAD & Modeling — Syllabus

A 6-week program. Each week ships the standard 13-artifact format (README, resources, 2 lecture notes, 3 exercises, a challenge, a mini-project, quiz, homework).

## Week 01 — OnShape Onboarding & Sketch Fundamentals

Get oriented in OnShape's browser-based, cloud-native, fully parametric workspace and learn to draw constrained 2D sketches that drive every 3D feature that follows. A good sketch is the foundation of a robust part, so we invest the whole first week in disciplined sketching and constraint thinking before extruding anything.

- **Lectures:** OnShape Tour: Documents, Workspaces, the Feature Tree, and Cloud Versioning; Sketching with Intent: Geometric Constraints, Dimensions, and Fully-Defined Sketches
- **Exercises:** Guided sketching drills: create a Document, set units, draw lines/arcs/rectangles/circles on the Top plane, then apply coincident, horizontal/vertical, parallel, perpendicular, tangent, equal, and concentric constraints until each sketch turns black (fully defined). Add driving dimensions and watch geometry update parametrically.
- **Challenge:** Take a dimensioned 2D engineering drawing of a flat gasket or bracket profile and reproduce it as a single fully-defined sketch using the minimum number of dimensions, leaning on constraints instead of over-dimensioning.
- **Mini-project:** Begin the running project: model a simple flat 'name plate' or hobby-grade flat washer-style part. This week deliver only the fully-defined master sketch (no 3D yet) plus a short written walkthrough of every constraint and dimension you used and why the sketch is fully defined.
- **Key tech:** OnShape, Sketch tool, Geometric constraints, Driving dimensions, Feature tree, Cloud versioning

## Week 02 — Extrudes, Revolves & Solid Part Modeling

Turn sketches into solids. We cover the two workhorse features — Extrude and Revolve — plus the dress-up features (fillet, chamfer, shell, draft) that make parts manufacturable. By the end you can build a complete single-body part from a sketch and reason about add/remove/intersect Boolean operations.

- **Lectures:** From 2D to 3D: Extrude (New/Add/Remove), Depth Options, and Boolean Solids; Revolves, Holes, and Dress-Up Features: Fillet, Chamfer, Shell, and Draft
- **Exercises:** Modeling tasks: extrude a profile to a blind/through depth, cut a pocket with a remove extrude, revolve a profile 360 and partial angles to make a pulley or knob, place counterbored and countersunk holes with the Hole feature, and apply fillets, chamfers, and a shell to hollow a part.
- **Challenge:** Model a single-body bottle or cup from a revolved profile that must be shelled to a uniform wall thickness, then add a filleted base — reproduce a target part from a photo and a few key dimensions.
- **Mini-project:** Extend Week 1's master sketch into a finished solid part: extrude/revolve it to real thickness, add at least one mounting hole, and apply fillets/chamfers for manufacturability. Deliver the part plus a step-by-step modeling walkthrough.
- **Key tech:** Extrude, Revolve, Hole feature, Fillet, Chamfer, Shell, Boolean operations

## Week 03 — References, Planes & Multi-Feature Parts

Real parts need geometry built off other geometry. This week introduces construction planes, axes, and reference features, plus the productivity tools — patterns, mirror, sweep, and loft — that let one feature define many. We also discuss design intent: ordering features so edits propagate predictably.

- **Lectures:** Reference Geometry: Construction Planes, Offset/Angled Planes, Axes, and Mate Connectors; Multiplying Geometry: Linear & Circular Patterns, Mirror, Sweep, and Loft
- **Exercises:** Create offset and angled planes and sketch on them, sketch on a part face, build a swept handle along a path, loft between two profiles, and use linear and circular patterns plus mirror to populate a bolt-hole circle and a vent grille without re-sketching.
- **Challenge:** Model a multi-feature part such as a finned heat sink or a flanged pipe elbow that requires at least one non-default plane, one swept or lofted feature, and a pattern — built so changing a single driving dimension cleanly rebuilds the whole part.
- **Mini-project:** Promote the mini-project to a properly multi-feature part: add a patterned or mirrored feature set and at least one feature built on a non-default plane. Audit your feature tree, rename features meaningfully, and document the design-intent ordering in the walkthrough.
- **Key tech:** Construction planes, Mate connectors, Linear/circular pattern, Mirror, Sweep, Loft, Design intent

## Week 04 — Assemblies & Mates

Move from single parts to working assemblies. We cover inserting parts, the OnShape mate system (fastened, revolute, slider, planar, cylindrical, ball, pin-slot), and how mate connectors define degrees of freedom. You'll build an assembly that actually articulates and learn top-down vs bottom-up assembly strategy.

- **Lectures:** The Mate System: Degrees of Freedom and Choosing Fastened, Revolute, Slider, and Cylindrical Mates; Assembly Strategy: Insert vs In-Context Design, Sub-Assemblies, and the Standard Content Library
- **Exercises:** Assembly tasks: insert multiple parts, fasten a base, add a revolute mate to make a hinge swing, a slider mate for a drawer, and a cylindrical mate for a shaft; pull fasteners from the Standard Content library; group parts into a sub-assembly; check for clearance and interference.
- **Challenge:** Assemble a working 4-bar linkage or a simple hinged box from parts you model, mated so it has exactly the intended degrees of freedom and moves through its full range without interference.
- **Mini-project:** Turn the project into a multi-part assembly: model one or two mating components for your Week 3 part and join them with appropriate mates so at least one joint articulates. Deliver the assembly plus a walkthrough listing each mate and the degree of freedom it controls.
- **Key tech:** Assemblies, Mates, Degrees of freedom, Sub-assemblies, Standard Content library, Interference detection

## Week 05 — Drawings, Dimensions, GD&T & Configurations

Communicate and parameterize your design. We produce a proper drawing — orthographic and section views, dimensions, title block, BOM — and introduce GD&T basics and tolerancing. Then we make parts flexible with variables and Configurations, so one model yields a whole family of sizes.

- **Lectures:** Drawing Package: Orthographic & Section Views, Dimensioning, Title Blocks, BOM, and GD&T Basics; Parametric Power: Variables, Equations, and Configurations for Part Families
- **Exercises:** Create a drawing from a part: place standard and section views, add dimensions and a few GD&T callouts (datums, flatness, position), fill the title block, and auto-generate a bill of materials. Then add a Variable Studio and a Configurations table to drive a part into three sizes from one model.
- **Challenge:** Produce a manufacturing-ready drawing of an earlier part — fully dimensioned, toleranced, with at least one section view and a basic GD&T frame — and a configured version that switches between metric size variants from a dropdown.
- **Mini-project:** Parameterize the assembly's key part with Variables and a Configurations table (at least two size/variant options), then create a drawing for that part with views, dimensions, a title block, and a BOM. Deliver the drawing PDF plus a walkthrough of the configuration logic.
- **Key tech:** Drawings, Section views, Dimensioning, GD&T, Variables, Configurations, Bill of Materials

## Week 06 — Capstone: Multi-Part Mechanism & Drawing Package

Bring every skill together. Over the week you design, model, assemble, and document an original multi-part mechanism that moves — combining robust parametric parts, real mates, configurations, and a complete drawing package. This is a hackathon-style capstone judged on function, parametric robustness, and documentation quality.

- **Lectures:** Designing a Working Mechanism: From Concept Sketch to Articulating Assembly; Shipping a CAD Deliverable: Versions, Releases, Export Formats, and the Drawing Package
- **Exercises:** Capstone build tasks done in stages: scope and concept-sketch the mechanism, model each component as a clean parametric part, assemble with the correct mates so it articulates, add at least one configured/variable-driven part, then generate the full drawing set and BOM and export STEP/STL.
- **Challenge:** Demonstrate the mechanism's full range of motion in the assembly, prove parametric robustness by changing a key driving variable and confirming the whole assembly rebuilds cleanly, and present the design in a short walkthrough.
- **Mini-project:** Capstone deliverable: an original multi-part mechanism (e.g., a gripper, scissor lift, gear train, or hinged enclosure) of 3+ parts that articulates via mates, includes at least one configured part, and ships with a complete drawing package (assembly drawing, key part drawings, BOM), exported STEP/STL files, and a written design walkthrough.
- **Key tech:** OnShape, Assemblies, Mates, Configurations, Drawing package, STEP/STL export, Version control & releases

