# CONTRIBUTING

How we work on the Final Report without LaTeX merge conflicts. Based on what
worked for the Preliminary Report — see [`ai_context/PROPOSAL.md`](ai_context/PROPOSAL.md)
for the reasoning behind every rule.

## The golden rule

**1 content file = 1 PR.**

One PR changes one file in `sections/`, `tables/`, or `teams/<team>/`
(plus its own figures). Assembler files (`main.tex`, section files that only
`\input` others), `preamble.tex`, and table masters change only via `infra/`
PRs by the maintainer.

## Branch naming

`<type>/<scope>-<short-slug>` — lowercase, hyphens:

| Type | Used for | Example |
|---|---|---|
| `des/` | design content (§3, after the tree is defined) | `des/rover-chassis` |
| `safety/` | safety systems content (§4) | `safety/estop` |
| `test/` | your team's test rows | `test/suspension` |
| `moc/` `rio/` `ll/` `sci/` | the other sections | `ll/electronics`, `rio/trend-chart` |
| `infra/` | preamble, CI, docs, table masters | `infra/design-tree` |
| `fix/` | typos, small corrections | `fix/units-in-power-budget` |

## PR flow

1. Branch → open a **Draft PR** immediately (work-in-progress stays visible).
2. Title: `<TYPE> <scope>: short title`, e.g. `TEST suspension: wheel load results`.
3. Fill the PR template: what the PR adds, cross-references, what remains.
4. Mark **Ready for review** when done — the maintainer (Dmytro) merges.
5. CI attaches the compiled PDF to every PR — check your pages there;
   no screenshots needed.

## Where to write what

| I want to… | Edit |
|---|---|
| Add/update my team's **test rows + results** | `teams/<team>/tests.tex` (only the `\<team>testrows` macro) |
| Add my team's **lessons learnt** | `teams/<team>/lessons.tex` (only the `\<team>llrows` macro) |
| Write **design content** (§3) / **safety content** (§4) | wait for the design tree (`infra/design-tree` PR after the team session) — do **not** create structure there yourself |
| Add **RIO** entries | talk to the PM — the register is centrally owned, IDs must match the Preliminary |
| Add a **figure** | `teams/<team>/figures/` (team asset) or `figures/` (shared) |
| Change packages, styles, units | `infra/` PR to `preamble.tex` — ask first |

### Test rows (7 cells per row)

```latex
ID & Name & Description & Req. & Pass/Fail criteria & Results & Status \\
```

- Keep the Preliminary test IDs (`SUS-01` … `DRO-07`).
- **Results** = the measured value against the criterion (e.g. "0.62 m
  turning radius measured" vs "≤ 0.7 m"), not "ok".
- **Status** = `Passed` / `Failed` / `Planned` — honest, per the jury's ask.
- A failed test is *good content*: state the design modification that followed.

### Lessons Learnt rows (6 cells per row)

```latex
ID & Title & Root cause & Description & Recommendation & Impact \\
```

ID scheme: `LL-<TEAM>-NN` (e.g. `LL-SUS-01`). Submit candidates freely —
the best are curated to fit ~3 pages.

## Tiny contract

Every content file starts with a comment block:

```latex
% Teams: <who writes here>
% Status: stub | draft | ready
```

Update it as you work; never delete it. (The old `Requirements` field is
gone — we do not reference requirements inside the report. The single
exception is the test table's *Req.* column, which the rubric scores.)

## Content standards

- **Evidence first (§3/§4):** lead with a photo of built hardware, a
  dimensioned drawing, a cross-section, a schematic, or a calculation table.
  Renders only where hardware does not exist yet. Text says only what the
  figure cannot.
- **Units:** `siunitx` everywhere — see README. Hand-written units fail review.
- **Labels:** `\label{fig:...}` / `\label{tab:...}` on everything you add;
  reference with `\autoref` (sections) or `\ref` (tables/figures).
- **Diagrams:** drawn outside LaTeX, exported as PDF. Keep the editable
  source (e.g. `.drawio`) next to the export in the same figures folder.
- **Figures:** `\includegraphics[width=...]{teams/arm/figures/gripper_v2}` —
  no file extension needed.

## Merge checklist (CI enforces the mechanical parts)

- [ ] Compiles: `latexmk -pdf main.tex` — **CI**
- [ ] No placeholders `[X]`, `[Add content …]`, `\lipsum` — **CI**
- [ ] Page count within budget — **CI warning** (hard fail at freeze)
- [ ] Tiny contract updated — reviewer
- [ ] Units via siunitx, labels present — reviewer

## Common mistakes

| Mistake | Do instead |
|---|---|
| One PR touches 3–4 files | Split: 1 content file = 1 PR |
| Rows added directly to `tables/test_plan.tex` | Edit your `teams/<team>/tests.tex` macro |
| Creating subsections under §3/§4 before the team session | Wait for the `infra/design-tree` PR |
| `10kg`, `1920x1080` in text | `\qty{10}{\kilo\gram}`, `\numproduct{1920 x 1080}` |
| Inline TikZ in a section file | Draw outside LaTeX, export PDF, `\includegraphics` |
| "Results: ok" | Measured value vs the pass criterion |
| Duplicating a table in a second file | One table = one file in `tables/` |

## Questions

Team chat, or open an issue in this repository.
