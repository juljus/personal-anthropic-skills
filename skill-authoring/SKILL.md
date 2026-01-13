---
name: skill-authoring
description: Guide for creating effective agent skills. Use when users want to create a new skill (or update an existing skill) that extends an agent's capabilities with specialized knowledge, workflows, or tool integrations.
---

# Skill Authoring

Skills are modular packages that extend the agent with specialized knowledge, workflows, and tools. They provide:

1. Specialized workflows for specific domains
2. Tool integrations for file formats or APIs
3. Domain expertise (schemas, business logic)
4. Bundled resources (scripts, references, assets)

## Core Principles

### Default to REMOVE, Not ADD

When creating or editing skills, bias toward deletion. If uncertain whether content is needed, remove it. The agent can ask for clarification.

**Reject these suggestions:**
- "Add more context" - Can the agent infer it?
- "Add error handling section" - Does it justify token cost?
- "Add troubleshooting" - Will the agent truly reference it?

If someone (or you) suggests adding content, challenge it first. Most additions fail the test.

### Extreme Minimalism (CRITICAL)

**Line count challenge:**
- **30-50 lines**: Mastery
- **50-100 lines**: Excellent
- **100-150 lines**: Acceptable
- **150-200 lines**: Complex skills only - question every line

The context window is a public good. Every word has a cost. Challenge EVERY sentence: "Does the agent truly need this?" Most don't make the cut.

**Default assumption: the agent is already very smart.** Only add what the agent cannot infer. Think through each word. Remove filler ruthlessly.

Prefer concise examples over verbose explanations. One clear example beats paragraphs of explanation.

### Set Appropriate Degrees of Freedom

Match the level of specificity to the task's fragility and variability:

**High freedom (text-based instructions)**: Use when multiple approaches are valid, decisions depend on context, or heuristics guide the approach.

**Medium freedom (pseudocode or scripts with parameters)**: Use when a preferred pattern exists, some variation is acceptable, or configuration affects behavior.

**Low freedom (specific scripts, few parameters)**: Use when operations are fragile and error-prone, consistency is critical, or a specific sequence must be followed.

Think of the agent as exploring a path: a narrow bridge with cliffs needs specific guardrails (low freedom), while an open field allows many routes (high freedom).

### Anatomy of a Skill

```
skill-name/
├── SKILL.md (required)
│   ├── YAML frontmatter: name, description
│   └── Markdown instructions
└── Bundled Resources (optional)
    ├── scripts/      - Executable code
    ├── references/   - Documentation loaded as needed
    └── assets/       - Files used in output
```

**Scripts**: Repeated or fragile code. Token efficient, can execute without loading.

**References**: Documentation, schemas, API docs. Keeps SKILL.md lean.
- For large files (>10k words), include grep patterns in SKILL.md
- No duplication between SKILL.md and references

**Assets**: Templates, images, boilerplate for output. Not loaded into context.

**Don't include**: README.md, CHANGELOG.md, or other auxiliary docs.

### Progressive Disclosure

Three-level loading:
1. **Metadata** (name + description) - Always loaded
2. **SKILL.md body** - When skill triggers
3. **Bundled resources** - As needed

Keep SKILL.md under 150 lines (200 max for complex skills). Split into references when approaching limit.

**Multiple domains/frameworks**: Organize references by category:
```
my-skill/
├── SKILL.md (overview)
└── references/
    ├── variant-a.md
    └── variant-b.md
```

Agent loads only the relevant reference. Keep references one level deep. Add TOC for files >100 lines.

## Skill Creation Process

1. Understand with concrete examples
2. Determine scope (personal vs project)
3. Plan reusable contents
4. Create directory
5. Implement and write SKILL.md
6. Sanity check
7. Iterate

### Step 1: Understand with Concrete Examples

Understand how the skill will be used. Ask:
- "What should this skill do?"
- "Can you give examples?"
- "What would trigger this skill?"

Conclude when functionality is clear.

### Step 2: Determine Scope

Ask:
- **Personal** (`~/.claude/skills/`) - Available across all projects
- **Project** (`.claude/skills/`) - Current workspace only

Skip if already specified.

### Step 3: Plan Reusable Contents

Identify helpful resources:
- Repeated code → `scripts/`
- Boilerplate → `assets/`
- Documentation → `references/`

### Step 4: Create Directory

Choose kebab-case name (<= 64 chars):
- Personal: `mkdir -p ~/.claude/skills/<skill-name>`
- Project: `mkdir -p .claude/skills/<skill-name>`

Create subdirs as needed: `scripts/`, `references/`, `assets/`

### Step 5: Implement and Write SKILL.md

When creating the skill, remember that the skill is being created for another instance of an agent to use. Include information that would be beneficial and non-obvious to the agent. Consider what procedural knowledge, domain-specific details, or reusable assets would help another agent instance execute these tasks more effectively.

**Before making changes: Default to REMOVE, not ADD. Challenge every addition.**

#### Start with Reusable Skill Contents

Create resources: `scripts/`, `references/`, `assets/`. Test all scripts.

#### Write SKILL.md

**Writing Guidelines:** Always use imperative/infinitive form.

##### Frontmatter

Write the YAML frontmatter with `name` and `description`:

- `name`: The skill name
- `description`: **This is the PRIMARY TRIGGERING MECHANISM.** What determines when the agent loads your skill.
    - Include what the skill does AND specific triggers/contexts.
    - Descriptions are ALWAYS loaded (context cost). Be complete but concise - typically 1-3 sentences.
    - List specific triggers clearly. Use "Use when" pattern.
    - Example: "Create and manage X. Use when user needs to: (1) do A, (2) do B, (3) do C."

Do not include any other fields in YAML frontmatter.

##### Body

Instructions for using the skill. Use imperative form. Aim for <100 lines, max 150, complex skills 200.

### Step 6: Sanity Check

- `name` matches folder, is unique
- `description` includes ALL triggers (concise)
- Line count: Aim for <100, acceptable up to 150. No filler - every sentence earns its place
- Resources linked from SKILL.md
- Scripts tested

### Step 7: Iterate

Use the skill, notice inefficiencies, update SKILL.md or resources.