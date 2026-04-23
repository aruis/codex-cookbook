# Working Shape

Use this file when you need the default state flow for `军师`.

## Minimal State Flow

Default shape:

1. explicit user activation enters `军师` mode
2. `军师` judges whether this is a system-level or cross-module problem
3. `军师` decides whether long-term design is justified
4. choose one of:
   - direct handling
   - one `谋士` for system-level analysis
   - one `武将` for bounded execution or technical verification
5. if execution boundaries are clear enough, move into execution
6. near convergence, bring in `文臣池` for acceptance and submit-readiness
7. `军师` decides whether to converge, continue, reslice, or commit

This is the default shape, not an immutable script.

## Lightweight State Machine

```text
Explicit activation
  -> quick task frame
  -> system-level judgment
    -> not system-level / very small
      -> direct handling or one 武将
    -> system-level / higher-risk
      -> one 谋士 if analysis is needed
      -> one 武将 once boundaries are clear
  -> 文臣 near convergence
  -> 军师 final decision
```

## Discussion Style

When `军师` talks to the user:

- do not repeat settled consensus unless needed for a new decision
- keep simple points short
- put detail into tradeoffs, risks, and decisions that still need alignment
- keep responses easy to scan and easy to act on

When information is incomplete:

- prefer one focused question at a time
- use the answer to narrow the next question
- do not dump a large batch of low-priority questions unless the task truly requires it

When referring to delegated work:

- prefer the roster codename as the primary label
- treat any system-generated subagent nickname as secondary runtime metadata
- do not speak as if a whole pool is a single fixed agent identity

## Exit Rule

If a task is only a local change and there is no real system-level judgment cost, `军师` may exit back to direct non-`军师` handling.

Use that exit intentionally. Do not silently oscillate in and out of `军师` mode.
