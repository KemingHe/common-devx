# README - Documentation Review

> **Last Updated**: 2026-02-23 by Keming He

Review and correct documentation for consistency, correctness, and drift. Documentation edits only - no functional code changes.

## Quick Start

Ask your AI agent to review documentation:

- "Review the docs in agent-skills/"
- "Check this README for issues"
- "Audit documentation before commit"

## What It Checks

| Dimension | Examples |
| :--- | :--- |
| Consistency | Version sync, naming patterns |
| Correctness | Valid YAML, working links |
| Completeness | Required sections, no placeholders |
| Freshness | Last Updated dates, versions |
| Characters | QWERTY-only everywhere; no smart quotes, emojis, or special Unicode; no em-dashes or `--`/` -- ` in prose; use ` - ` for separation. Exception: `↑` |
| Inline formatting | `_underscore_` italics; colon outside bold (`**Topic**:`) |
| Linter | IDE/editor warnings when available |
| Output quality | Soft-wrapped bullets or prose; sentences broken across hard newlines; orphaned `(optional)` labels; unfilled `[placeholder]` text |

## Common Catches

- Forgetting to update "Last Updated" date
- Version mismatch between frontmatter and footer
- Stale links after file renames
- Leftover `[TODO]` placeholders
- Ignoring linter warnings on markdown files

## Files

- [`SKILL.md`](./SKILL.md) - AI instructions for documentation review

## Related

- [`skill-creation/README.md`](../skill-creation/README.md) - How to create new skills
- [`commit-message/README.md`](../commit-message/README.md) - Generate commit messages
