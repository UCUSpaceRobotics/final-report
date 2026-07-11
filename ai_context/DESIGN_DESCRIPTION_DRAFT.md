# Final Design Description — Draft Notes (handwritten, transcribed)

Transcription of handwritten planning notes (photographed pages) sketching
the content and figure/photo requirements for §3 Final Design Description.

**This is a draft brainstorm, not the finalized section tree.** It covers
only the **rover** side, has several items marked TBD or unassigned, and
does not yet address the Drone Design Description, Drone Technical Budget,
Drone Critical Parts, or Drone Innovations (all required by
[`DELIVERABLE_REQUIREMENTS.md`](DELIVERABLE_REQUIREMENTS.md) §3). Treat this
as input to the Phase 3 team session (see `STATUS.md`), not its output — **no
`sections/design/` LaTeX structure should be created from this file yet.**

## Reading notes — uncertain transcriptions

- "max ni[gu/vantazh]... capacity" (Robotic hand overview, item 2) — hard to
  read; likely "max payload/load capacity" (possibly the Ukrainian
  *навантаження*/*вантажопідйомність* written in Latin script).
- "Photo with unified [...]" near the gripper photo grid (item 2) — partly
  obscured; best guess is "Photo with unified end-effector."
- Item 6 (6-DOF Manipulator): "Martha should create ~~[word]~~" — the
  crossed-out word is illegible.
- The rotated page (photo labeled "9. Navigational Stack" / "6/7/8...") is
  hard to read at the fold; the box under "9. Navigational Stack" says
  "Photo of electronics," which may be a placeholder reused from elsewhere
  rather than intentional.
- Item 7 of the critical-parts list is present as a bare "7." with nothing
  written under it — left blank in the original.

## Overall structure sketched

```
Final Design Description
├─ Product Tree                          (1 × A4)
├─ Work Breakdown Structure (WBS)        (1 × A4)
├─ Organisation Breakdown Structure (OBS)(1 × A4)
├─ Rover Design Description
│   1. Rover's design overview
│   2. Robotic hand overview
│   3. Science container
│   4. Electronics overview
│   5. Ground station overview
│   6. Hardware overview                (content TBD)
│   7. Software overview                (content TBD)
│   8. Communication overview           (content TBD)
│   9. Navigational Stack               (block schemes of localisation pipeline)
├─ Rover Technical Budget
│   1. Mass
│   2. Power
│   3. Data link budget
├─ Critical Parts Required for On-Site ERC Tasks (rover)
│   1. Rocker-only suspension
│   2. Wheels design
│   3. Gripper design
│   4. Astro-bio gripper
│   6. 6-DOF Manipulator                (unassigned decomposition — owner: Martha)
│      (5 moved to Innovative Design Solutions below; 7 dropped — was blank)
├─ Rover Innovative Design Solutions
│   • Unified sample gripper            (content/photo requirements TBD)
└─ [not covered in these notes — see "Gaps" below]
```

The numbered "Rover Design Description" list (1–9) and the numbered
"Critical Parts" list (originally 1–7, now 1–4 + 6) are **two separate
lists** in the original notes — both start over at 1. They likely become two
separate subsections under Rover Design Description, per the official
template's structure (design description, then technical budget, then
critical parts, then innovations).

## Rover Design Description (items 1–9)

Each item lists the figures/photos the author sketched as boxes on the page
— read these as "this subsection needs at least these visuals," consistent
with the evidence-first rule in `DECISIONS.md`.

**1. Rover's design overview**
> "Indomitus Mars rover is a rocker-only suspension rover..." (text trails
> off in the original, presumably continues in the actual write-up)
- Rover's scheme with sizes
- Rover's photo #1
- Rover's photo #2

**2. Robotic hand overview**
- Covers: size, reach, weight, max payload/load capacity (see reading note)
- Hand's scheme with sizes
- Photo with gripper
- Photo with bio gripper
- Photo of hand
- Photo with unified end-effector (see reading note)
- Note in original: *"all photos of grippers depict them in action"*

**3. Science container**
- Covers: size, capacity (how big rocks it can contain), what weights it
  can measure, what precision
- Scheme of container with sizes
- Photo of collecting sand
- Photo of collecting rock
- Note in original: *"will not be represented at next chapters"* — i.e.
  the science container is fully described here and deliberately not
  repeated elsewhere in the report.

**4. Electronics overview**
- General information
- Structural scheme
- Photo of electronics

**5. Ground station overview**
- Covers: general info, capabilities (number of monitors, buttons, etc.)
- GS's scheme with sizes
- Photo of operator using it

**6. Hardware overview** — no further detail captured on these pages.

**7. Software overview** — no further detail captured on these pages.

**8. Communication overview** — no further detail captured on these pages.

**9. Navigational Stack**
- Block schemes of localisation pipeline

## Rover Technical Budget

Separate subsection, not part of the numbered design-description list above
(matches the official rubric's "Rover technical budget: Mass, Power, Data
Link" line item):

1. **Mass** — same approach as in the Preliminary Report, recalculated.
2. **Power** — amps, and other required electrical specs.
3. **Data link budget** — ground station ↔ rover
   (note in original questions whether internal/onboard communication
   should also be covered here: *"internal communication?"*).

## Critical Parts Required for On-Site ERC Tasks (rover)

Matches the official rubric's "Description of critical parts required to
attempt the on-site ERC tasks" line item.

**1. Rocker-only suspension**
- How this suspension suits us; its obstacle-overcoming capabilities
- Scheme with sizes
- Photo of suspension
- Photo of overcoming obstacles

**2. Wheels design**
- Explain how this design suits us; how it benefits us on regolith terrain
- Scheme of wheel on disc and bracket
- Photo of the wheel
- Photo during work traversing sand

**3. Gripper design**
- Covers: characteristics, size, capabilities
- Detailed scheme with the names of parts
- Photo of working on panel

**4. Astro-bio gripper**
- Note in original: *"same as previous"* — follow the same format as
  item 3 (Gripper design).

**6. 6-DOF Manipulator** — *unassigned/undecided.* Notes: "IDK how to
decompose it. Martha should do it. She can add additional sections."
Owner: **Martha** (decomposition and content still to be defined).

## Rover Innovative Design Solutions

**Unified sample gripper** — moved here from the Critical Parts list (was
item 5, crossed out there with the side note *"maybe more to[wards]
innovative design"*). Content/photo requirements not yet defined.

## Gaps — not addressed in these notes

These are required by the official rubric
(`DELIVERABLE_REQUIREMENTS.md` §3) but have no corresponding notes here:

- **Drone Design Description** (structure 0–4 pts + excellence 0–10 pts,
  0 if fully COTS)
- **Drone Technical Budget** (mass, power, data link)
- **Drone critical parts** for on-site ERC tasks
- **Drone innovative design solutions**

## Open items before this can become the agreed design tree

1. Resolve items 6–8 of the Rover Design Description list (Hardware /
   Software / Communication overview) — no figure/content requirements
   captured yet.
2. Martha to decompose item 6 (6-DOF Manipulator) and confirm what
   additional sections it needs.
3. Define content/photo requirements for "Unified sample gripper" under
   Rover Innovative Design Solutions.
4. Produce the drone-side equivalent of every section above.
5. Reconcile the apparent overlap between "Robotic hand overview" (item 2
   of the design description) and "Gripper design" / "Astro-bio gripper"
   (items 3–4 of critical parts) — decide whether these describe different
   scopes or need to be merged to avoid duplicate content.
