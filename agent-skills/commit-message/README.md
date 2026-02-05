# README - Commit Message Generation

> **Last Updated**: 2026-02-05 by Keming He

Generate conventional commit messages by analyzing staged changes and repository context.

## Quick Start

Use this skill when you need to:

- Write a commit message for staged changes
- Follow conventional commit standards
- Review commit history patterns

Tell your AI agent: "Generate a commit message" or "Write commit msg for staged changes".

## Files

```plaintext
commit-message/
├── SKILL.md                        # AI instructions for generating commits
├── README.md                       # This file
└── assets/
    ├── commit-template-long.md     # Full commit format with all sections
    └── commit-template-short.md    # Minimal commit format
```

## Commit Types

| Type | When to Use |
| :--- | :--- |
| `feat` | New feature or capability |
| `fix` | Bug fix |
| `docs` | Documentation only |
| `refactor` | Code change, no feature/fix |
| `chore` | Maintenance, dependencies |

## Constraints

- Title max 50 characters, imperative mood
- QWERTY keyboard typeable only (no em-dashes, smart quotes, emojis)
- Include only sections with meaningful content

## Related

- [../skill-creation/README.md](../skill-creation/README.md) - How skills are structured
- [../../CONTRIBUTING.md](../../CONTRIBUTING.md) - Project git conventions

---

> README Template v2.0.0 - KemingHe/common-devx
