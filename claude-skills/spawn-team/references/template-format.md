# Team Template Format

## Directory Structure

```
~/.claude/team-templates/<template-name>/
  template.yml        # Team structure (required)
  lead.md             # Lead agent orchestration prompt (required)
  <member-name>.md    # Per-member prompt layer (required per member, can be empty)
```

## template.yml

```yaml
description: "What this team does"

members:
  - name: reviewer
    agent: code-reviewer       # References ~/.claude/agents/code-reviewer.md
    description: "Reviews code for quality and security"  # For lead's context
    model: sonnet              # Optional model override
    color: blue                # Optional color

  - name: implementer
    agent: my-implementer
    description: "Implements features and writes tests"
    model: opus
    color: green
```

## Member Fields

| Field | Required | Description |
|-------|----------|-------------|
| `name` | yes | Addressable name in the team. Must match a `<name>.md` file in the template dir |
| `agent` | yes | References a custom agent from `~/.claude/agents/` |
| `description` | yes | Short description for the lead's context (not sent to the agent) |
| `model` | no | `sonnet`, `opus`, `haiku`, or full model ID. Inherits if omitted |
| `color` | no | `red`, `blue`, `green`, `yellow`, `purple`, `orange`, `pink`, `cyan` |

## Prompt Layering

```
Final prompt = base prompt from ~/.claude/agents/<agent>.md
             + contents of <member-name>.md from template dir
```

The `.md` file is always required for each member. Leave empty if no team-specific context needed.

## lead.md

Orchestration instructions for the team lead (the current session). Defines:
- Team goal and strategy
- Task creation approach
- Coordination patterns
- Completion criteria
