# README - README Generation

> **Last Updated**: 2026-02-05 by Keming He

AI skill for generating self-contained directory READMEs that enable developers to instantly understand any part of a codebase without reading parent documentation.

## Why This Matters

READMEs are **entry points**, not documentation. A developer landing on any directory should understand its purpose within 30 seconds - without needing to read the parent first.

| Principle | What It Means |
| :--- | :--- |
| Self-contained | Stands alone - provides its own context |
| 30-second test | Purpose clear at first scan |
| Loose coupling | Works even if directory moves |

## Directory Structure

```plaintext
readme/
├── SKILL.md                    # AI instructions + philosophy
├── README.md                   # This file (demonstrates the pattern)
└── assets/
    └── readme-template.md      # Template for generating READMEs
```

## Quick Links

- [`SKILL.md`](./SKILL.md) - Full generation process and anti-patterns
- [`assets/readme-template.md`](./assets/readme-template.md) - Copy-paste starting point

## Getting Started

Tell your AI agent:

```plaintext
Create a README for [directory-path]
```

The AI will analyze the directory and generate a self-contained README following the template.

## Related

- [`documentation-review/README.md`](../documentation-review/README.md) - Review READMEs for consistency
- [`skill-creation/README.md`](../skill-creation/README.md) - How agent skills work

---

> README Template v2.0.0 - KemingHe/common-devx
