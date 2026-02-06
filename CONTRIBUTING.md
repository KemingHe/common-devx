# Contributing

> **Last Updated**: 2026-02-06 by Keming He

How to contribute to `common-devx` - adding skills, guides, and templates.

## Prerequisites

Before contributing, ensure you have:

- SSH key configured for GitHub access (see [`use-cases-ssh-authentication.md`](./human-guides/use-cases-ssh-authentication.md))
- GPG key configured for commit signing (see [`use-cases-gpg-commit-signing.md`](./human-guides/use-cases-gpg-commit-signing.md))

## Development Model

This repository uses **trunk-based development**:

- `main` is the single source of truth
- Feature branches are short-lived (days, not weeks)
- All PRs merge to `main` via squash-and-merge
- Rebase before submitting PR (see [`use-cases-git.md`](./human-guides/use-cases-git.md))

## Requirements

> [!IMPORTANT]
>
> All contributions require an approved issue first.

| ✅ Do | ❌ Don't |
| :--- | :--- |
| Wait for issue approval from [@KemingHe](https://github.com/KemingHe) | Start work before approval |
| One PR per issue | Multi-issue PRs |
| Keep branches short-lived | Long-standing feature branches |
| Rebase before submitting PR | Merge commits from main |
| Self-review all content | Submit unreviewed AI-generated content (AI-slop) |
| Respond to feedback within 14 days | Let PR go stale |

**AI-assisted contributions are welcome**, but you must review and understand _every line_. PRs that appear to be unreviewed AI output will be closed.

## Contribution Types

| Type | Location | Guide |
| :--- | :--- | :--- |
| Agent skills | `agent-skills/[skill-name]/` | [`skill-creation/README.md`](./agent-skills/skill-creation/README.md) |
| Human guides | `human-guides/` | `[type]-[tech-and-description].md` pattern |
| GitHub templates | `.github/` | Edit directly |

## Workflow

```plaintext
1. Issue  -->  2. Approval  -->  3. Branch  -->  4. Work  -->  5. Review  -->  6. PR
```

### 1. Create Issue

Use [issue templates](./.github/ISSUE_TEMPLATE/) to describe your proposed change.

### 2. Get Approval

| Issue Type | When to Proceed |
| :--- | :--- |
| Bug fix | Once confirmed as valid bug |
| Feature request | When labeled `approved` |
| Minor doc fix | Can proceed (typos, broken links) |
| Significant change | When labeled `approved` |

### 3. Branch

```shell
git checkout -b [type]/[description]/[your-username]
```

### 4. Work

Follow conventions below. Use AI tools if helpful, but review everything.

### 5. Self-Review

Before submitting:

- [ ] You can explain every change
- [ ] Follows existing patterns
- [ ] No `[TODO]` or `[TBD]` placeholders
- [ ] Links work, versions match (frontmatter = footer)
- [ ] Last Updated date is current

### 6. Submit PR

Link to the approved issue. Use the [PR template](./.github/pull_request_template.md).

## Conventions

**Commits**: `type(scope): description`

| Type | Use For |
| :--- | :--- |
| `feat` | New skill, guide, template |
| `fix` | Corrections |
| `docs` | README updates |
| `refactor` | Restructuring |

**Branches**: `[type]/[description]/[username]`

**Files**:

- Skills: `agent-skills/[skill-name]/SKILL.md`
- Guides: `human-guides/[type]-[tech-and-description].md`

## Questions

Open a [GitHub issue](https://github.com/KemingHe/common-devx/issues).

---

> Contributing Guide v2.2.0 - KemingHe/common-devx
