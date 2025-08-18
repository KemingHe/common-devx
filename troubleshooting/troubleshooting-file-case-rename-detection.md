# Troubleshooting - File Case Rename Detection

> Update on 2025-08-18 by @KemingHe

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
> **Why not `git config core.ignorecase false`?**
>
> Breaks compatibility with case-insensitive filesystems and causes merge conflicts.

---

> File Case Rename Detection - KemingHe/common-devx
