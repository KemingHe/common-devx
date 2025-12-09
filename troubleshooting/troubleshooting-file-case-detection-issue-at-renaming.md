# Troubleshooting - File Case Detection Issue at Renaming

> **Last Updated**: 2025-09-13 by Keming He

## Problem

Git doesn't detect case-only renames on case-insensitive systems (macOS, Windows, by default):

```shell
mv readme.md README.md
git status  # Shows "nothing to commit"
```

## Solution

```bash
# Use git mv for case changes
git mv readme.md README.md
git commit -m "refactor(README.md): correct casing"
```

> [!CAUTION]
>
> **Why not `git config core.ignorecase false`?**
>
> Breaks compatibility with case-insensitive filesystems and causes merge conflicts.

---

> File Case Detection Issue at Renaming Resolution v1.0.1 - KemingHe/common-devx
