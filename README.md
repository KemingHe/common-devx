# README - Common DevX

> **Last Updated**: 2026-03-21 by Keming He

Ready-to-use AI skills and human guides for consistent documentation, standardized workflows, and faster project setup. MIT licensed, zero dependencies.

## Repository Structure

```plaintext
common-devx/
├── .agents/skills/        # AI skills (see catalog below)
├── .github/               # GitHub issue and PR templates
├── .gitlab/               # GitLab issue and MR templates
├── human-guides/          # Developer guides
├── CONTRIBUTING.md        # How to contribute
├── LICENSE                # MIT license
├── README.md              # This file
└── SECURITY.md            # Security guidance
```

## Available Skills

| Skill | Category | Description |
| :--- | :--- | :--- |
| [Commit Message Creation](./.agents/skills/commit-message-creation/README.md) | ⚙️ Git Workflow | Generate conventional commit messages following project standards |
| [GitLab Sync](./.agents/skills/dot-gitlab-sync/README.md) | ⚙️ Git Workflow | Sync .github/ and .gitlab/ template directories with platform-specific transformations |
| [Issue Creation](./.agents/skills/issue-creation/README.md) | ⚙️ Git Workflow | Generate issues following repository templates for GitHub or GitLab |
| [Pull/Merge Request Creation](./.agents/skills/pull-merge-request-creation/README.md) | ⚙️ Git Workflow | Generate PR (GitHub) or MR (GitLab) descriptions following repository templates |
| [Contacts Management](./.agents/skills/contacts-management/README.md) | 📁 Project Management | Manage contact information by adding, updating, or validating entries |
| [Documentation Review](./.agents/skills/documentation-review/README.md) | 📁 Project Management | Review and correct documentation for consistency, correctness, and drift |
| [Living Design Documents](./.agents/skills/living-design-documents/README.md) | 📁 Project Management | Create and maintain structured design documentation that drives development |
| [Meeting Agenda Creation](./.agents/skills/meeting-agenda-creation/README.md) | 📁 Project Management | Generate meeting agendas with topics, timing, and preparation requirements |
| [Meeting Memo Creation](./.agents/skills/meeting-memo-creation/README.md) | 📁 Project Management | Generate meeting memos capturing decisions, actions, and key discussions |
| [README Creation](./.agents/skills/readme-creation/README.md) | 📁 Project Management | Generate self-contained README files that enable instant developer onboarding |
| [Senior Mentor](./.agents/skills/senior-mentor/README.md) | 🧠 Meta | Transform into a senior mentor for guided learning through Socratic questioning |
| [Skill Creation](./.agents/skills/skill-creation/README.md) | 🧠 Meta | Create or refactor Agent Skills following the agentskills.io specification |

> **Note**: Emojis in this table are a deliberate exception to the project's no-emoji convention, used here to aid visual scanning of skill categories.

## Human Guides

Developer reference docs for Git, shell, SSH, and GPG workflows. See [`human-guides/README.md`](./human-guides/README.md) for the full index.

## References

- [`CONTRIBUTING.md`](./CONTRIBUTING.md) - How to contribute
- [`SECURITY.md`](./SECURITY.md) - Security guidance
- [GitHub Issues](https://github.com/KemingHe/common-devx/issues) - Questions and requests
