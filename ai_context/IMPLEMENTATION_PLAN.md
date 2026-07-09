# Implementation Plan — ERC 2026 Final Report

Executes `PROPOSAL.md` (rev. 2). Ordered so the repo compiles end-to-end from
day one and content lands via independent per-team PRs.

**Deliberately out of scope for now:** the internal structure of
**§3 Final Design Description** and **§4 Safety Systems**. The team has not
yet decided what goes into them. Both exist only as assembler stubs
(section heading + scoring rubric comment + TODO) until Phase 2 defines their
trees. No `sections/design/` or `sections/safety/` folders are created before
that decision.

---

## Phase 0 — Repo bootstrap (`infra/skeleton`, one PR, owner: Dmytro)

Goal: `latexmk -pdf main.tex` produces a complete 8-section PDF with stubs.

- [ ] `.gitignore` (LaTeX aux, editor droppings, `*.synctex.gz`)
- [ ] `preamble.tex` ported from the old repo: drop `lipsum`, keep `todonotes`
      (until freeze), keep siunitx + custom units, colors, `L{}/C{}/R{}`
      column types, compliance/risk helper commands, fancyhdr, `attachfile2`
- [ ] `metadata.tex` (`\teamname`, `\projectname`, `\submissiondate`,
      `\revisionnum`) + `main.tex` assembler
- [ ] Section stubs, each with its scoring rubric as a comment header:
  - `sections/00_cover.tex` — port from old repo; heading per Final rules
  - `sections/01_matrix_of_compliance.tex` — includes `tables/moc_summary`
  - `sections/02_test_plan.tex` — includes `tables/test_plan`
  - `sections/03_final_design_description.tex` — **stub only** (see above)
  - `sections/04_safety_systems.tex` — **stub only** (see above)
  - `sections/05_rio_analysis.tex` — methodology skeleton incl. empty L/S
    scale tables; includes `tables/rio_table`; trend-chart figure slot
  - `sections/06_lessons_learnt.tex` — includes `tables/lessons_learnt`
  - `sections/07_science_geology.tex` — map figure slot + 800-word budget note
- [ ] Table masters in `tables/`: `moc_summary.tex`, `test_plan.tex`
      (columns: *No · Name · Description incl. approach · Req. · Pass/Fail ·
      Results · Status* — the Req. column stays **only here**: it is scored in
      the official test table; requirements are not referenced anywhere else
      in the report, we dropped that scheme), `rio_table.tex` (single table,
      L/S/RI for R/O/I),
      `lessons_learnt.tex` (*ID · Title · Root cause · Description ·
      Recommendation · Impact*)
- [ ] `teams/<team>/` for all 7 teams (arm, drone, electronics,
      ground_station, navigation, science, suspension): `tests.tex` and
      `lessons.tex` with empty `\<team>testrows` / `\<team>llrows` macros so
      the masters compile; `figures/` with `.gitkeep`
- [ ] `figures/` for shared assets; `appendix/` placeholder for `moc.xlsx`
- [ ] Compile check locally; commit the verified skeleton

## Phase 1 — Tooling & docs (parallel `infra/*` PRs, owner: Dmytro)

- [ ] `infra/ci`: GitHub Actions — build PDF (TeX Live), upload artifact on
      every PR; placeholder lint (`[X]`, `[Add content`, `\lipsum`; `\todo`
      joins the list at freeze) as a separate check; page count via `pdfinfo`
      (warn > 35 effective pages)
- [ ] `infra/pr-template`: `.github/pull_request_template.md` — summary of
      what the PR adds, cross-refs, what remains, merge checklist
- [ ] `infra/docs`: `README.md` + `CONTRIBUTING.md` in English, written from
      `PROPOSAL.md` (branch naming, 1-leaf-1-PR, tiny contract, figure
      conventions, siunitx, build command). README must match reality —
      no described-but-nonexistent folders
- [ ] Archive `old_report/` reference materials stay as-is; `STARTING_POINT.md`
      and `PROPOSAL.md` remain the design record

## Phase 2 — Carry-over data from the Preliminary (content PRs, can start
right after Phase 0)

These ports unblock everyone and satisfy "IDs must match" constraints:

- [ ] `rio/port-preliminary`: R-01…R-10, O-01, I-01…I-03 into
      `tables/rio_table.tex` with statuses as of today; add L/S to O/I rows
      (jury ask); collect RI values for the trend chart
      (16 / 12 / 12 / 10 / 9 / 9 / 9 / 8 / 6 / 6)
- [ ] `test/port-preliminary` (per team, 7 PRs): the 37 tests
      (SUS-01…DRO-07) from the Preliminary appendix into `teams/*/tests.tex`,
      re-shaped to the new columns; *Results/Status* honest — measured value
      where a test ran, `Planned` otherwise
- [ ] `moc/summary`: compliance summary table (72 requirements baseline) +
      the prose paragraph the jury asked for (stub until second-iteration
      statuses are assessed)
- [ ] `rio/trend-chart`: chart drawn outside LaTeX (per diagram policy),
      exported PDF; needs Final-phase RI values, so lands late — create the
      data file + figure slot now

**Gate A — skeleton merged, CI green, carry-over data in.** From here every
team can work without touching shared files.

## Phase 3 — Structure decisions for §3 and §4 (team session, owner: Dmytro)

Input for the session, already agreed in `PROPOSAL.md`:

- jury action items that must land *somewhere* in §3/§4 (dimensioned
  drawings + cross-sections, drone photos, E-stop button circuit, drone data
  link budget, critical parts, innovations, PT/WBS/OBS);
- the FDD content rule (evidence first, prose minimal);
- the emergency-esp pitch (decides one safety slot);
- page budget: FDD 15 pages, Safety 3.5.

Output: agreed section trees → one `infra/design-tree` PR creating the
folders, leaf files with tiny contracts, and the two assemblers. Only after
this do `des/*` and `safety/*` content PRs start.

## Phase 4 — Content writing (per-team PRs, rules from CONTRIBUTING)

- [ ] §1 MoC second-iteration pass: leads review their requirements, then a
      dedicated session (test team + Dmytro + Ozhhovych) resolves statuses;
      update `moc.xlsx` + summary
- [ ] §2 test execution results as tests run — each result lands as a small
      `test/<team>` PR updating the team's rows
- [ ] §3/§4 per the Phase 3 trees (`des/*`, `safety/*` branches)
- [ ] §5 RIO update: re-assess every risk (unchanged-majority scores low),
      make generic risks subsystem-specific, finish the trend chart
- [ ] §6 Lessons Learnt: every team submits candidates via `ll/<team>` PRs;
      Dmytro curates to fit 3 pages; include the budget-transparency LL from
      the jury feedback
- [ ] §7 Science geology (Bohdan): composite map (location + regional
      geological + CTX/HiRISE close-up with ellipse, path, 3 ROIs) + ≤800 words

## Phase 5 — Freeze week (owner: Dmytro)

- [ ] Only `fix/*` PRs allowed
- [ ] CI placeholder lint + page count switch to **hard fail**; remove
      `todonotes`
- [ ] Embed final `moc.xlsx` into the PDF; verify attachment opens
- [ ] File naming exactly per the Rules (`<TeamName>_FinalReport_ERC2026.pdf`
      pattern — verify against the Rules text; wrong naming −10 / risk of 0)
- [ ] Margin/font sanity pass (≥10 pt body, 8 pt only in RIO tables)
- [ ] Final RF Form prepared and submitted **separately**, matching the real
      RF state (judges cross-check at RF check)

---

## Dependencies at a glance

```
Phase 0 (skeleton) ─→ Phase 1 (CI/docs) ─┐
        └─→ Phase 2 (carry-over data) ───┼─→ Gate A ─→ Phase 4 (content)
Phase 3 (§3/§4 trees, team session) ─────┘         ↘ Phase 5 (freeze)
```

Phases 1–3 run in parallel after Phase 0; §3/§4 content is the only work
blocked on the team session.
