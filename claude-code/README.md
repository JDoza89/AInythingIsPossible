# Claude Code

Drop-in skills, subagents, and commands for [Claude Code](https://docs.claude.com/claude-code).

## Install

- **Agents**: copy files from `agents/` into `~/.claude/agents/` (user-level) or `.claude/agents/` (project-level).
- **Skills**: copy directories from `skills/` into `~/.claude/skills/` or `.claude/skills/`.
- **Commands** (when added): copy files from `commands/` into `~/.claude/commands/` or `.claude/commands/`.

## What's here

### Model routing

A pattern for letting cheap models do cheap work, so you don't pay Opus prices to grep a file.

- `skills/model-router/` — decision rubric for *when* to delegate to *which* tier (Haiku / Sonnet / Opus).
- `agents/cheap-lookups.md` — Haiku-pinned subagent for narrow, well-defined lookups (grep, single-file reads, existence checks).

Use the skill as the guide; use the agent as a target to delegate to.
