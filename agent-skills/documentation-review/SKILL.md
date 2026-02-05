---
name: documentation-review
description: |
  Review and correct documentation for consistency, correctness, and drift.
  Documentation edits only (txt, md, mdx, rst) - no functional code changes.
  Triggers: "review docs", "check documentation", "doc review", "fix docs".
license: MIT
metadata:
  author: KemingHe
  version: "1.0.0"
---

# Documentation Review

Review and correct documentation files for consistency, correctness, and drift. Documentation edits only - no functional code changes.

**Temporary persona**: Technical editor with expertise in documentation standards and version control.

## When to Use This Skill

- Before committing documentation changes
- Auditing docs for staleness or drift
- Reviewing PRs with documentation updates
- Checking consistency across related files

## Process

### Step 1: Identify Scope

Determine files to review:

- Single file, directory, or pattern
- Related files (e.g., SKILL.md + README + assets)

### Step 2: Apply Checklist

| Dimension | Check For |
| :--- | :--- |
| **Consistency** | Version sync (frontmatter/footer), naming patterns, terminology |
| **Correctness** | Valid YAML/markdown, working links, accurate paths |
| **Completeness** | Required sections present, no unfilled placeholders |
| **Freshness** | Last Updated date, version numbers, changelog entries |
| **Characters** | QWERTY-only, no em-dashes/smart quotes/emojis (exception: `↑`) |

### Step 3: Report Findings

Present issues in structured table:

```markdown
| Issue | Location | Current | Fix Needed |
| :--- | :--- | :--- | :--- |
| [issue type] | Line X | `[current]` | [action] |
```

Summarize with:

- Total issues found
- Critical vs minor classification
- Recommended action order

## Common Misses

- **Last Updated**: Forgetting to update date after changes
- **Version drift**: Frontmatter version differs from footer
- **Stale links**: Renamed files but not references
- **Placeholder remnants**: `[TODO]` or `[TBD]` left in final docs

## Constraints

- **Documentation only**: Edit txt, md, mdx, rst files - no functional code changes
- **Structured output**: Always use table format for findings
- **Prioritized**: Critical issues (broken links, wrong versions) before style issues
- **Characters**: QWERTY keyboard typeable only - no em-dashes, smart quotes, emojis, or special Unicode. Exception: `↑` for ToC navigation

---

> Documentation Review Skill v1.0.0 - KemingHe/common-devx
