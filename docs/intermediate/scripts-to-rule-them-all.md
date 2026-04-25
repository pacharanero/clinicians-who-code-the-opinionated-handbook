# Scripts To Rule Them All

Every repository should have a single, predictable way to do the common things: set up the project, run the tests, start the server, open a console.

The pattern is called Scripts To Rule Them All, originally documented by GitHub: <https://github.com/github/scripts-to-rule-them-all>.

## The pattern

A directory at the root of the repository, containing small scripts with standardised names. Anyone with a working terminal can clone the repo and run these scripts without reading the README first.

The canonical names from the GitHub original:

- `script/bootstrap` — install dependencies, set up the environment from scratch.
- `script/setup` — first-time-only setup (database creation, seed data).
- `script/update` — pull updates and bring the environment in line with current dependencies.
- `script/server` — start the dev server.
- `script/test` — run the test suite.
- `script/console` — open a REPL with the app context loaded.
- `script/cibuild` — what CI runs.

I personally use a single-letter directory `s/` instead of `script/`, because I type it a lot. Pick whichever you prefer; the key is consistency *across your own repos*.

## Why this matters

You will work on dozens of repositories over your time as a clinician-developer. Some you wrote, some you didn't, some you wrote two years ago and don't remember.

If every repo follows the same convention, you can:

- Clone any project and run `./s/test` (or `./script/test`) to see if you've got it working, before reading anything.
- Onboard collaborators in one command: `./s/bootstrap`.
- Move between repos all day without context-switching the build system in your head.

Without the convention, every repo has its own shape. One uses `make test`, another uses `pytest`, another wants you to remember the `--config tests/local.yaml` flag. Each context switch is friction.

## What the scripts contain

The scripts themselves are usually very short. They're wrappers, not implementations. The real work is in `make`, `pytest`, `pip`, `docker compose`, or whatever your project actually uses. The scripts give those tools a stable, project-agnostic interface.

A `s/test` for a Python project might be:

```bash
#!/usr/bin/env bash
set -euo pipefail
cd "$(dirname "$0")/.."
exec uv run pytest "$@"
```

Three lines of meaningful content. The `set -euo pipefail` makes sure failures actually fail. The `cd` makes the script work from anywhere. The `exec` lets pytest take over the process so signals work properly.

A `s/bootstrap` for the same project might:

- Check `python --version` is acceptable.
- Install `uv` if missing.
- Run `uv sync` to install dependencies.
- Copy `.env.example` to `.env` if `.env` doesn't exist.
- Print a one-line "you're ready, run `./s/server`" message.

Make the scripts loud about what they're doing and quiet when there's nothing to say.

## Make them executable, commit them to the repo

Set the executable bit (`chmod +x s/*`) and commit it. This is one of the few cases where file modes really do matter and Git tracks them.

If you're on Windows, scripts can be Bash for use in WSL, or PowerShell for native Windows, or both. For NHS work, assume some collaborators are on Windows and document accordingly.

## Doctor: an honourable mention

GitHub's original convention also includes `script/server` and `script/cibuild`. Some teams add `script/doctor`, which checks that everything needed to develop the project is present and prints actionable messages if not (right Python version, right Node version, Docker running, etc.). A `doctor` script that prints "your `gh` CLI isn't installed; run `brew install gh` to fix this" pays for itself within hours of a new collaborator joining.

## Documenting it

The README of any repo with this convention should have a short section near the top:

```markdown
## Quick start

    ./s/bootstrap   # install dependencies
    ./s/server      # start the dev server
    ./s/test        # run tests
```

That's the entire setup section. The scripts are the documentation.

## Cross-references

- [Distribution and Packaging](distribution-and-packaging.md) for shipping the finished product.
- [Documentation](documentation.md) for the wider documentation strategy.
