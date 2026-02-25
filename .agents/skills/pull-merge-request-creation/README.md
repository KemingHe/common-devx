# README - GitHub Pull Request Generation

> **Last Updated**: 2026-02-05 by Keming He

Generate GitHub pull request descriptions following repository templates to communicate changes, impact, and value.

## Quick Start

Use this skill when you need to:

- Create a PR description for branch changes
- Document changes for code review
- Communicate technical decisions and business value

Tell your AI agent: "Create a PR description" or "Write PR for my changes".

## Template Discovery

This skill searches for templates in order:

1. `.github/pull_request_template.md`
2. Repository-wide search for pull_request_template.md
3. Falls back to minimal structure if none found

## PR Types

| Type | When to Use |
| :--- | :--- |
| `feat` | New feature or capability |
| `fix` | Bug fix |
| `docs` | Documentation only |
| `refactor` | Code change, no feature/fix |
| `chore` | Maintenance, dependencies |

## Files

- [`SKILL.md`](./SKILL.md) - AI instructions for PR generation

## Related

- [`github-issue/README.md`](../github-issue/README.md) - Generate issue descriptions
- [`commit-message/README.md`](../commit-message/README.md) - Generate commit messages
- [`.github/pull_request_template.md`](../../.github/pull_request_template.md) - Repository PR template

---

> README Template v2.0.0 - KemingHe/common-devx
