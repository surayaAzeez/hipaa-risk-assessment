# HIPAA Security Rule Gap Analysis — Practice Project

A self-directed project where I worked through a complete HIPAA Security Rule gap
analysis and risk assessment for a fictional medical practice I made up for the purpose.

**This was a learning exercise, not a real engagement.** Northwind Family Health doesn't
exist. I invented the clinic and its problems so I'd have something concrete to assess.
Everything else is real: the control set is all 65 standards and implementation
specifications in 45 CFR Part 164 Subpart C, pulled from eCFR; the risk method is NIST
SP 800-30 Rev. 1; the implementation guidance is NIST SP 800-66 Rev. 2.

## Why I picked HIPAA

Most beginner GRC portfolios are a NIST CSF spreadsheet. HIPAA is harder in ways I
wanted to learn:

- **It's law, not guidance.** Every control has an enforceable citation, and I had to
  read the actual regulation rather than a framework summary.
- **Required vs. Addressable.** "Addressable" doesn't mean optional, which I didn't know
  when I started. Under § 164.306(d)(3) you have to either implement the spec, implement
  a documented equivalent, or write down why it isn't reasonable for you. Doing none of
  the three is a violation. Ten of my findings are exactly that — a spec with no control
  *and* no documented decision.
- **There's a live rule change to reason about.** HHS proposed a major Security Rule
  overhaul in January 2025. It's still not final (HHS now estimates July 2027), so I had
  to assess against the current rule while noting where the proposal would move things.

## What's here

| File | What it is |
|---|---|
| `01-scenario.md` | The clinic I invented, its systems, where ePHI lives, and how I scored risk |
| `02-hipaa-gap-analysis.xlsx` | The main artifact — 4 tabs, see below |
| `03-policies/` | Three policies I drafted to close specific gaps |
| [`04-summary-report.pdf`](04-summary-report.pdf) | Write-up of what I found — **readable in the browser** |
| `04-summary-report.docx` | Same report, editable |

### The spreadsheet

| Tab | Rows | What it does |
|---|---|---|
| Asset Inventory | 14 | Where ePHI lives, criticality, owner |
| Control Gap Assessment | 65 | Every § 164.308 / .310 / .312 / .314 / .316 standard and spec |
| Risk Register | 15 | Likelihood × Impact scoring, treatment, residual risk |
| POA&M | 20 | Remediation items with owner, cost, target date |

Scoring cells are formulas, not typed numbers — change a likelihood rating and the
score, tier, colour, and the summary counts on the first tab all update.

**Control Gap Assessment** — first 12 of 65 rows:

![Control gap assessment](images/gap-analysis-preview.png)

Each row carries the CFR citation, whether the spec is Required or Addressable, a status,
the evidence you'd need to verify it, and the gap in this scenario.

**Risk Register** — first 9 of 15 risks:

![Risk register](images/risk-register-preview.png)

Likelihood and Impact are the only inputs (shaded). Score, tier, residual score, and
residual tier are formulas.

## What I found in the scenario

| | |
|---|---|
| Standards and specs assessed | 65 |
| Implemented | 3 |
| Partially implemented | 24 |
| Not implemented | 32 |
| Alternative measure / Not applicable | 1 / 5 |
| Risks | 3 Critical, 9 High, 3 Moderate |

The pattern that came out of it was more interesting than the individual gaps. The only
three controls that fully pass are ones where a vendor supplies the safeguard
automatically — the EHR's audit trail, TLS, cloud backup integrity checks. Every control
that needs the clinic itself to *do something on a schedule* — review logs, test a
restore, train staff, revoke a leaver's account — is missing. That's what a practice with
no dedicated security person looks like, and it's the thing the summary report leads with.

## What I learned

- Reading the regulation directly is very different from reading a framework crosswalk.
  Half of what I thought I knew about HIPAA came from vendor blog posts and was wrong or
  out of date.
- The distinction between a control existing and a control being *evidenced* is most of
  the job. In an OCR investigation the entity has to demonstrate compliance, so an
  undocumented control and an absent one look the same. I rated a lot of things
  "Partially Implemented" for that reason alone.
- Risk scoring is easy to do and hard to do honestly. My first pass had everything as
  High. Forcing myself to define what Likelihood 3 vs. 4 actually means, and to accept
  that one risk stays High even after remediation, made the register a lot more useful.
- Business associate agreements are the cheapest thing to get right and, going by OCR
  enforcement, one of the most commonly missed.

## How to do this yourself

Everything I used is free:

1. **eCFR** (ecfr.gov) — the actual text of §§ 164.308–164.316
2. **HHS SRA Tool** (healthit.gov) — free assessment tool, currently v3.6
3. **NIST SP 800-66 Rev. 2** — HIPAA implementation guidance, including a crosswalk to
   NIST SP 800-53
4. **NIST SP 800-30 Rev. 1** — Appendix I for likelihood, Appendix H for impact
5. **HHS OCR breach portal** — real breaches at real practices, useful for picking
   realistic threat scenarios instead of inventing them

Invent a scenario specific enough to force decisions. Vague scenarios produce vague
findings.
