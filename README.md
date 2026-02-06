# README - Common DevX

> **Last Updated**: 2026-02-06 by Keming He

Ready-to-use AI skills and human guides for consistent documentation, standardized workflows, and faster project setup. MIT licensed, zero dependencies.

## What This Repository Contains

| Directory | Purpose | Audience |
| :--- | :--- | :--- |
| [`agent-skills/`](./agent-skills/README.md) | AI-consumable skills for documentation tasks | AI agents |
| [`human-guides/`](./human-guides/README.md) | Reference docs, troubleshooting, workflows | Developers |
| [`.github/`](./.github/) | Issue and PR templates | GitHub users |

## Quick Start

### For AI Agents

Tell your agent:

```plaintext
Generate a commit message for my staged changes
```

Available skills: commit messages, issues, PRs, meeting memos, READMEs, and more. See [`agent-skills/README.md`](./agent-skills/README.md).

### For Developers

Browse [`human-guides/`](./human-guides/README.md) for:

- Git, shell, SSH, and GPG workflows (`use-cases-*.md`)
- Diagnostic procedures (`diagnosis-*.md`)

### For Projects

Copy templates to your project:

1. `.github/` - Issue and PR templates
2. `CONTRIBUTING.md` - Development workflow
3. Individual skills or guides as needed

## Directory Structure

```plaintext
common-devx/
├── agent-skills/           # AI skills (see agent-skills/README.md)
├── human-guides/           # Developer guides (see human-guides/README.md)
├── .github/                # GitHub templates
│   ├── ISSUE_TEMPLATE/     # Bug report, feature request
│   └── pull_request_template.md
├── CONTRIBUTING.md         # Development workflow
├── SECURITY.md             # Security and verification
├── LICENSE                 # MIT license
└── README.md               # This file
```

## References

- [`agent-skills/README.md`](./agent-skills/README.md) - Full skill catalog
- [`human-guides/README.md`](./human-guides/README.md) - Guide index
- [`CONTRIBUTING.md`](./CONTRIBUTING.md) - How to contribute
- [`SECURITY.md`](./SECURITY.md) - Security guidance
- [GitHub Issues](https://github.com/KemingHe/common-devx/issues) - Questions and requests

---

> README Template v2.0.0 - KemingHe/common-devx
