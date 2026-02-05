# Troubleshooting - Git File Case Detection

> **Last Updated**: 2026-02-05 by Keming He

Git doesn't detect case-only file renames on case-insensitive systems (macOS, Windows).

## Symptom

```shell
mv readme.md README.md
git status                        # Shows "nothing to commit"
```

## Solution

Use `git mv` for case changes:

```shell
git mv readme.md README.md
git commit -m "refactor: correct filename casing"
```

## Why Not `git config core.ignorecase false`?

Breaks compatibility with case-insensitive filesystems and causes merge conflicts. Use `git mv` instead.

---

> Troubleshooting - Git File Case Detection v2.0.0 - KemingHe/common-devx
