---
name: external-write
description: Write files outside workspace sandbox (e.g., ~/.claude/skills). Use when creating/editing personal agent skills or other files that must exist outside the current workspace.
---

# Skill: External Write (staging + rsync)

## Use when
- Creating/editing files outside workspace (e.g., personal skills in `~/.claude/skills/`).

## Rules
- Stage everything in `_tmp_external_write/<target-name>/`.
- Publish with `rsync`.
- Always clean up the staging directory.
- Open all relevant published files with `code`.

## Procedure

### 1) Stage inside workspace
Create files under:
- `_tmp_external_write/<target-name>/...`

Edit normally (workspace tools), no heredocs.

### 2) Publish with rsync
Use trailing slashes so contents sync correctly:
- `mkdir -p <dest>`
- `rsync -a --delete _tmp_external_write/<target-name>/ <dest>/`

Examples:
- Destination (personal skills): `~/.claude/skills/<skill-name>`
- Command:
  - `mkdir -p ~/.claude/skills/<skill-name>`
  - `rsync -a --delete _tmp_external_write/<skill-name>/ ~/.claude/skills/<skill-name>/`

### 3) Clean up (always)
After publish (even on failure), delete staging:
- `rm -rf _tmp_external_write/<target-name>`

If doing multi-step shell work, prefer a trap:
- `trap 'rm -rf _tmp_external_write/<target-name>' EXIT`

### 4) Open published files for user review
After publishing, open destination files with `code` so user can verify:
- `code <dest>/SKILL.md <dest>/...`

Example:
- `code ~/.claude/skills/<skill-name>/SKILL.md`

## Notes
- Files in the destination are not automatically used just because they exist; link resources from `SKILL.md` if you want them reliably discoverable.
