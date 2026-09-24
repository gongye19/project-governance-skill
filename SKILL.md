---
name: project-governance
description: Initialize evidence-based goals, architecture, runtime flows, and progress records for a brand-new software project without inventing unknown fields. Use automatically only when starting from zero in a new or empty project directory. For an existing project, use only when the user explicitly invokes project-governance or explicitly asks to adopt it; do not use for ordinary maintenance.
---

# Project Governance

Keep four project documents aligned so every change remains traceable over time.

## Activation boundary

- Use this skill automatically only when creating a project from zero in a newly created or effectively empty directory, before meaningful application code or project structure exists.
- Treat a directory containing a meaningful working product or established codebase as an existing project. Do not activate this skill merely because that project is being planned, implemented, reviewed, documented, or maintained.
- For an existing project, use this skill only when the user explicitly invokes `$project-governance`, names `project-governance`, or explicitly asks to adopt this governance system.
- When explicitly adopting it in an existing project, derive the initial current-state documents from repository evidence and user input. Label them as an adoption baseline and do not fabricate retroactive task history.

## Required documents

Use these paths unless the project already has clearly equivalent documents. Reuse existing equivalents instead of creating duplicates.

- `docs/GOAL.md`: the current project goal `GOAL`, measurable acceptance criteria `CRITERION1`, `CRITERION2`, ..., and explicit prohibitions `FORBIDDEN1`, `FORBIDDEN2`, ...
- `docs/ARCHITECTURE.md`: the current architecture divided into layers `LAYER1`, `LAYER2`, ...
- `docs/FLOW.md`: the current real processing flow, with steps `STEP1`, `STEP2`, ...
- `docs/PROGRESS.md`: the chronological task record, with tasks `TASK1`, `TASK2`, ... and numbered substeps `1`, `2`, ...

When a required document is missing, create it from the matching file in `assets/`. Replace its instructional placeholder text with project facts; do not invent facts that cannot be determined from the repository or the user.

## Progressive initialization

- Create the four documents even when the project is still uncertain, but record only facts supported by the user or repository evidence. Completeness is not a goal by itself.
- Write `待确认` or `尚未定义` for an unknown goal, boundary, criterion, prohibition, architecture layer, or flow. Keep any useful known direction without converting assumptions into facts.
- Do not allocate `CRITERION<n>`, `FORBIDDEN<n>`, `LAYER<n>`, or `STEP<n>` merely to fill a template. An empty section is valid until a real item is defined.
- A value explicitly marked `待确认` is not an active contract. Its first confirmed definition does not retire a previous identifier, but the decision and evidence must be recorded in the active `TASK`. After confirmation, normal stability and change-control rules apply.
- Ask for a decision only when the missing information would materially change the next action. Otherwise continue with bounded discovery or reversible work and keep the uncertainty visible.

## Identifier contract

Each identifier word has exactly one meaning:

- `GOAL`: the single overall project goal. Do not use it for a task or feature.
- `CRITERION<n>`: an acceptance criterion proving whether `GOAL` is achieved.
- `FORBIDDEN<n>`: one explicit constraint the project must not violate. It is stronger than an out-of-scope item and records something that must be actively avoided.
- `LAYER<n>`: an architecture layer or major architectural block.
- `STEP<n>`: a step in the real end-to-end system flow.
- `TASK<n>`: one development, modification, verification, or documentation task.

Keep identifiers stable:

- Allocate a new identifier as one greater than the highest identifier ever used in that document.
- Never renumber, recycle, or silently change the meaning of an existing identifier.
- When retiring a `CRITERION`, `FORBIDDEN`, `LAYER`, or `STEP`, retain it in a short retired section with its original meaning, retirement date, and replacement identifier when one exists.
- Only `GOAL`, `CRITERION<n>`, `FORBIDDEN<n>`, `LAYER<n>`, `STEP<n>`, and `TASK<n>` are valid identifiers. Do not abbreviate them or invent another identifier word or numbering scheme.
- In conversation and work summaries, refer to the active task as `TASK<n>` and list its substeps beneath it as `1`, `2`, `3`, ... . Refer to a specific substep as `TASK<n>/步骤 <n>` when needed.

## Task communication

Do not create a `TASK` for a casual question, explanation, brainstorm, or read-only inspection unless it leads to an actual project change.

Before starting an actual update, state only the essentials:

```text
TASK<n> <task name>
类型：<Delivery（正式交付）| Maintenance（正式维护）| Experiment（实验）| Goal review（目标复审）>
目标：<what this task should achieve; related GOAL/CRITERION and any governing FORBIDDEN>
修改：<affected LAYER/STEP or “none”>
步骤：1. ...  2. ...  3. ...
```

Keep the same `TASK<n>`, task type, and numeric substeps in every later update. Start each progress update and final result by repeating the active `TASK<n>`, its type, and the current substep or outcome, so the user can immediately tell whether the work is experimental, formal, or a goal review. Never switch to abbreviations or another numbering scheme. Do not renumber or delete an existing substep; append a new number when new work is discovered, and mark an abandoned step as cancelled. More detail is optional and should appear only when the task actually needs it.

## Goal change control

Treat `GOAL` and active `CRITERION` and `FORBIDDEN` entries as stable by default, not immutable forever. Preserve a clear contract when it remains valid, but proactively propose a review when evidence shows that the current contract is wrong, unreasonable, obsolete, internally inconsistent, unmeasurable, or no longer represents the user's actual intended outcome.

Do not apply change control to content still explicitly marked `待确认`; confirming it for the first time is initialization, not a contract change. Do not use this exception to relabel an already accepted contract as uncertain.

A goal review is warranted when, for example:

- new domain knowledge invalidates an assumption behind `GOAL` or a `CRITERION`;
- a `CRITERION` measures a proxy that can pass while the real goal fails;
- two active criteria contradict each other;
- a criterion cannot be measured reliably under the project's hard constraints;
- the operating environment, user need, or reason for an active `FORBIDDEN` has materially changed.

Implementation difficulty, a failed result, sunk effort, the current architecture, a preferred technology, or a desire to reduce work is not sufficient evidence for changing `GOAL/CRITERION/FORBIDDEN`.

When a review is warranted:

1. Do not silently edit `GOAL/CRITERION/FORBIDDEN` or continue toward an outcome known to be wrong.
2. Present the concrete evidence, the current wording, the proposed wording, the reason for changing it, the consequences of keeping it, and the impact on active `CRITERION/FORBIDDEN/LAYER/STEP/TASK` entries.
3. Classify the proposed change as stronger, equivalent, or weaker. Explicitly call out any scope expansion, scope reduction, threshold reduction, or measurement change.
4. Obtain explicit user approval before changing `GOAL.md` or implementing against the proposed contract. If the issue invalidates the active task, pause that implementation; otherwise continue under the existing contract while the proposal remains undecided.
5. Record the review and its decision in a dedicated `TASK<n>`. Keep rejected proposals in progress history without changing `GOAL/CRITERION/FORBIDDEN`.

For an approved change:

- `GOAL` remains the single identifier `GOAL`; record its exact before/after text, approval, and date in the goal-review task.
- Keep a `CRITERION<n>` only for wording clarification that does not change its scope, threshold, or measurement. For a material change, retire the old criterion and allocate the next unused `CRITERION<n>`.
- Keep a `FORBIDDEN<n>` only for wording clarification that does not change the prohibited behavior or constraint. For a material change, retire the old prohibition and allocate the next unused `FORBIDDEN<n>`.
- Update project boundaries and non-goals when the approved change affects scope.

Judge ordinary task completion against the `GOAL/CRITERION/FORBIDDEN` baseline that existed when the task started. Never rewrite the contract after seeing the result merely to make the task pass.

## Task admission

Before allocating or implementing a `TASK<n>`, classify it as exactly one of:

- **Delivery (formal):** directly advances one or more named `CRITERION` entries through an approved implementation direction.
- **Maintenance (formal):** preserves `GOAL/CRITERION/FORBIDDEN` and intended external behavior while repairing reliability, security, operability, or maintainability.
- **Experiment:** tests an uncertain method or assumption related to `GOAL/CRITERION/FORBIDDEN`; its result is evidence, not an accepted product or architecture decision.
- **Goal review:** evaluates a potentially necessary change to `GOAL`, `CRITERION`, `FORBIDDEN`, project boundaries, or non-goals; it may end with approval or with the current contract retained.

These are task types, not new identifier prefixes: every type still uses `TASK<n>`.

When no `CRITERION` is confirmed yet, use an Experiment or Goal review for discovery and definition work. Do not classify implementation as Delivery or claim product acceptance until it can be judged against a confirmed criterion.

If a requested task cannot be tied to a `CRITERION`, a documented assumption behind `GOAL/CRITERION/FORBIDDEN`, maintenance, or a goal review, stop before implementation and present it as a scope proposal. If it conflicts with an active `FORBIDDEN`, do not implement it unless a Goal review explicitly changes that prohibition. Approval for nearby work does not approve the expansion.

Keep each task inside its stated purpose. Do not add adjacent features, speculative flexibility, unrelated refactors, or extra deliverables to the same `TASK`.

## Experiment lifecycle

Before an Experiment starts, record its hypothesis, linked `GOAL/CRITERION/FORBIDDEN`, affected `LAYER/STEP`, and the observable success or stop condition. Keep the change reversible and clearly label temporary code, data, flags, branches, or outputs as experimental.

Do not present an experiment as the accepted current architecture or flow. Keep experimental design in its `TASK<n>` record until it is adopted. Close the experiment with evidence and exactly one outcome:

- **Adopt:** create a linked Delivery or Maintenance `TASK<n>` to formalize, verify, document, and clean up the change.
- **Reject or inconclusive:** retain the result in progress history and remove disposable experimental artifacts during closeout.
- **Goal evidence:** when the result shows that `GOAL/CRITERION/FORBIDDEN` may be wrong, unreasonable, or unmeasurable, create a linked Goal review `TASK<n>` and follow goal change control. A failed experiment alone is not permission to weaken the contract.

## Complexity gate

Reuse existing `LAYER` and `STEP` entries whenever they can satisfy the linked `CRITERION` entries. Add a layer, subsystem, service, dependency, runtime flow step, or parallel path only when the current design cannot meet the linked criterion without it.

Record each material complexity increase in the active `TASK`, including:

- what is being added;
- which `CRITERION` requires it;
- why the existing `LAYER/STEP` structure is insufficient;
- the simplest rejected alternative.

If complexity or scope grows materially beyond the approved task, stop and request approval instead of silently expanding the plan.

## Version closeout

Before reporting a new version complete or making an authorized commit, clean up the files touched or produced by the task:

- Remove confirmed temporary files, debug outputs, superseded drafts, reproducible candidate data, commented-out code, and old implementations no longer required by active `GOAL/CRITERION/FORBIDDEN`.
- Do not keep `old`, `backup`, `copy`, or version-suffixed duplicates in the current tree merely for safety; Git preserves code history.
- Keep `GOAL.md`, `ARCHITECTURE.md`, and `FLOW.md` at the current version instead of adding parallel old copies. Keep `PROGRESS.md` chronological.
- Add recurring generated or local-only files to the project's ignore rules when appropriate.
- Preserve non-reproducible raw data, database migrations, required fixtures, secrets/configuration owned by the user, and published or historical artifacts required for audit, rollback, or an explicit retention contract.
- If a file's ownership, reproducibility, or retention need is unclear, do not delete it without user approval. Never perform a broad cleanup outside the task's known files.
- After cleanup, update stale references, rerun the relevant verification, inspect the final diff/status, and record a short cleanup note in the active `TASK`.

Cleanup is part of finishing the version. Creating the Git commit itself still requires the user's request or authorization.

## Working protocol

For project development work:

1. Read the four documents before planning or changing code. If they are missing, initialize them first.
2. Apply task admission, state whether the task is formal, experimental, or a goal review, capture the starting `GOAL/CRITERION/FORBIDDEN` baseline, and identify the affected `CRITERION`, `FORBIDDEN`, `LAYER`, and `STEP` identifiers.
3. Allocate one new `TASK<n>` for the approved unit of work. Continue the same `TASK<n>` across status updates; do not rename it between messages.
4. Briefly record the task type, goal, affected `CRITERION/FORBIDDEN/LAYER/STEP`, numeric substeps, modifications, verification, time, and status in `PROGRESS.md`.
5. When evidence calls `GOAL/CRITERION/FORBIDDEN` into question, follow goal change control. Do not edit the contract or implement against a proposed contract until it is explicitly approved and recorded in a goal-review task.
6. Implement and verify against the starting `GOAL/CRITERION/FORBIDDEN` baseline. For an Experiment, follow its decision rule and lifecycle. Update `ARCHITECTURE.md` or `FLOW.md` only when the accepted current state actually changes.
7. Perform version closeout, then keep `GOAL.md`, `ARCHITECTURE.md`, and `FLOW.md` as current-state documents and `PROGRESS.md` chronological.

Do not edit source code merely to make it match stale documentation. Determine the intended truth from the user request and repository, then update code and current-state documents consistently.

## Progress rules

Each `TASK<n>` entry must contain:

- task name, type, goal, status, and time;
- related `CRITERION`, governing `FORBIDDEN`, and affected `LAYER/STEP`, using `无` when none;
- numbered substeps;
- what changed and how it was verified.

For an Experiment, also record its hypothesis, decision rule, evidence, outcome, and linked follow-up task when one exists. Record other related historical tasks, goal-review evidence and decisions, user approval, scope boundaries, or complexity justification only when they are relevant. Do not make ordinary tasks carry empty governance boilerplate.

Append new tasks in numeric order. Preserve completed historical entries. Correct a historical mistake with a dated correction note or a new task rather than rewriting history invisibly.

## Completion check

Before reporting a project change complete, confirm:

- the task type was visible in its record and user-facing updates;
- experimental work was not represented as a formal accepted change, and its outcome was recorded;
- the task passed against its starting `GOAL/CRITERION/FORBIDDEN` baseline;
- any evidence that `GOAL/CRITERION/FORBIDDEN` is flawed was surfaced rather than ignored;
- `GOAL` and active `CRITERION` and `FORBIDDEN` entries changed only through explicit approval and recorded history;
- the result stays within project boundaries, the task's stated non-goals, and all active `FORBIDDEN` constraints;
- active `LAYER` entries describe the implemented architecture;
- active `STEP` entries describe the real executable flow;
- every added `LAYER`, `STEP`, dependency, service, or parallel path is necessary for a linked `CRITERION` and recorded in the current `TASK`;
- temporary and superseded task artifacts were removed, while required history and non-reproducible data were preserved;
- the current `TASK` records what changed and how it was verified;
- every identifier used in the summary exists in its corresponding document.
