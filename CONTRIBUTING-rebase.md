# Contributing - Git Rebase

> Updated on 2025-09-13 by @KemingHe

Step-by-step process for safely rebasing feature branches when working with squash-and-merge PRs.

## When Rebasing is Required

Squash-and-merge creates commits already merged to `main` in branch history, making simple rebasing fail or create duplicates.

> [!IMPORTANT]
>
> Required when:
>
> - Branch shows 10+ commits but contains only few new changes
> - Simple `git rebase main` creates conflicts or duplicate commits
> - Branch history contains commits from recently merged PRs

## Rebase Strategies

### Strategy 1: Simple Rebase (Standard Case)

> [!TIP]
>
> Use when branch diverged cleanly from current `main` with no merged commits in history.

```shell
# Update main and rebase
git fetch origin main
git switch main && git pull origin main
git switch feature-branch
git rebase main

# Push updated branch
git push --force-with-lease origin feature-branch
```

### Strategy 2: Selective Rebase (Complex Case)

> [!TIP]
>
> Use when branch contains already-merged commits that need exclusion.

```shell
# Update main
git fetch origin main
git switch main && git pull origin main
git switch feature-branch

# Find last merged commit to exclude
git log main..HEAD --oneline

# Rebase onto main, excluding commits up to last-merged-commit
git rebase --onto main last-merged-commit

# Push updated branch
git push --force-with-lease origin feature-branch
```

> [!NOTE]
>
> `last-merged-commit` is the SHA of the last commit that was already merged to `main`.

## Conflict Resolution

```shell
# During rebase conflicts
git add .                    # stage resolved files
git rebase --continue        # continue rebase

# Cancel rebase if needed
git rebase --abort
```

## Recovery Commands

```shell
# View recent branch states
git reflog

# Reset to previous state if rebase went wrong
git reset --hard previous-commit-sha
```

## Essential Commands Reference

```shell
# Diagnosis
git log main..HEAD --oneline    # commits unique to branch
git merge-base main HEAD        # where branch diverged

# Rebase operations
git rebase main                 # simple rebase
git rebase --onto main abc1234  # selective rebase

# Safety
git push --force-with-lease origin branch-name    # safe force push
git rebase --abort                                # cancel rebase
```

## Critical Requirements

- **Always use `--force-with-lease`** - prevents overwriting concurrent changes
- **Verify commits before pushing** - check `git log main..HEAD --oneline`
- **Test functionality after rebase** - ensure changes work correctly

---

> Git Rebase Guide v1.0.1 - KemingHe/common-devx
