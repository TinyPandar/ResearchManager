---
name: research-planning
description: Plan or reshape a research or engineering experiment when the user is defining a new goal, changing methodology, data semantics, system boundaries, success criteria, or asking for a Draft Plan. Do not use for routine implementation or experiment execution whose contract is already clear.
---

Use this skill to turn an uncertain or changing research idea into a decision-ready plan.

The user's explicit instructions take precedence over this workflow guidance. Do not ask for confirmation that the user has already provided.

1. Identify the research goal, non-goals, constraints, success criteria, and the specific decision that must be made.
2. Inspect existing code, data, docs, runs, or external facts read-only when they can resolve uncertainty. Ask the user only when missing information would materially change the research conclusion, interface contract, irreversible action, or cost boundary.
3. Separate facts already observed from assumptions and hypotheses. Never invent project state, experimental evidence, or unavailable measurements.
4. When a substantial plan is needed, define the smallest useful Draft Plan: inputs/outputs and shape or coordinate contracts, method choice, baselines/controls, validation, resource needs, risks, stop conditions, completion criteria, and downstream handoffs.
5. Prefer concrete options with tradeoffs over open-ended questions. If one option is clearly compatible with the user's stated intent and low risk, recommend it and continue.
6. Route follow-up work to `research-data`, `research-implementation`, or `research-experiment` only when those workflows are actually needed. Independent work may be delegated in parallel when it cannot conflict on files or external state.

Read `docs/WORKFLOW.md` when the task spans several lifecycle stages. Read `agents/README.md` only when you need the stable role handoff contract.

The workflow is complete when the user has either a directly actionable plan or the requested research decision, with important assumptions, validation criteria, and unresolved risks made explicit.
