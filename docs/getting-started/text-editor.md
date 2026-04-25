# Which text editor?

Another source of needless options paralysis. Let's end it now.

## Use VS Code

Microsoft's Visual Studio Code (VS Code) has won. It's free, open source, fast, stable, well-maintained, and has by far the largest extension ecosystem. Most tutorials assume you're using it. Most of the AI coding tools either are VS Code or are forks of VS Code.

For a clinician-developer just starting out, the answer is VS Code. Don't agonise.

Download: <https://code.visualstudio.com/download>

### Suggested VS Code extensions

Don't install all of these on day one. Install the first few and add the others as you start using the relevant tools.

- **Python** (Microsoft) — essential for Python work.
- **Pylance** — fast type checking for Python.
- **Ruff** — Python linting and formatting.
- **GitLens** — supercharges the Git integration.
- **GitHub Pull Requests** — review and respond to PRs without leaving the editor.
- **Markdown All In One** — for writing notes and docs.
- **Markdown Preview GitHub Styling** — see your Markdown the way GitHub will render it.
- **YAML** — for config files, CI workflows, Docker Compose.
- **Docker** — for working with containers.
- **rust-analyzer** — when you start writing Rust.
- **Live Share** — for remote pair programming.

For visual themes, I use Solarized Dark almost everywhere. Pick something easy on the eyes; you're going to spend a lot of hours looking at it.

## AI-assisted editors

The biggest change in the last two years is the rise of AI-assisted editors. These either are VS Code with AI features bolted on, or are forks of VS Code with deeper AI integration:

- **GitHub Copilot.** The original AI pair programmer, integrated into VS Code as an extension. Rapidly improved from the autocomplete it started as. A safe default if you want AI assistance without leaving the standard VS Code.
- **Cursor.** A fork of VS Code with much deeper AI integration. Multi-file changes, agent mode, codebase-wide context. Many serious developers I know have switched.
- **Windsurf** (formerly Codeium). Another AI-first fork in the same space as Cursor. Different design philosophy, similar capabilities.
- **Claude Code.** Not an editor as such, but a terminal-based AI coding assistant from Anthropic. Runs alongside whatever editor you use. Increasingly my own default for substantial tasks because it can run commands, read files, and iterate without me having to copy-paste.

You don't have to commit to one. Many clinician-developers I know use VS Code with Copilot for most editing, and reach for Claude Code or Cursor for larger tasks. The right combination depends on how you like to work.

For more on using these tools well, see [AI-Assisted Development](../advanced/ai-assisted-development.md).

## Learn `nano` for when there is no GUI

Sometimes you'll need to edit a configuration file on a remote server through SSH. There's no GUI, just a terminal. You can't open VS Code.

Learn `nano`. It's available on essentially every Linux server. It's not the most powerful terminal editor (vim and emacs both have more capability), but it's by far the easiest to use, and for the rare edits you'll do on remote servers, ease beats power.

To edit a file:

```bash
nano <FILENAME>
```

- If the file doesn't exist, it'll be created.
- Navigate with the arrow keys. Normal typing works as you'd expect.
- ++ctrl+k++ deletes a whole line.
- ++ctrl+o++ saves.
- ++ctrl+x++ exits.
- If you can't save, the file is probably owned by root. Run with `sudo nano <FILENAME>`.

That's enough nano to get by.

## What about vim, emacs, neovim?

If you already use one of these, keep using it. The ecosystem (LSP, AI integrations, plugin managers) for vim and neovim is genuinely good, and many serious developers swear by them.

If you don't already use one, don't start now. The learning curve is steep, the productivity gain (relative to a well-configured VS Code) is small, and the time is better spent learning to code or building something. Maybe in a few years.

## Don't hop between editors

A common trap when starting out is to spend a week on VS Code, get frustrated, try Cursor, then Sublime Text, then PyCharm, then back to VS Code. Each switch costs days.

Pick one (VS Code), commit to it for at least three months, and learn its keyboard shortcuts and configuration. You will be more productive than someone who has lightly tried five editors.

!!! tip "Tip: don't invent anything; transplant ideas from elsewhere"
    Look at how the 'real' industry (outside of healthcare) solves generic problems, and bring those solutions into healthcare technology. That's most of what I'm doing most of the time. Examples: open RFC standards, version control, automation, open source.

    Note also where healthcare culture has got it right, and the tech industry should be learning from us. The 'precautionary principle' (proving something is safe before using it widely) is how we do Evidence Based Medicine, and is sadly not widely practised in much of the tech industry, where 'move fast and break stuff' was an actual maxim.
