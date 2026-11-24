# Audit

Read-only. Nothing changes until the user approves the findings. Audit the tracked files; among untracked files, look only at notes and output sitting in folders an agent reads.

## Reading depth

Read in full: the entry points, the agent instruction files and the folders they point to, the largest source files, and the files touched most often by fix commits (`git log --grep` for fix, bug, workaround). Sweep the rest of the scope with searches, one per slop class. The report states which areas were read and which were only searched.

When the repo already lists a problem in its task or backlog file, cite it as known in one line instead of ranking it as new.

## Slop classes

Sweep every class across the whole scope. A class name is the finding's label in the report.

1. **Dead**: unused files, exports and dependencies; flags that are always on or always off; commented-out code; unreachable branches. When the project already has a dead-code tool installed (knip for JS/TS, vulture for Python), run it; otherwise search for imports by module path and by basename. Files a framework loads by convention (routes, server functions, migrations, config, tests) count as dead only when nothing registers or calls them.
2. **Workaround**: a symptom patched instead of its cause. Swallowed errors, retries or sleeps around a race, type escapes (`any`, `@ts-ignore`, `# type: ignore`), lint disables, null checks for values the types guarantee, output fixed in a second place instead of at the source, a special case for one ID or one input. A catch around untrusted input or a call that handles its failure is intended. Report the root cause once with the number of sites, and name the worst files.
3. **Duplicate**: several implementations of one concept, helpers rewritten per file, blocks copied three or more times. Two copies stay inline.
4. **Hollow layer**: a wrapper that only passes calls through, an abstraction with one implementation and no second in sight, configuration for a value nobody changes.
5. **Noise**: comments that restate the code, debug logging and scripts left from past investigations, TODOs with no decision behind them, scaffolding never filled in.
6. **Agent residue**: plan, summary and handoff notes from past sessions; committed investigation output (browser logs, generated PDFs, scratch scripts); the same rule repeated across instruction files; docs and comments that describe behavior the code no longer has.
7. **Hollow test**: a test that asserts its own mocks, a snapshot nobody reads, a skipped test, two tests that check the same thing.

A class with no findings goes into the coverage line of the report.

A tracked file that holds credentials is a high-stakes finding: name the file and never print its contents.

## Evidence and confidence

Every finding carries `file:line` and how you verified it: tool output, a search with zero hits, a `git log` line. Tag each one:

- **verified**: the evidence settles it.
- **likely**: the evidence points one way, but something outside the repo could still use or need it (an external caller of a route, a migration that may not have run).
- **uncertain**: only the user can settle it.

## Rank

- **high**: on a path the next reader meets in normal work (an entry point, a shared module, an agent instruction file), or actively misleading there.
- **medium**: misleading, but off the main path.
- **low**: clutter that costs a glance.

Within a rank, misleading findings come before clutter, and verified before likely.

The audit is done when every class has been swept across the whole scope, every finding carries evidence, confidence and rank, the high-stakes findings are marked report-only, and the coverage line names what was read and what was only searched.
