# POL-003 · Security Incident Response Plan

> Part of a self-directed HIPAA practice project. Northwind Family Health is a fictional clinic; this policy was drafted to close specific gaps found in that scenario. The CFR citations are real.

| | |
|---|---|
| **Owner** | Security Official (Practice Administrator) |
| **Version** | 1.0 |
| **Effective** | 1 June 2026 |
| **Review / test cycle** | Reviewed annually; tabletop exercise annually |
| **Closes findings** | A-20, A-21, D-04 |
| **Addresses risks** | R-13 (High), and the response capability for R-01, R-05, R-08 |

---

## 1. Purpose and the problem this solves

45 CFR § 164.308(a)(6) requires procedures to identify and respond to security
incidents, mitigate their harmful effects, and document them and their outcomes.

Before this plan, Northwind had none of that. The 2026 risk analysis surfaced two
incidents in interviews — a lost phone with mailbox access in 2024, and a suspected
phishing click in 2025 — that were never recorded, never investigated, and never
assessed for whether they were reportable breaches. Both are now permanently
undocumented, which is itself a violation of § 164.308(a)(6)(ii) and § 164.316(b).

The most expensive part of a breach at a practice this size is rarely the intrusion.
It is discovering afterwards that no one can reconstruct what happened, and that the
60-day notification clock at § 164.404 started running on a date nobody recorded.

## 2. Definitions

| Term | Definition |
|---|---|
| **Security incident** | Attempted or successful unauthorized access, use, disclosure, modification, or destruction of information, or interference with system operations (§ 164.304) |
| **Breach** | Acquisition, access, use, or disclosure of PHI in a manner not permitted by the Privacy Rule that compromises its security or privacy (§ 164.402) |
| **Unsecured PHI** | PHI not rendered unusable, unreadable, or indecipherable through encryption or destruction meeting HHS guidance |

**Every breach is an incident. Not every incident is a breach.** A phishing email that
nobody clicked is an incident to log. An unencrypted stolen laptop is presumed to be a
breach. Encryption is what converts the second case into the first, which is the
practical argument for PM-10.

## 3. Response team

| Role | Held by | Responsibility |
|---|---|---|
| Incident Commander | Security Official | Declares the incident and its severity, owns all decisions, owns the breach determination |
| Technical Lead | IT Lead | Containment, evidence preservation, eradication, recovery |
| Clinical Lead | Clinical Director | Patient safety and continuity of care; authorizes downtime procedures |
| Communications Lead | Managing Partner | All external communication — patients, media, payers |
| Legal / Privacy | External counsel (retained) | Breach determination review, regulatory notification, law enforcement liaison |

Contact details, including after-hours numbers and two deputies for each role, are in
Appendix A and verified quarterly.

**No workforce member other than the Communications Lead speaks to media, patients, or
regulators about an incident.**

## 4. Severity classification

| Level | Criteria | Declaration | Response begins |
|---|---|---|---|
| **SEV-1** | Confirmed unauthorized access to ePHI; ransomware; any event affecting patient care across a site | Incident Commander, immediately | Immediate, 24/7 |
| **SEV-2** | Suspected unauthorized access; single-system compromise; lost unencrypted device | Incident Commander within 2 hours | Within 4 hours |
| **SEV-3** | Policy violation without confirmed disclosure; single-user malware, contained; misdirected communication to one recipient | Security Official within 1 business day | Within 1 business day |
| **SEV-4** | Attempted and blocked attack; near miss; phishing reported and not actioned | Logged only | Logged, reviewed monthly |

When severity is unclear, classify higher. Downgrading later is cheap; discovering
you under-responded is not.

## 5. Reporting — what every workforce member must know

> **If you think something is wrong, report it. You will never be penalised for
> reporting an incident, including one you caused. You may be penalised for
> concealing one.**

| Channel | Availability |
|---|---|
| security@northwindfamilyhealth.example | Monitored during business hours |
| Security Official mobile (in Appendix A, posted at each station) | 24/7 |
| Any supervisor, who escalates immediately | 24/7 |

Report within **one hour** of noticing. Do not attempt to investigate, do not delete
anything, do not power the device off unless instructed, and do not forward a
suspicious email to colleagues.

Report if you: clicked a link and entered credentials; lost a device; sent ePHI to the
wrong person; saw a record you should not have; noticed unfamiliar activity on your
account; found a door or cabinet that should have been locked; or received an
unexpected request for patient information.

## 6. Response phases

### 6.1 Detect and report
Log the incident in the Incident Register with a timestamp. **The date of discovery is
recorded here and it governs the notification clock under § 164.404.** Record it
accurately even if it is inconvenient.

### 6.2 Triage — within 1 hour for SEV-1/2
Assign severity. Activate the team. Establish an incident channel. Begin a running
timeline; every action gets a time and an actor.

### 6.3 Contain
Priority order: **patient safety, then evidence, then eradication.**

| Scenario | Immediate containment |
|---|---|
| Compromised credentials | Disable account, revoke sessions and MFA tokens, reset, check mailbox rules and forwarding |
| Ransomware | Isolate affected hosts from the network — do not power off, memory is evidence. Verify backup isolation and immutability before anything else. Activate downtime procedures |
| Lost or stolen device | Remote wipe, revoke tokens, confirm encryption status from the device register |
| Misdirected ePHI | Contact the recipient, request deletion and written confirmation, retain the confirmation |
| Malicious insider | Disable access before notifying the individual; involve HR and counsel first |

Preserve evidence before remediating: memory and disk images for SEV-1, full logs
exported and hashed, and the exact incident timeline. Do not restore from backup until
the initial access vector is understood, or you will restore into the same compromise.

### 6.4 Assess for breach — the step most often skipped

Any incident involving PHI requires a documented risk assessment under
§ 164.402(2), evaluating **all four** factors:

1. The nature and extent of the PHI involved, including identifier types and the
   likelihood of re-identification
2. The unauthorized person who used the PHI or to whom it was disclosed
3. Whether the PHI was actually acquired or viewed
4. The extent to which the risk to the PHI has been mitigated

The Rule creates a **presumption of breach**. Notification is required unless Northwind
demonstrates a low probability that PHI was compromised, based on these four factors.
"We think it was probably fine" is not a demonstration. The written assessment is the
demonstration, and it is retained for six years whichever way it concludes.

Two exclusions may apply and must be documented if relied upon: unintentional
good-faith acquisition by a workforce member acting within scope, and inadvertent
disclosure between authorized persons at the same entity — in both cases only where the
information is not further used or disclosed impermissibly.

If the PHI was encrypted to HHS standards, the safe harbor at § 164.402 applies and it
is not a breach of *unsecured* PHI. Record the encryption evidence.

### 6.5 Notify

| Recipient | Deadline | Authority |
|---|---|---|
| Affected individuals | Without unreasonable delay, **no later than 60 calendar days from discovery** | § 164.404 |
| HHS Secretary — breach affecting 500+ | Contemporaneously with individual notice, no later than 60 days | § 164.408(b) |
| HHS Secretary — breach affecting <500 | Annual log, within 60 days of the end of the calendar year | § 164.408(c) |
| Prominent media in the State — 500+ residents of a State | No later than 60 days from discovery | § 164.406 |
| Business associate → Northwind | Per the BAA; Northwind's standard is 15 calendar days | § 164.410 |
| Ohio Attorney General | Per Ohio Rev. Code 1349.19 where applicable | State law |
| Cyber insurer | Per policy, typically 72 hours — **notify early, before engaging vendors** | Contract |
| Law enforcement / FBI IC3 | As advised by counsel | — |

Individual notice must include what happened, the date of the breach and of discovery,
the types of information involved, steps individuals should take, what Northwind is
doing, and contact procedures. Written notice by first-class mail is the default;
substitute notice applies where contact information is insufficient for ten or more
individuals.

Do not notify before counsel has reviewed the notice. Do not delay notification past
60 days while waiting for a complete investigation — the Rule does not permit it.

### 6.6 Recover
Restore from verified clean backups. Rebuild rather than clean where compromise is
suspected. Reset all credentials that could plausibly have been exposed. Monitor
intensively for 30 days. Return to normal operations only on the Incident Commander's
declaration.

### 6.7 Learn
A post-incident review within 10 business days of closure, producing: a factual
timeline; root cause; what detection should have caught it and did not; and specific,
owned, dated corrective actions entered into the POA&M and the Risk Register.

Blameless as to individuals, unsparing as to controls.

## 7. Documentation

The Incident Register records, for every incident regardless of severity: incident ID,
date and time of discovery and of occurrence, discoverer, description, severity,
systems and ePHI involved, individuals affected, containment and eradication actions
with timestamps, the four-factor breach assessment and its conclusion, notifications
made, root cause, and corrective actions.

Retained six years per § 164.316(b)(2)(i).

## 8. Testing

| Activity | Frequency |
|---|---|
| Tabletop exercise (rotating scenario: ransomware, insider, lost device, BA breach) | Annually |
| Contact list verification | Quarterly |
| Plan review and update | Annually, and after every SEV-1 or SEV-2 |
| Notification template review with counsel | Annually |

A plan that has never been tested is a document, not a capability — the same reasoning
that applies to untested backups under R-07.

---

### Appendix A — Contact roster
*Maintained separately, distributed to the response team, posted at each nurses' station,
and available offline in printed form at each site. An incident response plan that lives
only on the file server the ransomware just encrypted is of no use.*
