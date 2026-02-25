# README - Issue Generation

> **Last Updated**: 2026-02-25 by Keming He

Generate issues following repository templates for bug reports, feature requests, and enhancements. Supports both GitHub and GitLab with automatic platform detection.

## Quick Start

Use this skill when you need to:

- Create a bug report with reproduction steps
- Request a new feature or enhancement
- Document technical debt or improvements

Tell your AI agent: "Create a bug report for [problem]" or "Write a feature request for [functionality]".

## Platform Support

The skill auto-detects the platform by checking for `.github/` or `.gitlab/` directories at project root.

| Platform | Template Location | Frontmatter |
| :--- | :--- | :--- |
| GitHub | `.github/ISSUE_TEMPLATE/` | YAML frontmatter required |
| GitLab | `.gitlab/issue_templates/` | No frontmatter |

## Issue Types

| Type | Title Format | Use Case |
| :--- | :--- | :--- |
| Bug | `bug(scope): description` | Problems, errors, unexpected behavior |
| Feature | `feat(scope): description` | New functionality, enhancements |

## Files

- [`SKILL.md`](./SKILL.md) - AI instructions for issue generation

## Related

- [`pull-merge-request-creation/`](../pull-merge-request-creation/README.md) - Generate PR/MR descriptions
- [`commit-message-creation/`](../commit-message-creation/README.md) - Generate commit messages
