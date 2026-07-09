# Project Overview

## What this repo is

LaTeX source for the **Final Report**, the main written deliverable of the
**European Rover Challenge (ERC) 2026** for team **UCU Space Robotics**
(Ukrainian Catholic University), project name **Indomitus** — a Mars rover
and companion drone.

The Final Report is a continuation and extension of the team's **Preliminary
Report**, which scored **126.75 / 150**. The Final Report covers the same
system after the manufacturing and testing phase: updated compliance status,
executed test results, the as-built design, safety systems, an updated risk
analysis, lessons learnt, and a regional geology analysis for the science
task. Full scoring breakdown: [`DELIVERABLE_REQUIREMENTS.md`](DELIVERABLE_REQUIREMENTS.md).

The old Preliminary Report repo is **not** this repo's ancestor in git — it's
archived reference material analyzed once, at the start, to decide what to
keep and what to fix (see `creation_context/STARTING_POINT.md`). This repo
was built fresh.

## Team & roles referenced in the repo

Roles matter more than names for understanding the workflow — most content
rules are written generically ("the maintainer", "the test-plan owner", "the
lessons curator") so they survive people changing roles. Names that appear in
committed files, as of this writing:

- **Mykola** — curates `tables/lessons_learnt.tex` (teams send candidates,
  he inserts the curated set); also pitching a new safety subsystem
  ("emergency-esp") for the Safety Systems section.
- **Bohdan** — owns §7 Science: Regional Geology Analysis.
- Seven subteams contribute content and figures: `arm`, `drone`,
  `electronics`, `ground_station`, `navigation`, `science`, `suspension`
  (mirrored as `teams/<team>/figures/` in the repo).
- One **maintainer** merges all PRs into `develop` and performs releases
  (tag + merge to `main` + version bump) — see `DECISIONS.md` for the
  branching model.

## Current phase

Repository bootstrap is done: a compiling LaTeX skeleton, CI, and contributor
docs are in place. Content writing has not started for most sections.
Sections 3 (Final Design Description) and 4 (Safety Systems) are
**deliberately structureless stubs** — the team has not yet held the session
that decides their internal breakdown (leaf files, ordering). Do not
scaffold `sections/design/` or `sections/safety/` until that decision is
made and lands as its own PR. Exact status of every phase:
[`STATUS.md`](STATUS.md).

## Where to look for what

| Question | File |
|---|---|
| How do I contribute / what are the rules? | `/CONTRIBUTING.md` |
| What's the repo layout and standards, in brief? | `/README.md` |
| What exactly is scored, and how much is it worth? | `DELIVERABLE_REQUIREMENTS.md` |
| Why is X built this way? | `DECISIONS.md` |
| What's done, what's next? | `STATUS.md` |
| What did the Preliminary Report look like, and what feedback did it get? | `creation_context/STARTING_POINT.md`, `creation_context/PROPOSAL.md` §"Jury feedback" |
| What did the team actually discuss before this was built? | `creation_context/chat_with_team.md` |
| What does the official template require, verbatim? | `creation_context/[TEMPLATE]_02_TEAMNAME_FINAL_REPORT_Rev.1.docx.md` |
