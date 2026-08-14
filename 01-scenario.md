# The Scenario

I made up a clinic so I'd have something concrete to assess. Everything below is
invented. I tried to make it realistic rather than convenient — a practice that's
neglectful in the ordinary way small businesses are, not one that's deliberately
reckless.

---

## The clinic

**Northwind Family Health, LLC** — primary care and pediatrics, three locations in the
Columbus, Ohio area (Dublin, Westerville, Grove City).

| | |
|---|---|
| HIPAA status | Covered entity — a provider transmitting standard transactions electronically (45 CFR § 160.103) |
| Workforce | 85 people: 12 physicians, 6 NPs, 31 clinical, 24 administrative, 8 management, 4 IT/facilities |
| Patient records | ~42,000 active, ~118,000 including inactive |
| Revenue | ~$21M |
| Security staff | None. IT is two people. The Practice Administrator is the Security Official as a side duty |

That last row drives most of the findings. Northwind isn't malicious — it's a small
business where security is nobody's actual job. The Security Rule allows controls scaled
to size and cost (§ 164.306(b)(2)), but it doesn't excuse a control being absent. The
difference between "we chose something smaller" and "nobody ever thought about it" is
what the assessment is trying to document.

## Systems

| ID | System | ePHI? | Criticality |
|---|---|---|---|
| SYS-01 | MedStream EHR (cloud, business associate) | Yes — primary | Critical |
| SYS-02 | ClearPath RCM, billing/claims (cloud, BA) | Yes | High |
| SYS-03 | Microsoft 365 — Exchange, SharePoint, Teams (BA) | Yes, incidental | High |
| SYS-04 | FS-01 file server, on-prem Windows Server 2019 | Yes | High |
| SYS-05 | Buckeye Imaging results feed, inbound SFTP (BA) | Yes | Moderate |
| SYS-06 | AfterHours answering service portal (BA) | Yes | Moderate |
| SYS-07 | FaxLogic digital fax appliance | Yes | Moderate |
| SYS-08 | Backups — Veeam → NAS → Wasabi | Yes, copies of everything | Critical |
| SYS-09 | Active Directory / DNS / DHCP | Identity only | Critical |
| SYS-10 | Workstations (62) | Yes, cached | High |
| SYS-11 | Laptops (14) | Yes, cached | High |
| SYS-12 | Clinical tablets (9) | Yes | Moderate |
| SYS-13 | Network — FortiGate ×3, Meraki APs ×11 | Transit only | Critical |
| SYS-14 | Check-in kiosks (6) | Yes, session | Moderate |

**12 of 14 systems touch ePHI.**

Two of these — the answering service portal and the fax appliance — I wrote into the
scenario as systems management doesn't know about, because shadow IT is realistic and
because building the inventory is supposed to surface things. The fax appliance turns
out to be one of the worse findings: ~61,000 unencrypted images going back to 2021 with
no retention limit and a default admin password.

## Business associates

| BA | Service | Agreement | Problem |
|---|---|---|---|
| MedStream | EHR | Yes, 2021 | No breach notification deadline in the contract |
| ClearPath | Billing / clearinghouse | Expired, 2016 | Predates the 2013 Omnibus Rule — no subcontractor flow-down, no incident reporting |
| Microsoft | Email / productivity | Standing DPA | Fine |
| AfterHours | After-hours triage | **None, ever** | Has handled patient symptoms and callback numbers since 2019 |
| Buckeye Imaging | Radiology | Yes, 2022 | Fine, though SFTP keys never rotated |

Three of five deficient. I chose this because an absent BAA is a violation on its own —
independent of whether any ePHI is ever mishandled — and OCR has issued penalties on
that basis alone.

## Where ePHI flows

```
Patient ──► Check-in kiosk ──TLS──► MedStream EHR (cloud) ──► ClearPath ──► Payers
                                         ▲     ▲
Remote provider ──password only──────────┘     │ SFTP
   ⚠ no MFA                                    │
                                        Buckeye Imaging

Scanned intake ──SMB──► FS-01 ──Veeam──► NAS ──► Wasabi
                          ⚠ unpatched      ⚠ same network as production, restore never tested

Inbound fax ──► FaxLogic ──► ~61,000 unencrypted images on local disk, no retention limit

After-hours call ──► AfterHours portal ──plaintext email──► on-call provider
                       ⚠ no BAA                              ⚠ no email encryption
```

## Facilities

| Site | Staff | Physical issues I wrote in |
|---|---|---|
| Dublin (HQ) | 41 | IT closet propped open for ventilation during the day; no camera; keypad code unchanged since 2019 |
| Westerville | 26 | Network cabinet locked, key in an unlocked front-desk drawer |
| Grove City | 18 | Key custody is actually fine here — I wanted at least one site to pass |

No visitor logs anywhere. Reception screens at two sites face the waiting area with no
privacy filters.

---

## How I assessed it

### Control set
All 65 standards and implementation specifications in 45 CFR §§ 164.308, 164.310,
164.312, 164.314, and 164.316. I pulled the text from eCFR rather than a summary, and
used NIST SP 800-66 Rev. 2 for what each control actually means in practice.

### Status ratings

| Rating | Meaning |
|---|---|
| Implemented | Control is in place and would hold up to evidence |
| Partially Implemented | Control exists but has scope, consistency, or documentation problems |
| Not Implemented | Control absent — or an addressable spec with no documented decision either way |
| Alternative Measure | Addressable spec not done as written, documented equivalent in place |
| Not Applicable | Documented reason it doesn't apply (clearinghouse and group health plan provisions) |

### The evidence column

Each control lists **what evidence you'd need** to verify it — a document to inspect, a
configuration to check, a report to sample, a control to test. I wrote this column
because working out *how you'd prove a control works* turned out to be the part of the
exercise I understood least at the start.

The rule I gave myself: an interview alone is never enough to rate something Implemented.
If the only support for a control is somebody saying it happens, that's Partially
Implemented with "not documented" as the defect. In an OCR investigation the entity has
to demonstrate compliance, so an undocumented control and an absent one are in the same
position.

### Required vs. Addressable

22 standards and 32 implementation specifications, each marked Required (R) or
Addressable (A). Addressable is the part I got wrong initially. Under § 164.306(d)(3) you
must do one of three things for each addressable spec:

1. Implement it, or
2. Implement a documented equivalent, or
3. Document why it isn't reasonable and appropriate for you

Ten addressable specs in this scenario fall into a fourth category that doesn't legally
exist — no control and no written decision. I rated those Not Implemented, and the gap
text names the missing *determination*, not just the missing control. Several of them
would probably be fine as documented decisions. None is fine as a silence.

### Risk scoring

`Risk = Likelihood (1–5) × Impact (1–5)`, per NIST SP 800-30 Rev. 1.

**Likelihood**

| | |
|---|---|
| 5 | Happening now, or expected within 12 months |
| 4 | Reasonably expected within 1–2 years |
| 3 | Plausible within 2–3 years |
| 2 | Would take unusual circumstances |
| 1 | Theoretical |

**Impact** — highest of three axes wins:

| | Patient safety | Regulatory | Operations |
|---|---|---|---|
| 5 | Care unsafe | Breach >500 people | All sites down >72h |
| 4 | Care delayed | Reportable breach | One site down >72h |
| 3 | Isolated disruption | Reportable to HHS annually (<500) | Degraded 1–3 days |
| 2 | No safety effect | Internal finding | Localized, <1 day |
| 1 | None | None | Absorbed normally |

**Tiers:** 20–25 Critical (30 days) · 12–16 High (90 days) · 6–10 Moderate (180 days or
formally accept) · 1–5 Low (monitor).

I picked threat sources from NIST SP 800-30r1 Appendix D, then narrowed them using the
HHS OCR breach portal — so the 15 risks are things that actually cause reported breaches
at small practices, not a generic threat list.

### What I deliberately left out

- **Privacy Rule (Subpart E)** — different control set, would have doubled the work
- **Penetration testing** — I can't test a clinic that doesn't exist; it shows up as a
  recommendation instead
- **PCI DSS** for card payments at the front desk — noted as an unassessed exposure
- **Ohio state law** — flagged where it exceeds HIPAA, not assessed

I listed these because an assessment that doesn't say what it didn't cover isn't much
of an assessment.
