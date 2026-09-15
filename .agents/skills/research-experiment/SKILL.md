---
name: research-experiment
description: Launch, resume, monitor, diagnose, compare, or archive formal research experiments, training or evaluation runs, GPU jobs, checkpoints, and experiment-tracking records. Do not use for changing model/data semantics or for ordinary code-level tests.
---

Use this skill for reproducible execution and evidence collection from formal experiments.

The user's explicit instructions take precedence over this workflow guidance. If the user already asked to run an experiment and the resource/cost boundary is clear, do not add a redundant approval pause.

1. Before launch or resume, verify the code/ref, configuration, data version, seed, runtime dependencies, resource target, checkpoint policy, output path, and stop condition that matter to this run.
2. Treat formal runs as immutable evidence. Record at least the commit SHA or code version, config snapshot, data version, seed, launch command, platform task/job ID when available, log/output path, and checkpoint location.
3. Launch or resume only the requested run. Do not silently swap datasets, checkpoints, configs, GPUs, metrics, or methods to make a run succeed.
4. During diagnosis, distinguish infrastructure/runtime failures from research-behavior failures. Routine operational fixes that preserve the experiment contract may be applied and verified; changes to model, loss, data semantics, or the scientific question must return to `research-implementation` or `research-planning`.
5. Do not stop, delete, overwrite, or replace a running external experiment unless the current user request already authorizes that action.
6. Report observed status and evidence, not inferred success: command, task/PID, resources, run directory, checkpoints, key metrics, failures, and whether the run is complete, active, or blocked.
7. When comparing runs, use the intended baseline and note any differences in code, data, config, seed, or environment that weaken the comparison.

Read `agents/experiment_manager.md` when role boundaries or handoff details matter. Read `docs/WORKFLOW.md` when the experiment is part of a larger research iteration.

The workflow is complete when the requested run action has been performed, its state is verifiable, reproducibility metadata is recorded, and remaining operational or scientific risks are explicit.
