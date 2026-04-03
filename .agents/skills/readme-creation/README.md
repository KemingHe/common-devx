# README - README Generation

AI skill for generating self-contained directory READMEs that enable developers to instantly understand any part of a codebase without reading parent documentation.

## Why This Matters

READMEs are **entry points**, not full documentation. A developer landing on any directory should understand its purpose within 30 seconds - without needing to read the parent first.

| Principle | What It Means |
| :--- | :--- |
| Self-contained | Stands alone - provides its own context |
| 30-second test | Purpose clear at first scan |
| Loose coupling | Works even if directory moves |

## Directory Structure

```plaintext
readme-creation/
├── assets/
│   ├── readme-template.md           # Template for generating READMEs
│   └── upgrade-from-*.md            # Migration guides for breaking changes
├── README.md
└── SKILL.md                         # AI instructions + philosophy
```

## Getting Started

Tell your AI agent:

```plaintext
Create a README for [directory-path]
```

The AI will analyze the directory and generate a self-contained README following the template.

## Quick Links

- [`SKILL.md`](./SKILL.md) - Full generation process and anti-patterns
- [`assets/readme-template.md`](./assets/readme-template.md) - Copy-paste starting point
- [`assets/upgrade-from-v3-0-0.md`](./assets/upgrade-from-v3-0-0.md) - Remove "Last Updated" from legacy READMEs
