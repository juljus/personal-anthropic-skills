---
name: dev-workflow
description: Development workflow emphasizing test-first development, task classification, and appropriate tracking. Use when starting implementation, planning changes, or structuring development work.
---

# Development Workflow

## Task Classification

Use project knowledge to classify tasks:

**Analysis** - Read-only, exploration, debugging, reporting
- Just do it. No approvals needed.

**Minor/Iterative** - Small fixes, iterations, minor improvements
- Discuss briefly if approach unclear
- Implement and commit
- No tracking needed unless complex

**Major** - New features, refactoring, architectural changes, risky modifications
- Full workflow required
- Track work (GitHub issue, task branch, or equivalent)
- Communicate throughout

## Major Work Workflow

### 1. Understand & Discuss
- Read existing code/docs first
- Propose approach in discussion
- Wait for alignment on direction before implementing

### 2. Track Work
Track significant work appropriately:
- GitHub issues (include plan in description)
- Task branches with descriptive names
- Project-appropriate tracking system

Do not create separate plan files - embed plans in tracking.

### 3. Implement

**Test-First Cycle (CRITICAL):**
1. Write test
2. Run test - **MUST fail**
3. **FREEZE test** - Do not modify during implementation
4. Implement code
5. Run test - should pass
6. Commit

**Never modify tests during implementation.** If test needs changes, stop and discuss - it indicates misunderstanding.

**Additional rules:**
- Bugs require reproduction test first
- Commit frequently, atomically
- Follow git-workflow skill for commits
- Refactoring requires passing tests before changes

### 4. Complete & Report
- Verify work meets intent
- Run all tests
- Summarize changes
- Close tracking when confirmed complete

## Principles

- **Communicate proportionally to risk** - Higher risk = more discussion
- **Test-first is non-negotiable** - Especially for bugs and features
- **Use judgment** - You have project context, apply it
- **Commit early and often** - Small, logical units
