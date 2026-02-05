# Skill Creation

> **Last Updated**: 2026-02-05 by Keming He

Create or refactor Agent Skills following the agentskills.io specification.

## Quick Start

Use this skill when you need to:

- Create a new skill from scratch
- Convert an existing prompt to skill format
- Validate or refactor existing skills

Tell your AI agent: "Create a skill for [task]" or "Convert this prompt to a skill".

## Files

```plaintext
skill-creation/
├── SKILL.md                    # AI instructions for creating skills
├── README.md                   # This file
└── assets/
    └── skill-template.md       # SKILL.md template with placeholders
```

## Skill Structure

Every skill follows this structure:

```plaintext
skill-name/
├── SKILL.md              # Required: frontmatter + instructions
├── README.md             # Required: human documentation
├── assets/               # Optional: templates, static resources
├── references/           # Optional: detailed docs, acceptance criteria
└── scripts/              # Optional: executable code
```

## Frontmatter Requirements

```yaml
---
name: skill-name          # Must match directory name
description: |            # What + when + triggers
  What this skill does.
  When to use it. Triggers: "keyword".
license: MIT              # Optional: license reference
metadata:
  author: Name
  version: "1.0.0"
---
```

## Constraints

- QWERTY keyboard typeable only (no em-dashes, smart quotes, emojis). Exception: `↑` for ToC
- Keep SKILL.md under 500 lines
- Directory name must match `name` field in frontmatter

## Related

- [agentskills.io/specification](https://agentskills.io/specification) - Official specification
- [../README.md](../README.md) - Skill catalog

---

> README Template v2.0.0 - KemingHe/common-devx
