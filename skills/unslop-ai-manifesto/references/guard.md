# Guard

A mistake seen twice gets a guardrail, so no reviewer has to catch it a third time.

## Choose the check

For each slop class with two or more findings, pick the cheapest check that catches it, in this order:

1. A stricter compiler or type setting.
2. A rule in the project's existing linter (unused code, type escapes, lint disables, console output, duplicate imports).
3. The dead-code tool from the audit, run in the project's lint or CI script.
4. A test that reproduces a bug the subtract mode fixed.
5. A small script in the repo's scripts folder, wired into the lint or CI script.

What no tool can see goes into the project's lessons or agent instruction file as one positive line, in the file the agent already reads.

## Enable it

- Run the check on the cleaned code first. Enable it only when it passes, or when every remaining hit is a finding the user chose to keep, written as a reviewed exception.
- Wire it into the lint, test or CI command the project already runs.
- Make each failure message name the fix, such as the shared helper to use instead.

Guard is done when every class with two or more findings has an enabled, passing check or a written reason it has none, and the baseline still holds.
