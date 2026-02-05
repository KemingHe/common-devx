# README - Agent Skills

> **Last Updated**: 2026-02-05 by Keming He

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
- [`../CONTRIBUTING.md`](../CONTRIBUTING.md) - Contributing guidelines
- [`../SECURITY.md`](../SECURITY.md) - Security and verification guidance

---

> README Template v2.0.0 - KemingHe/common-devx
