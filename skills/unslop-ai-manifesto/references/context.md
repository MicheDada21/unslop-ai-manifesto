# Context

Clean what the next agent reads before it writes code: agent instruction files (`AGENTS.md`, `CLAUDE.md`, editor rule folders, Copilot instructions), docs folders, code comments, example files and task or plan notes. Slop here spreads fastest, because agents copy it into new code.

## Rules

- Check every claim against the repo: the command exists in the scripts, the path exists, the behavior matches the code. Fix or delete each claim that fails.
- Keep each rule in one place. When two files say the same thing, keep it in the file the other one already points to, and replace the copy with a pointer or delete it.
- Delete what restates the environment: script lists, dependency lists, directory trees an agent can read in one command. Keep what the agent cannot find by looking: conventions, the reasons behind choices, gotchas.
- Rewrite prohibitions as the behavior wanted, so the file names what to do.
- Keep comments that say why; delete comments that say what the next line does.
- Delete plan, summary and notes files for work that has shipped. Keep open work in the project's task file.
- Leave the README to `clear-vision-readme` when it is installed; otherwise fix only false claims in it.

Context is done when every agent-read file in scope is true for the current code and states each rule once.
