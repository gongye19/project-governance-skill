# Project Governance

An Agent Skill for initializing traceable governance when creating a software project from zero.

It is selected automatically only for a brand-new project in a new or empty directory. For an existing project, invoke it explicitly when you want to adopt this governance system; ordinary maintenance should not trigger it.

It maintains four stable views of a project:

- `GOAL`, `CRITERION<n>`, and `FORBIDDEN<n>`: goal, measurable acceptance criteria, and numbered constraints the project must not violate
- `LAYER<n>`: architecture layers
- `STEP<n>`: real end-to-end runtime flow
- `TASK<n>`: chronological tasks with numeric substeps

Tasks are classified as formal delivery, formal maintenance, experiment, or goal review. Experiments remain reversible and produce evidence; they do not silently become accepted architecture or weaken the goal.

## Install

### Codex

```sh
git clone https://github.com/gongye19/project-governance-skill.git ~/.codex/skills/project-governance
```

Invoke it with `$project-governance`. Codex may select it automatically only while creating a project from zero in a new or empty directory.

### Claude Code

```sh
git clone https://github.com/gongye19/project-governance-skill.git ~/.claude/skills/project-governance
```

Invoke it with `/project-governance`. Claude Code may select it automatically only while creating a project from zero in a new or empty directory.

Start a new agent session after installation.

## Included files

- `SKILL.md`: governance rules and workflow
- `assets/GOAL.md`: goal and acceptance-criteria template
- `assets/ARCHITECTURE.md`: architecture-layer template
- `assets/FLOW.md`: runtime-flow template
- `assets/PROGRESS.md`: chronological task template
- `agents/openai.yaml`: Codex display metadata

## License

MIT
