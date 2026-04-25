# SAFETY.md

Every clinical software repository should have a `SAFETY.md` file in its root.

That's the headline. The rest of this chapter explains what it is, why it matters, and how to start one without drowning in process.

## What is SAFETY.md?

`SAFETY.md` is a convention, in the same family as `README.md`, `CONTRIBUTING.md`, `CODE_OF_CONDUCT.md`, and `SECURITY.md`. It's a single Markdown file at the root of your repo that describes the clinical safety position of the software: what it does clinically, what could go wrong, and how the project manages that risk.

The convention is documented at <https://github.com/pacharanero/SAFETY.md>. Disclosure: I started it. I think it's important.

## Why a Markdown file and not a spreadsheet?

Because spreadsheets are how clinical safety documentation goes to die.

The traditional approach to DCB0129 and DCB0160 is a Word document with a clumsy 'Document Control' table on the front, and a hazard log in Excel that no developer ever looks at. The document drifts out of sync with the code within weeks. Nobody reads it. When the regulator asks for it, somebody scrambles to update it.

`SAFETY.md` flips this. The safety documentation lives in the same repository as the code, in the same format as the rest of your developer docs, edited by the same people, reviewed in the same pull requests, versioned by the same Git history. Every change to the safety case is attributed to a person and a commit. When code changes affect safety, the same PR can update the safety documentation.

This is what 'twenty-first century version control' looks like applied to clinical safety. Git already solves attribution, history, review, and rollback. Use it.

## What goes in a SAFETY.md?

At minimum:

- **What the software does clinically.** A short, plain-English description of the clinical purpose. Not the marketing description, the safety-relevant description.
- **Who the intended users are.** Clinicians? Patients? Both? At what level of training?
- **What the safety strategy is.** What does the project do to keep users safe? Testing, code review, version control, staging environments, pre-release sign-off.
- **A summary of identified hazards.** What could go wrong, and what has been done about it.
- **Who is the Clinical Safety Officer (CSO).** Even if it's just you, name yourself.
- **Where to report a safety concern.** A real email address or issue tracker label.

That's it for Tier 1. You can fit it on one page.

## Tiered structure for bigger projects

The convention is deliberately tiered so it scales with the project. From the upstream spec:

- **Tier 1.** A single `SAFETY.md`. Project overview, safety strategy, hazard summary. Suitable for a small low-risk tool.
- **Tier 2.** Add `SAFETY-CASE.md`, `HAZARD-LOG.md`, `SAFETY-PLAN.md` as separate files. Suitable for something more substantial.
- **Tier 3.** Move to a `safety/` directory with one Markdown file per hazard, with required frontmatter, enforced by a GitHub Action. Suitable for a regulated product.
- **Tier 4.** Safety documentation lives in its own repository, linked to one or more code repositories. Rare, but possible.

You almost certainly want to start at Tier 1.

## Relationship to DCB0129 and DCB0160

DCB0129 is the standard for manufacturers of health IT systems. DCB0160 is the standard for organisations deploying them. Both require a hazard log, a clinical safety case, and a Clinical Safety Officer.

`SAFETY.md` is not a replacement for compliance with these standards. It's a way of *doing* the work the standards require, in a format that developers will actually maintain. If your project is in scope of DCB0129, your `SAFETY.md` (and the files it references) is your evidence.

For a deeper dive on the regulatory landscape, see [Medical Device Regulation](medical-device-regulation.md).

## Doing the work

If you've never done clinical safety documentation before, the upstream repo has templates. Copy one, fill in the blanks honestly, commit it. Update it when you change something safety-relevant. Review it before each release. That's the loop.

The mistake people make is treating safety documentation as a one-off compliance exercise. It's not. It's an ongoing record of how you understand the risks of your software. The first version will be incomplete. That's fine. Commit it anyway, and improve it.

## Encouraging adoption

If you maintain or contribute to clinical software, add a `SAFETY.md` to it. If you find a clinical software repo without one, open an issue. The more projects that adopt the convention, the more normal it becomes, and the easier it is for the next clinician-developer to follow suit.
