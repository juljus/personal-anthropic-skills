---
name: debugging
description: Systematic debugging approach emphasizing temporal awareness, narrow scope, and appropriate investigation strategies. Use when investigating bugs, analyzing failures, or troubleshooting issues.
---

# Debugging

## State Assumptions First

Before investigating, explicitly state:
- **Environment** - Local? Staging? Production? Which instance?
- **Time context** - When did issue occur? What time range matters?
- **Current time** - Query frequently to maintain temporal awareness
- **Expected behavior** - What should happen?

## Temporal Awareness (CRITICAL)

Time moves during debugging. Agents lack inherent time sense - develop it:

- **Query current time frequently** - Not just for ranges, but to stay oriented
- **Data goes stale** - What you checked 10 minutes ago may have changed
- **Systems evolve** - Services restart, data updates, state shifts
- **Be explicit about "when"** - "As of [time], the state was..."
- **Understand operations take time** - Nothing is instant

This makes you a better collaborator and keeps investigations grounded.

## Investigation Approach

### When Reproducible
1. **Reproduce reliably** - Create minimal reproduction case
2. **Write failing test** - Capture the bug (follows good development workflow)
3. **Isolate** - Binary search, remove variables
4. **Fix** - Make test pass
5. **Verify** - Confirm fix, check for regressions

### When Not Reproducible (Production, Intermittent)
1. **Pin down symptom** - Falsifiable statement of what's wrong
2. **Identify source of truth** - Logs? Database? Metrics? Where's reliable data?
3. **Narrow scope** - Smallest time range, fewest services, minimal data
4. **Compare** - Expected vs observed behavior
5. **Expand cautiously** - Only when narrow investigation exhausted

## Core Principles

**Scope Management:**
- Start narrow, expand only when stuck
- Prefer precise queries over broad sweeps
- One variable at a time

**Safety:**
- Default to read-only operations
- For writes/deletes: show exact operation, ask explicit approval
- State impact before executing

**Tooling:**
- Prefer MCP servers when available
- Use project-specific debugging tools (debuggers, profilers, tracers)
- Apply project knowledge to choose appropriate tools

## Common Investigation Patterns

**"Nothing is happening"** → Check errors, logs, connectivity
**"Wrong data"** → Verify environment, input sources, transformations  
**"Intermittent"** → Tighten time window, look for patterns, check resource constraints
**"Used to work"** → Identify what changed (code, config, data, environment)
