# Project Governance

An Agent Skill for keeping software projects traceable without freezing goals too early.

It maintains four stable views of a project:

- `G` and `C<n>`: goal and measurable acceptance criteria
- `L<n>`: architecture layers
- `S<n>`: real end-to-end runtime flow
- `T<n>`: chronological tasks with numeric substeps

Tasks are classified as formal delivery, formal maintenance, experiment, or goal review. Experiments remain reversible and produce evidence; they do not silently become accepted architecture or weaken the goal.

## Install

### Codex

```sh
git clone https://github.com/gongye19/project-governance-skill.git ~/.codex/skills/project-governance
```

Invoke it with `$project-governance`, or let Codex select it automatically for project planning and implementation work.

### Claude Code

```sh
git clone https://github.com/gongye19/project-governance-skill.git ~/.claude/skills/project-governance
```

Invoke it with `/project-governance`, or let Claude Code select it automatically when relevant.

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
