# Contributing

> **Last Updated**: 2026-03-21 by Keming He

How to contribute to `common-devx` - adding skills, guides, and templates.

## Contribution Types

| Type | Location | Guide |
| :--- | :--- | :--- |
| Agent skills | `.agents/skills/[skill-name]/` | [`skill-creation/README.md`](./.agents/skills/skill-creation/README.md) |
| Human guides | `human-guides/` | `[type]-[tech-and-description].md` pattern |
| GitHub templates | `.github/` | Edit directly |
| GitLab templates | `.gitlab/` | Edit directly, or use `dot-gitlab-sync` skill |

## Workflow

```plaintext
1. Issue  -->  2. Approval  -->  3. Branch  -->  4. Work  -->  5. Review  -->  6. PR
```

### 1. Create Issue

Use [issue templates](./.github/ISSUE_TEMPLATE/) to describe your proposed change.

### 2. Get Approval

| Issue Type | When to Proceed |
| :--- | :--- |
| Bug fix | After maintainer confirms it is a valid bug |
| Feature request | After maintainer comments with approval |
| Minor doc fix | Can proceed (typos, broken links) |
| Significant change | After maintainer comments with approval |

### 3. Branch

```shell
git checkout -b [type]/[description]/[your-username]
```

### 4. Work

Follow conventions below. _Use AI tools if helpful, but you must review everything._

### 5. Self-Review

Before submitting:

- [ ] You can explain every change
- [ ] Follows existing patterns
- [ ] No `[TODO]` or `[TBD]` placeholders
- [ ] Links work, frontmatter versions are correct
- [ ] `Last Updated` date is current for relevant files
- [ ] Run [documentation-review](./.agents/skills/documentation-review/README.md) skill on changes if using an agent (recommended)

### 6. Submit PR

Link to the approved issue. Use the [PR template](./.github/pull_request_template.md).

## Skill Catalog Maintenance

The root README contains a skill catalog table that must be kept in sync when adding or modifying skills.

### Catalog Design

| Element | Convention |
| :--- | :--- |
| **Location** | Root `README.md`, ["Available Skills" section](./README.md#available-skills) |
| **Structure** | Single table with 3 columns: `Skill`, `Category`, `Description` |
| **Link target** | Each skill links to its `README.md` (human-facing docs) |
| **Sort order** | By category (Git Workflow, Project Management, Meta), then _alphabetical within each category_ |
| **Emoji usage** | Emojis permitted in Category column only as visual aid, with explicit note explaining exception |

### Categories

| Category | Use For |
| :--- | :--- |
| ⚙️ Git Workflow | Skills producing Git workflow artifacts (commits, PRs, MRs, issues, template syncing) |
| 📁 Project Management | Skills for documentation, meetings, design docs, and project organization |
| 🧠 Meta | Skills about how AI operates rather than what it produces (mentoring, skill creation) |

> **Note**: Emojis in this table are a deliberate exception to the project's no-emoji convention, used here to aid visual scanning of skill categories.

### Adding a New Skill to Catalog

When adding a new skill:

1. Determine the appropriate category based on the skill's primary purpose
2. Summarize or extract the first sentence from the skill's `SKILL.md` frontmatter `description` field
3. Add a new row to the catalog table in category order, alphabetically within the category
4. Link to the skill's `README.md` file (not `SKILL.md`)
5. Use the skill's human-readable display name in the Skill column

**Rationale**: Categories help users quickly find relevant skills. Git Workflow and Project Management are the primary use cases. Meta is for skills that don't produce artifacts but change AI behavior or manage other skills. _Single-skill categories are avoided to maintain a scannable structure._

## Guide Catalog Maintenance

The root README contains a guide catalog that must be kept in sync when adding or modifying guides.

### Design

| Element | Convention |
| :--- | :--- |
| **Location** | Root `README.md`, ["Human Guides" section](./README.md#human-guides) |
| **Structure** | Grouped by type prefix (`### Diagnosis`, `### Use Cases`), bullet lists within each |
| **Link target** | Each guide links directly to its `.md` file |
| **Sort order** | Alphabetical within each type group |

### Adding a New Guide to Catalog

When adding a new guide:

1. Determine the type prefix (`diagnosis-` or `use-cases-`, or create a new type)
2. Add a bullet under the appropriate `###` heading, alphabetically sorted
3. Use format: `[Human-Readable Title](./human-guides/filename.md) - brief description`
4. If creating a new type, add a new `###` heading in logical order

**Rationale**: Simpler than the skill catalog - guides use a flat bullet list grouped by type prefix rather than a table with categories. The file naming pattern (`[type]-[description].md`) provides implicit categorization.

## Requirements

> [!IMPORTANT]
>
> All contributions require an approved issue first.

| Do | Don't |
| :--- | :--- |
| Wait for issue approval from [@KemingHe](https://github.com/KemingHe) | Start work before approval |
| One PR per issue | Multi-issue PRs |
| Keep branches short-lived | Long-standing feature branches |
| Rebase before submitting PR | Merge commits from main |
| Self-review all content | Submit unreviewed AI-generated content (AI-slop) |
| Respond to feedback within 14 days | Let PR go stale |

**AI-assisted contributions are welcome**, but you must review and understand _every line_. PRs that appear to be unreviewed AI output will be closed.

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

- Skills: `.agents/skills/[skill-name]/SKILL.md`
- Guides: `human-guides/[type]-[tech-and-description].md`

## Prerequisites

Before contributing, ensure you have:

- SSH key configured for GitHub access (see [`use-cases-ssh-authentication.md`](./human-guides/use-cases-ssh-authentication.md))
- GPG key configured for commit signing (see [`use-cases-gpg-commit-signing.md`](./human-guides/use-cases-gpg-commit-signing.md))

This repository uses **trunk-based development**:

- `main` is the single source of truth
- Feature branches are short-lived (days, not weeks)
- All PRs merge to `main` via squash-and-merge
- Rebase before submitting PR (see [`use-cases-git.md`](./human-guides/use-cases-git.md))

## Questions

Open a [GitHub issue](https://github.com/KemingHe/common-devx/issues).
