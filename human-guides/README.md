# README - Human Guides

> **Last Updated**: 2026-02-06 by Keming He

Reference documentation for developers - workflows, troubleshooting, and diagnostic guides. Human-readable (not AI skills).

## Platform Support

All guides target **macOS / Linux** with POSIX-compatible shells (sh, bash, zsh) unless noted otherwise. Each guide includes a Platform section with **Windows** alternatives.

## File Naming Pattern

All guides follow: `[type]-[tech-and-description].md`

| Type | Purpose |
| :--- | :--- |
| `use-cases-` | Common workflows and operations |
| `diagnosis-` | Specific investigation procedures |

New types welcome - use descriptive prefixes that categorize the content.

## Current Guides

### Use Cases

- [`use-cases-git.md`](./use-cases-git.md) - Git command-line workflows
- [`use-cases-shell.md`](./use-cases-shell.md) - Shell operations
- [`use-cases-gpg-commit-signing.md`](./use-cases-gpg-commit-signing.md) - GPG commit signing
- [`use-cases-ssh-authentication.md`](./use-cases-ssh-authentication.md) - SSH authentication (Git + servers)

### Diagnosis

- [`diagnosis-terraform-state-migration.md`](./diagnosis-terraform-state-migration.md) - Terraform state migration

## Adding New Guides

1. Choose or create a type prefix that fits the content
2. Name the file: `[type]-[tech-and-description].md`
3. Include Platform section after metadata
4. Include problem statement, steps, and verification

## References

- [`agent-skills/README.md`](../agent-skills/README.md) - AI-assisted documentation skills
- [`CONTRIBUTING.md`](../CONTRIBUTING.md) - Contributing guidelines

---

> README Template v2.0.0 - KemingHe/common-devx
