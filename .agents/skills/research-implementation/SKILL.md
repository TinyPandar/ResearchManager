---
name: research-implementation
description: Implement, debug, refactor, or verify research code, models, configs, pipelines, losses, metrics, loaders, and tests when the research and data contracts are already defined. Do not use to redefine the research question, data semantics, or to run a formal long experiment.
---

Use this skill to carry an agreed research design through implementation and verification.

The user's explicit instructions take precedence over this workflow guidance. Bias toward completing reversible implementation work rather than pausing for routine approvals.

1. Read the smallest amount of code and configuration needed to understand the affected interface. Reuse established project conventions before inventing new abstractions.
2. Preserve the agreed research, data, shape, coordinate, loss, and metric contracts. If implementation reveals that one of those contracts must materially change, surface the conflict and route that decision through `research-planning` instead of silently changing semantics.
3. Make the smallest coherent change that solves the requested problem. Keep unrelated dirty files and user changes intact.
4. Verify behavior at the level where regressions could occur. Use meaningful unit, integration, shape/coordinate, numerical, or real-size smoke tests as appropriate; do not add low-value tests solely to mirror trivial implementation details.
5. When a test or diagnostic exposes a routine bug inside the requested scope, fix it and rerun the affected check without requesting another approval. Broaden testing only when failures, risk, or the size of the change justify it.
6. Do not claim an experiment result from code-level tests. Formal training/evaluation runs belong to `research-experiment`.
7. Report changed files, interfaces and shapes, configs, compatibility implications, verification commands/results, resource requirements, and remaining risks.

Read `agents/implementation_manager.md` when role boundaries or downstream handoff details matter. Read `docs/WORKFLOW.md` only when the task spans multiple lifecycle stages.

The work is complete when the requested implementation is present, relevant verification passes or a concrete blocker is documented, and the result is ready for the next requested stage.
