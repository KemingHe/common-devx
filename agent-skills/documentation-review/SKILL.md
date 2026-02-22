---
name: documentation-review
description: |
  Review and correct documentation for consistency, correctness, and drift.
  Documentation edits only (txt, md, mdx, rst) - no functional code changes.
  Triggers: "review docs", "check documentation", "doc review", "fix docs".
license: MIT
metadata:
  author: KemingHe
  version: "1.2.0"
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
| **Linter** | Check IDE/editor linter errors when available |
| **Output quality** | Soft-wrapped bullets or prose continuation lines; orphaned conditional section labels (e.g., `(optional)` still present after populating); non-QWERTY characters; unfilled bracketed placeholders; terminology inconsistency; KISS/DRY violations |

### Step 3: Check Linter Errors

When linter tooling is available (IDE, markdownlint, etc.):

- Run linter on files in scope
- Include linter errors in findings table
- Distinguish between new errors (introduced by changes) and pre-existing

Common markdown linter catches:

- Missing language specifier on fenced code blocks
- Inconsistent list indentation
- Trailing whitespace or missing final newline
- Invalid link references

### Step 4: Report Findings

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
- **Linter errors**: Ignoring IDE warnings on markdown files

## General Doc Constraints

Apply to all generated output. If a discovered template deviates from any rule (e.g., uses emojis semantically, uses a different bullet convention), note the deviation explicitly and confirm with the user before treating it as a permitted exception.

- **Characters**: QWERTY keyboard typeable only - no em-dashes, smart quotes, emojis, or special Unicode. Exception: `↑` for ToC navigation
- **Bullets**: Use dash (`-`) for all unordered lists; one bullet per complete thought; never wrap a bullet's content mid-sentence onto a continuation line; split into separate distinct bullets if too long or multi-thought. Nested sub-bullets for component grouping are permitted.
- **Prose lines**: One sentence per line; never wrap mid-sentence to a continuation line
- **Optional sections**: Strip `(optional)` or any parenthetical conditional label (e.g., `(if operational)`) from section headers when populating; omit the entire section (header and body) when unused
- **Consistency**: Use the same term for the same concept throughout; match the voice and tense of the template; do not mix header levels for parallel sections
- **Completeness**: Populate all template placeholders with actual content; do not leave bracketed placeholders (e.g., `[Job Title]`), `[TODO]`, or `[TBD]` in generated output
- **KISS and DRY**: Each section and bullet conveys unique information - no redundancy or overlap

> General Doc Constraints v1.0.0 - KemingHe/common-devx

## Skill Constraints

- **Documentation only**: Edit txt, md, mdx, rst files - no functional code changes
- **Structured output**: Always use table format for findings
- **Prioritized**: Critical issues (broken links, wrong versions) before style issues
- **Linter-aware**: Check and report linter errors when tooling is available

---

> Documentation Review Skill v1.2.0 - KemingHe/common-devx
