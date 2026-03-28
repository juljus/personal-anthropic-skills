---
name: agent-communication
description: Principles for writing token-efficient, action-oriented instructions to agents. Use when creating agent prompts, rules, documentation, or improving agent communication.
---

# Agent Communication

## Token Efficiency (Highest Priority)

- **Remove first, add last** - Delete redundancy before adding content
- **Merge overlapping rules** - Combine when clarity improves
- **Challenge every sentence** - Does the agent truly need this?
- **Keep net tokens flat** - New info doesn't justify token bloat

## Action-Oriented Language

- **Prefer action-trigger questions** - "Ask X?" > "Wait for X"
- **Use imperative mood** - "Do this" > "You should do this"
- **Short, natural phrasing** - For frequent actions, be concise
- **Stricter wording only when critical** - Safety/production issues only

## Rule Reduction Process

1. Remove redundancy if intent stays unchanged
2. Merge overlapping rules if result is clearer
3. Replace vague steps with action-trigger wording if compliance improves
4. Add new text only if above cannot express it

## Writing Guidelines

- **Assume agent intelligence** - Don't over-explain
- **Be specific when needed** - Vague rules breed errors
- **Front-load critical info** - Most important rules first
- **Test with action** - If unclear, rewrite shorter
