---
name: git-workflow
description: Git workflow with conventional commits, safety guardrails, and granular commit strategy. Use when performing git operations, making commits, creating branches, or managing version control.
---

# Git Workflow

## Commit Convention

Follow conventional commits format:

```
<type>[optional scope]: <description>

[optional body]

[optional footer(s)]
```

## Safety Rules

- **Never auto-push or auto-create PRs** - Always ask first
- **Add files individually** - No wildcards (`-A`, `.`, `*`)
- **Only commit your changes** - Not pre-existing modifications
- **Check for related issues** - Close or ask to close if commit resolves them

## Workflow

- **Prefer MCP git tools when available** over terminal commands
- **Multiple small commits > one large commit**
- **Commit timing**: Auto-commit when logical step completes, or propose when appropriate
- **Branching**: For large work, propose branches. Respect user preference for working in main
- **Naming**: Use kebab-case for repos and branches
