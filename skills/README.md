# Skills Index

This repository currently contains one coordinated skill system centered on `junshi`.

## Structure

- [`junshi/`](./junshi): lead-agent orchestration skill
- [`junshi-moushi/`](./junshi-moushi): delegated capability and plan analysis role
- [`junshi-wujiang/`](./junshi-wujiang): delegated bounded execution and technical validation role
- [`junshi-wenchen/`](./junshi-wenchen): delegated review, acceptance, and convergence role

## How The Pieces Fit

`junshi` is the lead role. It decides whether to:

- handle a task directly
- send one `谋士` for capability-level analysis
- send one `武将` for execution or technical fact-finding
- bring in one `文臣` near convergence for acceptance and submit-readiness

The child skills are not standalone orchestration systems. They are role contracts used under `junshi`.

## Entry Points

- main lead skill: [`junshi/SKILL.md`](./junshi/SKILL.md)
- state flow: [`junshi/references/working-shape.md`](./junshi/references/working-shape.md)
- decision appendix: [`junshi/references/decision-rules.md`](./junshi/references/decision-rules.md)
- artifact templates: [`junshi/references/artifact-templates.md`](./junshi/references/artifact-templates.md)
- dispatch prompt snippets: [`junshi/references/dispatch-prompts.md`](./junshi/references/dispatch-prompts.md)

## Activation Rule

`junshi` requires explicit user activation. It should not auto-enter from complexity or indirect hints alone.

For the exact triggering contract, use [`junshi/SKILL.md`](./junshi/SKILL.md) as the source of truth.
