# README - Pull/Merge Request Generation

> **Last Updated**: 2026-02-26 by Keming He

Generate pull request (GitHub) or merge request (GitLab) descriptions following repository templates to communicate changes, impact, and value. Supports both GitHub and GitLab with automatic platform detection.

## Quick Start

Use this skill when you need to:

- Create a PR (GitHub) or MR (GitLab) description for branch changes
- Document changes for code review
- Communicate technical decisions and business value

Tell your AI agent: "Create a PR description" or "Write MR for my changes".

## Platform Support

The skill auto-detects the platform by checking for `.github/` or `.gitlab/` directories at project root.

| Platform | Template Location | Frontmatter |
| :--- | :--- | :--- |
| GitHub | `.github/pull_request_template.md` | Optional YAML frontmatter |
| GitLab | `.gitlab/merge_request_templates/` | No frontmatter |

## PR/MR Types

| Type | When to Use |
| :--- | :--- |
| `feat` | New feature or capability |
| `fix` | Bug fix |
| `docs` | Documentation only |
| `refactor` | Code change, no feature/fix |
| `chore` | Maintenance, dependencies |

## Files

- [`SKILL.md`](./SKILL.md) - AI instructions for PR/MR generation
