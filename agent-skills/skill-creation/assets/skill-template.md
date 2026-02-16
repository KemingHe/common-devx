---
name: [skill-name]
description: |
  [One-line summary of what this skill does.]
  [When to use it.] Triggers: "[keyword1]", "[keyword2]", "[keyword3]".
license: [license]
metadata:
  author: [AuthorName]
  version: "1.0.0"
---

# [Skill Name]

[Brief description of the skill's purpose.]

**Temporary persona**: [Optional: Brief expertise statement, e.g., "Senior engineer with expertise in X."]

## When to Use This Skill

- [Scenario 1 that triggers this skill]
- [Scenario 2 that triggers this skill]
- [Scenario 3 that triggers this skill]

## Asset Resolution

1. Check `./assets/[template-name].md` (skill-local)
2. If not found, search `**/[template-name].md` in repository
3. If still not found, [fallback action: ask user or generate from scratch]

<!-- OPTIONAL: Include safety section for skills that interact with external systems
## [System] Operations (Read-Only)

This skill performs read-only reconnaissance. Never modify [system] state.

**Setup**: [Preparation required, e.g., "Pipe git commands to `cat` to avoid interactive mode."]

**Safe commands**:

```shell
[command1] | cat                  # [description]
[command2] | cat                  # [description]
```

**Forbidden operations**: Never use [list of prohibited commands].

**Prefer remote tools**: Use [MCP/API alternatives] when available.
-->

## Process

### Step 1: [Gather Context]

[Instructions for initial information gathering]

- [What to analyze]
- [What to ask user if needed]

### Step 2: [Perform Action]

[Core instructions for the skill's main task]

### Step 3: [Generate Output]

[Instructions for producing the final output]

## Output Format

```[format]
[Expected output structure with placeholders]
```

## Constraints

- **Characters**: QWERTY keyboard typeable only - no em-dashes, smart quotes, emojis, or special Unicode. Exception: `↑` for ToC navigation
- [Constraint 1: e.g., character limits, format requirements]
- [Constraint 2: e.g., what NOT to do]
- [Constraint 3: e.g., required validations]

## Examples

### Good Example

```[format]
[Example of correct output]
```

### Bad Example

```[format]
[Example of incorrect output with explanation]
```

[Explanation of why it's bad]

---

> [Skill Name] Skill v1.0.0 - KemingHe/common-devx
