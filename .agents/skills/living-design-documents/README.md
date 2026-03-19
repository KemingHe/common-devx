# README - Living Design Documents

> **Last Updated**: 2026-03-19 by Keming He

Create and maintain three living design documents (Core Decisions, Taxonomy, Parked) that guide development through structured design thinking. Documents graduate upward as content matures from deferred analysis to detailed specifications to load-bearing policies.

## Quick Start

Use this skill when you need to:

- Bootstrap design documentation for a new project
- Document design decisions during development
- Manage growing project complexity with structured docs
- Perform design audits (7 days for solo projects, 30 days for teams)
- Generate valuable open questions that catch surprises before development

Tell your AI agent: "Create design docs for this project" or "Update design taxonomy for [component]" or "Audit design documents".

## Document Types

| Document | Content | Graduation Path |
| :--- | :--- | :--- |
| Core Decisions | One-sentence load-bearing policies | Terminal - content stays here |
| Taxonomy | Detailed component specifications | FROM Parked when analyzed; TO Core when load-bearing |
| Parked | Deferred analysis and granular details | TO Taxonomy when analysis complete |

## Files

```plaintext
living-design-documents/
├── SKILL.md                                    # AI instructions for design docs
├── README.md                                   # This file
└── assets/
    ├── design-core-decisions-template.md       # Project-wide policies
    ├── design-taxonomy-[component]-template.md # Component specifications
    └── design-parked-[component]-template.md   # Deferred details
```

## Skill Constraints

- Line limits: <200 ideal, 200-500 recommend split, >500 must split
- Audit intervals: 7 days (solo), 30 days (team)
- Core Decisions: inward refs only, never refs out
- Open Questions: mandatory at doc level in all documents
- Related Issues: `### [Subcomponent] - Related Issues` with 2-5 word descriptions

## License

MIT License
