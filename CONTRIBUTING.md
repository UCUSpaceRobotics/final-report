# CONTRIBUTING

How we work on the Final Report without LaTeX merge conflicts. Based on what
worked for the Preliminary Report — see [`ai_context/PROPOSAL.md`](ai_context/PROPOSAL.md)
for the reasoning behind every rule.

## The golden rule

**1 content file = 1 PR.**

One PR changes one file in `sections/` or `tables/` (plus its own figures).
Assembler files (`main.tex`, section files that only `\input` others) and
`preamble.tex` change only via `infra/` PRs by the maintainer. The test-plan
and lessons tables are each owned by one person and filled all at once —
teams hand in their material instead of editing those files (see below).

## Branching model

Two long-lived branches:

- **`develop`** — the working trunk. All content branches are cut from here,
  and all content PRs merge back into here.
- **`main`** — always a clean, released state. Only ever updated by the
  maintainer merging `develop` in, as a deliberate release step (see below).
  Never commit to it directly, never branch from it.

**Cut your branch from `develop`, and merge your PR into `develop`.**

### Releases (maintainer only)

1. Tag the current tip of `main` with the outgoing revision
   (e.g. `v1.0-final-draft`) — this preserves exactly what was released
   before it gets superseded.
2. Merge `develop` → `main`.
3. Bump `\revisionnum` in `metadata.tex`, commit on `main`.

Old revisions are recovered via `git checkout <tag>` — no `rel/*` branches
needed, tags are enough since revisions are never patched after the fact.

## Branch naming

`<type>/<scope>-<short-slug>` — lowercase, hyphens:

| Type | Used for | Example |
|---|---|---|
| `des/` | design content (§3, after the tree is defined) | `des/rover-chassis` |
| `safety/` | safety systems content (§4) | `safety/estop` |
| `test/` | test-plan table updates (table owner) | `test/june-results` |
| `moc/` `rio/` `ll/` `sci/` | the other sections | `ll/curated-batch`, `rio/trend-chart` |
| `infra/` | preamble, CI, docs, table masters | `infra/design-tree` |
| `fix/` | typos, small corrections | `fix/units-in-power-budget` |

## PR flow

1. Branch from `develop` → open a **Draft PR against `develop`** immediately
   (work-in-progress stays visible).
2. Title: `<TYPE> <scope>: short title`, e.g. `TEST suspension: wheel load results`.
3. Fill the PR template: what the PR adds, cross-references, what remains.
4. Mark **Ready for review** when done — the maintainer merges into `develop`.
5. CI attaches the compiled PDF to every PR — check your pages there;
   no screenshots needed.

## Where to write what

| I want to… | Edit |
|---|---|
| Report **test results** | hand the measured values to the test-plan owner — rows live in `tables/test_plan.tex` and are inserted all at once |
| Propose a **lesson learnt** | send the candidate to the curator (Mykola) — rows live in `tables/lessons_learnt.tex` |
| Write **design content** (§3) / **safety content** (§4) | wait for the design tree (`infra/design-tree` PR after the team session) — do **not** create structure there yourself |
| Add **RIO** entries | talk to the PM — the register is centrally owned, IDs must match the Preliminary |
| Add a **figure** | `teams/<team>/figures/` (team asset) or `figures/` (shared) |
| Change packages, styles, units | `infra/` PR to `preamble.tex` — ask first |

### Test rows (table owner; 7 cells per row)

```latex
ID & Name & Description & Req. & Pass/Fail criteria & Results & Status \\
```

- Keep the Preliminary test IDs (`SUS-01` … `DRO-07`).
- **Results** = the measured value against the criterion (e.g. "0.62 m
  turning radius measured" vs "≤ 0.7 m"), not "ok". Teams: report exactly
  this to the owner.
- **Status** = `Passed` / `Failed` / `Planned` — honest, per the jury's ask.
- A failed test is *good content*: state the design modification that followed.

### Lessons Learnt rows (curator; 6 cells per row)

```latex
ID & Title & Root cause & Description & Recommendation & Impact \\
```

ID scheme: `LL-<TEAM>-NN` (e.g. `LL-SUS-01`) so provenance stays visible.
Send candidates freely — the best are curated to fit ~3 pages.

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
| Editing the test/lessons tables when you are not their owner | Hand your results/candidates to the owner/curator |
| Creating subsections under §3/§4 before the team session | Wait for the `infra/design-tree` PR |
| `10kg`, `1920x1080` in text | `\qty{10}{\kilo\gram}`, `\numproduct{1920 x 1080}` |
| Inline TikZ in a section file | Draw outside LaTeX, export PDF, `\includegraphics` |
| "Results: ok" | Measured value vs the pass criterion |
| Duplicating a table in a second file | One table = one file in `tables/` |

## Questions

Team chat, or open an issue in this repository.
