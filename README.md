# README - Common DevX

> **Last Updated**: 2026-02-25 by Keming He

Ready-to-use AI skills and human guides for consistent documentation, standardized workflows, and faster project setup. MIT licensed, zero dependencies.

## What This Repository Contains

| Directory | Purpose | Audience |
| :--- | :--- | :--- |
| [`.agents/skills/`](./.agents/skills/README.md) | AI-consumable skills for documentation tasks | AI agents |
| [`human-guides/`](./human-guides/README.md) | Reference docs, troubleshooting, workflows | Developers |
| [`.github/`](./.github/) | Issue and PR templates (GitHub) | GitHub users |
| [`.gitlab/`](./.gitlab/) | Issue and MR templates (GitLab) | GitLab users |

## Quick Start

### For AI Agents

Tell your agent:

```plaintext
Generate a commit message for my staged changes
```

Available skills: commit messages, issues, PRs/MRs, meeting memos, READMEs, and more. See [`.agents/skills/README.md`](./.agents/skills/README.md).

### For Developers

Browse [`human-guides/`](./human-guides/README.md) for:

- Git, shell, SSH, and GPG workflows (`use-cases-*.md`)
- Diagnostic procedures (`diagnosis-*.md`)

### For Projects

Copy `.agents/skills/` into your project - no modification needed regardless of public/private or GitHub/GitLab repo:

```plaintext
your-project/
└── .agents/skills/    # Copy this directory as-is
```

Optionally copy `.github/` and/or `.gitlab/` for issue and PR/MR templates.

<!-- TODO: Add npx skills add KemingHe/common-devx install path (see #45) -->

## Directory Structure

```plaintext
common-devx/
├── .agents/skills/        # AI skills (see .agents/skills/README.md)
├── .github/               # GitHub templates
│   ├── ISSUE_TEMPLATE/    # Bug report, feature request
│   └── pull_request_template.md
├── .gitlab/               # GitLab templates
│   ├── issue_templates/   # Bug report, feature request
│   └── merge_request_templates/
├── human-guides/          # Developer guides (see human-guides/README.md)
├── CONTRIBUTING.md        # Development workflow
├── SECURITY.md            # Security and verification
├── LICENSE                # MIT license
└── README.md              # This file
```

## References

- [`.agents/skills/README.md`](./.agents/skills/README.md) - Full skill catalog
- [`human-guides/README.md`](./human-guides/README.md) - Guide index
- [`CONTRIBUTING.md`](./CONTRIBUTING.md) - How to contribute
- [`SECURITY.md`](./SECURITY.md) - Security guidance
- [GitHub Issues](https://github.com/KemingHe/common-devx/issues) - Questions and requests
