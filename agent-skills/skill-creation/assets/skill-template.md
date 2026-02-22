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

## General Doc Constraints

Apply to all generated output. If a discovered template deviates from any rule (e.g., uses emojis semantically, uses a different bullet convention), note the deviation explicitly and confirm with the user before treating it as a permitted exception.

- **Characters**: QWERTY keyboard typeable only - no em-dashes, smart quotes, emojis, or special Unicode. Exception: `↑` for ToC navigation
- **Bullets**: Use dash (`-`) for all unordered lists; one bullet per complete thought; never wrap a bullet's content mid-sentence onto a continuation line; split into separate distinct bullets if too long or multi-thought. Nested sub-bullets for component grouping are permitted.
- **Prose lines**: One sentence per line; never wrap mid-sentence to a continuation line
- **Optional sections**: Strip `(optional)` or any parenthetical conditional label (e.g., `(if operational)`) from section headers when populating; omit the entire section (header and body) when unused
- **Consistency**: Use the same term for the same concept throughout; match the voice and tense of the template; do not mix header levels for parallel sections
- **Completeness**: Populate all template placeholders with actual content; do not leave bracketed placeholders (e.g., `[Job Title]`), `[TODO]`, or `[TBD]` in generated output
- **KISS and DRY**: Each section and bullet conveys unique information - no redundancy or overlap

> General Doc Constraints v1.0.0 - KemingHe/common-devx

## Skill Constraints

- [Constraint 1: e.g., character limits, format requirements specific to this skill]
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
