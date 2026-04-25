# Keeping Notes

Note-keeping is a developer practice. For a clinician-developer, it is a clinical safety practice too.

## Why notes

The brain is a poor long-term store. The best mental model of your project from six months ago is gone. You can rebuild some of it from the code, but the *why* (why this approach, why this trade-off, why this library and not the other one) is rarely in the code itself. It needs to be written down.

A few specific cases:

- **Decision logs.** When you chose Django over FastAPI for a project, or PostgreSQL over MySQL, the reasoning at the time mattered. In a year, you'll be tempted to change the choice without remembering why you made it.
- **Audit trails.** For clinical software, you may need to demonstrate why a decision was made and when. Notes in version control provide this for free.
- **The thing that bit you last time.** A bug took you three days to find. The next time you see it, you don't want to spend three days again.
- **Onboarding yourself.** A project you haven't touched for a year is a stranger's project. Notes are how past-you talks to future-you.

## Plain files on disk

The longest-lived format is also the simplest. **Markdown files in a Git repository.**

- They open in any text editor.
- They render well on GitHub, in your IDE, in Obsidian, on the command line.
- They version cleanly. `git diff` on a Markdown file is readable.
- They will still be readable in twenty years, which is more than I can say for any cloud note app I have used.

Avoid:

- Notes in proprietary apps that lock the data behind an export menu.
- Notes in cloud services that may not exist in five years.
- Notes in handwriting on paper. They will be lost. The exception is during a meeting where opening a laptop is rude; transcribe into Markdown afterwards.

## Markdown everywhere

Markdown is the lingua franca of developer notes. Use it for:

- Personal notes (a single repo of `.md` files works well).
- Project README and supporting docs (`README.md`, `CONTRIBUTING.md`, `SAFETY.md`).
- Architecture Decision Records (ADRs).
- Meeting notes you want to keep.
- Drafts for blog posts, presentations, papers.

If you find yourself in a situation where you can't use Markdown, write the note in a plain `.txt` file or a comment in code rather than reaching for Word.

## Tools

- **VS Code** (or your text editor of choice). Notes alongside code. No app to switch to.
- **Obsidian.** Plain Markdown files on disk, with linking, tagging, search, and a graph view layered on top. Good for a personal knowledge base.
- **Claude Code (or another AI tool) as a thinking partner.** Talking through a decision with an AI, then asking it to write up the conclusion as a note, is a productive workflow. Write the conclusion yourself; let the AI do the formatting.
- **Logseq** if you prefer outliner-style note-taking.

The choice of tool matters less than the discipline of writing things down at all.

## Architecture Decision Records (ADRs)

For any project that's going to live for more than a few months, keep a `docs/adr/` directory with one Markdown file per significant decision. The format is light:

```markdown
# ADR 0007: Use Django for the new patient portal

Date: 2026-04-15
Status: Accepted

## Context

We need a patient-facing portal with user accounts, an admin interface,
and a relatively simple data model. The team is small (one developer,
me) and the deadline is six months.

## Decision

Use Django.

## Consequences

- Faster to a working prototype than FastAPI plus a separate frontend.
- Comes with auth, admin, ORM, templates out of the box.
- Server-rendered HTML is fine for this use case.
- If we need a separate API later, we can add Django REST Framework or
  bolt on a FastAPI service.
```

That's the whole ADR. It takes ten minutes to write and saves hours of 'wait, why did we...' a year later.

## Note-keeping in the context of clinical projects

For clinical projects, the bar is higher than personal note-keeping.

- **The hazard log is a kind of note.** See [SAFETY.md](../advanced/safety-md.md).
- **Decision records are evidence.** A regulator may ask why you chose to handle a particular clinical scenario in a particular way. An ADR with a date and a rationale is a strong answer.
- **Incident notes are essential.** When something goes wrong, the contemporaneous notes are part of the incident record. Write them while it's happening, not from memory afterwards.
- **Meeting notes for clinical sign-off** should be saved to the project repo, not lost in someone's email.

In short: if it might matter for safety or compliance, it goes in version control.

## A simple personal practice

A pattern I'd recommend:

- One `notes/` directory in your home, version-controlled.
- One file per topic, named in `slug-case.md`.
- A `daily/` subdirectory with one file per day for working notes.
- A `decisions/` subdirectory for personal ADRs.

Sync via Git, back up to a private remote. Search with `ripgrep` or your editor.

You'll never regret writing a note. You'll regret not writing one, eventually.
