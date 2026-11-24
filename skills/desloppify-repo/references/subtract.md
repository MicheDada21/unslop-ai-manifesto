# Subtract

Work through the approved code findings from highest impact down, one batch at a time.

## One batch

1. Group approved findings of one class and one area into a batch a reviewer can read in a few minutes: up to about 200 added or changed lines. Pure deletions can run larger, because they are quick to review.
2. For a **workaround**, fix the cause at its source, then remove every site that worked around it. A fix at the source that changes behavior ends the batch and goes to the user as a finding.
3. For a **duplicate**, keep the implementation with the best tests and the most callers, move every caller to it and delete the others.
4. For **dead** code, delete it outright; git keeps the history.
5. Run the baseline commands plus a targeted check of the flows the interview named that pass through the batch: run the command, call the route, run the test that covers it.
6. Commit the batch as the project's delivery policy says, with a message that states the effect.

A batch is done when the baseline still holds, the targeted check shows the same output as before, and the commit exists.

## When a batch breaks

Diagnose for up to 3 focused rounds. When the baseline still fails after the third, revert the batch, report the finding as left with the failing output, and move to the next batch.
