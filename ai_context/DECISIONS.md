# Decisions Log

Every non-obvious choice baked into this repo, with the reasoning. If you're
about to "fix" something that looks odd, check here first — it's probably
deliberate. Newest first isn't enforced; entries are grouped by topic.

## Scope & content

**RF Form is a separate document, outside the 35-page report.**
The template contradicts itself on this (see `DELIVERABLE_REQUIREMENTS.md`
→ "Known template issues"). The team resolved it in favor of the RF Form
section's wording, so the report's page budget uses the full 35 pages.

**Requirements are not referenced inside the report body.**
The Preliminary Report's workflow had every design leaf carry a
`Requirements:` field in its tiny contract, and PRs cited `REQ-*` IDs. The
team dropped this for the Final Report — it added bookkeeping overhead
without being scored anywhere except one place. The **single exception**:
the Test Plan table's *Req.* column, because "all requirements to be
verified by test are mentioned" is explicitly worth points (0–1 pt,
Test Plan structure).

**Every figure and table must be referenced from the prose around it,
always via `\autoref` — `\ref` is forbidden.** A `\label` alone isn't
enough — orphan figures that are labeled but never cited in the
surrounding text are treated as a review mistake (see `CONTRIBUTING.md`,
"Common mistakes"). `\autoref` inserts the right name ("Figure", "Table",
"§") automatically, so content never hand-types `Figure~`/`Table~` before
a reference — one less thing to get out of sync if a label's target type
changes.

**Design content leads with evidence, not prose ("FDD content rule").**
The Preliminary Report scored well on structure but the jury explicitly
asked for more photos, dimensioned drawings, cross-sections, and asked why
the drone was never shown despite an extensive description. Rule for every
Final Design Description leaf: lead with a photo of built hardware, a
dimensioned drawing/cross-section, a schematic, or a calculation table.
Renders are allowed only where the hardware doesn't physically exist yet,
and never as the sole figure for anything the jury specifically flagged
(rover element detail, the drone itself).

**Sections 3 (Final Design Description) and 4 (Safety Systems) have no
internal structure yet, on purpose.**
Every other section's tree was derivable from the Preliminary Report's
structure or the template. These two need a team decision (page-budget
trade-offs, whether to fold in a new safety subsystem, how granular the
design tree should be) before scaffolding — see `STATUS.md` for what
that decision needs to produce.

**Test Plan and Lessons Learnt are single owner-edited tables, not
per-team files.**
The repo initially used the Preliminary's per-team macro pattern (each team
editing `teams/<team>/tests.tex` defining a `\<team>testrows` macro,
assembled into one longtable). This was reversed: both tables
(`tables/test_plan.tex`, `tables/lessons_learnt.tex`) are now edited
directly by one owner (the test-plan owner; the lessons curator) who
inserts rows all at once from material teams hand over. Reason: for these
two sections specifically, the owner wants to see and shape the whole
picture at once rather than reviewing scattered per-team PRs.

**No CODEOWNERS.**
Considered for automatic review-request routing per folder, rejected —
the team didn't want it.

**Everything in English.**
Report content and repository docs (README, CONTRIBUTING) are English.
(`ai_context/creation_context/` historical chat logs are the exception,
since they're a verbatim archive.)

## Repository structure

**Ordering lives only in assembler files; content files are unnumbered.**
The Preliminary Report repo encoded section numbers into folder/file names
(e.g. `2_3_5_link_performance_analysis.tex`). When two subsections were
pruned, the team just commented them out rather than renumbering everything
— leaving permanent gaps. This repo's content files get stable, descriptive
names; only the ordering inside assembler files encodes sequence. Exception:
the eight top-level `sections/*.tex` files keep two-digit prefixes, because
those seven sections are fixed by the template and will not reorder.

**One table = one file = one label.**
The Preliminary Report had the same table (test plan, MoC summary, RIO
register) defined in two places with diverging columns — a maintenance trap.
Every large table now lives in exactly one file under `tables/`, included
exactly once.

**Diagrams are drawn outside LaTeX and imported as exported PDFs.**
Team decision — no inline TikZ, no TikZ requirement at all for this report.
Source tool is whatever the author prefers (draw.io / EasyEDA / CAD /
Figma); keep the editable source next to the exported PDF in the relevant
`figures/` folder.

## Workflow

**Branch from `develop`, merge into `develop`.**
`develop` is the working trunk. `main` only moves via a deliberate release
step by the maintainer: tag `main`'s current tip (preserving the outgoing
revision) → merge `develop` into `main` → bump `\revisionnum` in
`metadata.tex`. No `rel/*` branches — tags are sufficient because a released
revision is never patched after the fact.

**1 content file = 1 PR.**
Carried over from the Preliminary Report, where it minimized merge
conflicts and sped up review. Assembler files, `preamble.tex`, and the
table masters change only via `infra/*` PRs.

**Every PR needs a screenshot of the compiled section pasted into the PR
body**, in addition to CI's full-PDF artifact. The maintainer reviews from
the PR itself; downloading and opening the PDF for every review is friction
that a pasted image removes.

**CI runs on every branch, not just `main`/`develop`.**
So status is visible before a PR even exists. Blocking a merge on green CI
additionally requires a GitHub branch-protection rule on `develop`
("require status checks to pass") — the workflow file alone cannot enforce
that.

**Page-count hard-fail and the placeholder-lint `\todo` check are both
deferred to freeze week**, not enabled from day one. Rationale: during
active writing, §3/§4 are still stubs and page counts will swing wildly
before they mean anything; blocking WIP PRs on a not-yet-meaningful limit
would just be noise. Both are pre-wired in `.github/workflows/build.yml`,
commented out, ready to flip.

## Jury feedback → binding requirements

The Preliminary Report scored 126.75/150. Every piece of jury feedback was
converted into a specific, located action item — see
`creation_context/PROPOSAL.md` → "Jury feedback → binding action items" for
the full table (feedback text ↔ required change ↔ which file it lands in).
Highlights: the E-stop button circuit schematic was missing and must appear
in Safety Systems; L/S scale tables are required in the RIO methodology
(the Preliminary only had prose); risks like R-01 were too generic and must
name the specific subsystem; the drone was never actually shown despite an
extensive description.
