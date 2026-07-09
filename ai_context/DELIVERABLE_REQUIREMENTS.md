# Deliverable Requirements — ERC 2026 Final Report

Distilled from the official template
(`creation_context/[TEMPLATE]_02_TEAMNAME_FINAL_REPORT_Rev.1.docx.md`).
Where the template contradicts itself (it has copy-paste debt from the
Preliminary Report template — see "Known template issues" below), the
resolution the team agreed on is marked **RESOLVED**.

## Format

| Parameter | Value |
|---|---|
| Page | A4, searchable PDF |
| Length | max **35 pages**, excluding cover page, list of contents/figures/tables, and Appendix 3 (Requirements) |
| Language | English |
| Font | minimum 10 pt; **8 pt allowed in RIO tables only** |
| Margins | ≥ 2.54 cm (1 inch) on all edges |
| Appendices | required: compliance matrix (MoC) to requirements |

## Scoring — 150 points total

### 1. Matrix of Compliance Update — 0–10 pts
- MoC delivered (0–3): `.xlsx` **embedded** in the PDF = 3 pts; separate
  `.xlsx` file = 1 pt; anything else = 0 pts.
- Update to MoC (0–7): compliance status assessment (0–3) + assessment of
  comments related to compliance status (0–4).
- **Compliance status reflects the final foreseen design state**, not the
  current one — e.g. rover is 80 kg now but 75 kg is the plan → status is
  Compliant, not Partially/Non-Compliant.

### 2. Test Plan — 0–20 pts
- Structure (0–5): all requirements verified by test are mentioned (0–1) ·
  Test ID/Name/Description (0–1) · test setup described (0–1) · pass/fail
  criteria + test status provided (0–1) · tests timeline provided (0–1).
- Technical excellence (0–15): assessment of the test plan focused on
  **results of already-conducted tests**, impact on requirements'
  compliance, and design modifications made as a consequence.
- Template's suggested columns: Test No. · Test Name · Description (incl.
  Approach) · Requirements Tested · Pass/Fail Criteria · Results of the
  Tests · Test Status (Passed/Failed).

### 3. Final Design Description — 0–40 pts
- Rover structure (0–6): PT, WBS, OBS — both rover and drone (0–2) · rover
  design description (0–1) · rover technical budget: mass, power, data
  link (0–1) · critical parts for on-site ERC tasks (0–1) · innovative
  design solutions highlighted (0–1).
- Rover design description excellence (0–20).
- Drone structure (0–4): design description (0–1) · technical budget: mass,
  power, data link (0–1) · critical parts (0–1) · innovations (0–1).
- Drone design description excellence (0–10; **0 pts if the drone is fully
  COTS**).
- Template's own advice: "provide as much as possible schematics, figures,
  photos and limit the text to the necessary minimum. In general it applies
  to the whole document."

### 4. Safety Systems — 0–10 pts
1. Describe the safety system: architecture, time sequence, diagrams, etc.
2. Prove the solution is robust: reliability analysis in a concise
   engineering way.
3. Describe emergency behaviour — triggered by the system itself, the
   operator, or an external actor hitting the emergency button. Ideally,
   test results with figures/photos.

### 5. RIO Analysis (second iteration) — 0–20 pts
- Quality of updates to the Preliminary's qualitative assessment (0–15):
  risks, descriptions, mitigation actions, status; opportunities and issues
  mentioned. **Score is low if the majority of risks are unchanged** — that
  reads as "risk assessment not performed."
- Trend chart (0–5): risk index changes across phases, style per
  ECSS-M-ST-80C Fig. 5-7. Phases for this report: Preliminary Report → Final
  Report (some ERC materials also mention a Proposal phase before that).
- L/S scale: Likelihood 1 (Rare) – 5 (Almost Certain); Severity 1
  (Negligible) – 5 (Catastrophic); Risk Index = L × S.
- Response strategies — risks/issues: Avoid, Mitigate, Accept, Transfer,
  Escalate. Opportunities: Exploit, Share, Enhance, Accept, Escalate.
- Impact types: Time, Cost, Scope, Quality, Resources, Economic, Managerial,
  Technical, Generic.
- Grading emphasizes: risks named specifically (not generic) · L/S assessed
  and justified · RI calculated per entry · opportunities/issues present,
  not just risks · valid owners named · a suitable response strategy per
  entry · quality of mitigation actions.

### 6. Lessons Learnt — 0–20 pts
- Structure (0–5): ID & title (0–1) · root cause (0–1) · description (0–1)
  · recommendations for the future (0–1) · assessment of the impact (0–1).
- Quality of the assessment (0–15).
- Reference example: NASA LLIS, https://llis.nasa.gov/lesson/10801

### 7. Science: Regional Geology Analysis — 0–10 pts
Select and justify a landing site in a pre-defined Mars region. Constraints:
geologically interesting within a rover traverse of up to 30 km; landable
with current techniques (atmospheric thickness, landing area); safe for the
rover (local slopes < 20°, few large boulders, survivable winter thermal
conditions). Two A4 pages total:
1. **Composite map** (one A4): location map (global scale) + regional
   geological map (Astrogeology Science Centre publications) + close-up map
   (CTX or HiRISE) marked with the landing ellipse, planned rover path, and
   three regions of interest.
2. **Report**, up to 800 words: technical justification (why safe to land)
   + scientific justification (why worth landing, w.r.t. the 3 ROIs).
   Tools: Google Earth Pro (Mars) or JMars.

### Final RF Form — 0–20 pts, separate document
Delivered separately, via the link defined in the Rules, as the final
version of the Preliminary RF Form. **RF judges cross-check it against the
actual RF state at the ERC finals** — mismatches are penalized.

## Penalties (deducted from the score received)

| Violation | Penalty |
|---|---|
| Wrong font size | −10 pts |
| Wrong margins | −5 pts |
| Wrong number of pages | −X pts, where X = s·n/(n+35); s = score without penalty (max 35), n = pages over the limit |
| Glaring formatting issues (e.g. still in "reviewing mode") | −5 pts |
| Wrong naming of the report file | −10 pts |
| Wrong naming of the MoC | −10 pts |

Wrong naming — especially without the team name — risks the deliverable not
being found at all, i.e. **0 pts**, not just the penalty.

## Known template issues, and how we resolved them (RESOLVED)

The template document itself has unresolved copy-paste debt from the
Preliminary Report template. Treat the *Rules* as authoritative over the
template's prose when they conflict.

- **RF Form page counting** — the document-requirements block says the RF
  Form *is* included in the 35-page limit; the RF Form section itself says
  it is *not* included. **RESOLVED: the RF Form is a separate document,
  outside the 35 pages.** The report's page budget uses the full 35 pages.
- Template header says "European Rover Challenge 2025" and title
  "Proposal" — leftover text from a prior template, ignored.
- Template's table of contents lists "Lessons Learnt" twice; the second
  instance is actually the Science: Regional Geology Analysis section.
- **PT / WBS / OBS** (undefined by the template) — **RESOLVED**: Product
  Tree, Work Breakdown Structure, Organisation Breakdown Structure. Product
  Trees for rover and drone already exist from the Preliminary Report
  (its Figures 15–16) and only need updating; WBS (work packages) and OBS
  (team organisation chart) are new diagrams for the Final Report.
