# Decision Rules

Use this file when `军师` needs the heavier decision details without bloating the main skill text.

## In This File

- `Time Scale And Mode`
- `When To Call 谋士池`
- `Analysis Escalation`
- `Chain-Depth Checkpoint`
- `Technical Debt And Temporary Fixes`
- `武将 Execution Autonomy`
- `Parallelism Rules`
- `Planning Changes`
- `Stop Rule For Over-Abstraction`
- `Review And Commit`

## Time Scale And Mode

Distinguish among:

- long-term construction
- staged transition
- short-term stop-bleeding

Do not apply the same standard to all three.

Choose mode by situation:

- use diagnosis when the situation is still unclear
- use reproduction-first for bug work when blind fixing would be risky
- use planning-first when the task has multiple branches or unresolved decisions
- use direct execution once the main line is already clear

Do not keep planning mode always on. Return to execution once the path is stable enough.

## When To Call 谋士池

Default: `军师` thinks first. `谋士池` is for high-risk judgment, not routine pre-analysis.

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

Do not expand into detailed planning unless the task has clearly crossed into higher-risk territory.

## Analysis Escalation

Default limit:

- at most `1` system-level analysis
- if truly needed, at most `1` deeper implementation-level follow-up

After that, either move into execution or state the blocking reason explicitly.

Stop analyzing and move to execution when:

- clear execution boundaries can already be defined
- risk still exists, but implementation plus feedback is now more useful than more speculation

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

Do not run this checkpoint mechanically on every step. Use it when a line of work has become noticeably long or its payoff has become uncertain.

## Technical Debt And Temporary Fixes

If debt or structural weakness is discovered during main-line execution:

- if it blocks correctness, stability, or the minimum deliverable, explain why it must be handled now, then handle it
- otherwise, record it and keep the main line moving

When using a temporary workaround or fallback:

- do not adopt it silently
- state the better long-term path
- state why that path is not being taken now
- state the risk, limitation, and intended recovery path

## 武将 Execution Autonomy

Planning constrains direction, not every implementation detail.

`武将` may adjust details locally as long as the change does not silently alter:

- the task goal
- the approved capability boundary
- the mid/long-term direction

Allowed local adjustments include:

- changing exact code landing points
- adjusting class or method organization
- making small implementation refinements needed to complete the loop
- correcting detail mistakes in the written plan

`武将` must escalate when a change starts to affect:

- new core abstractions
- new high-risk areas not already in scope
- clearly expanded write scope
- the original task split or parallelization assumptions
- a core assumption in the plan

## Parallelism Rules

Default to one `武将`.

Parallelize only when both are true:

- the task can be separated by clear system or responsibility boundaries
- write scopes are basically non-overlapping

Do not parallelize only because the task is large.

Collapse back to serial convergence if:

- multiple `武将` begin touching the same core files or abstraction layer
- supposedly independent slices prove strongly coupled in execution

## Planning Changes

Separate `local adjustment` from `planning change`.

- `武将池` may adjust execution details locally
- `武将池` may report planning drift
- `文臣池` may record and organize drift
- `谋士池` updates planning content when the plan itself must change
- `军师` decides whether to accept planning changes

No pool other than `军师` should silently redefine task direction.

## Stop Rule For Over-Abstraction

Stop further abstraction when:

- further abstraction no longer clearly improves reuse or system clarity
- the new abstraction still has no clear reuse scenario

At that point, shift from digging to convergence.

## Review And Commit

For review-like requests:

- submit-readiness, acceptance, and review of current changes -> `文臣池` first
- requirement, plan, and implementation-path review -> `谋士池`
- implementation-side technical validation, path walkthrough, and local feasibility checks -> `武将池` when technical facts need to be verified

`军师` should not personally read through the full change set as the main reviewer unless the diff is trivial or the user explicitly wants a personal review from `军师`.

Validation quality rules:

- acceptance criteria should be explicit, not empty wording
- verification should prove the problem is really solved, not only bypassed or coincidentally passing
- do not expand the main scope just to make validation look more complete
