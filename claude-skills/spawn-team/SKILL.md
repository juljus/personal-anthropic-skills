---
name: spawn-team
description: "Create an agent team from a template. Use when: (1) user invokes /spawn-team, (2) user wants to create, spawn, or start a new agent team, (3) user references team templates."
---

## Prerequisites

Agent teams require `CLAUDE_CODE_EXPERIMENTAL_AGENT_TEAMS=1`. If `TeamCreate` fails, tell the user to enable it in `~/.claude/settings.json` under `env` or as a shell environment variable.

## Usage

`/spawn-team <template-name>` — spawn a team from a template.
No argument? List available templates from `~/.claude/team-templates/`.

## Template Location

`~/.claude/team-templates/<name>/` — each template is a directory.

## Execution

1. Read `template.yml` for team structure and members
2. Read `lead.md` — adopt as orchestration instructions for the session
3. Ask user for a team name (or derive from template + project context)
4. `TeamCreate` with team name
5. For each member in `template.yml`:
   - Spawn with `subagent_type` from `agent` field, passing their `<name>.md` as additional prompt context
   - Apply `model`, `color` from `template.yml`

Read member `.md` files for coordination context — they describe how members interact with each other.

Format spec: `references/template-format.md`
