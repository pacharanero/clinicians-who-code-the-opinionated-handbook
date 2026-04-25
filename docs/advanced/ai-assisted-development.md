# AI-Assisted Development

The biggest change in software development since I wrote the first version of this handbook is that the computer now writes a lot of the code.

For a clinician-developer, this is unambiguously good news. The bottleneck has always been time and typing speed, not ideas. AI-assisted development gives you back the time and removes most of the typing.

It also introduces new failure modes that matter especially in clinical software.

## What is 'vibe coding'?

The term 'vibe coding' was coined for the practice of describing what you want in natural language and letting the AI write the code, without reading every line. It's enormously productive for prototypes and personal tools.

It is **not** a safe practice for clinical software. For clinical code, you read every line, run every test, and reason about every edge case, just like you always did. The AI helps you write faster; it does not absolve you of understanding the code.

I prefer the term 'quality vibe engineering' for the disciplined version: AI does the typing, the human does the thinking, the tests do the proving.

## The tools

The landscape changes monthly. As of writing, the serious contenders for clinician-developers are:

- **Claude Code** (Anthropic). Terminal-based, agentic. Excellent for working in existing codebases, planning multi-file changes, running tests, and iterating. My personal default.
- **Cursor**. A fork of VS Code with deep AI integration. Familiar editor experience with strong AI features.
- **GitHub Copilot**. The original. Now significantly more capable than the autocomplete it started as. Tightly integrated with VS Code and GitHub.
- **Windsurf** (formerly Codeium). Another AI-first editor in the same space as Cursor.

You don't need to pick one and stick with it. Most clinician-developers I know use two or three for different tasks.

## How to use AI tools well

**Treat the AI as a junior developer who never sleeps.** It is fast, it is capable, it gets things wrong in surprising ways. It needs supervision and clear instructions. Give it small, well-scoped tasks and review the output.

**Read the diff.** Always. Especially in clinical code. The AI will sometimes write code that looks plausible but does the wrong thing in an edge case. Reading the diff is non-negotiable.

**Make the tests do the work.** Before letting the AI change a function, make sure the function has tests. The tests are how you'll know if the AI broke something. This is a virtuous cycle: AI tools also write very good tests.

**Use it for the boring stuff first.** Boilerplate, refactoring, writing tests, generating documentation, writing migration scripts. These are tasks where the AI is reliably faster than you and the cost of a mistake is low.

**Use it for the scary stuff carefully.** Clinical calculations, dose calculators, decision logic. The AI can write these too, but you need to validate the output against the clinical source of truth, not just check that the tests pass. Tests can be wrong if the AI wrote them based on a misunderstanding.

**Give it context.** Most AI coding tools support a per-project instructions file: `CLAUDE.md`, `AGENTS.md`, `.cursorrules`, and similar. Write one. Tell the AI what the project is, what conventions it should follow, what patterns to avoid. A pattern I use is to keep the real instructions in `agent-instructions.md` and have the vendor-specific files just point at that, so I'm not maintaining four copies.

## Prompt engineering for code generation

A few patterns that consistently produce better results:

- **State the constraints, not just the goal.** 'Write a function that calculates eGFR using CKD-EPI 2021, takes serum creatinine in µmol/L, returns a value in mL/min/1.73m², and raises if creatinine is <= 0.'
- **Reference the source of truth.** 'Use the formula from the NICE guideline NG203, not the older MDRD formula.' Better, paste the formula directly.
- **Ask for tests.** 'Write the tests first, then the implementation.' Test-driven prompting tends to produce more correct code.
- **Ask for the simplest thing that works.** AIs love to over-engineer. Ask for the smallest implementation, then add complexity only when needed.
- **Iterate.** The first answer is rarely the final answer. Treat the AI like a pair programmer: refine, push back, ask for alternatives.

## When to trust AI output and when not to

Trust it (with review) for:

- Boilerplate and scaffolding.
- Writing tests for code you wrote.
- Refactoring within a single file.
- Writing documentation from existing code.
- Translating between languages or frameworks.
- Explaining unfamiliar code.

Be cautious for:

- Multi-file changes that touch core business logic.
- Anything involving clinical calculations or decision logic.
- Security-sensitive code (authentication, cryptography, input validation).
- Code that runs against real patient data.

Validate independently for:

- Clinical formulas (check the source).
- Anything that produces a number that will be acted on clinically.
- Anything new from an AI that confidently cites a library, function, or API. AIs hallucinate APIs that don't exist.

## Clinical safety implications

AI-generated code is still your responsibility. The hazard log doesn't get a 'the AI wrote it' column.

A few specific risks worth naming:

- **Hallucinated APIs.** The AI invents a function that doesn't exist, the code looks fine, the tests miss it. Run the code.
- **Plausible-but-wrong formulas.** The AI confidently uses a formula that's close but not correct. Validate against the clinical source.
- **Silent assumption changes.** A refactor changes a default value or units conversion in a way that's correct in the new context but not the old.
- **Test pollution.** The AI writes a test that asserts the buggy behaviour, the test passes, you don't notice.

The mitigation in every case is the same: read the code, run the tests, and validate against an external source of truth for anything clinically significant.

## AI and open source licensing

AI training data includes large amounts of open source code under various licences. The legal status of AI-generated output is contested and evolving. A few practical points:

- If you're contributing AI-generated code to an open source project, check the project's contribution policy.
- Be cautious about asking an AI to reproduce 'well-known' code or algorithms that may be under restrictive licences.
- For commercial work, check your AI tool vendor's IP indemnification position. Some tools offer it, some don't.

This area is changing fast. By the time you read this, some of the answers will have moved on. The principle that holds: be honest about what's AI-generated and where it came from.
