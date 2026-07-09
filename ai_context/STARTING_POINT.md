# Starting Point — Analysis of the Old ERC 2026 Preliminary Report

This document distills everything worth knowing from `old_report/` (the ERC 2026
*Preliminary* Report repo) into one place. It is the agreed baseline from which
we will design the structure of the new report in this repo.

---

## 1. What the old repo was

A modular LaTeX report for a Mars rover + drone project (UCU Space Robotics,
project *Indomitus*), targeting the ERC 2026 Preliminary Report deliverable.

Key philosophy (from `README_old.md` / `old_report_recap.md`):

- **Short and dense.** Hard page limit forces minimal text; information is
  carried by tables, diagrams, photos, and 3D renders. Big diagrams go to
  appendices.
- **Modular by construction.** `main.tex` is only an assembler; every piece of
  content lives in its own small file so that many people can work in parallel
  without merge conflicts.
- **Team-parallel workflow.** "1 subsection file = 1 PR" rule; test plan rows
  are owned per team via macros.

## 2. Old repository architecture

```
main.tex                      # entry point — only \include/\input, no content
preamble.tex                  # all packages, colors, styles, custom commands
sections/                     # one file per top-level report chapter
  cover.tex
  matrix_of_compliance.tex          # §1 MoC          (0–25 pts)
  preliminary_test_plan.tex         # §2 Test Plan    (0–25 pts)
  preliminary_design_description.tex# §3 Design       (assembler for design tree)
  rio_analysis.tex                  # §4 RIO Analysis (0–25 pts)
  project_budget.tex                # §5 Budget       (0–27 pts)
sections/design/<N_chapter>/<N_M_section>/<N_M_K_leaf>.tex   # design content
teams/<team>/tests.tex        # per-team test rows (\XXXtestrows macros)
teams/<team>/figures/         # team-owned figure assets (actual practice)
tables/                       # large standalone tables (compliance, RIO, tests)
figures/{tikz,photos,cad}/    # documented layout (partially followed)
appendix/requirements.tex     # full ERC requirements table
```

### Design chapter hierarchy (deepest, most structured part)

```
1_product_trees_physical_breakdown/   # rover PBS, drone PBS, wiring diagram
2_rover_design_description/
  2_1_mechanical_design/              # chassis, locomotion, steering, arm,
                                      # joints, end-effector, sample storage, drill
  2_2_electrical_power_subsystem/     # batteries + hot-swap, power distribution
  2_3_communication_subsystem/        # architecture, freq plan, link analysis,
                                      # bandwidth, redundancy (2 leaves pruned)
  2_4_onboard_sensor_imaging_systems/ # nav sensors, science sensors, cameras
  2_5_software_architecture/          # overview, localization, autonomy, arm SW, science SW
  2_6_environmental_compliance/       # IP rating, dust/mud/rain, low-light
  2_7_operations/                     # ground station, wired→wireless, teleop, visual feedback
3_rover_technical_budgets/            # mass, CoG/slope stability, power, data link
4_rover_safety_systems/               # e-stop (physical + RF), warning lamp + 5s delay, human detection
5_drone_design_description/           # platform, landing pad, weather; avionics;
                                      # comms/GCS; localization/perception; autonomy
6_drone_technical_budgets/            # mass, power, data link
7_drone_safety_systems/               # signaling/delays, failsafes, flight ops & certification
```

LaTeX sectioning depth: `section → subsection → subsubsection → paragraph`
(secnumdepth/tocdepth = 4), so leaf files sit at `\paragraph` level.

## 3. Standards to carry forward (proven, keep)

### Units — `siunitx`, mandatory
- Never hand-written units (`10kg`, `1920x1080` are errors).
- `\qty{45}{\kilo\gram}`, `\qtyrange{-40}{85}{\degreeCelsius}`, `\ang{360}`,
  `\qtyproduct{1.2 x 0.8 x 0.5}{\meter}`, `\num{2.4e-5}`.
- Custom units declared **only** in `preamble.tex` via `\DeclareSIUnit`
  (existing: `\fps`; docs also mention `\mAh`, `\pixel`).

### Labels & cross-references
- Prefixes: `sec:` / `subsec:` / `subsubsec:` / `par:` / `tab:` / `fig:`.
- `\autoref{...}` for sections (autoref names remapped to `§`), `\ref` for tables.

### Figures & diagrams
- Complex diagrams are **never** drawn inline in section files.
- TikZ diagrams: standalone `.tex` files, included via `\input{figures/tikz/...}`.
- Electrical schematics: EasyEDA → PDF export → `figures/cad/`.
- Mechanical/CAD: SolidWorks/FreeCAD → PDF → `figures/cad/`.
- Photos: `figures/photos/`, extension omitted in `\includegraphics`.
- In practice team assets lived in `teams/<team>/figures/` — the new structure
  must pick one convention and enforce it (see §6).

### Preamble assets worth reusing (from `preamble_old.tex`)
- Geometry: A4, 2.54 cm margins on all sides (ERC requirement).
- Colors: `ercblue` (0,70,127) used for headings, links, header rule.
- Column types `L{}/C{}/R{}` for fixed-width ragged/centered table columns.
- Header/footer via `fancyhdr` with team name + "ERC 2026".
- Title formatting via `titlesec` (blue section titles with rule).
- Helper commands:
  - Compliance: `\compliant`, `\partlycompliant`, `\noncompliant`, `\notapplicable`
  - Risk levels: `\riskhigh`, `\riskmedium`, `\risklow`
  - Metadata: `\teamname`, `\projectname`, `\submissiondate`, `\revisionnum`
- `attachfile2` for embedding the MoC `.xlsx` into the PDF.
- **Remove for final:** `lipsum`, probably `todonotes`.

### Build
```bash
latexmk -pdf main.tex && latexmk -c
```

## 4. Workflow / contribution rules (from `CONTRIBUTING_old.md`)

- **1 leaf subsection file = 1 PR.** PR title convention: `DES <id>: short title`.
- PR description lists: which `REQ-*` it closes, cross-references added, what
  remains, and a screenshot of the compiled text.
- Each design leaf file starts with a **tiny contract** block:
  `Teams / Requirements / Status` — never deleted, updated as work progresses.
- Merge checklist: contract filled, no `[Add content ...]` placeholders, at
  least one explicit `REQ-*` mention, document compiles locally.
- Test plan: each team edits only `teams/<team>/tests.tex`, defining a
  `\<team>testrows` macro; a master longtable assembles all teams' rows.
- Never edit the assembler file (`preliminary_design_description.tex`) when
  just adding content to a leaf.

## 5. External (ERC) constraints that shaped everything

| Constraint | Value |
|---|---|
| Format | A4, searchable PDF |
| Page limit | 30 total (25 body + 5 appendices; cover & TOC excluded) — appendices count toward 30 |
| Language | English |
| Min font | 10 pt |
| Margins | ≥ 2.54 cm all sides |
| File name | `<TeamName>_PreliminaryReport_ERC2026.pdf` |
| MoC | `.xlsx` embedded into the PDF (e.g. via Foxit) |
| Extra deliverable | Preliminary RF Form submitted separately (missing = DQ) |

Scoring breakdown embedded as comments in the old section files (useful as a
content checklist): MoC 25 pts, Test Plan 25 pts, RIO 25 pts, Budget 27 pts.
RIO limits: max 10 risks (top by Risk Index = L×S on 1–5 scales), max 5
opportunities, max 5 issues.

## 6. Known weaknesses of the old setup (fix in the new structure)

1. **Fragile numeric ordering.** Folder/file names encode the section numbers
   (`2_3_5_link_performance_analysis.tex`). Any insertion/re-order forces mass
   renames and breaks git history. Evidence it already hurt: subsections 2.3.3
   and 2.3.4 were pruned by commenting them out in the assembler, leaving
   number gaps. → New repo should order via the assembler file only, with
   *unnumbered, stable* content file names (or accept numbering but document
   the renumber procedure).
2. **Duplicate table definitions with clashing labels.** The test-plan
   longtable exists both inline in `sections/preliminary_test_plan.tex` and in
   `tables/test_plan.tex` (with *different* column sets: one has a separate
   Setup column, the other merges Description & Setup and adds Timeline). Same
   story for the MoC summary (`tab:moc_summary` defined in both
   `matrix_of_compliance.tex` and `tables/compliance_summary.tex`) and the RIO
   tables (`tab:risks` etc. inline in `rio_analysis.tex` *and* in
   `tables/rio_table.tex`). → New rule: a table lives in exactly one file;
   sections only `\input` it.
3. **Docs vs reality drift.** README describes a root `figures/{tikz,photos,cad}`
   layout and `appendix/requirements.tex`, but actual practice used
   `teams/<team>/figures/` and appendix content in `main.tex`. → Pick one
   convention and make the README match reality.
4. **Placeholder debt.** Templates were full of `[X]`, `[Risk title]`,
   `[Add content ...]`; the checklist relied on humans catching them. → Keep
   the "no placeholders at merge" rule; consider a CI grep for `[X]`/`REQ-???`.
5. **Mixed-language docs with broken encoding.** README/CONTRIBUTING are
   Ukrainian (fine) but the stored copies have mangled UTF-8. → Re-author
   cleanly; decide language policy (docs UA is fine, report is English).
6. **Timeline presented twice** in the test plan (Gantt figure placeholder +
   month table). → Choose one representation.
7. **Cover file typo** (`cover)old.tex`) — trivial, but symptomatic; add basic
   name hygiene.

## 7. Ideas / principles to adopt for the new report structure

1. **Keep:** `main.tex` assembler + `preamble.tex` split; leaf-file-per-
   subsection; per-team test macro pattern; tables in `tables/`; siunitx and
   label conventions; ERC-blue visual identity; scoring rubrics as comments at
   the top of each section file (they double as content checklists).
2. **Keep the engineering-narrative ordering** — the document follows the
   report organization (system → subsystems → budgets → safety), not the
   requirements matrix. Requirements are cross-referenced from content
   (`REQ-*`), not the other way around.
3. **Change:** decouple file names from section numbers (ordering lives only
   in the assembler); single source of truth per table; one figures
   convention (recommend keeping `teams/<team>/figures/` since that's what
   people actually did, plus `figures/` for shared assets).
4. **Add:** a lightweight compile check (CI or pre-commit `latexmk`), a
   placeholder linter, and a page-count check against the limit.
5. **Reconfirm the deliverable requirements** for the *new* report (this repo
   is `final-report` — page limits, section list, scoring, and file naming for
   the ERC 2026 Final Report will differ from the Preliminary ones above and
   must be pulled from the current ERC rules before the structure is frozen).

---

*Sources: `old_report/old_report_recap.md`, `README_old.md`,
`CONTRIBUTING_old.md`, `preamble_old.tex`, and the old section/table `.tex`
files in `old_report/`.*
