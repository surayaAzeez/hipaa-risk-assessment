# POL-001 · Information Security Policy

> Part of a self-directed HIPAA practice project. Northwind Family Health is a fictional clinic; this policy was drafted to close specific gaps found in that scenario. The CFR citations are real.

| | |
|---|---|
| **Owner** | Security Official (Practice Administrator) |
| **Approved by** | Managing Partner |
| **Version** | 1.0 |
| **Effective** | 1 June 2026 |
| **Supersedes** | HIPAA Compliance Binder (2014), withdrawn in full |
| **Review cycle** | Annually, and upon material environmental or operational change |
| **Closes findings** | D-01, D-02, D-05, A-01, A-03, A-04, A-06 |

---

## 1. Purpose

This policy establishes how Northwind Family Health, LLC protects the confidentiality,
integrity, and availability of the electronic protected health information it creates,
receives, maintains, and transmits, as required by 45 CFR § 164.316(a) and
§ 164.306(a).

It replaces the 2014 compliance binder in its entirety. That document was a purchased
template, was never adopted, and does not describe the environment Northwind operates
today.

## 2. Scope

This policy applies to:

- All workforce members as defined at 45 CFR § 160.103 — employees, contractors,
  volunteers, students, and trainees, whether or not paid by Northwind
- All three clinic locations and all remote work locations
- All information systems listed in the Asset and ePHI Inventory
- All business associates, through the terms of their business associate agreements

## 3. Policy statements

### 3.1 Security Official (§ 164.308(a)(2))

The Practice Administrator is designated Security Official. Unlike the 2014
designation, this role now carries defined obligations, time, and authority:

| Obligation | Cadence |
|---|---|
| Maintain the risk analysis and risk management plan | Annual, plus on material change |
| Chair the Security Review Committee | Quarterly |
| Review the POA&M and report status to the Managing Partner | Quarterly |
| Perform or oversee the information system activity review | Monthly |
| Approve access to ePHI systems and oversee access reviews | Quarterly |
| Own incident response and breach determination | As required |
| Maintain the policy set and documentation retention | Annual |

The Security Official is allocated a minimum of 8 hours per month for these duties and
holds approval authority for security expenditure up to $5,000 without further sign-off.

### 3.2 Risk analysis and risk management (§ 164.308(a)(1)(ii)(A)–(B))

Northwind shall maintain a current, documented, accurate and thorough risk analysis
covering all ePHI it holds, regardless of location or medium.

- A full risk analysis is performed at least annually.
- The risk analysis is refreshed on any material change: a new system holding ePHI,
  a new business associate, a new clinic, a significant change to network architecture,
  or a reportable security incident.
- Every identified risk is recorded in the Risk Register with an owner, a treatment
  decision, and — where the decision is to accept — written rationale approved by the
  Managing Partner.
- Remediation is tracked in the POA&M with target dates aligned to risk tier:
  Critical 30 days, High 90 days, Moderate 180 days.

### 3.3 Flexibility of approach (§ 164.306(b))

Northwind is a small practice and will select controls that are reasonable and
appropriate to its size, complexity, technical infrastructure, and cost, as the Rule
permits. This flexibility is a basis for choosing a *proportionate* control. It is
never a basis for choosing *no* control and not writing anything down.

For every addressable implementation specification, Northwind shall do one of three
things and document which:

1. Implement the specification as written; or
2. Implement a documented equivalent alternative measure; or
3. Document why the specification is not reasonable and appropriate in this
   environment, and what compensating measure, if any, applies.

A specification with no implementation and no documented determination is a
non-compliance, not a choice.

### 3.4 Workforce security and training (§ 164.308(a)(3), (a)(5))

- Every workforce member completes security awareness training within 14 days of hire
  and annually thereafter. Completion is recorded and retained.
- Phishing simulation exercises are conducted monthly, with directed follow-up training
  for those who interact with a simulated message.
- Security reminders are issued at least quarterly.
- Access is granted on a least-privilege basis against a defined role. Access changes
  on role change; it does not accumulate.
- System access is revoked within four hours of a workforce member's separation.

### 3.5 Sanctions (§ 164.308(a)(1)(ii)(C))

Failure to comply with this policy is subject to sanctions applied consistently
regardless of role or seniority:

| Conduct | Sanction |
|---|---|
| Negligent violation, first occurrence, no ePHI disclosed | Documented counselling and retraining |
| Negligent violation, repeat, or ePHI disclosed | Written warning; retraining; access review |
| Access to a record without a treatment, payment, or operations purpose | Final written warning to termination; reportable to licensing board where applicable |
| Deliberate access for personal gain, curiosity, or malice | Termination; referral to OCR and law enforcement as required |
| Concealing or failing to report a known incident | Final written warning to termination |

Sanctions are documented in the personnel file and retained for six years.

### 3.6 Technical safeguards (§ 164.312)

| Requirement | Standard |
|---|---|
| Authentication | Multi-factor authentication required for all access to ePHI systems, without exception for remote access or administrative accounts |
| Unique identification | Individual accounts only. Shared accounts are prohibited; the three legacy shared accounts are remediated under PM-01 and PM-07 |
| Encryption at rest | Full-disk encryption on every endpoint and server storing ePHI, with escrowed recovery keys. A device that cannot be encrypted may not store ePHI |
| Encryption in transit | TLS 1.2 or higher for all system interfaces. ePHI sent by email must use message encryption |
| Automatic logoff | 5 minutes on public-facing workstations, 10 minutes on clinical workstations, 15 minutes elsewhere |
| Audit controls | Logging enabled on all ePHI systems, retained six years, and **reviewed monthly** — recording without examination does not satisfy § 164.312(b) |

### 3.7 Physical safeguards (§ 164.310)

- Server and network equipment is housed in locked spaces at all times. Propping a
  door open for ventilation is prohibited.
- Entry codes are rotated on the separation of any workforce member who knew them, and
  semi-annually regardless.
- Visitors sign in, are badged, and are escorted in non-public areas.
- Screens displaying ePHI are positioned or filtered so they are not readable from
  patient waiting areas.
- Electronic media is sanitized per NIST SP 800-88 before re-use or disposal, and
  certificates of destruction are retained.

### 3.8 Business associates (§ 164.308(b), § 164.314(a))

No vendor may create, receive, maintain, or transmit ePHI on Northwind's behalf before
a compliant business associate agreement is executed. The Security Official maintains a
BAA register reviewed annually. Each agreement must include, at minimum, the elements
required at § 164.314(a)(2)(i) and a breach notification deadline of no more than
15 calendar days, so that Northwind can meet its own 60-day obligation under
§ 164.410.

### 3.9 Incident response (§ 164.308(a)(6))

All suspected security incidents are reported immediately to the Security Official.
Response follows POL-003 Incident Response Plan. Every incident involving PHI receives
a documented four-factor breach risk assessment under § 164.402(2).

### 3.10 Contingency planning (§ 164.308(a)(7))

Northwind maintains a Contingency Plan with a documented RTO of 8 hours and RPO of
24 hours. Backups are immutable and isolated from the production network. A restore
test is performed and documented at least semi-annually. Backup success is not evidence
of recoverability; a documented restore is.

### 3.11 Documentation (§ 164.316(b))

All documentation required by the Security Rule — policies, risk analyses,
evaluations, training records, incident records, log reviews, access reviews,
contingency tests, and sanctions — is retained for six years from creation or from the
date it was last in effect, whichever is later, and is made available to the workforce
members responsible for implementing it.

## 4. Exceptions

Exceptions require written request to the Security Official stating the business
justification, the duration, and the compensating control. Approved exceptions are
recorded in the Risk Register with an expiry date and are reviewed at each quarterly
Security Review Committee. No exception may be granted to the multi-factor
authentication or encryption-at-rest requirements.

## 5. Related documents

- POL-002 Access Control Policy
- POL-003 Incident Response Plan
- Asset and ePHI Inventory
- Risk Register and POA&M
- Security Risk Analysis, 3 April 2026
