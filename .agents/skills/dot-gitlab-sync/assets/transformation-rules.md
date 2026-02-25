# Transformation Rules - GitHub to GitLab Template Sync

Reusable reference for all platform-specific transformations when syncing `.github/` and `.gitlab/` template directories.

## Platform Terminology

| GitHub Term | GitLab Equivalent |
| :--- | :--- |
| PR / PRs | MR / MRs |
| pull request | merge request |
| pull_request_template.md | merge_request_template.md |
| `.github/pull_request_template.md` | `.gitlab/merge_request_templates/merge_request_template.md` |
| `.github/ISSUE_TEMPLATE/` | `.gitlab/issue_templates/` |
| `.github/ISSUE_TEMPLATE/config.yml` | No GitLab equivalent (omit) |
| issue/PR number | issue/MR number |

## Template Format Differences

| Aspect | GitHub | GitLab |
| :--- | :--- | :--- |
| Issue template YAML frontmatter (name, about, title, labels) | Required | Not used (remove) |
| PR/MR template YAML frontmatter | Optional | Not used (remove) |
| Template directory casing | ISSUE_TEMPLATE/ (uppercase) | issue_templates/ (lowercase) |
| PR/MR template location | Root `.github/pull_request_template.md` | `.gitlab/merge_request_templates/merge_request_template.md` |

## Legitimate Exceptions (Do NOT Transform)

- **GitHub as a platform reference**: e.g., GitHub profile links in contacts are social references, not hosting terminology
- **Git commands**: `git pull` is a git operation, not GitHub terminology

## Grep Patterns for Validation

```shell
# Find residual GitHub terminology in .gitlab/ (review each hit)
rg -i "github" .gitlab/ --glob "*.md" | cat

# Find residual PR terminology in .gitlab/
rg "\bPRs?\b" .gitlab/ --glob "*.md" | cat

# Find residual GitLab terminology in .github/
rg -i "gitlab" .github/ --glob "*.md" | cat

# Find residual MR terminology in .github/
rg "\bMRs?\b" .github/ --glob "*.md" | cat
```
