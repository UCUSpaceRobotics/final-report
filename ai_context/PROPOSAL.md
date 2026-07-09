# Proposal — Structure, Guidelines & Workflow for the ERC 2026 Final Report

Based on: `STARTING_POINT.md` (analysis of the Preliminary Report repo), the
official Final Report template, the team discussion (`chat_with_team.md`), the
submitted Preliminary Report (scored **126.75/150**), and the jury feedback
(`old_report/preliminary_report_feedback.md`).

Status: **rev. 2 for team review** — updated with team decisions and jury feedback.

---

## 1. The deliverable (what the rules demand)

| Parameter | Value |
|---|---|
| Sections (fixed order) | 1 MoC Update · 2 Test Plan · 3 Final Design Description · 4 Safety Systems · 5 RIO Analysis · 6 Lessons Learnt · 7 Science: Regional Geology |
| Scoring | MoC 10 · Test Plan 20 · FDD 40 · Safety 10 · RIO 20 · LL 20 · Science 10 · Final RF Form 20 (separate doc) = **150 pts** |
| Format | A4, searchable PDF, English |
| Length | **max 35 pages** (excluding cover, ToC/LoF/LoT, and Appendix 3 – Requirements) |
| Fonts | ≥ 10 pt everywhere; **8 pt allowed only in RIO tables** |
| Margins | ≥ 2.54 cm all edges |
| MoC | second iteration, `.xlsx` **embedded** in the PDF (3 pts; separate file only 1 pt) |
| Penalties | wrong report/MoC naming −10 each · wrong font −10 · wrong margins −5 · extra pages −X (formula) · review-mode artifacts −5 |

**Resolved decisions:**

- **RF Form is a separate document, outside the 35 pages** — the page budget
  below uses the full 35 pages for report content.
- **PT / WBS / OBS** = Product Tree, Work Breakdown Structure, Organisation
  Breakdown Structure. PTs for rover and drone already exist from the
  Preliminary (its Figures 15–16) and only need updating; WBS (work packages)
  and OBS (team organisation chart) are new diagrams.
- **Everything is in English** — report and repo docs (README, CONTRIBUTING).
- Template copy-paste debt ("ERC 2025", title "Proposal", "Lessons Learnt"
  listed twice in its ToC) is ignored; the Rules take precedence.

### Page budget (proposal — enforced softly via CI warning)

| # | Section | Pages | Rationale |
|---|---|---|---|
| 1 | MoC summary | 1 | table **+ short prose** (jury asked for text, not counts alone) |
| 2 | Test Plan | 6.5 | 15/20 pts are for *results & conclusions* — give it room |
| 3 | Final Design Description | 15 | 40 pts; rover ≈ 9.5, drone ≈ 4, PT/WBS/OBS ≈ 1.5 |
| 4 | Safety Systems | 3.5 | jury wants the E-stop circuit + architecture, sequences, test evidence |
| 5 | RIO Analysis | 3.5 | table at 8 pt + trend chart |
| 6 | Lessons Learnt | 3 | table format, best entries only |
| 7 | Science: Geology | 2 | fixed by rules: composite map (1 A4) + ≤800 words |
| — | reserve | 0.5 | slack for overflow |
| | **Total** | **35** | |

---

## 2. Repository structure

Principles (fixes for the pain points from the old repo):

1. **Ordering lives only in assembler files.** Content files/folders have
   stable, descriptive, **unnumbered** names → inserting/pruning a subsection
   never causes renames (old repo had to comment out 2.3.3/2.3.4 and live with gaps).
   Top-level `sections/` files keep two-digit prefixes only because the 7
   sections are fixed by the template and cannot reorder.
2. **One table = one file = one label**, always in `tables/`, included exactly
   once (old repo had `tab:moc_summary`, the test longtable and the RIO tables
   defined twice with diverging columns).
3. **Diagrams are made outside LaTeX** (team decision): draw.io / EasyEDA /
   CAD / Figma → export **PDF** → `figures/`. No inline TikZ in section files;
   no TikZ requirement at all this time.
4. **README describes reality** — one figures convention, enforced.

```
main.tex                        # assembler only: metadata + \input of sections
preamble.tex                    # packages, styles, colors, custom commands
metadata.tex                    # \teamname, \projectname, \revisionnum, dates
.github/
  workflows/build.yml           # CI: compile, placeholder lint, page count
  pull_request_template.md      # what the PR adds, what remains, checklist
sections/
  00_cover.tex
  01_matrix_of_compliance.tex   # §1 (rubric as comment header)
  02_test_plan.tex              # §2 assembler: intro + \input tables/test_plan
  03_final_design_description.tex  # §3 assembler for the design tree
  04_safety_systems.tex         # §4 assembler
  05_rio_analysis.tex           # §5 methodology + \input tables/rio + trend chart
  06_lessons_learnt.tex         # §6 intro + \input tables/lessons_learnt
  07_science_geology.tex        # §7 (Bohdan; map figure + ≤800 words)
sections/design/                # leaf lists mirror the submitted Preliminary
  breakdowns/                   # product_tree_rover.tex, product_tree_drone.tex
                                #   (update Prelim Figs 15-16), wbs.tex, obs.tex (NEW)
  rover/
    mechanical/                 # chassis_geometry.tex, drive_selection.tex,
                                #   wheels.tex, manipulator.tex, actuators.tex,
                                #   end_effectors.tex, sample_storage.tex
    power/                      # batteries_hotswap.tex, distribution.tex
    comms/                      # architecture.tex, frequency_plan.tex,
                                #   link_performance.tex, bandwidth.tex, redundancy.tex
    sensors/                    # navigation_suite.tex, science_suite.tex, cameras.tex
    software/                   # localization.tex, navigation.tex,
                                #   arm_planning.tex, science_autonomy.tex
    operations/                 # ground_station.tex, teleoperation.tex
    budgets/                    # mass.tex, cog_stability.tex, power.tex, data_link.tex
    critical_parts.tex          # NEW: parts critical for on-site ERC tasks
    innovations.tex             # NEW: highlight of innovative solutions
  drone/
    platform.tex                # MUST show the drone: photos + labeled overview
    landing_platform.tex  avionics.tex  comms.tex  localization.tex  vision.tex
    budgets/                    # mass.tex, power.tex, data_link.tex
                                #   (data link was MISSING in the Preliminary —
                                #    the rubric requires mass + power + data link)
    critical_parts.tex  innovations.tex
sections/safety/                # promoted to its own top-level section (10 pts)
  architecture_time_sequence.tex   # system-level: architecture + timing diagrams
  estop.tex                     # physical + RF e-stop; incl. the BUTTON CIRCUIT
                                #   schematic the jury flagged as missing
  wheel_lock.tex  indicators_delays.tex  human_detection.tex
  emergency_esp.tex             # Mykola's new system — slot reserved
  reliability_analysis.tex  test_evidence.tex   # test results, figures, photos
teams/<team>/                   # arm, drone, electronics, ground_station,
  figures/                      #   navigation, science, suspension -
                                #   team-owned assets (photos, exported PDFs)
                                # NOTE: tests/lessons are NOT per-team files -
                                # both tables are owner-edited, rows inserted
                                # all at once (decision 2026-07-09)
tables/
  moc_summary.tex  test_plan.tex  rio_table.tex  lessons_learnt.tex
figures/                        # shared assets only (cover, system-level diagrams)
appendix/
  moc.xlsx                      # embedded into the PDF at release time
```

### FDD content rule: concrete data first (team decision + jury feedback)

The Preliminary passed on renders and well-worded prose; the Final will not.
Every design leaf must **lead with evidence** and keep text to what the
evidence cannot say:

- at least one of: **photo of the built hardware**, **dimensioned drawing /
  cross-section**, **schematic**, or a **calculation table** per leaf;
- renders only where hardware doesn't physically exist yet — and never as the
  sole figure for items the jury flagged (rover element details, the drone);
- **overall dimension drawings** of the rover and the drone are mandatory
  figures (jury explicitly asked for overall dimensions and cross-sections);
- keep the calculation style that already worked well (drive-torque, CoG,
  power, link-budget tables) and extend it with **measured values** where
  tests have run.

### What carries over from the old repo unchanged

- `main.tex` + `preamble.tex` split; ERC-blue identity; `L{}/C{}/R{}` column
  types; compliance (`\compliant` …) and risk (`\riskhigh` …) helper commands;
  `attachfile2`; fancyhdr header/footer.
- **siunitx mandatory** — never hand-written units; custom units only via
  `\DeclareSIUnit` in `preamble.tex`.
- Label prefixes `sec:/subsec:/subsubsec:/par:/tab:/fig:` + `\autoref`.
- Scoring rubric as a comment header in each section file (doubles as checklist).
- Per-team macro pattern for tests — now also used for Lessons Learnt.
- Remove `lipsum` from the preamble; keep `todonotes` until the freeze week.

### New content obligations (didn't exist in the Preliminary)

| Item | Where | Owner |
|---|---|---|
| WBS + OBS (PTs exist from the Preliminary, need updating) | `design/breakdowns/` | PM |
| Drone **data link** budget (absent from the Preliminary; rubric requires mass + power + data link) | `design/drone/budgets/data_link.tex` | drone + ground station |
| Critical parts for on-site tasks | `design/{rover,drone}/critical_parts.tex` | leads, sourced from requirements sweep |
| Innovative solutions highlight | `design/{rover,drone}/innovations.tex` | all leads propose, PM curates |
| Test **results** + design modifications | test table gains *Results* and *Passed/Failed* columns | test team |
| Risk **trend chart** (ECSS-M-ST-80C fig. 5-7 style; phases: Preliminary → Final; **Risk IDs must match the Preliminary Report**) | `sections/05_rio_analysis.tex` + external figure | PM + test team |
| Lessons Learnt (ID, root cause, description, recommendation, impact) | `tables/lessons_learnt.tex`, curator-edited; teams send candidates | curator (Mykola) |
| Regional Geology (composite map + ≤800 words) | `sections/07_science_geology.tex` | Bohdan |

The new test-plan table columns (per template): *Test No. · Name · Description
(incl. approach) · Requirements Tested · Pass/Fail Criteria · Results · Status*.
Existing test IDs from the Preliminary should be preserved where the test is the same.

### Jury feedback → binding action items (Preliminary: 126.75/150)

Every item below is treated as a merge-blocking requirement for its section.

| Jury feedback (O/PRR) | Action in the Final Report | Where |
|---|---|---|
| MoC: table was great, but "text would streamline the experience" | short prose paragraph interpreting the compliance summary, not counts alone | `01_matrix_of_compliance.tex` |
| Test Plan: "run the tests, report the achieved value against each criterion, add results and status columns" — design praised, data missing | *Results* + *Passed/Failed* columns; every executed test states the **measured value vs its criterion**; not-yet-run tests keep an honest status; keep the 37 Preliminary test IDs (SUS-01 … DRO-07); state design modifications that followed from failures | `02_test_plan.tex`, `tables/test_plan.tex` (owner-edited) |
| Design (b): "missing emergency stop button circuit" | E-stop button circuit schematic included | `safety/estop.tex` |
| Design (b): "more detailed pictures of rover elements, cross-section, and overall dimensions" | dimensioned drawings + cross-sections per the FDD content rule above | `design/rover/*` |
| Design (c): drone description extensive "but it is not shown how the drone looks at all" | real photos + labeled overview figure of the built drone, first thing in the drone chapter | `design/drone/platform.tex` |
| RIO: "include within methodology description tables of likelihood/severity" | L/S scale **tables** in the methodology (Preliminary had prose only) | `05_rio_analysis.tex` |
| RIO: "Issues and Opportunities should have their likelihood and severity tracked as well" | single RIO table (per Final template) with L/S/RI columns filled for O-* and I-* entries too | `tables/rio_table.tex` |
| RIO: "some risks are quite general (i.e. R-01 → determine which system is critical)" | make generic risks concrete (name the subsystem) while keeping IDs traceable; highlight & explain every modification, as the template demands | `05_rio_analysis.tex` |
| Budget: "specify COTS vs custom … explain the source of the budget in words" | no Budget section in the Final Report — carry into the next season's Proposal; candidate **Lessons Learnt** entry | `06_lessons_learnt.tex` / future |

RIO continuity data for the trend chart (from the submitted Preliminary):
R-01 (RI 16), R-02/R-03 (12), R-04 (10), R-05–R-07 (9), R-08 (8), R-09/R-10 (6);
plus O-01 and I-01…I-03. **IDs must match**; removals/additions must be
highlighted and justified.

---

## 3. Workflow

### Branch naming (requested: clear rules)

`<type>/<scope>-<short-slug>`, lowercase, hyphens:

| Type | Used for | Example |
|---|---|---|
| `des/` | design leaf content | `des/rover-chassis`, `des/drone-avionics` |
| `test/` | team test rows | `test/suspension` |
| `safety/` | safety section files | `safety/emergency-esp` |
| `moc/` `rio/` `ll/` `sci/` | the other sections | `rio/trend-chart`, `ll/electronics` |
| `infra/` | preamble, CI, docs | `infra/ci-page-count` |
| `fix/` | typos, small corrections | `fix/units-in-power-budget` |

### PR rules (keeps the model that worked: 1 leaf file = 1 PR)

1. One PR changes **one** content file (plus its own figures). Assemblers,
   `preamble.tex` and `tables/` masters are changed only via `infra/` PRs.
2. Title: `<TYPE> <scope>: short title` — e.g. `DES rover/comms: link budget analysis`.
3. Open as **Draft** immediately (work-in-progress visible), mark **Ready for
   review** when done; the maintainer merges — same as last time.
4. PR description (enforced by the PR template): what the PR adds,
   cross-references added, what remains.
5. **No screenshots needed anymore** — CI uploads the compiled PDF as an
   artifact on every PR, so the reviewer reads the real output.
6. Tiny contract kept at the top of every content file
   (`% Teams: … / Status: …`) — update, never delete. (The old `Requirements`
   field is dropped: we no longer reference requirements inside the report;
   the only place they appear is the test table's *Req.* column, which the
   official rubric scores.)

### Merge checklist (CI enforces the mechanical parts)

- [ ] compiles (`latexmk -pdf main.tex`) — **CI**
- [ ] no placeholders `[X]`, `[Add content…]`, `\lipsum` (`\todo` at freeze) — **CI grep**
- [ ] page count ≤ 35 effective pages — **CI warning** (hard fail at freeze)
- [ ] tiny contract filled — reviewer

### CI (GitHub Actions, `infra/` to set up first)

1. Build PDF with `latexmk` (TeX Live container), upload as artifact.
2. Placeholder linter (grep list above) — fails the check.
3. Page count via `pdfinfo` minus cover/ToC/appendix offset — warns, then hard
   limit during freeze week.

### Editor policy

Any editor is fine (TeXStudio for writing, VS Code for git/Copilot). The repo
guarantees this by keeping files small and self-contained; no editor-specific
files committed (`.gitignore` covers aux files and editor droppings).

### Timeline gates (proposal)

1. **Skeleton merged** — repo compiles end-to-end with section stubs + CI green.
2. **Content complete** — every leaf file filled, drafts merged.
3. **Freeze week** — only `fix/` PRs; page-count check becomes hard-fail;
   remove `todonotes`; embed `moc.xlsx`; verify naming
   `<TeamName>_FinalReport_ERC2026.pdf` (exact pattern from the Rules — wrong
   naming is −10 and risks 0 pts for the deliverable).

---

## 4. Open questions for the team

1. **Design tree granularity**: the rover tree above mirrors the submitted
   Preliminary — do we compress subsections that are unchanged since then and
   spend the freed pages on photos/drawings/test data? (35 pages is tight;
   FDD excellence = evidence, not prose.)
2. **emergency-esp**: safety slot reserved above — Mykola to pitch the idea
   before we commit page budget to it.
3. **WBS/OBS format**: single combined diagram per structure or per-vehicle?
   (PTs stay per-vehicle as in the Preliminary.)

---

*Next step once agreed: bootstrap the skeleton (`infra/skeleton` PR) — preamble
ported from the old repo minus `lipsum`, section stubs with rubric headers,
tables masters, team folders, CI workflow, README + CONTRIBUTING rewritten from
this document.*
