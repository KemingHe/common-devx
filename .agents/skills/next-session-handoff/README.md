# README - Next Session Handoff

Generate structured handoff documents for context transfer across AI session boundaries.

## Quick Start

Use this skill when you need to:

- Preserve session context before starting a new conversation
- Transfer decisions, objectives, and resources to the next session
- Prevent the next session from re-debating settled questions

Tell your AI agent: "Generate a session handoff" or "Wrap up this session with a handoff".

## Directory Structure

```plaintext
next-session-handoff/
├── assets/
│   └── handoff-template.md         # 5-section handoff document template
├── README.md                       # This file
└── SKILL.md                        # AI instructions for generating handoffs
```

## Handoff Structure

| # | Section | Purpose |
| :--- | :--- | :--- |
| 1 | Context | What happened, where we are, why this work exists |
| 2 | Key Decisions | What was settled, rejected, or learned |
| 3 | Next Objectives | What specifically needs to happen next |
| 4 | Resources | Issues, files, skills, tools to reference |
| 5 | Constraints | Security, scope boundaries, blockers |

## Skill Constraints

- Output as markdown code block for copy-paste only
- Human-mediated context transfer (not A2A)
- Distill signal from the session rather than transcribing
- User reviews and approves before copying to next session
