# Commit Template - Long Format

Use for complex changes with multiple impacts or breaking changes.

**Plaintext only**: No markdown formatting. Use dashes, indents, and ALL CAPS headers for structure.

```plaintext
type(scope): brief description in imperative mood

closes #[issue-number]
closes #[issue-number]

BREAKING CHANGES
- [API or interface changes that require user action]

CHANGES
- [Key change 1]
- [Key change 2]
- [Key change 3]

IMPACT
- [How this affects users/system]
- [Performance or behavior changes]

TECHNICAL NOTES
- [Implementation details worth noting]
- [Dependencies or constraints]
```

## Section Guidelines

| Section | Required | When to Include |
| :--- | :--- | :--- |
| Title | Yes | Always |
| closes # | No | When resolving issues |
| BREAKING CHANGES | No | When backwards compatibility breaks |
| CHANGES | Yes | Always - list what changed |
| IMPACT | No | When user-facing behavior changes |
| TECHNICAL NOTES | No | When implementation details matter |

## Formatting for Complex Changes

When changes span multiple areas, use topic prefixes and nested bullets:

```plaintext
CHANGES
- [Component/Area 1]
  - [Specific change]
  - [Specific change]
- [Component/Area 2]
  - [Specific change]
```

**Agent guidance**:

- Group related changes under component/area as parent bullets
- Use 2-space indented sub-bullets for details
- Collapse trivial changes into single bullets
- Expand complex changes with context
- Ask user if grouping is unclear or if emphasis needed

---

> Commit Template Long v2.0.0 - KemingHe/common-devx
