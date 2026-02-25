# README - GitHub-GitLab Template Sync

> **Last Updated**: 2026-02-25 by Keming He

Synchronize `.github/` and `.gitlab/` template directories with automatic platform-specific transformations. Handles YAML frontmatter, terminology (PR/MR), directory structure, and template naming differences.

## Quick Start

Use this skill when you need to:

- Sync issue or PR/MR templates after editing one platform's directory
- Set up `.gitlab/` templates from existing `.github/` templates
- Audit both directories for consistency

Tell your AI agent: "Sync my GitHub templates to GitLab" or "Update .gitlab/ from .github/".

## Supported Transformations

| Aspect | GitHub | GitLab |
| :--- | :--- | :--- |
| Issue template dir | `.github/ISSUE_TEMPLATE/` | `.gitlab/issue_templates/` |
| PR/MR template | `.github/pull_request_template.md` | `.gitlab/merge_request_templates/` |
| YAML frontmatter | Required for issues | Not used |
| Terminology | PR, pull request | MR, merge request |

## Files

- [`SKILL.md`](./SKILL.md) - AI instructions for template sync
- [`assets/transformation-rules.md`](./assets/transformation-rules.md) - Platform transformation reference

## Related

- [`issue-creation/`](../issue-creation/README.md) - Unified issue generation (uses templates from both platforms)
- [`pull-merge-request-creation/`](../pull-merge-request-creation/README.md) - Unified PR/MR generation
