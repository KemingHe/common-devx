---
name: skill-creation
description: |
  Create or refactor Agent Skills following the agentskills.io specification.
  Use when creating new skills, converting prompts to skills, or validating skill structure.
  Triggers: "create skill", "new skill", "SKILL.md", "agent skill", "convert prompt".
license: MIT
metadata:
  author: KemingHe
  version: "1.0.0"
---

# Skill Creation

Create Agent Skills following the [agentskills.io](https://agentskills.io) specification for platform-agnostic AI capabilities.

## When to Use This Skill

- Creating a new skill from scratch
- Converting an existing prompt to skill format
- Refactoring or validating existing skills
- Understanding skill structure and best practices

## Asset Resolution

1. Check `./assets/skill-template.md` for the SKILL.md template
2. If not found, search `**/skill-template.md` in repository
3. If still not found, use the specification below to generate from scratch

## Process

### Step 1: Gather Context

Before creating a skill, understand:

- **Purpose**: What task does this skill accomplish?
- **Triggers**: What keywords or scenarios should activate this skill?
- **Inputs**: What information does the agent need from the user?
- **Outputs**: What should the agent produce?
- **Assets**: Are there templates or reference materials needed?

### Step 2: Create Directory Structure

```plaintext
skill-name/
├── SKILL.md              # Required: instructions + frontmatter
├── README.md             # Required: human documentation
├── assets/               # Optional: templates, static resources
├── references/           # Optional: detailed docs, acceptance criteria
└── scripts/              # Optional: executable code
```

**Naming rules** (from [agentskills.io](https://agentskills.io)):

- Lowercase letters, numbers, and hyphens only
- 1-64 characters
- No leading/trailing hyphens
- No consecutive hyphens (`--`)
- Directory name must match `name` field in frontmatter

### Step 3: Write SKILL.md Frontmatter

Required and recommended fields:

```yaml
---
name: skill-name
description: |
  One-line summary of what this skill does.
  When to use it and trigger keywords.
license: MIT
metadata:
  author: AuthorName
  version: "1.0.0"
---
```

**Description guidelines**:

- 1-1024 characters
- First sentence: what the skill does
- Second sentence: when to use it
- Include trigger keywords for agent discovery

### Step 4: Write SKILL.md Body

Follow this structure (adapt sections as needed):

1. **Title**: `# Skill Name` (human-readable)
2. **When to Use**: Scenarios that trigger this skill
3. **Asset Resolution**: How to find templates (local first, then search)
4. **Process**: Step-by-step instructions for the agent
5. **Output Format**: Expected output structure
6. **Constraints**: Rules and limitations
7. **Examples**: Good/bad examples if helpful
8. **Footer**: Version tag `> Skill Name vX.Y.Z - Repo`

### Step 5: Create Assets (if needed)

Place templates in `assets/` subdirectory:

- Use descriptive names: `{purpose}-template.md`
- Templates should be self-documenting with placeholders
- Include version footer in templates

### Step 6: Create README.md

Human-readable documentation:

```markdown
# Skill Name

Brief description for humans browsing the repository.

## Quick Start

How to use this skill with your AI agent.

## Files

- `SKILL.md` - AI instructions
- `assets/` - Templates used by this skill

## Related

Links to related skills or documentation.
```

## Output Format

When creating a skill, produce three files:

1. **SKILL.md** - Complete with frontmatter and body
2. **README.md** - Human documentation
3. **assets/*.md** - Template files (if applicable)

Present each file in a markdown code block with the filename as header.

## Constraints

- **Frontmatter**: Must be valid YAML with `name` and `description`
- **Name matching**: Directory name must equal `name` field
- **Line limit**: Keep SKILL.md under 500 lines (move details to references/)
- **Token budget**: Body should be <5000 tokens for efficient loading
- **Progressive disclosure**: Only essential instructions in SKILL.md; details in assets/references
- **Asset resolution**: Always instruct to check local `./assets/` first, then search
- **Characters**: QWERTY keyboard typeable only - no em-dashes, smart quotes, emojis, or special Unicode. Exception: `↑` for ToC navigation

## Specification Reference

Full specification: [agentskills.io/specification](https://agentskills.io/specification)

### Frontmatter Fields

| Field | Required | Constraints |
| :--- | :--- | :--- |
| `name` | Yes | 1-64 chars, lowercase, hyphens, must match directory |
| `description` | Yes | 1-1024 chars, what + when + triggers |
| `license` | No | License name or file reference |
| `compatibility` | No | Environment requirements (1-500 chars) |
| `metadata` | No | Key-value pairs (author, version, etc.) |
| `allowed-tools` | No | Space-delimited tool list (experimental) |

### Optional Directories

| Directory | Purpose | When to Use |
| :--- | :--- | :--- |
| `assets/` | Templates, images, data files, static resources | Skill produces output based on templates |
| `references/` | Detailed docs, acceptance criteria, domain-specific files | SKILL.md exceeds 500 lines or needs test criteria |
| `scripts/` | Executable code (Python, Bash, JavaScript) | Skill needs to run code for reliable execution |

---

> Skill Creation v1.0.0 - KemingHe/common-devx
