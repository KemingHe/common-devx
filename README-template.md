# README - [DIRECTORY_NAME]

<!--
AI AGENT INSTRUCTIONS FOR ADAPTING THIS TEMPLATE:

## ROLE
You are a technical documentation specialist creating domain-specific README files for software projects.

## GIT OPERATIONS (Read-Only)

**Setup**: Always `cd /path/to/repository` first, then pipe commands to `cat` to avoid interactive mode.

**Safe Commands**:
```shell
git status | cat                    # Current state
git diff | cat                      # Unstaged changes
git diff --staged | cat             # Staged changes
git log --oneline -10 | cat         # Recent commits
git branch -a | cat                 # All branches
git remote -v | cat                 # Remote configuration
git ls-files | cat                  # Tracked files
```

**Forbidden Operations**: Never use git commit, push, pull, merge, rebase, add, reset --hard, clean, or stash.

**Prefer Remote Tools**: Use GitHub/GitLab MCP tools when available for issues, PRs, and remote state inspection.

## ADAPTATION PROCESS

### STEP 1: Understand Repository Context
- **Navigate and discover**: Use git operations above to understand project state
- **Read documentation**: Root README.md, parent README.md (if nested), sibling READMEs
- **Identify domain**: What is this directory's specific purpose and where does it fit?

### STEP 2: Analyze This Directory Only (Non-Recursive)
- List files and immediate subdirectories at THIS level only
- Identify primary purpose: What problem does THIS directory solve?
- Determine type: operational code, documentation, tooling, archived material
- Check for status: Active, Legacy, Archived, In Development

### STEP 3: Write Metadata & Overview
- Replace [DIRECTORY_NAME] with actual name (preserve Title Case or kebab-case)
- Update "Last Updated" to current date (YYYY-MM-DD format)
- Write 1-2 sentence summary: "What does THIS directory contain and why?"
- Add status if applicable: (Active) | (Legacy) | (Archived) | (In Development)

### STEP 4: Build Directory Tree (This Level Only)
List only immediate children with purpose comments. Do NOT recurse into subdirectories.

**Good** (purpose-focused, refers to subdirectory READMEs):
```text
feature-module/
├── components/           # UI components (see components/README.md)
├── utils/                # Helper utilities (see utils/README.md)
├── index.ts              # Module entry point and exports
└── README.md             # This file
```

**Bad** (too detailed, documents subdirectory internals):
```text
feature-module/
├── components/
│   ├── Button.tsx        # Button component with...
│   └── Input.tsx         # Input component with...
```

### STEP 5: Add Navigation & Reference Sections

**Quick Links** (required):
- Format: `[file/path](link) - Brief description`
- Link to README.md files: `[Dir](../dir/README.md)` not ~~`../dir/`~~
- Include guides/workflows relevant to this directory
- Include key entry-point files

**Prerequisites** (operational directories only):
- Format: `**Tool/Item** requirement - See [guide](link)`
- Tools with versions, required access/credentials (3-5 items max)
- Link to setup guides, never duplicate installation steps

**Getting Started** (operational directories only):
- Format: `**Action name**: Description - See [guide](link)`
- 3-5 steps for most common use case
- Link to comprehensive guides, don't duplicate them

**References** (required):
- Format: `[file/resource](link) - Brief description`
- Links to related READMEs and docs NOT already mentioned above
- 2-3 external resources maximum

## CONSTRAINTS - KISS & DRY

### Purpose
READMEs are for **onboarding** (what is this?), **navigation** (where to find details), and **context** (why it exists). NOT for tutorials, API docs, or duplicating other files.

### Length and Scannability
- **Target**: ~50 lines, maximum 100 lines
- **Reading time**: Under 1 minute (quick scan should reveal directory purpose)
- **If exceeding 100 lines**: Directory may be too complex - prompt developer to consider breaking into subdomain directories with their own 
READMEs

### Domain Separation
Each README documents ONLY its level. Parent mentions children exist and links to their READMEs. NO overlap.

### Eliminate Redundancy
- Directory tree has inline comments? Don't repeat in "Key Files" table
- External resource mentioned inline? Don't repeat in References
- Covered in Quick Links? Don't repeat in Getting Started
- **Rule**: Say it once, say it well, link to it elsewhere

### Always Link to README.md
Use `[Dir](../dir/README.md)` not ~~`../dir/`~~ so users land on documentation, not file listings.

## SECTION REQUIREMENTS

**Required** (all READMEs):
1. Title with metadata (date, author)
2. Overview (1-2 sentences + optional status)
3. Directory Structure (this level only, with purpose comments)
4. Quick Links (to READMEs and key docs)
5. References (non-redundant links only)

**Conditional** (operational directories only):
- Prerequisites (tools/access, 3-5 items, link to setup guides)
- Getting Started (3-5 steps for common use case, link to comprehensive guides)

DELETE THIS ENTIRE COMMENT BLOCK when generating the actual README.
-->

> **Last Updated**: YYYY-MM-DD by [First Name Last Name]

## Overview

[1-2 sentence executive summary: What does this directory contain and why does it exist?]

[Optional status indicator: (Active) | (Legacy) | (Archived) | (In Development)]

## Directory Structure

```text
[directory-name]/
├── [file.ext]            # Brief purpose description
├── [subdir1]/            # Brief purpose - See subdir1/README.md for details
├── [subdir2]/            # Brief purpose - See subdir2/README.md for details  
└── README.md             # This file
```

<!-- 
IMPORTANT: Only list items at THIS level. Do NOT drill into subdirectories.
Their contents are documented in their own README.md files.
-->

## Quick Links

- [`../docs/guide.md`](../docs/guide.md) - Related workflow or guide
- [`../other-dir/README.md`](../other-dir/README.md) - Related directory documentation
- [`./subdir/README.md`](./subdir/README.md) - Subdirectory details

<!-- DELETE Prerequisites and Getting Started sections if NOT an operational directory -->

## Prerequisites

<!-- INCLUDE only for operational directories (code, scripts, configs) -->
<!-- OMIT for pure documentation or archived directories -->

- **Tool Name** >= version - See [`setup-guide.md`](../docs/setup-guide.md)
- **Access/Credential** required - See [`access-guide.md`](../docs/access-guide.md)
- **Prior Setup** - See [`prerequisite-workflow.md`](../docs/prerequisite-workflow.md)

## Getting Started

<!-- INCLUDE only for directories where users execute commands/workflows -->
<!-- OMIT for pure documentation, archived, or reference directories -->
<!-- Focus on THE MOST COMMON use case only -->

1. **Action name**: Brief description

   ```shell
   command-example
   ```

2. **Action name**: Brief description - See [`detailed-guide.md`](../docs/detailed-guide.md)

3. **Action name**: Brief description

For complete workflows, see:

- [`comprehensive-workflow.md`](../docs/comprehensive-workflow.md)

## References

<!-- Link to README.md files and essential docs NOT already mentioned above -->
<!-- Do NOT repeat links from Quick Links or Getting Started -->

- [`../related-dir/README.md`](../related-dir/README.md) - Related directory documentation
- [`../docs/decision.md`](../docs/decision.md) - Decision rationale or guide
- [External resource](https://url.com) - When to use this resource

> README Template v1.0.2 - KemingHe/common-devx
