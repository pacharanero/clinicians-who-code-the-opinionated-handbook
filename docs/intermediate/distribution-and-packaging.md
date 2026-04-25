# Distribution and Packaging

The point of writing software is for someone to use it. Packaging is how you cross the gap between 'it works on my machine' and 'someone else can run it'.

For a clinician-developer, packaging well matters more than for a typical developer. The people you most want to reach (other clinicians) are usually not equipped to debug a broken `pip install`. If installation fails, they don't try harder, they walk away.

## Why packaging matters

A few specific reasons it matters in clinical software:

- **Reproducibility.** A packaged version of your software has known dependencies and a known version. The output is reproducible. For clinical software, reproducibility is a safety property.
- **Safety.** A user installing your tool by copying source code from GitHub gets whatever HEAD currently is, including any half-finished changes. A user installing a release gets the version you signed off as fit for purpose.
- **Shareability.** If installation is one command, your tool can spread. If installation requires a half-day of fiddling, it won't.
- **Audit trail.** Versioned releases mean you can answer the question 'what version was running on the day of the incident?'. Source-from-GitHub installs can't.

## Python packaging

The modern Python packaging story is much better than it used to be. The pieces:

- **`pyproject.toml`** is the single configuration file. Project metadata, dependencies, build system, tool configuration. Everything in one place.
- **A build backend** turns your source into a distributable artefact. Hatchling, Setuptools, Poetry, and PDM are all reasonable choices. Hatchling is a sensible default.
- **A package index.** PyPI is the canonical public index. For internal NHS work, you may want a private index (Artifactory, AWS CodeArtifact, etc.).
- **`uv` or `pip`** install packages on the user's machine.
- **`pipx`** installs Python applications (CLIs) in their own isolated environments, avoiding dependency conflicts. If you're shipping a CLI for clinicians, recommend `pipx`.

A minimal `pyproject.toml` for a CLI:

```toml
[project]
name = "ckd-epi-calculator"
version = "0.1.0"
description = "Calculate eGFR using CKD-EPI 2021"
requires-python = ">=3.11"
dependencies = ["click>=8.0"]

[project.scripts]
ckd-epi = "ckd_epi.cli:main"

[build-system]
requires = ["hatchling"]
build-backend = "hatchling.build"
```

`pip install .` from the source, or `python -m build` to produce a wheel for distribution. `pipx install ckd-epi-calculator` once it's on PyPI.

## Rust packaging

Rust's packaging story is, to be blunt, easier than Python's.

- **`Cargo.toml`** is the project file.
- **`cargo build --release`** produces a single statically-linked binary.
- **`cargo install`** installs from source for users who have Rust.
- **`crates.io`** is the public package index for libraries.
- **GitHub Releases** is where you publish pre-built binaries for users who don't have Rust.

A clinician downloading your Rust tool might not have Rust installed. Build binaries for Linux, macOS (Intel and Apple Silicon), and Windows in CI, and attach them to a GitHub Release. A one-line `curl` install becomes possible.

## Docker

Use Docker when:

- The software has non-trivial system dependencies (databases, native libraries, specific OS versions).
- You're deploying server-side and want reproducible deployments.
- You want to ship a complete environment, not just a Python or Rust binary.

Don't use Docker when:

- You're shipping a simple CLI to end users. A binary or a `pipx`-installable package is friendlier.
- The user is a clinician on a Windows laptop with no Docker experience. The barrier to entry is too high.

For server deployments, write a clean `Dockerfile`, build a tagged image in CI, push to a registry (GitHub Container Registry, Docker Hub, your organisation's registry), and deploy from there.

## Versioning and changelogs

**Use Semantic Versioning** (`MAJOR.MINOR.PATCH`) unless you have a strong reason not to. <https://semver.org/>

- `MAJOR` for breaking changes.
- `MINOR` for new functionality, backwards-compatible.
- `PATCH` for bug fixes, backwards-compatible.

For pre-`1.0` software (which is most personal projects), the rules are looser, but the discipline of thinking about it is valuable.

**Keep a CHANGELOG.md.** The format from <https://keepachangelog.com/> is a good default: a section per release, grouped into Added, Changed, Deprecated, Removed, Fixed, Security.

For clinical software, the changelog is part of the audit trail. 'What changed in v1.4.2 that might explain the incident on Tuesday?' becomes a single-file lookup, not a Git archaeology project.

## Making your tool easy for other clinicians to install

Some practical guidance, in priority order:

1. **One command to install.** `pipx install your-tool`, or `cargo install your-tool`, or `curl https://example.com/install.sh | sh`. Anything more is a barrier.
2. **One command to run.** After install, `your-tool --help` should work. Default behaviour should be useful.
3. **No extra accounts or services.** Don't require a sign-up, an API key, or a database. If those are unavoidable, document the smallest possible setup.
4. **Cross-platform.** Most clinicians are on Windows. Test on Windows. If you can't, say so in the README.
5. **A real README.** Installation, a worked example, what to do when it goes wrong, where to file bugs.

The best test of your packaging is to ask a friend to install it on a machine they've never set up for development. Watch them do it without offering help. The frustrations you observe are bugs.

## Cross-references

- [Documentation](documentation.md) for what should accompany a release.
- [Scripts To Rule Them All](scripts-to-rule-them-all.md) for the developer-side equivalent.
