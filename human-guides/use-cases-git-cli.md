# Use Cases - Git CLI

> **Last Updated**: 2026-02-05 by Keming He

Essential git workflows for trunk-based development. Organized by development lifecycle.

## Table of Contents

- [Use Cases - Git CLI](#use-cases---git-cli)
  - [Table of Contents](#table-of-contents)
  - [Clone and Setup](#clone-and-setup)
  - [Create Feature Branch](#create-feature-branch)
  - [Work on Changes](#work-on-changes)
    - [Check Status](#check-status)
    - [Commit Changes](#commit-changes)
    - [View History](#view-history)
  - [Keep Branch Current](#keep-branch-current)
    - [Simple Rebase (Most Cases)](#simple-rebase-most-cases)
    - [Selective Rebase (After Squash-Merge)](#selective-rebase-after-squash-merge)
    - [Cancel Rebase](#cancel-rebase)
  - [Submit and Merge](#submit-and-merge)
  - [Post-Merge Cleanup](#post-merge-cleanup)
  - [Stashing Work in Progress](#stashing-work-in-progress)
    - [Stash and Restore](#stash-and-restore)
    - [Manage Stashes](#manage-stashes)
  - [Recovery and Troubleshooting](#recovery-and-troubleshooting)
    - [Reset Operations](#reset-operations)
    - [Recovery](#recovery)
    - [Related Guides](#related-guides)

## Clone and Setup

```shell
# Clone repository
git clone https://github.com/username/repo-name.git
cd repo-name

# Verify remotes
git remote -v

# Check current state
git status
git branch -a
```

> [↑ Back to Table of Contents](#table-of-contents)

---

## Create Feature Branch

> [!IMPORTANT]
>
> Always branch from up-to-date `main`. One branch = one issue.

```shell
# Update main first
git switch main
git pull origin main

# Create feature branch
git switch -c [type]/[description]/[username]
git push -u origin [type]/[description]/[username]
```

**Branch naming**: `type/description/username`

| Type | Use For |
| :--- | :--- |
| `feat` | New features |
| `fix` | Bug fixes |
| `docs` | Documentation |
| `refactor` | Code restructuring |

> [↑ Back to Table of Contents](#table-of-contents)

---

## Work on Changes

### Check Status

```shell
git status                    # Full status
git status -s                 # Short format
git diff                      # Unstaged changes
git diff --staged             # Staged changes
```

### Commit Changes

```shell
git add .                     # Stage all
git add [file]                # Stage specific file
git commit -m "type(scope): description"
```

### View History

```shell
git log --oneline -10         # Recent commits
git log main..HEAD --oneline  # Commits on this branch only
git log --oneline --graph     # Visual branch structure
git show [commit-sha]         # Full details of a commit
```

> [↑ Back to Table of Contents](#table-of-contents)

---

## Keep Branch Current

> [!IMPORTANT]
>
> Rebase regularly to avoid conflicts. Always rebase before submitting PR.

### Simple Rebase (Most Cases)

```shell
# Update main and rebase
git fetch origin main
git rebase origin/main

# If conflicts occur
git add .                     # Stage resolved files
git rebase --continue         # Continue rebase

# Push updated branch
git push --force-with-lease origin [branch-name]
```

### Selective Rebase (After Squash-Merge)

Use when your branch contains commits from a previously squash-merged PR.

```shell
# Find where to cut
git log main..HEAD --oneline

# Rebase excluding already-merged commits
git rebase --onto origin/main [last-merged-commit-sha]

# Push updated branch
git push --force-with-lease origin [branch-name]
```

> [!TIP]
>
> `[last-merged-commit-sha]` is the SHA of the last commit that was already merged to main via squash-merge.

### Cancel Rebase

```shell
git rebase --abort            # Cancel and restore previous state
```

> [↑ Back to Table of Contents](#table-of-contents)

---

## Submit and Merge

```shell
# Verify branch is ready
git log main..HEAD --oneline  # Review your commits
git diff main..HEAD --stat    # Summary of changes

# Push final changes
git push origin [branch-name]
```

Then create PR on GitHub linking to the approved issue.

> [↑ Back to Table of Contents](#table-of-contents)

---

## Post-Merge Cleanup

After PR is merged:

```shell
# Update local main
git switch main
git pull origin main

# Delete local feature branch
git branch -D [branch-name]

# Delete remote feature branch (if not auto-deleted)
git push origin --delete [branch-name]

# Clean stale references
git fetch origin --prune
```

> [↑ Back to Table of Contents](#table-of-contents)

---

## Stashing Work in Progress

Temporarily save changes when switching context.

### Stash and Restore

```shell
# Save current work, add -u flag to include unstaged files
git stash -m "WIP: description"

# Switch to other branch, do work, return

# Restore stashed work
git stash pop                 # Apply and remove from stash
git stash apply               # Apply but keep in stash
```

### Manage Stashes

```shell
git stash list                # View all stashes
git stash show -p             # View stash contents
git stash drop                # Delete latest stash
git stash clear               # Delete ALL stashes
```

> [↑ Back to Table of Contents](#table-of-contents)

---

## Recovery and Troubleshooting

### Reset Operations

| Mode | Effect |
| :--- | :--- |
| `--soft` | Undo commit, keep staged changes |
| `--mixed` | Undo commit, unstage changes (default) |
| `--hard` | Undo commit, discard all changes |

```shell
git reset HEAD~1              # Undo last commit (mixed)
git reset --soft HEAD~1       # Undo commit, keep staged
git reset --hard HEAD~1       # Undo and discard (DESTRUCTIVE)
```

### Recovery

```shell
git reflog                    # View recent branch states
git reset --hard [commit-sha] # Reset to specific state
```

### Related Guides

- [`troubleshooting-gpg-signing-lock.md`](./troubleshooting-gpg-signing-lock.md) - GPG signing issues
- [`troubleshooting-git-file-case-detection.md`](./troubleshooting-git-file-case-detection.md) - File case sensitivity

> [↑ Back to Table of Contents](#table-of-contents)

---

> Use Cases - Git CLI v2.0.0 - KemingHe/common-devx
