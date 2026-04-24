# CwC Opinionated Handbook - v1.0 Spec

Target: Launch at Clinicians Who Code (un)Conference, York, June 20 2026

## Purpose

A practical, opinionated guide for clinicians who want to build healthcare
software safely, openly, and quickly. Written in the first person, direct,
with strong opinions held lightly. Not a textbook - a handbook from one
clinician-developer to another.

## Format

- Docusaurus or Zensical for docs (replacing MkDocs - see note below)
- Hosted on GitHub Pages
- Source on GitHub - open to community PRs
- Tag v1.0 release to coincide with conference

### Note on MkDocs

MkDocs Material is no longer recommended due to the upstream licensing
debacle. Migrate to Docusaurus (more mature, React-based, strong community)
or Zensical (newer, cleaner, worth evaluating). Decision needed before
starting content work as it affects build pipeline.

---

## Existing Content - Review and Update Required

### Getting Started

- [ ] What Language Should I Learn? - answer is still Python, but update
      framing for AI-assisted coding era; Python even more relevant as the
      language of AI/ML tooling. Add Rust as second language recommendation.
- [ ] Why Python? - review and update
- [ ] Learning Python - check links, update resources
- [ ] Learning Django - review; still the right recommendation for full-stack?
- [ ] REMOVE Flask - consolidated into FastAPI recommendation
- [ ] Web Frameworks - needs significant update; Django for full-stack,
      FastAPI for APIs, landscape has changed
- [ ] Which text editor? - full rewrite; VS Code has won, cover Cursor,
      Windsurf, Claude Code
- [ ] What the hell is a shell? - light touch review, likely still valid
- [ ] Where and how to work - review

### Basics

- [ ] Conventions used in this book - review
- [ ] Obtaining Focus - review; likely still relevant
- [ ] Glossary - extend and update
- [ ] Mantras - review and extend
- [ ] What is Open Source and why should I care? - core argument stronger
      than ever, update with recent NHS examples
- [ ] Sources of Help and Support - full update needed (see Community section)
- [ ] Usability and User Experience - review

### Intermediate

- [ ] Git - review; core content likely solid, update tooling references
- [ ] REST and APIs - update; FastAPI as the recommendation, add FHIR R4/R5
- [ ] Documentation - review
- [ ] Managing servers - update for cloud/container era
- [ ] Productivity tools - full rewrite needed

### Advanced

- [ ] Legals - significant update; DTAC, DCB0129/0160, AI Act, software as
      a medical device
- [ ] NHS IT - update for current landscape; ICBs, Federated Data Platform,
      FHIR mandates

---

## New Content Required

### Languages (update and extend existing)

#### Python - primary language (existing, update)

- Still the answer for almost everything
- Even more relevant as the language of AI/ML tooling
- Community critical mass argument now stronger than ever

#### Rust - second language recommendation (new)

- When and why to reach for Rust instead of Python
- Performance-critical code
- Memory safety without a garbage collector
- System-level tooling
- CLIs - Rust is excellent for distributable, fast command-line tools
- Interoperability with Python via PyO3 if needed
- Learning resources

#### FastAPI (new - replaces Flask)

- The opinionated recommendation for APIs in Python
- Why FastAPI over Flask - automatic docs, type hints, async, speed
- Getting started
- FHIR endpoints with FastAPI

### Scripts To Rule Them All (new)

- The pattern: every repo has a `script/` directory with standard entrypoints
- `script/setup` - get the project running from scratch
- `script/test` - run the test suite
- `script/server` - start the dev server
- `script/console` - open a REPL with the app context loaded
- Why this matters - you can hop between repos and `script/setup` always works
- Reference: <https://github.com/github/scripts-to-rule-them-all>

### Distribution and Packaging (new)

- Why packaging matters - reproducibility, safety, shareability
- Python packaging - pyproject.toml, PyPI, pipx
- Rust packaging - Cargo, crates.io
- Docker - when and why
- Making your tool easy for other clinicians to install and run
- Versioning and changelogs

### Documentation (update existing, expand)

- Why documentation is a clinical safety issue, not just a nice-to-have
- Docusaurus - getting started, recommended for most projects
- Zensical - evaluate as alternative
- README.md as the front door
- CHANGELOG.md
- Inline code documentation
- API documentation with FastAPI's built-in OpenAPI support

### Keeping Notes (new)

- Notes as a core developer practice
- Plain files on disk - the case for longevity and portability
- Markdown everywhere - .md as the default format
- Tools - Obsidian, VS Code, Claude Code as a thinking partner
- Note-keeping in the context of clinical projects - audit trails,
  decision logs, architecture decision records (ADRs)

### SAFETY.md (new - high priority)

- Clinical safety as a first-class concern in open source health software
- The SAFETY.md convention - <https://github.com/pacharanero/SAFETY.md>
- What to put in a SAFETY.md
- Why every clinical software repo should have one
- Relationship to DCB0129/0160
- How SAFETY.md fits into a broader clinical risk management approach
- Encouraging adoption across the community

### Medical Device Regulation (new - high priority)

- Software as a Medical Device (SaMD) - what it means and when it applies
- The regulatory landscape - MHRA, CE/UKCA marking post-Brexit
- DCB0129 - clinical risk management for health IT systems
- DCB0160 - clinical risk management for manufacturers
- DTAC - Digital Technology Assessment Criteria
- AI Act implications for AI-assisted clinical tools
- Practical steps - when to get a regulatory consultant involved
- Resources and further reading

### AI-Assisted Development (new - high priority)

- What is vibe coding / quality vibe engineering?
- AI coding tools - Claude Code, Cursor, GitHub Copilot, Windsurf
- How to use AI tools well as a clinician-developer
- Prompt engineering for code generation
- When to trust AI output and when not to
- Clinical safety implications of AI-generated code
- AI and open source licensing considerations

### Clinical Safety (new - high priority)

- DCB0129 and DCB0160 in practice
- Testing strategies for clinical software
- What to do when you find a bug in production clinical software
- SAFETY.md (cross-reference dedicated section)

### FHIR and Interoperability (new)

- What is FHIR and why should I care?
- FHIR R4 in the NHS context
- Practical FHIR - Python FHIR libraries
- SNOMED, LOINC, dm+d - terminologies for clinicians who code

### Security (new)

- Basic security hygiene for clinical software
- Secrets management - never commit credentials
- Authentication and authorisation
- Data minimisation and pseudonymisation

### Community (new - replaces/expands Sources of Help)

- Clinicians Who Code on Digital Health Networks
- Clinicians Who Code on OpenHealthHub (openhealthhub.org)
- Reddit communities
- Discord servers
- Bluesky follows worth having
- YouTube channels - Everything Digital Health and others
- Conferences - CwC (un)Conference and others
- How to contribute back to the community

### Career and Context (new)

- Making time to code as a clinician
- How to talk to your employer about coding projects
- Contributing to NHS digital transformation from the inside
- Finding your people

---

## Things to Remove

- Flask section - replaced by FastAPI
- Donate page - replace with Contribute page pointing to GitHub and community

---

## Stretch Goals

- Community contributions chapter - invite PRs from conference attendees
- Case studies - real clinician-built tools (with permission)
- Additional forewords from community members

---

## Notes for Claude Code

- Migrate from MkDocs to Docusaurus or Zensical - decision needed first
- Writing style: direct, first-person, opinionated - avoid hedging
- Avoid corporate or academic tone
- Short paragraphs, concrete examples over abstract discussion
- State strong opinions clearly and explain the reasoning
- Do not use em dashes
- All new pages need adding to nav config
- Check all external links are live before v1.0
- Reference repos for style and content:
  - <https://github.com/pacharanero/SAFETY.md>
  - <https://github.com/github/scripts-to-rule-them-all>
