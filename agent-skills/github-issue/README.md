# README - GitHub Issue Generation

> **Last Updated**: 2026-02-05 by Keming He

Generate GitHub issues following repository templates for bug reports, feature requests, and enhancements.

## Quick Start

Use this skill when you need to:

- Create a bug report with reproduction steps
- Request a new feature or enhancement
- Document technical debt or improvements

Tell your AI agent: "Create a bug report for [problem]" or "Write a feature request for [functionality]".

## Template Discovery

This skill searches for templates in order:

1. `.github/ISSUE_TEMPLATE/` (`bug-report.md`, `feature-request.md`)
2. Repository-wide search for ISSUE_TEMPLATE
3. Falls back to minimal structure if none found

## Issue Types

| Type | Title Format | Use Case |
| :--- | :--- | :--- |
| Bug | `bug(scope): description` | Problems, errors, unexpected behavior |
| Feature | `feat(scope): description` | New functionality, enhancements |

## Files

- [`SKILL.md`](./SKILL.md) - AI instructions for issue generation

## Related

- [github-pull-request](../github-pull-request/) - Generate PR descriptions
- [.github/ISSUE_TEMPLATE/](../../.github/ISSUE_TEMPLATE/) - Repository issue templates

---

> README Template v2.0.0 - KemingHe/common-devx
