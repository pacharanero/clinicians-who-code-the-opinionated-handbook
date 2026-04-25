# Queries for Marcus

Open questions and decisions left over from the Phase 3 content scaffold. Resolve as you do the editing pass.

## Decisions / divergences from the spec

1. **`s/` vs `script/` for the Scripts To Rule Them All chapter.**
   The spec uses the upstream GitHub convention name `script/`. Your own repos consistently use the shorter `s/` (medical-markdown, security, rcpch-audit-engine, new-repo-template all use `s/`). I wrote the chapter recommending `s/` because that's what you actually do, and noted the upstream convention is `script/`. Confirm or override.

2. **`new-repo-template` does NOT yet have an `s/` directory** despite being your template. Suggests the convention isn't yet baked in to your scaffold. Worth fixing in that repo if you genuinely advocate for it in the handbook.

3. **Where does FastAPI live in the nav?**
   I put it under Getting Started (next to Web Frameworks, Learning Django). The spec lists it under Languages. It could equally sit in Intermediate. Move if you'd prefer.

4. **`basics/community.md` vs `basics/support.md`.**
   The spec said "Community (new - replaces/expands Sources of Help)". I left both pages and made them complementary: support.md is "stuck on a technical problem, where to look" and community.md is "where are my people". You may prefer to merge them or delete support.md.

5. **`docs/about.md` is a stub.**
   Currently just "Marcus Baw — Is a GP". Needs writing. Spec didn't explicitly call it out for rewrite. Left alone.

6. **`docs/foreword.md`, `docs/introduction.md`, `docs/Thoughts-from-Mark-Bailey.md`** — not touched in this pass.
   - `introduction.md` has placeholder bullets in the ATLS Story section that need finishing.
   - `Thoughts-from-Mark-Bailey.md` is guest content; not edited.
   - `foreword.md` — also untouched.

7. **`Thoughts-from-Mark-Bailey.md` filename** uses Title-Case-Hyphens, against your global preference for `slug-case`. Renaming would break any inbound links. Left as-is. Decide whether to rename and fix any references.

## Existing pages flagged in the spec but not rewritten

The spec asks for review or update of several existing pages. I did substantive rewrites only of `text-editor.md` and `web-frameworks.md`. The following are still on the to-do list:

- `basics/glossary.md` — extend per spec.
- `basics/mantras.md` — review and extend per spec.
- `basics/open-source.md` — refresh with recent NHS examples per spec.
- `basics/usability.md` — review.
- `basics/focus.md`, `basics/conventions-in-this-book.md` — light review only needed.
- `getting-started/what-language.md` — update framing for AI-assisted era.
- `getting-started/why-python.md` — update.
- `getting-started/learning-python.md` — fix the truncated `pyenv` tip on line 45 ("...will automatically select your" — your what?). Update resources list. Note: the page currently embeds the glossary via the `--8<--` snippet syntax; check it still works in Zensical.
- `getting-started/learning-django.md` — review whether still the right Django recommendation.
- `getting-started/shell.md` — light review.
- `getting-started/workplace.md` — currently a 12-line stub. Needs writing.
- `intermediate/git.md` — update tooling references.
- `intermediate/rest-and-apis.md` — update for FastAPI focus, add FHIR R4/R5 link.
- `intermediate/documentation.md` — expand per spec; mention Zensical.
- `intermediate/managing-servers.md` — update for cloud/container era.
- `intermediate/accessories.md` — full rewrite per spec.
- `advanced/legals.md` — significant update per spec; substantial overlap now with the new `medical-device-regulation.md`. Consider merging or repositioning legals as a "you may also need to know about" companion.
- `advanced/nhs-it.md` — update for current landscape (ICBs, FDP, FHIR mandates).

## Content placeholders / things I had to guess at

These are statements in the new content where I made a reasonable guess but you should verify:

- **`fastapi.md`** — the eGFR example uses a placeholder calculation (`egfr = 100.0`). Replace with a real CKD-EPI 2021 implementation if you want it to be a more useful example.
- **`fhir-and-interoperability.md`** — I recommend `fhir.resources` (Pydantic-based) over `fhirclient`. Confirm this matches your view.
- **`security.md`** — I name `pip-audit`, `gitleaks`, `detect-secrets` as default tools. Substitute your preferred names if different.
- **`community.md`** — I describe several communities (Discord, Reddit, Bluesky) in general terms. Add specific server invites or @-handles where you have them.
- **`career-and-context.md`** — written in your voice but generic. Worth adding personal anecdotes if you want it to land harder.
- **`ai-assisted-development.md`** — I describe Claude Code as your "personal default". Confirm or change.
- **`medical-device-regulation.md`** — the CE/UKCA dates and EU MDR / UK regulation status are accurate as of writing but this area moves fast. Re-check before launch in June 2026.

## Things outside the spec but worth considering

- **Repo-root `README.md`** added. May want a banner image or shields (CI status, license).
- **`.editorconfig`** at the repo root would help future contributors keep consistent formatting.
- **`CODE_OF_CONDUCT.md`** for the repo since you're inviting community PRs.
- **`LICENSE` file** — worth confirming it exists and is the licence you intend.
- **`scratch-notes.md`** (formerly `docs/README.md`) contains substantial draft content for chapters that don't exist yet (Databases, Clinical Software Patterns, Avoid Unnecessary Mappings, Acknowledgements). Worth mining for content as you do the editing pass.
- **`todo.md`** (formerly `docs/todo.md`) — the items there are a fair plan for v1.0 → v1.1.
