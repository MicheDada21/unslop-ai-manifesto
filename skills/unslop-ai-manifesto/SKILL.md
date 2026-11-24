---
name: unslop-ai-manifesto
description: "Subtracts slop from a repository, from dead code and stacked workarounds to stale agent docs, in small batches that keep behavior, then adds guardrails. Use when refactoring a repo or cleaning up after agents."
---

# Unslop AI manifesto

Slop is anything that costs its next reader more effort than went into making it: code, tests, comments, docs, agent instructions. In a repository it compounds, because every agent reads what is there and copies it. This skill subtracts slop, keeps behavior identical and hands the user batches they can review in minutes.

## Modes

Pick the mode from the request. With no mode named, run them in this order and stop after audit for the user's approval.

| Mode | Does | Done when | Read |
| --- | --- | --- | --- |
| interview | Settles scope, stakes and what the user reviews | No open question would change what gets edited | Interview, below |
| audit | Read-only inventory of slop with evidence, ranked by impact | Every slop class is swept across the scope and every finding carries evidence, confidence and rank | [references/audit.md](references/audit.md) |
| subtract | Removes and consolidates code in behavior-preserving batches | Every approved code finding is fixed or reported as left, and the baseline still holds | [references/subtract.md](references/subtract.md) |
| context | Cleans what the next agent reads: agent instruction files, comments, docs, examples, task notes | Every agent-read file is true for the current code and states each rule once | [references/context.md](references/context.md) |
| guard | Turns recurring findings into automated checks | Every finding class seen twice has an enabled, passing check, or a stated reason it has none | [references/guard.md](references/guard.md) |

## Rules for every mode

- Before deciding anything, read the repo's agent instruction files, its README, its lessons or decisions files and two neighbors of each file you touch. Match their conventions.
- Establish a **baseline** before the first edit: run the project's existing build, typecheck, lint and test commands and record which pass. A batch holds the baseline when the same set still passes. Proof is the command output, quoted in the report.
- Aim for the smallest change that meets the intent. Deleting beats rewriting; consolidating into the best existing implementation beats writing a new one.
- Keep behavior identical: public APIs, exports, CLI flags, URLs, env vars, data schemas and user-visible output. A bug or behavior change you discover becomes a finding for the user, fixed only with their approval.
- Treat high-stakes code (auth, payments, permissions, data migrations, security) as report-only: list its findings and edit it only for the items the user approves one by one.
- Hand off what another skill owns, when it is installed: design tokens and repeated UI to `design-system-refactor`, the README to `clear-vision-readme`. Without the skill, and for dependency upgrades, list the finding for the user.
- When delegation is available, give the audit's heavy reading to fresh-context helpers, one per area, with the slop classes from the audit reference. Keep edits to one writing agent at a time.
- Each batch is one theme and one commit whose message states the effect; commit and push as the project's delivery policy says.

## Interview

Read the repo first and ask only what it leaves open. Ask through the client's question widget, up to 4 closed questions per round, each with a recommended option first and room for free text; with no widget, a short numbered list. Cover:

1. Scope: the whole repo or named paths, and which areas are frozen.
2. Outcomes: the user flows or commands that must keep working, which become the targeted checks of each batch.
3. Stakes: which areas count as high-stakes beyond the list above, and whether a prototype or throwaway area should be skipped.
4. Review: whether the user approves only the audit plan or each batch too.

## Report

The report must cost the user less attention than the work took, so it fits on one screen.

- After audit: up to 10 findings, highest impact first, one line each with the class, rank, confidence, the place, why it costs the next reader and the proposed fix; high-stakes findings carry `report-only`. Under them, one line with the count of lower-ranked findings left out and one coverage line. Then ask which findings to fix, through the question widget.
- After each batch: one line with the commit, the baseline result and the measured change (lines and files removed, dependencies dropped, checks added).
- At the end: the measured totals, the findings left and why, and the checks the guard mode added.

Inspired by [No AI Slop: A Manifesto](https://slopmanifesto.com), written by the speakers and attendees of AIE Code Summit 2026.
