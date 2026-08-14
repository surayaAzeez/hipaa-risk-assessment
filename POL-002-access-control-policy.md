# POL-002 · Access Control and Identity Management Policy

> Part of a self-directed HIPAA practice project. Northwind Family Health is a fictional clinic; this policy was drafted to close specific gaps found in that scenario. The CFR citations are real.

| | |
|---|---|
| **Owner** | Security Official, with IT Lead as operational owner |
| **Version** | 1.0 |
| **Effective** | 1 June 2026 |
| **Review cycle** | Annually |
| **Closes findings** | A-07, A-08, A-10, A-13, A-14, A-19, T-01, T-02, T-03, T-04, T-09 |
| **Addresses risks** | R-01 (Critical), R-04 (High), R-11 (High) |

---

## 1. Purpose

To ensure that access to electronic protected health information is granted only to
authorized workforce members, limited to what their role requires, and removed promptly
when it is no longer needed — as required by 45 CFR §§ 164.308(a)(3), 164.308(a)(4),
and 164.312(a) and (d).

This policy exists because the 2026 risk analysis found eleven active accounts
belonging to people who no longer worked at Northwind, one of which had been used
eleven days after the person left.

## 2. Roles and access model

### 2.1 Defined roles

Access is granted against one of nine defined roles, never assembled ad hoc:

| Role | EHR access | Billing system | File server | Admin rights |
|---|---|---|---|---|
| Physician / NP | Full clinical | View own encounters | Clinical share | No |
| Nurse / MA | Full clinical | None | Clinical share | No |
| Front desk | Demographics, scheduling, insurance | Payment posting | Intake share | No |
| Referral coordinator | Clinical read, referral write | None | Clinical share | No |
| Billing clerk | **Encounter and diagnosis codes only — not clinical notes** | Full | Billing share | No |
| Billing manager | Encounter and diagnosis codes only | Full + adjustments | Billing share | No |
| Practice Administrator | Full clinical + audit reports | Full | All shares | No |
| IT Lead / IT Technician | **No clinical access by default** | None | Administrative | Yes, named admin account |
| Student / per-diem | Supervised clinical, time-limited | None | Clinical share | No |

The billing role's exclusion from clinical notes is deliberate. The 2026 assessment
found a billing clerk with full chart access; nothing in the billing workflow requires
it, and the Privacy Rule's minimum necessary standard does not permit it.

IT staff hold no standing clinical access. Where an IT task requires access to ePHI,
it is granted temporarily through the emergency access procedure in § 6 and logged.

### 2.2 Least privilege and separation of duties

- Access beyond a role's standard permission set requires written justification and
  approval by the Security Official.
- The requester of elevated access may not also approve it. The 2026 assessment found
  the IT Lead had done both on at least two occasions; this is now prohibited.

## 3. Provisioning

1. The hiring manager submits an Access Request Form naming the workforce member,
   start date, role, and site. Verbal requests are not actioned.
2. HR confirms the clearance check is complete. Clearance checks are now required for
   **all** roles, not only clinical — the two accounts with domain administrator rights
   had never received one.
3. The Security Official approves.
4. IT provisions the role's standard permission set. Nothing beyond it.
5. The form is retained for six years as evidence under § 164.316(b).

Access is not provisioned before security awareness training is complete.

## 4. Modification

A role change generates a new Access Request Form. IT applies the new role's permission
set and **removes the prior role's permissions in the same action**. Access does not
accumulate across roles. The 2026 assessment found three of twenty sampled users still
holding rights from a previous position.

## 5. Deprovisioning

| Trigger | Action | SLA |
|---|---|---|
| Planned separation | Disable all accounts, revoke MFA tokens, collect devices | By end of last working day |
| Immediate separation | Disable all accounts before the workforce member leaves the premises | Immediate |
| Extended leave >30 days | Disable accounts, retain for reinstatement | Within 24 hours |
| Business associate offboarding | Revoke interface credentials, rotate shared keys | Within 4 hours |

**HR must notify IT of every separation.** The separation checklist now contains an IT
access-revocation step that must be signed before the checklist is closed. This is the
single control that would have prevented the eleven orphaned accounts.

Accounts are disabled, not deleted, and retained for 90 days so that audit history
remains attributable.

## 6. Emergency access (§ 164.312(a)(2)(ii))

MedStream's break-the-glass function may be used where a clinician requires access to a
record outside their normal permissions and delay would risk patient care.

- The user must enter a reason at the time of access.
- Every use generates an alert to the Security Official.
- Every use is reviewed within five business days and the review is documented.
- Use without a legitimate clinical justification is treated as unauthorized access
  under the sanction policy.

The capability existed before this policy. What did not exist was any rule for when it
may be used or any review of when it had been.

## 7. Authentication (§ 164.312(d))

### 7.1 Multi-factor authentication

MFA is **required for all users on all systems that store or provide access to ePHI**.
There are no exceptions for seniority, for convenience, or for on-site access.

Accepted factors, in order of preference:

1. Authenticator application with number matching
2. FIDO2 security key
3. Push notification with number matching

SMS is permitted only as a temporary fallback during enrolment and must be removed
within 30 days.

### 7.2 Passwords

| Setting | Standard | Basis |
|---|---|---|
| Minimum length | 14 characters | NIST SP 800-63B |
| Complexity composition rules | Not required | NIST SP 800-63B — composition rules reduce entropy in practice |
| Expiry | None, absent evidence of compromise | NIST SP 800-63B |
| Breached-password screening | Required at set and change | NIST SP 800-63B |
| Reuse across systems | Prohibited | — |
| Written on paper near a workstation | Prohibited | Two instances observed in 2026 |
| Password manager | Provided to all workforce members | — |

Removing forced expiry while raising minimum length and adding breach screening is a
net strengthening, and it aligns with current NIST guidance rather than the 2003-era
practice the environment had inherited.

### 7.3 Account lockout

Ten failed attempts within 15 minutes locks the account for 30 minutes. Lockout events
are alerted to the IT Lead and reviewed for patterns indicating password spraying.

## 8. Session management

| Context | Automatic logoff |
|---|---|
| Public-facing workstations and kiosks | 5 minutes |
| Clinical workstations and tablets | 10 minutes |
| Private offices | 15 minutes |
| MedStream application session | 15 minutes |
| Remote sessions | 15 minutes, with re-authentication at 12 hours |

Workforce members lock their screen whenever they step away, regardless of timer.

## 9. Access reviews (§ 164.308(a)(4)(ii)(C))

A user access review is performed **quarterly** for MedStream, ClearPath, Microsoft 365,
and Active Directory.

For each system the owner receives a full account listing with role and last login, and
must attest in writing that every account is current, correctly roled, and still
required. Accounts unused for 90 days are disabled unless the owner justifies retention.
Findings are remediated within 15 business days and the signed attestation is retained
for six years.

Privileged accounts — domain administrators, MedStream administrators, and billing
adjustment rights — are reviewed **monthly**.

## 10. Monitoring (§ 164.308(a)(1)(ii)(D), § 164.312(b))

The Security Official reviews the following monthly and signs the review:

| Report | What it catches |
|---|---|
| Same-surname access | Staff viewing relatives' records |
| Employee record access | Staff viewing colleagues' records |
| After-hours access | Access outside the user's working pattern |
| Break-the-glass usage | Emergency access without justification |
| Failed authentication summary | Password spraying, credential stuffing |
| Privileged account activity | Administrator misuse |
| Dormant account report | Accounts that should have been deprovisioned |

Reviews are documented even when nothing is found. An undocumented review did not happen.
