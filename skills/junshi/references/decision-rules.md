# Decision Rules

Use this file when `军师` needs the heavier decision details without bloating the main skill text.

## In This File

- `Time Scale And Mode`
- `When To Call 谋士池`
- `Analysis Escalation`
- `Chain-Depth Checkpoint`
- `Technical Debt And Temporary Fixes`
- `Parallelism Rules`
- `Review And Commit`
- `Stop Rule For Over-Abstraction`

## Time Scale And Mode

Distinguish among:

- long-term construction
- staged transition
- short-term stop-bleeding

Choose mode by situation:

- use diagnosis when the situation is still unclear
- use reproduction-first for bug work when blind fixing would be risky
- use planning-first when the task has multiple branches or unresolved decisions
- use direct execution once the main line is already clear

Do not keep planning mode always on. Return to execution once the path is stable enough.

## When To Call 谋士池

Default: `军师` thinks first. `谋士池` is for high-risk judgment, not routine pre-analysis.

`贾诩 / 庞统 / 郭嘉` may be used in parallel for analysis work when their reading or write scopes do not conflict.

Bring in `谋士池` when the task touches areas such as:

- core data or configuration structures
- execution flow or lifecycle behavior
- module wiring, dependency flow, or integration boundaries
- multiple modules or unclear subsystem boundaries

Default analysis output should answer:

- what kind of system-level change is really being introduced
- what the current system structure can already support
- where the structural gap is
- whether deeper analysis is necessary before execution

## Analysis Escalation

Default limit:

- at most `1` system-level analysis
- if truly needed, at most `1` deeper implementation-level follow-up

After that, either move into execution or state the blocking reason explicitly.

Stop analyzing and move to execution when:

- clear execution boundaries can already be defined
- implementation plus feedback is now more useful than more speculation

## Chain-Depth Checkpoint

If a branch has already stretched across multiple rounds and the return on more digging is becoming unclear, pause before continuing the same line.

Judge:

- what has already been gained
- what is still missing
- what the next round is most likely to add
- the main risk and cost of continuing

Then decide whether the best next move is:

- continue deeper
- converge now
- switch direction
- pause here

Do not run this checkpoint mechanically on every step.

## Technical Debt And Temporary Fixes

If debt or structural weakness is discovered during main-line execution:

- if it blocks correctness, stability, or the minimum deliverable, explain why it must be handled now, then handle it
- otherwise, record it and keep the main line moving

When using a temporary workaround or fallback:

- do not adopt it silently
- state the better long-term path
- state why that path is not being taken now
- state the risk, limitation, and intended recovery path

## Parallelism Rules

- `谋士池`: may parallelize when task boundaries and write scopes do not conflict
- `武将池`: default to one person; only parallelize when task boundaries and write scopes are clearly non-conflicting
- `法正`: single-seat; do not parallelize

Collapse back to serial convergence when supposedly independent slices begin touching the same core files, abstractions, or shared write targets.

When delegated work can proceed asynchronously, do not stall the thread only to wait for non-blocking results.

If `法正` lacks technical facts needed for review, test, or commit-side handling, supplement with a `武将` validation pass instead of opening another `法正` line.

## Review And Commit

- `法正` should handle review, test closure, submit-readiness, and commit-side handling when explicitly assigned
- `军师` should not personally do the substantive review unless the diff is trivial or the user explicitly wants a personal review
- acceptance criteria should be explicit
- verification should prove the problem is really solved, not only bypassed or coincidentally passing

## Stop Rule For Over-Abstraction

Stop further abstraction when:

- further abstraction no longer clearly improves reuse or system clarity
- the new abstraction still has no clear reuse scenario

At that point, shift from digging to convergence.
