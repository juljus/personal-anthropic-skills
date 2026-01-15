---
name: git-commit
description: Git commit guidelines with conventional format, safety checks, and granular strategy. Use when making commits, staging changes, or writing commit messages.
---

# Git Commit

## Pre-Commit Verification

Before committing, verify:
- **Review changes** - Check `git status` and `git diff` to see what you're committing
- **Tests pass** - Run relevant tests (ties to dev-workflow)
- **Only your changes** - Not pre-existing modifications or unrelated files
- **Atomic scope** - Each commit is one logical change

## Commit Message Format

Follow conventional commits:

```
<type>[optional scope]: <description>

[optional body]

[optional footer(s)]
```

**Types**: feat, fix, docs, chore, refactor, test, style, perf, ci, build

## Commit Strategy

- **Multiple small commits > one large commit** - Break work into logical units
- **Commit timing**: Auto-commit when logical step completes, or propose when appropriate
- **Stage intentionally** - Add files individually, know what you're committing
- **Prefer MCP git tools when available** over terminal commands

## Safety Rules

- **Never auto-push or auto-create PRs** - Always ask first
- **Add files individually** - No wildcards (`-A`, `.`, `*`)
- **Check for related issues** - Close or ask to close if commit resolves them

## Workflow Integration

- **Branching**: For large work, propose branches. Respect user preference for working in main
- **Naming**: Use kebab-case for repos and branches
