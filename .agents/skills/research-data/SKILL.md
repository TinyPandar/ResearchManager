---
name: research-data
description: Create, transform, version, inspect, or validate research datasets, labels, coordinates, splits, generated samples, or data previews. Use when data semantics or quality are the task; do not use for model implementation or formal training runs.
---

Use this skill for reproducible research data work.

The user's explicit instructions take precedence over this workflow guidance. Stay within the agreed research and data semantics; if those semantics themselves must change, route that decision through `research-planning` rather than silently redefining the task.

1. Confirm the minimum data contract needed for the requested work: source/provenance, sample meaning, shape and dtype, coordinate system, labels, split rules, randomness, version/output path, and acceptance checks. Infer routine details when they are already implied by project conventions.
2. Inspect the real data pipeline and existing versions before generating or converting data. Do not substitute hand-made or AI-generated previews for outputs that are supposed to come from the project pipeline.
3. For a new or changed generator, first produce a small real sample when that materially reduces risk; inspect it with the same loader/validator that downstream code will use.
4. Preserve historical evidence. Prefer a new immutable version or output path when semantics, generation logic, labels, or splits change. Do not overwrite an existing research dataset unless the user explicitly requests it.
5. Validate relevant invariants such as counts, split leakage, shape/dtype, coordinate range, class/target distribution, file integrity, deterministic seeding, and loader compatibility. Run only checks that can reveal meaningful errors.
6. Report exact paths, version identifiers, sample counts, split summary, contract, validation commands/results, provenance, and remaining leakage or quality risks.

Read `agents/data_manager.md` when role boundaries or handoff details matter. Read `docs/WORKFLOW.md` only when the task also spans planning, implementation, or formal experiments.

Do not modify model/loss behavior to compensate for incorrect data, and do not launch a formal training run as part of this skill.
