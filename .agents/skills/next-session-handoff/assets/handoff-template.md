# Handoff Template

Use for generating session handoff documents. Fill all sections with session-specific content. Omit sections that have no meaningful content rather than leaving placeholders.

**Markdown only**: Output as a markdown code block for user copy-paste.

```markdown
# Handoff - [branch or topic name]

Branch: [current branch name]
Date: [YYYY-MM-DD]
Previous session: [one-line summary of what was accomplished]

## Context

[2-4 sentences: what work is being done, why it exists, and where it stands. Include the triggering event or goal that started this work. State what was completed in this session and what remains.]

## Key Decisions

- [Decision 1: what was decided and why]
- [Decision 2: what was rejected and why]
- [Lesson or gotcha discovered during this session]

## Next Objectives

1. [Highest priority next task - what specifically needs to happen]
2. [Second priority task]
3. [Third priority task or deferred item with blocker noted]

## Resources

### Issues

- #[number]: [title] ([status])

### Files

- [path/to/key/file.md] - [why this file matters for next session]

### Skills

- [skill-name] - [what it's needed for]

### Tools

- [tool or CLI command] - [what it's needed for]

## Constraints

- [Security rule or policy that applies]
- [Scope boundary - what is explicitly out of scope]
- [Blocker - what cannot proceed until X resolves]
```

## Section Guidelines

| Section | Purpose | Audience |
| :--- | :--- | :--- |
| Context | What happened, where we are, why this work exists | Human and AI |
| Key Decisions | What was settled, rejected, or learned - prevents re-litigation | Human and AI |
| Next Objectives | What specifically needs to happen next, in priority order | Human and AI |
| Resources | Issues, files, skills, tools to reference - with precise paths and numbers | Primarily AI |
| Constraints | Security, scope boundaries, blockers - hard rules | Human and AI |

## When to Omit Sections

- **Key Decisions**: Omit if the session was purely exploratory with no binding choices
- **Resources subsections**: Omit empty subsections (e.g., skip Tools if no specific tools were used)
- **Constraints**: Omit if no security, scope, or blocking constraints were discovered

Never omit Context or Next Objectives - these are required for every handoff.
