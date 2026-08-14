# How to put this on a resume (and talk about it)

## The rule for all of it

Describe it as a project, not as a job. Nobody expects an entry-level candidate to have
run a real HIPAA assessment for a real client — and if you imply you did, the first
specific question will expose it. "I built this to teach myself" is a completely
respectable answer and it's the one that survives follow-up questions.

Recruiters and hiring managers see a lot of Coursera certificates and very few artifacts.
A spreadsheet you can walk through line by line is worth more than another badge, even
though — maybe *because* — it's obviously a learning exercise.

---

## Resume section

Put it under **Projects**, not under Experience.

```
PROJECTS

HIPAA Security Rule Gap Analysis & Risk Assessment                    2026
Self-directed GRC project · github.com/yourname/hipaa-risk-assessment

• Assessed all 65 standards and implementation specifications of the HIPAA
  Security Rule (45 CFR Part 164 Subpart C) against a fictional 3-site medical
  practice, sourcing control text directly from eCFR and using NIST SP 800-66
  Rev. 2 as implementation guidance.
• Built a risk register of 15 risks scored with NIST SP 800-30 Rev. 1
  (Likelihood × Impact), with treatment decisions and residual risk ratings.
• Produced a 20-item POA&M with owners, cost estimates, and target dates
  sequenced by risk tier.
• Drafted three remediation policies (information security, access control,
  incident response) mapped to the specific CFR provisions they close.
• Documented the Required vs. Addressable analysis required by § 164.306(d)(3),
  identifying 10 addressable specifications implemented with no documented
  determination either way.
```

Trim to three bullets if space is tight. Keep the first two and the last one — the
Required vs. Addressable bullet is the one that signals you actually read the regulation.

### If you only have one line

```
HIPAA Security Rule gap analysis and risk register (self-directed project) —
assessed 65 controls against a fictional clinic, scored 15 risks per NIST
SP 800-30, produced a POA&M and three remediation policies. [link]
```

---

## LinkedIn

Post it as a featured project with a short write-up. Something like:

> I wanted to understand what a HIPAA risk analysis actually involves, so I invented a
> three-site medical practice and did one.
>
> All 65 standards and implementation specifications in 45 CFR Part 164 Subpart C, control
> text pulled from eCFR, risk scored with NIST SP 800-30. Gap analysis, risk register,
> POA&M, and three policies.
>
> Three things I didn't expect:
>
> "Addressable" doesn't mean optional. Under § 164.306(d)(3) you have to implement the
> spec, implement a documented equivalent, or write down why it isn't reasonable for you.
> Doing none of the three is a violation, and 10 of my findings were exactly that.
>
> The gap between a control existing and a control being *evidenced* is most of the work.
> The entity has to demonstrate compliance, so an undocumented control and an absent one
> are in the same position.
>
> The clinic I built failed in a pattern, not at random. The only controls that passed
> were ones a vendor supplies automatically. Everything requiring the practice to do
> something on a schedule — review logs, test a restore, train staff — was missing.
>
> All of it's fictional and the repo says so. Link below.

Don't ask for likes and don't add ten hashtags. The write-up does the work.

---

## Interview answers

### "Walk me through this project."

Sixty seconds, not five minutes:

> I wanted hands-on experience with a real regulation instead of a framework summary, so
> I invented a three-site medical practice — 85 staff, cloud EHR, a couple of business
> associates, no dedicated security person — and assessed all 65 Security Rule controls
> against it.
>
> I pulled the control text from eCFR, used NIST 800-66 for what each control means in
> practice, and scored 15 risks with NIST 800-30. The output is a gap analysis, a risk
> register, a POA&M, and three policies I wrote to close specific gaps.
>
> The most useful thing I got out of it was the pattern in the results. Only three
> controls fully passed, and all three were ones where a vendor supplies the safeguard
> automatically. Everything requiring the clinic to do something recurring was missing.
> That reframed how I think about compliance — it's less about buying controls and more
> about whether anyone actually owns operating them.

Then stop. Let them ask.

### "What's the difference between Required and Addressable?"

This is the question that separates people who read the rule from people who read a blog
post about it. Know it cold.

> Required means you implement it, no discretion. Addressable means you assess whether
> it's reasonable and appropriate for your environment, and then do one of three things:
> implement it, implement a documented equivalent, or document why it isn't reasonable
> and don't implement it. Section 164.306(d)(3).
>
> The thing people get wrong is thinking addressable means optional. It doesn't — it means
> you get flexibility about *how*, in exchange for documenting your reasoning. In my
> project, 10 addressable specs had no control and no documented decision, which is a
> fourth option that doesn't legally exist. I rated those as failures rather than choices,
> and the finding text names the missing determination, not just the missing control.

### "What was your highest-severity finding and why?"

> Remote access to the EHR with a password alone — no MFA. I scored it 25, Likelihood 5
> times Impact 5, under § 164.312(d).
>
> Likelihood 5 because credential theft is the leading way healthcare breaches start, and
> the same scenario had no security training since 2019, so phishing would probably work.
> Impact 5 because it's the whole record set — 118,000 patients — and with no log review
> the attacker would look like a provider working from home.
>
> What made it worth leading with is that the fix is free. MFA was already in the EHR
> licence and nobody had turned it on.

### "How did you decide on likelihood and impact scores?"

Be honest that this was the hard part:

> Badly, on the first pass. Almost everything came out High, which makes a register
> useless — if everything's a priority, nothing is.
>
> So I went back and wrote definitions before scoring. Likelihood 5 is happening now or
> expected within a year; 3 is plausible within two to three years. Impact I scored
> against three axes — patient safety, regulatory exposure, and operational continuity —
> and took the highest. Then I rescored everything against the definitions instead of
> against my gut, and the distribution actually spread out.
>
> The other thing I made myself do was leave one risk High after remediation. Staff
> phishing susceptibility — training reduces it, it doesn't eliminate it. A register where
> everything drops to Low after a year of work isn't credible.

### "What would you do differently?"

> Write the evidence column first. I did it last, and working out what would actually
> prove a control works clarified what the control *means* better than re-reading the
> regulation did.
>
> And I'd be more honest earlier about the limits. It's a scenario I designed, so the
> findings are ones I planted. The skill I practiced was mapping problems to controls,
> citing them, scoring them, and explaining them — not discovering them. A real assessment
> deals with evidence that's incomplete or contested by the people who gave it to you, and
> I suspect that's most of the actual difficulty.

### "This is fictional — what does it prove?"

Don't get defensive. It's a fair question with a good answer.

> That I can read a regulation and work systematically through it, which is most of the
> job. The scenario is invented; the control set, the citations, and the method aren't.
> If you handed me a real environment tomorrow, the thing I'd be missing is evidence
> collection and dealing with people, not the framework.
>
> I'd rather show you something I actually built and be upfront about what it is than
> show you a certificate.

---

## Things to avoid

| Don't | Because |
|---|---|
| Put it under Experience | It isn't. Someone will ask who the client was |
| Say "led a HIPAA assessment" | You didn't lead anything; you did a project |
| Say "identified 32 gaps" without context | You wrote the scenario that contains them |
| Claim tools you didn't use | If you list the SRA Tool, download it and click through it first |
| Bury the fictional framing | Put it in the README's first paragraph. Being upfront reads as integrity; being caught reads as the opposite |
| Memorize the answers above word for word | Interviewers can hear it. Know the substance, use your own words |

---

## Putting it on GitHub

You don't need git or the command line. The web upload works fine.

**1. Make an account** at github.com if you don't have one. Your username becomes part of
the URL, so pick something you'd put on a resume — `surayaazeez` over `xX_cyber_Xx`.

**2. Create the repository.** Click **+** (top right) → **New repository**.

| Field | Use |
|---|---|
| Repository name | `hipaa-risk-assessment` |
| Description | `HIPAA Security Rule gap analysis and risk register — self-directed GRC project` |
| Visibility | **Public** (a private repo can't be linked from a resume) |
| Add a README | **Leave unchecked** — you already have one |

**3. Upload.** On the empty repo page, click **uploading an existing file**. Drag the
whole unzipped project folder's *contents* in — not the folder itself, or everything ends
up one level too deep. Wait for all files including `images/` to finish, then
**Commit changes**.

**4. Check it rendered.** Refresh. You should see your README as the front page with both
spreadsheet screenshots visible. If the images show as broken links, the `images/` folder
didn't upload — add it separately.

**5. Add topics.** Click the gear next to "About" and add: `hipaa`, `grc`, `risk-assessment`,
`compliance`, `cybersecurity`. It makes the repo findable and looks deliberate.

**6. Pin it.** On your profile page, **Customize your pins** → select this repo. Otherwise
it's buried.

### What your resume link looks like

```
github.com/yourusername/hipaa-risk-assessment
```

Put it in your header next to your email, and again in the project entry. Write it without
`https://` — it's shorter and still clickable in most PDF readers.

### Two things people get wrong

**Don't upload the zip file.** GitHub will show it as a single binary blob nobody can
open. Upload the individual files so the README renders and the PDF previews.

**Check the README on your phone.** Most first views of a resume link are on mobile. The
tables should still be legible; if they're not, that's worth knowing before a recruiter
sees it.

## Before you publish

- [ ] Replace every placeholder — the report has `[Your Name]` on the cover
- [ ] Read the whole thing once out loud. If a sentence doesn't sound like you, rewrite it
- [ ] Download the HHS SRA Tool and actually run through it, so you can talk about it
- [ ] Open the spreadsheet and change one likelihood score, so you know the formulas work
      and can demo it if someone shares their screen with you
- [ ] Pick three findings you can explain without notes
- [ ] Make sure the "this is fictional" line is visible without scrolling on GitHub
- [ ] Open your own repo link in a private browser window — that's what a recruiter sees

## What to build next

If this goes well and you want a second project that pairs with it:

1. **The same clinic under a different framework.** Map your 65 HIPAA controls to NIST
   CSF 2.0 or ISO 27001 Annex A and see where they don't line up. Crosswalking is a real
   GRC task and the overlaps are genuinely interesting.
2. **A vendor risk assessment.** Take the five business associates from the scenario and
   build a due diligence questionnaire, a tiering model, and a review cadence. Third-party
   risk is where a lot of entry-level GRC work actually is.
3. **A SOC 2 readiness assessment** for a small SaaS company. Different audience, same
   muscles, and it's the framework most startups hire for.

Two solid projects beat five shallow ones. Finish this one properly first.
