# Clinical Safety

Clinical safety is not a chapter. It's a practice. This chapter is a starting point.

If you've read [Medical Device Regulation](medical-device-regulation.md) and [SAFETY.md](safety-md.md), you have the regulatory and documentation frame. This chapter is about the day-to-day work.

## The mindset

Software that touches clinical decisions can hurt people. Not in theory, in practice. The list of high-profile clinical software failures is depressingly long: insulin pump dose miscalculations, radiotherapy machines, EHRs that hid critical allergies, COVID test results lost in a spreadsheet row limit.

The clinician-developer has an unfair advantage in clinical safety: you have done the clinical work. You know what happens when an EHR shows the wrong patient's results. You know what an out-of-range potassium feels like at 3am. You can imagine the failure modes of your own software in a way that pure software engineers often can't.

Use that advantage. The first hazard analysis on your own code should be: 'how could this hurt a patient if it gave the wrong answer at the wrong moment?'

## DCB0129 and DCB0160 in practice

The standards demand:

- A named **Clinical Safety Officer (CSO)** with appropriate training.
- A **clinical safety case** describing the system, its intended use, its hazards, and the mitigations.
- A **hazard log** that lists each identified hazard with severity, likelihood, mitigations, and residual risk.
- A **clinical safety management plan** describing how clinical safety is managed across the project lifecycle.

In practice, what this looks like:

- Every release has a sign-off from the CSO that confirms the safety case is still valid.
- Every change that affects safety is reflected in the hazard log.
- Every hazard has a clear owner and a clear mitigation.
- Every incident triggers a review of the hazard log and (if needed) the safety case.

The format is up to you. See [SAFETY.md](safety-md.md) for a Markdown-and-Git approach.

## Testing strategies for clinical software

Test like you mean it.

- **Unit tests** for every clinical calculation. The eGFR, the BMI, the paracetamol weight-based dose, the gentamicin dosing window. Each calculation gets a test that asserts a known input gives a known output. When the rules change (and they do), the tests change in the same commit.
- **Property-based testing** for ranges and edge cases. Hypothesis (Python) or proptest (Rust) can throw thousands of inputs at a function and find the edge case you didn't think of. Negative weights, zero ages, dates in the future, unicode in names.
- **Integration tests** for end-to-end clinical flows. Order a test, get a result, render the report, file in the record. Don't just test the parts.
- **Clinical scenario tests.** Real (anonymised) clinical scenarios from your domain. Walk the scenarios through the software and assert the right outcome.
- **Regression tests for every bug.** When a clinician reports something, the fix isn't done until there's a test that would have caught it.
- **Load and performance tests** for anything that runs at scale. A correct answer that arrives too late is a wrong answer.

Aim for high coverage of the safety-critical code paths. Coverage tools tell you what's tested; they don't tell you what's *correct*. Look at both.

## Code review with safety in mind

For clinical code, code review is a safety control, not a style nicety. The reviewer should be asking:

- Could this calculation be wrong in any input range?
- What happens if the input is missing, null, or malformed?
- What happens at unit boundaries (mg/kg vs g/kg, mmol/L vs mg/dL)?
- What happens to existing patients when this changes?
- Is the change documented in `SAFETY.md` or the hazard log if it should be?

If your project is large enough to have a CSO who isn't the developer, the CSO should sign off safety-relevant PRs.

## What to do when you find a bug in production clinical software

A bug in clinical software in production is a clinical incident.

1. **Assess scope.** How many patients could be affected, and how badly? Is anyone in immediate harm? If yes, this is an emergency: pull the affected feature, contact users.
2. **Communicate.** Tell users (clinicians, patients, organisations) honestly and quickly. They need to know whether to mistrust recent outputs.
3. **Patch responsibly.** Fix the code, write the test that would have caught it, deploy.
4. **Update the hazard log.** This is now a known hazard with a known mitigation.
5. **Learn.** Was the bug a one-off, or symptomatic? If your test suite would not have caught it, that's a problem with the test suite as much as the code.
6. **Report to the regulator if required.** The MHRA has a Yellow Card scheme for medical device incidents. Vigilance reporting is mandatory for some categories of incident.

The instinct to hide a bug is human. Resist it. Clinical safety culture rewards honest disclosure and punishes cover-ups.

## Cross-references

- [SAFETY.md](safety-md.md) for the documentation convention.
- [Medical Device Regulation](medical-device-regulation.md) for the regulatory frame.
- [Security](security.md) for the security side of the safety story.
