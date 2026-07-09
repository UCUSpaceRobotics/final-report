# Status

Snapshot as of **2026-07-10**. Phases refer to
`creation_context/IMPLEMENTATION_PLAN.md` (written before the branching
model existed — read task content from there, but trust `DECISIONS.md` and
this file over its branch/owner references, which predate later decisions).

## Done

- **Phase 0 — Repo bootstrap.** `main.tex` assembler, `preamble.tex`
  (ported from the Preliminary, `lipsum` dropped), `metadata.tex`. All 8
  section files exist under `sections/` with their scoring rubric as a
  comment header. §3 (Final Design Description) and §4 (Safety Systems) are
  intentionally structureless stubs (see `DECISIONS.md`). Table masters
  exist for MoC summary, Test Plan, RIO register, and Lessons Learnt — all
  currently empty/stub content. `teams/<team>/figures/` scaffolded for all
  7 teams. Compiles clean: `latexmk -pdf main.tex` → 4 pages, no warnings
  (expected to grow once table stubs are ported/filled).
- **Phase 1 — Tooling & docs.** CI (`.github/workflows/build.yml`): compiles
  and uploads the PDF as an artifact, placeholder lint, page-count warning
  — runs on every push to every branch and on every PR. PR template
  requires a description, cross-references, and a **screenshot of the
  compiled section** pasted into the PR body. `README.md` and
  `CONTRIBUTING.md` written in English, covering the deliverable
  requirements, repo structure, standards, branching model, and PR flow.
- **Branching model implemented.** `develop` and `main` both exist as
  branches. Documented in `README.md`, `CONTRIBUTING.md`, and
  `creation_context/PROPOSAL.md`.
- **Test Plan / Lessons Learnt ownership model reversed** from per-team
  macro files to single owner-edited tables (see `DECISIONS.md`).

## Not started

- **Phase 2 — Carry-over data from the Preliminary.** None of the following
  have been ported yet:
  - RIO register: R-01…R-10, O-01, I-01…I-03 into `tables/rio_table.tex`
    (RI baseline for the trend chart: 16 / 12 / 12 / 10 / 9 / 9 / 9 / 8 / 6 / 6).
  - The 37 tests (SUS-01…DRO-07) into `tables/test_plan.tex`, reshaped to
    the new Results/Status columns.
  - MoC summary table (72-requirement baseline from the Preliminary).
  - Risk trend chart (needs Final-phase RI values, so it lands late, but the
    figure slot and methodology tables already exist in
    `sections/05_rio_analysis.tex`).
- **Phase 3 — Structure decisions for §3 and §4.** No team session has
  happened yet. Nothing should be scaffolded under `sections/design/` or
  `sections/safety/` until it does. Inputs the session needs to resolve are
  listed in `sections/03_final_design_description.tex` and
  `sections/04_safety_systems.tex` (`\todo` blocks) and in
  `creation_context/PROPOSAL.md` §4 "Open questions."
- **Phase 4 — Content writing.** Nothing written yet for any section beyond
  the stub `\todo` markers.
- **Phase 5 — Freeze week.** Not started. Placeholder/page-count hard-fails
  are wired but disabled; `moc.xlsx` doesn't exist yet; file naming and
  RF Form submission haven't been addressed.

## Open questions blocking Phase 3

From `creation_context/PROPOSAL.md` §4, still unresolved:

1. Design tree granularity — compress subsections unchanged since the
   Preliminary to free pages for evidence, or keep 1:1 with the Preliminary
   structure?
2. Mykola's "emergency-esp" safety subsystem pitch — decides whether one
   safety page-budget slot is spent on it.
3. WBS/OBS format — one combined diagram per structure, or per-vehicle
   (matching how the Product Trees are already split)?

## Git state at this snapshot

- `main`: has the bootstrap skeleton, CI/docs, and branching-model/screenshot
  policy commits. Not yet pushed past `origin/main`'s last sync point —
  check `git log origin/main..main` for what's still local-only.
- `develop`: exists, tracks `main`'s tip as of its creation — has not
  diverged with any content work yet, since Phase 2–4 haven't started.
- No tags exist yet (no release has happened).
