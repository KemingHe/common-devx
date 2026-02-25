# README - Agent Skills

> **Last Updated**: 2026-02-25 by Keming He

AI-consumable skills following the [agentskills.io](https://agentskills.io) specification. Each skill enables AI agents to perform specific documentation and workflow tasks.

## Directory Pattern

Each skill follows a consistent structure:

```plaintext
[skill-name]/
├── SKILL.md              # AI instructions (required)
├── README.md             # Human documentation (recommended)
├── assets/               # Templates and resources (optional)
├── references/           # Acceptance criteria, specs (optional)
└── scripts/              # Executable code (optional)
```

## Available Skills

| Skill | Purpose |
| :--- | :--- |
| [`commit-message-creation/`](./commit-message-creation/README.md) | Generate conventional commit messages |
| [`contacts-management/`](./contacts-management/README.md) | Extract and organize contact information |
| [`documentation-review/`](./documentation-review/README.md) | Review documentation for quality and consistency |
| [`issue-creation/`](./issue-creation/README.md) | Generate issues following repository templates (GitHub and GitLab) |
| [`meeting-agenda-creation/`](./meeting-agenda-creation/README.md) | Generate structured meeting agendas |
| [`meeting-memo-creation/`](./meeting-memo-creation/README.md) | Generate meeting memos and standup summaries |
| [`pull-merge-request-creation/`](./pull-merge-request-creation/README.md) | Generate PR/MR descriptions following repository templates (GitHub and GitLab) |
| [`readme-creation/`](./readme-creation/README.md) | Generate self-contained README files |
| [`senior-mentor/`](./senior-mentor/README.md) | Guided learning through Socratic questioning |
| [`skill-creation/`](./skill-creation/README.md) | Create new agent skills following the specification |

## Quick Start

Tell your AI agent:

```plaintext
Generate a commit message for my staged changes
```

The agent will locate and follow the appropriate skill.

## Creating New Skills

Use the `skill-creation` skill:

```plaintext
Create a new skill for [task description]
```

See [`skill-creation/README.md`](./skill-creation/README.md) for the full process.

## References

- [agentskills.io Specification](https://agentskills.io/specification) - Official standard
