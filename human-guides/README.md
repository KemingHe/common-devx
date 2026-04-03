# README - Human Guides

Reference documentation for developers - workflows, troubleshooting, and diagnostic guides. Human-readable (not AI skills).

## Platform Support

All guides target **macOS / Linux** with POSIX-compatible shells (sh, bash, zsh) unless noted otherwise. Each guide includes a Platform section with **Windows** alternatives.

## File Naming Pattern

All guides follow: `[type]-[tech-and-description].md`

| Type | Purpose |
| :--- | :--- |
| `diagnosis-` | Specific investigation procedures |
| `use-cases-` | Common workflows and operations |

New types welcome - use descriptive prefixes that categorize the content.

## Adding New Guides

1. Choose or create a type prefix that fits the content
2. Name the file: `[type]-[tech-and-description].md`
3. Include Platform section after metadata
4. Include problem statement, steps, and verification
5. Add an entry to the [guide catalog](../README.md#human-guides) in root README

## References

- [Guide Catalog](../README.md#human-guides) - full list of available guides
- [`.agents/skills/`](../.agents/skills/) - AI skills directory
- [`CONTRIBUTING.md`](../CONTRIBUTING.md) - contributing guidelines
