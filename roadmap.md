# CwC Handbook Roadmap

**Target launch:** v1.0 at the Clinicians Who Code (un)Conference, York, 20 June 2026.

**Current state:** v0.9 scaffold. Tooling migrated to Zensical, all high-priority new chapters drafted, several existing pages rewritten. Marcus's editing pass is the next phase.

This file consolidates the original `cwc-handbook-spec.md`, `todo.md`, and `scratch-notes.md`. Open editorial questions from the Phase 3 scaffold are tracked separately in [`queries.md`](queries.md).

---

## Mission

A practical, opinionated guide for clinicians who want to build healthcare software safely, openly, and quickly. Written in the first person, direct, with strong opinions held lightly. Not a textbook; a handbook from one clinician-developer to another.

**Style guide:**

- First-person, opinionated, avoid hedging.
- Avoid corporate or academic tone.
- Short paragraphs, concrete examples over abstract discussion.
- State strong opinions clearly and explain the reasoning.
- Do not use em dashes.
- All new pages need adding to nav config.
- British spellings.

---

## Format and tooling

- [x] Choose docs framework (Zensical chosen over Docusaurus for drop-in migration from MkDocs)
- [x] Migrate `mkdocs.yml`, `requirements.txt`, build pipeline to Zensical
- [x] Hosted on GitHub Pages via GitHub Actions (no more `gh-pages` branch)
- [x] Source on GitHub, open to community PRs
- [x] Repo-root `README.md` with mission and link to published site
- [x] Add `.gitignore` entries for `.venv/` and `__pycache__/`
- [ ] Tag v0.9 release for soak / pre-conference editing
- [ ] Tag v1.0 release at conference launch
- [ ] Check all external links are live before v1.0
- [ ] Add `LICENSE` file (confirm intended licence)
- [ ] Add `CODE_OF_CONDUCT.md` (since inviting community PRs)
- [ ] Add `.editorconfig` for consistent contributor formatting

---

## Existing content review

### Getting Started

- [ ] What Language Should I Learn? — update framing for AI-assisted era; reference Rust as second language. Typo fixes done; substantive update pending.
- [ ] Why Python? — review and update
- [ ] Learning Python — check links, update resources, **finish the truncated `pyenv local` tip on line 45** ("...will automatically select your" — your what?)
- [ ] Learning Django — review; still the right recommendation for full-stack?
- [x] REMOVE Flask — `learning-flask.md` deleted
- [x] Web Frameworks — rewritten: Django for full-stack, FastAPI for APIs, frontend trade-offs, mobile honest options
- [x] Which text editor? — rewritten: VS Code default, AI editors (Cursor/Windsurf/Copilot/Claude Code), kept nano section
- [ ] What is a Shell? — light review, likely still valid
- [ ] Where and How to Work — currently a 12-line stub, needs writing

### Basics

- [ ] Conventions used in this book — typo fixes done; full review pending
- [ ] Obtaining Focus — typo fixes done; remains relevant
- [ ] Glossary — extend and update
- [ ] Mantras — review and extend (incorporate "Avoid Unnecessary Mappings" and "Avoid Unnecessary Abbreviations" from old scratch notes?)
- [ ] What is Open Source? — refresh with recent NHS examples
- [ ] Sources of Help and Support — kept alongside new Community chapter; decide whether to merge or keep both
- [ ] Usability and User Experience — review

### Intermediate

- [ ] Git — review; update tooling references
- [ ] REST and APIs — update for FastAPI focus; add FHIR R4/R5 cross-link
- [ ] Documentation — expand (mention Zensical, README.md as front door, CHANGELOG, OpenAPI via FastAPI)
- [ ] Managing Servers — update for cloud/container era
- [ ] Productivity tools (`accessories.md`) — full rewrite needed

### Advanced

- [ ] Legals — significant update; substantial overlap with new `medical-device-regulation.md`. Consider merging or repositioning as companion.
- [ ] NHS IT — update for current landscape: ICBs, Federated Data Platform, FHIR mandates

---

## New content (scaffolded in v0.9)

### Languages

- [ ] Python — existing pages not yet updated for AI-era framing
- [x] Rust — `getting-started/rust.md` (when/why, PyO3 interop, learning resources)
- [x] FastAPI — `getting-started/fastapi.md` (replaces Flask; FHIR endpoints; testing)

### Patterns and process

- [x] Scripts To Rule Them All — `intermediate/scripts-to-rule-them-all.md` (uses your `s/` convention not upstream `script/` — see `queries.md`)
- [x] Distribution and Packaging — `intermediate/distribution-and-packaging.md` (Python, Rust, Docker, semver)
- [x] Keeping Notes — `intermediate/keeping-notes.md` (Markdown on disk, ADRs, tools)

### Clinical safety and regulation

- [x] SAFETY.md — `advanced/safety-md.md` (drew on your upstream pacharanero/SAFETY.md repo)
- [x] Medical Device Regulation — `advanced/medical-device-regulation.md`
- [x] Clinical Safety — `advanced/clinical-safety.md`

### Tooling and interop

- [x] AI-Assisted Development — `advanced/ai-assisted-development.md`
- [x] FHIR and Interoperability — `advanced/fhir-and-interoperability.md`
- [x] Security — `advanced/security.md`

### People

- [x] Community — `basics/community.md` (replaces/expands Sources of Help)
- [x] Career and Context — `basics/career-and-context.md`

### Removals

- [x] Flask section — gone
- [x] Donate page — replaced by `contribute.md`

---

## v1.1+ backlog (from old todo.md and scratch-notes.md)

### Cloud and infrastructure

- [ ] What is the cloud?
- [ ] Using the cloud
- [ ] Static sites
- [ ] What are servers? (basics-level)
- [ ] Workarounds for IT-blocked environments — Codeanywhere, GitHub Codespaces
- [ ] Continuous integration (dedicated treatment, beyond mentions in other chapters)
- [ ] Deployment patterns

### Languages and fundamentals

- [ ] Types of languages (interpreted vs compiled, static vs dynamic typing)
- [ ] Compilation — what it is and when it matters
- [ ] Frontend — JavaScript, HTML, CSS as a basics-level chapter
- [ ] Browser console — what it is, how to use it
- [ ] Debugging ("debuggering") — practical techniques

### Databases

- [ ] Databases chapter — Use PostgreSQL by default; know about Neo4j (graph) and MongoDB (document)

### Clinical software patterns

- [ ] Clinical Software Patterns — design patterns for healthcare; checklists
- [ ] Avoid Unnecessary Mappings (the '1 = male, 2 = female' anti-pattern)
- [ ] Avoid Unnecessary Abbreviations and Acronyms
- [ ] Clinical Calculators chapter — reference Rhidian Bramley's blog: <https://clinicalwebportal.home.blog/2019/07/23/clinical-calculators/>
- [ ] Integration patterns

### Workflow and people skills

- [ ] Git Workflow Checklist (fetch, branch hygiene, feature branches, commit messages)
- [ ] Code review practice
- [ ] Pair programming

### Working as a clinician-developer

- [ ] Charging for your time / consulting
- [ ] Apply for grants
- [ ] Build what you care about
- [ ] Working in open source (deeper than current basics chapter)

### Talking about your work

- [ ] Show Your Work (Austin Kleon-style chapter)
- [ ] Screenshotting
- [ ] Blogging
- [ ] Video recording / editing
- [ ] Audio editing
- [ ] Image editing
- [ ] Excalidraw
- [ ] reveal.js for presentations

### Community contributions

- [ ] Teach others
- [ ] Informal 'training posts' as a CPD route
- [ ] Wiki / forum patterns for community building

### Other

- [ ] Royal Colleges 3.0 — best practice as code
- [ ] Resources page including Interop Summit YouTube channel
- [ ] Acknowledgements page (existing names from scratch notes: Josh Case (Code Blue), Ian McNicoll, Mark Bailey, Louise Wilson & Kevin Monk)

---

## Stretch goals

- [ ] Community contributions chapter — invite PRs from conference attendees
- [ ] Case studies — real clinician-built tools (with permission)
- [ ] Additional forewords from community members

---

## Reference repos (style and content)

- <https://github.com/pacharanero/SAFETY.md>
- <https://github.com/github/scripts-to-rule-them-all>
- <https://github.com/rcpch/> — best-practice exemplars for clinical Django apps

---

## Snapshot: what's left for v1.0

The fastest path to v1.0 from here, in priority order:

1. **Marcus's editing pass** over the 13 new scaffolded chapters. They are first drafts; Marcus's voice and personal anecdotes need adding.
2. **Resolve open questions in [`queries.md`](queries.md)** (the `s/` vs `script/` call, where FastAPI sits in the nav, etc.).
3. **Finish the existing-content review list above**, especially `advanced/legals.md` (deduplicate against new MDR chapter) and `advanced/nhs-it.md` (current landscape).
4. **Fill the obvious stubs**: `about.md`, `getting-started/workplace.md`, `introduction.md`'s ATLS Story section.
5. **Link-check pass** before tag.
6. **Add `LICENSE`, `CODE_OF_CONDUCT.md`**.
7. **Tag v0.9** for community soak; **tag v1.0** at the conference.
