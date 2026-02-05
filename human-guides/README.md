# README - Human Guides

> **Last Updated**: 2026-02-05 by Keming He

Reference documentation for developers - workflows, troubleshooting, and diagnostic guides. Human-readable (not AI skills).

## File Naming Pattern

All guides follow: `[type]-[tech-and-description].md`

| Type | Purpose |
| :--- | :--- |
| `use-cases-` | Common workflows and operations |
| `diagnosis-` | Specific investigation procedures |
| `troubleshooting-` | Issue resolution guides |

New types welcome - use descriptive prefixes that categorize the content.

## Current Guides

### Use Cases

- [`use-cases-git-cli.md`](./use-cases-git-cli.md) - Git command-line workflows
- [`use-cases-linux-shell.md`](./use-cases-linux-shell.md) - Linux shell operations

### Diagnosis

- [`diagnosis-terraform-state-migration.md`](./diagnosis-terraform-state-migration.md) - Terraform state migration

### Troubleshooting

- [`troubleshooting-git-file-case-detection.md`](./troubleshooting-git-file-case-detection.md) - Git case sensitivity
- [`troubleshooting-gpg-signing-lock.md`](./troubleshooting-gpg-signing-lock.md) - GPG signing lock

## Adding New Guides

1. Choose or create a type prefix that fits the content
2. Name the file: `[type]-[tech-and-description].md`
3. Include problem statement, steps, and verification

## References

- [`../agent-skills/README.md`](../agent-skills/README.md) - AI-assisted documentation skills
- [`../CONTRIBUTING.md`](../CONTRIBUTING.md) - Contributing guidelines

---

> README Template v2.0.0 - KemingHe/common-devx
