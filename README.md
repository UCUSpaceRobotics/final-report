# ERC 2026 Final Report — UCU Space Robotics

LaTeX source of the **Final Report** for the European Rover Challenge 2026
(rover *Indomitus* + drone). Continuation of the Preliminary Report
(126.75/150); jury feedback and all structural decisions are recorded in
[`ai_context/`](ai_context/).

**Read [CONTRIBUTING.md](CONTRIBUTING.md) before writing anything.**

**Branching model** (details in CONTRIBUTING.md): `develop` is the working
trunk — branch from it, PR into it. `main` is always a clean released state,
tagged at each release (`v1.0-final-draft`, …) before `develop` merges in.
No `rel/*` branches — tags preserve old revisions.

## Deliverable requirements

| Parameter | Value |
|---|---|
| Sections (fixed order) | 1 MoC Update · 2 Test Plan · 3 Final Design Description · 4 Safety Systems · 5 RIO Analysis · 6 Lessons Learnt · 7 Science: Regional Geology |
| Scoring | MoC 10 · Test 20 · FDD 40 · Safety 10 · RIO 20 · LL 20 · Science 10 (+ RF Form 20, separate document) = 150 pts |
| Format | A4, searchable PDF, English |
| Length | max **35 pages**, excluding cover and ToC (RF Form is **not** part of this document) |
| Fonts / margins | ≥ 10 pt (8 pt allowed in RIO tables only); margins ≥ 2.54 cm |
| MoC | second iteration, `.xlsx` **embedded** in the PDF |
| Penalties | wrong report/MoC naming −10 each · wrong font −10 · wrong margins −5 · extra pages −X · review-mode artifacts −5 |

## Quick start

```bash
# toolchain (once):
sudo apt install texlive-full latexmk

# compile PDF and clean auxiliary files:
latexmk -pdf main.tex && latexmk -c
```

CI compiles every PR and attaches the PDF as an artifact, lints for
placeholders, and checks the page count — see
[.github/workflows/build.yml](.github/workflows/build.yml).

## Repository structure

```
main.tex                 # entry point - assembles sections, no content
preamble.tex             # packages, styles, colors, helper commands
metadata.tex             # team name, project name, revision, date
sections/                # one file per report section (00_cover ... 07_science_geology)
                         #   03 and 04 are stubs - structure pending team session
tables/                  # single source of truth for every large table
teams/<team>/figures/    # team-owned figure assets (photos, exported PDFs)
figures/                 # shared assets only (logos, system-level diagrams)
appendix/                # MoC .xlsx (embedded into the PDF at release)
ai_context/              # design record: proposal, implementation plan, feedback
Schematics.md # shared diagram and schematic rules for all subteams
```

Teams: `arm`, `drone`, `electronics`, `ground_station`, `navigation`,
`science`, `suspension`.

## Standards (short version — details in CONTRIBUTING.md)

- **Units**: every physical quantity via `siunitx` — `\qty{45}{\kilo\gram}`,
  `\qtyrange{-40}{85}{\degreeCelsius}`, `\ang{360}`,
  `\qtyproduct{1.2 x 0.8 x 0.5}{\meter}`, `\num{10000}`. Never write units by
  hand (`10kg`, `1920x1080` are errors). New units → `\DeclareSIUnit` in
  `preamble.tex` only (existing: `\fps`, `\mAh`, `\pixel`).
- **Labels**: `sec:` / `subsec:` / `subsubsec:` / `par:` / `tab:` / `fig:`;
  reference everything with `\autoref{...}` — `\ref` is forbidden, since
  `\autoref` inserts the name ("Figure", "Table", "§") automatically. Every
  figure/table must be referenced from the surrounding prose — no orphan,
  unmentioned figures.
- **Diagrams are drawn outside LaTeX** (draw.io / EasyEDA / CAD / Figma) and
  exported as **PDF**: team assets → `teams/<team>/figures/`, shared →
  `figures/`. No inline TikZ.
- **Evidence first** (§3 rule): every design leaf leads with a photo of built
  hardware, a dimensioned drawing/cross-section, a schematic, or a
  calculation table. Renders only where hardware does not exist yet.
- **One table = one file = one label**, in `tables/`, included exactly once.

## Page budget (soft, CI warns at 35)

MoC 1 · Test Plan 6.5 · FDD 15 · Safety 3.5 · RIO 3.5 · LL 3 · Science 2 ·
reserve 0.5 — **35 total**.

## Before submission (freeze week)

- [ ] All `\todo` gone, `todonotes` removed from `preamble.tex`
- [ ] CI page count and placeholder lint switched to hard fail
- [ ] `moc.xlsx` embedded into the PDF (e.g. Foxit PDF Editor); attachment opens
- [ ] File named exactly per the Rules: `UCU_Space_Robotics_FinalReport_ERC2026.pdf`
      (wrong naming −10 pts and the deliverable may not be found at all)
- [ ] Margins/fonts verified (≥ 10 pt body, 8 pt only in RIO tables)
- [ ] Final RF Form submitted **separately** and matching the real RF state
      (RF judges compare it at the RF check — differences = penalties)
