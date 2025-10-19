# Guide - Common Git Operations

> **Last Updated**: 2025-08-12 by @KemingHe

Essential git workflows organized by common developer scenarios for efficient repository management and collaboration.

> [!NOTE]
>
> - **Troubleshooting**:
>   - [GPG signing issue resolution](../troubleshooting/troubleshooting-gpg-signing-lock-issue.md)
> - **Advanced rebasing**: Reference [CONTRIBUTING-rebase.md](../CONTRIBUTING-rebase.md) if you use `squash-and-merge`
> - **Commit messages**: Use [prompt-commit-msg-gen.md](../prompts/prompt-commit-msg-gen.md) for AI-assisted conventional commits

## Table of Contents

- [Guide - Common Git Operations](#guide---common-git-operations)
  - [Table of Contents](#table-of-contents)
  - [Starting a New Project](#starting-a-new-project)
  - [Working on an Existing Project](#working-on-an-existing-project)
    - [Understanding the Repository](#understanding-the-repository)
  - [Creating a New Feature](#creating-a-new-feature)
  - [Working on Someone Else's Feature](#working-on-someone-elses-feature)
  - [Understanding Changes and History](#understanding-changes-and-history)
    - [Current State](#current-state)
    - [Commit History](#commit-history)
  - [Managing Work in Progress](#managing-work-in-progress)
    - [Stash Operations](#stash-operations)
    - [Reset Operations](#reset-operations)
  - [Keeping Repository Clean](#keeping-repository-clean)
    - [Update References](#update-references)
    - [Branch Management](#branch-management)

## Starting a New Project

Initialize a new repository and connect it to a remote.

```bash
# Initialize local repository
git init
git add .
git commit -m "feat: initial commit"

# Connect to remote and push
git remote add origin https://github.com/username/repo-name.git
git branch -M main
git push -u origin main
```

> [Back to Table of Contents](#table-of-contents)

## Working on an Existing Project

Clone a repository and understand its current state.

```bash
# Clone entire repository
git clone https://github.com/username/repo-name.git
cd repo-name

# Clone specific branch only
git clone -b branch-name https://github.com/username/repo-name.git
```

### Understanding the Repository

```bash
# View configured remotes
git remote -v                 # show remote URLs (fetch/push)
git remote show origin        # detailed remote information

# Check repository status
git status                    # full status with branch info
git status -s                 # short format

# View all branches
git branch -a                 # all branches (local + remote)
git branch -vv                # local branches with tracking info
```

> [Back to Table of Contents](#table-of-contents)

## Creating a New Feature

Start new feature development with proper branch naming and tracking.

> [!TIP] Conventional branch naming
>
> Format: `type/scope/github-username`
>
> - **Types**: `feat`, `fix`, `docs`, `style`, `refactor`, `test`, `chore`, `perf`, `ci`, `build`
> - **Examples**: `feat/basic-auth/johnsmith`, `fix/version-api/janedoe`, `docs/update-readme/kimlee`

```bash
# Create new feature branch with tracking
git switch -c feat/auth/username
git push -u origin feat/auth/username

# Check your work status
git status -b                 # include branch and tracking info
git diff                      # see unstaged changes
git diff --staged             # see staged changes
```

> [Back to Table of Contents](#table-of-contents)

## Working on Someone Else's Feature

Checkout and track existing remote branches for collaboration.

```bash
# Update remote references first
git fetch origin

# Checkout remote branch (creates local branch automatically)
git switch remote-branch-name

# Alternative: manually create local branch tracking remote
git switch -c local-branch-name origin/remote-branch-name
git switch --track origin/remote-branch-name    # auto-names local branch
```

> [Back to Table of Contents](#table-of-contents)

## Understanding Changes and History

Inspect repository state, changes, and commit history.

### Current State

```bash
# Working directory status
git status                    # full status
git status --porcelain        # machine-readable format

# View changes
git diff                      # unstaged changes
git diff HEAD                 # all changes vs last commit
git diff main..HEAD           # changes vs main branch
git diff --stat               # summary of changes
git diff filename             # changes in specific file
```

### Commit History

```bash
# View commit log
git log --oneline             # compact one-line format
git log --oneline -10         # last 10 commits
git log --oneline --graph     # visual branch structure
git log main..HEAD            # commits unique to current branch

# Detailed information
git log --stat                # files changed per commit
git log -p                    # full patch diff
git log --author="username"   # commits by author
```

> [Back to Table of Contents](#table-of-contents)

## Managing Work in Progress

Handle incomplete work with stashing and resetting.

### Stash Operations

```bash
# Stash changes temporarily
git stash                     # stash tracked files
git stash -u                  # include untracked files
git stash -m "description"    # stash with message

# Retrieve stashed work
git stash list                # view all stashes
git stash pop                 # apply and remove latest stash
git stash apply stash@{0}     # apply specific stash
git stash drop stash@{0}      # delete specific stash
```

### Reset Operations

> [!IMPORTANT] Reset modes
>
> - **soft**: Keep working directory and staging area
> - **mixed** (default): Keep working directory, reset staging area
> - **hard**: Reset everything (destructive)

```bash
# Reset commits
git reset HEAD~1              # undo last commit, keep changes
git reset --soft HEAD~1       # undo commit, keep staging
git reset --hard HEAD~1       # undo commit, discard changes

# Reset specific files
git reset filename              # unstage file
git reset --hard HEAD filename  # discard file changes
```

> [Back to Table of Contents](#table-of-contents)

## Keeping Repository Clean

Maintain repository health with regular updates and cleanup.

### Update References

```bash
# Fetch updates without merging
git fetch origin              # from origin remote
git fetch upstream            # from upstream remote

# Clean stale references
git remote prune origin       # remove deleted remote branches
git remote prune upstream     # clean upstream references

# Combined update and clean
git fetch origin && git remote prune origin
```

### Branch Management

```bash
# Review branch status
git branch --merged           # branches merged to current
git branch --no-merged        # branches not yet merged
git branch -r                 # list remote branches

# Delete branches
git branch -d branch-name     # delete merged branch
git branch -D branch-name     # force delete branch
git push origin --delete branch-name  # delete remote branch
```

> [Back to Table of Contents](#table-of-contents)

---

> Common Git Operations Guide v1.0.0 - KemingHe/common-devx
