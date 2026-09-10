---
name: project-governance
description: Prevent accidental goal and scope drift, distinguish experimental work from formal changes, allow evidence-based goal evolution, and maintain stable project goals, architecture, runtime flows, and progress records. Use when initializing a software project or planning, implementing, reviewing, or documenting project changes.
---

# Project Governance

Keep four project documents aligned so every change remains traceable over time.

## Required documents

Use these paths unless the project already has clearly equivalent documents. Reuse existing equivalents instead of creating duplicates.

- `docs/GOAL.md`: the current project goal `G` and measurable acceptance criteria `C1`, `C2`, ...
- `docs/ARCHITECTURE.md`: the current architecture divided into layers `L1`, `L2`, ...
- `docs/FLOW.md`: the current real processing flow, with steps `S1`, `S2`, ...
- `docs/PROGRESS.md`: the chronological task record, with tasks `T1`, `T2`, ... and numbered substeps `1`, `2`, ...

When a required document is missing, create it from the matching file in `assets/`. Replace its instructional placeholder text with project facts; do not invent facts that cannot be determined from the repository or the user.

## Identifier contract

Each prefix has exactly one meaning:

- `G`: the single overall project goal. Do not use it for a task or feature.
- `C<n>`: an acceptance criterion proving whether `G` is achieved.
- `L<n>`: an architecture layer or major architectural block.
- `S<n>`: a step in the real end-to-end system flow.
- `T<n>`: one development, modification, verification, or documentation task.

Keep identifiers stable:

- Allocate a new identifier as one greater than the highest identifier ever used in that document.
- Never renumber, recycle, or silently change the meaning of an existing identifier.
- When retiring a `C`, `L`, or `S`, retain it in a short retired section with its original meaning, retirement date, and replacement identifier when one exists.
- Do not invent alternative action labels such as `A1`, `P1`, `Step-A`, or a fresh numbering scheme.
- In conversation and work summaries, refer to the active task as `T<n>` and list its substeps beneath it as `1`, `2`, `3`, ... . Refer to a specific substep as `T<n>/步骤 <n>` when needed.

## Task communication

Do not create a `T` for a casual question, explanation, brainstorm, or read-only inspection unless it leads to an actual project change.

Before starting an actual update, state only the essentials:

```text
T<n> <task name>
类型：<Delivery（正式交付）| Maintenance（正式维护）| Experiment（实验）| Goal review（目标复审）>
目标：<what this task should achieve; related G/C>
修改：<affected L/S or “none”>
步骤：1. ...  2. ...  3. ...
```

Keep the same `T<n>`, task type, and numeric substeps in every later update. Start each progress update and final result by repeating the active `T<n>`, its type, and the current substep or outcome, so the user can immediately tell whether the work is experimental, formal, or a goal review. Never switch to letters or another numbering scheme. Do not renumber or delete an existing substep; append a new number when new work is discovered, and mark an abandoned step as cancelled. More detail is optional and should appear only when the task actually needs it.

## Goal change control

Treat `G` and active `C` entries as stable by default, not immutable forever. Preserve a clear goal when it remains valid, but proactively propose a review when evidence shows that the current contract is wrong, unreasonable, obsolete, internally inconsistent, unmeasurable, or no longer represents the user's actual intended outcome.

A goal review is warranted when, for example:

- new domain knowledge invalidates an assumption behind `G` or a `C`;
- a `C` measures a proxy that can pass while the real goal fails;
- two active criteria contradict each other;
- a criterion cannot be measured reliably under the project's hard constraints;
- the operating environment or user need has materially changed.

Implementation difficulty, a failed result, sunk effort, the current architecture, a preferred technology, or a desire to reduce work is not sufficient evidence for changing `G/C`.

When a review is warranted:

1. Do not silently edit `G/C` or continue toward an outcome known to be wrong.
2. Present the concrete evidence, the current wording, the proposed wording, the reason for changing it, the consequences of keeping it, and the impact on active `C/L/S/T` entries.
3. Classify the proposed change as stronger, equivalent, or weaker. Explicitly call out any scope expansion, scope reduction, threshold reduction, or measurement change.
4. Obtain explicit user approval before changing `GOAL.md` or implementing against the proposed contract. If the issue invalidates the active task, pause that implementation; otherwise continue under the existing contract while the proposal remains undecided.
5. Record the review and its decision in a dedicated `T<n>`. Keep rejected proposals in progress history without changing `G/C`.

For an approved change:

- `G` remains the single identifier `G`; record its exact before/after text, approval, and date in the goal-review task.
- Keep a `C<n>` only for wording clarification that does not change its scope, threshold, or measurement. For a material change, retire the old criterion and allocate the next unused `C<n>`.
- Update project boundaries and non-goals when the approved change affects scope.

Judge ordinary task completion against the `G/C` baseline that existed when the task started. Never rewrite the contract after seeing the result merely to make the task pass.

## Task admission

Before allocating or implementing a `T<n>`, classify it as exactly one of:

- **Delivery (formal):** directly advances one or more named `C` entries through an approved implementation direction.
- **Maintenance (formal):** preserves `G/C` and intended external behavior while repairing reliability, security, operability, or maintainability.
- **Experiment:** tests an uncertain method or assumption related to `G/C`; its result is evidence, not an accepted product or architecture decision.
- **Goal review:** evaluates a potentially necessary change to `G`, `C`, project boundaries, or non-goals; it may end with approval or with the current contract retained.

These are task types, not new identifier prefixes: every type still uses `T<n>`.

If a requested task cannot be tied to a `C`, a documented assumption behind `G/C`, maintenance, or a goal review, stop before implementation and present it as a scope proposal. Approval for nearby work does not approve the expansion.

Keep each task inside its stated purpose. Do not add adjacent features, speculative flexibility, unrelated refactors, or extra deliverables to the same `T`.

## Experiment lifecycle

Before an Experiment starts, record its hypothesis, linked `G/C`, affected `L/S`, and the observable success or stop condition. Keep the change reversible and clearly label temporary code, data, flags, branches, or outputs as experimental.

Do not present an experiment as the accepted current architecture or flow. Keep experimental design in its `T<n>` record until it is adopted. Close the experiment with evidence and exactly one outcome:

- **Adopt:** create a linked Delivery or Maintenance `T<n>` to formalize, verify, document, and clean up the change.
- **Reject or inconclusive:** retain the result in progress history and remove disposable experimental artifacts during closeout.
- **Goal evidence:** when the result shows that `G/C` may be wrong, unreasonable, or unmeasurable, create a linked Goal review `T<n>` and follow goal change control. A failed experiment alone is not permission to weaken `G/C`.

## Complexity gate

Reuse existing `L` and `S` entries whenever they can satisfy the linked `C` entries. Add a layer, subsystem, service, dependency, runtime flow step, or parallel path only when the current design cannot meet the linked criterion without it.

Record each material complexity increase in the active `T`, including:

- what is being added;
- which `C` requires it;
- why the existing `L/S` structure is insufficient;
- the simplest rejected alternative.

If complexity or scope grows materially beyond the approved task, stop and request approval instead of silently expanding the plan.

## Version closeout

Before reporting a new version complete or making an authorized commit, clean up the files touched or produced by the task:

- Remove confirmed temporary files, debug outputs, superseded drafts, reproducible candidate data, commented-out code, and old implementations no longer required by active `G/C`.
- Do not keep `old`, `backup`, `copy`, or version-suffixed duplicates in the current tree merely for safety; Git preserves code history.
- Keep `GOAL.md`, `ARCHITECTURE.md`, and `FLOW.md` at the current version instead of adding parallel old copies. Keep `PROGRESS.md` chronological.
- Add recurring generated or local-only files to the project's ignore rules when appropriate.
- Preserve non-reproducible raw data, database migrations, required fixtures, secrets/configuration owned by the user, and published or historical artifacts required for audit, rollback, or an explicit retention contract.
- If a file's ownership, reproducibility, or retention need is unclear, do not delete it without user approval. Never perform a broad cleanup outside the task's known files.
- After cleanup, update stale references, rerun the relevant verification, inspect the final diff/status, and record a short cleanup note in the active `T`.

Cleanup is part of finishing the version. Creating the Git commit itself still requires the user's request or authorization.

## Working protocol

For project development work:

1. Read the four documents before planning or changing code. If they are missing, initialize them first.
2. Apply task admission, state whether the task is formal, experimental, or a goal review, capture the starting `G/C` baseline, and identify the affected `C`, `L`, and `S` identifiers.
3. Allocate one new `T<n>` for the approved unit of work. Continue the same `T<n>` across status updates; do not rename it between messages.
4. Briefly record the task type, goal, affected `C/L/S`, numeric substeps, modifications, verification, time, and status in `PROGRESS.md`.
5. When evidence calls `G/C` into question, follow goal change control. Do not edit the contract or implement against a proposed goal until it is explicitly approved and recorded in a goal-review task.
6. Implement and verify against the starting `G/C` baseline. For an Experiment, follow its decision rule and lifecycle. Update `ARCHITECTURE.md` or `FLOW.md` only when the accepted current state actually changes.
7. Perform version closeout, then keep `GOAL.md`, `ARCHITECTURE.md`, and `FLOW.md` as current-state documents and `PROGRESS.md` chronological.

Do not edit source code merely to make it match stale documentation. Determine the intended truth from the user request and repository, then update code and current-state documents consistently.

## Progress rules

Each `T<n>` entry must contain:

- task name, type, goal, status, and time;
- related `C` and affected `L/S`, using `无` when none;
- numbered substeps;
- what changed and how it was verified.

For an Experiment, also record its hypothesis, decision rule, evidence, outcome, and linked follow-up task when one exists. Record other related historical tasks, goal-review evidence and decisions, user approval, scope boundaries, or complexity justification only when they are relevant. Do not make ordinary tasks carry empty governance boilerplate.

Append new tasks in numeric order. Preserve completed historical entries. Correct a historical mistake with a dated correction note or a new task rather than rewriting history invisibly.

## Completion check

Before reporting a project change complete, confirm:

- the task type was visible in its record and user-facing updates;
- experimental work was not represented as a formal accepted change, and its outcome was recorded;
- the task passed against its starting `G/C` baseline;
- any evidence that `G/C` is flawed was surfaced rather than ignored;
- `G` and active `C` changed only through explicit approval and recorded history;
- the result stays within project boundaries and the task's stated non-goals;
- active `L` entries describe the implemented architecture;
- active `S` entries describe the real executable flow;
- every added `L`, `S`, dependency, service, or parallel path is necessary for a linked `C` and recorded in the current `T`;
- temporary and superseded task artifacts were removed, while required history and non-reproducible data were preserved;
- the current `T` records what changed and how it was verified;
- every identifier used in the summary exists in its corresponding document.
