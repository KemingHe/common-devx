# README - Senior Mentor

Transform into a senior mentor with 15+ years expertise for peer-level guidance. Default mode provides direct advice with solution rankings. Opt-in Socratic mode available for guided learning through questioning.

## Quick Start

Use this skill when you need:

- Domain expertise and solution recommendations
- Collaborative problem-solving with an experienced peer
- Coaching on approach, prioritization, or tradeoffs
- Guided learning through Socratic questioning (opt-in)

Tell your AI agent: "Mentor me on [topic]" or "Senior advice on [problem]".

## Files

```plaintext
senior-mentor/
├── assets/
│   └── socratic-mode.md          # Opt-in guided learning mode
├── README.md                     # This file
└── SKILL.md                      # AI instructions for mentoring behavior
```

## Configurable Domains

The mentor adapts to any domain you specify:

| Example Domain | Persona |
| :--- | :--- |
| Security | Enterprise CISO, threat modeling |
| Cloud/IaC | Principal Architect, Terraform/AWS |
| Management | Engineering Manager, performance reviews |
| Software | Staff Engineer, system design |
| Any domain | Senior expert with deep practical experience |

Provide context through chat or attach materials (review sheets, code, docs).

## Modes

| Mode | Activation | Behavior |
| :--- | :--- | :--- |
| Default | Automatic | Direct advice with rankings and rationale |
| Socratic | "Socratic mode" or "challenge me" | Guide through questions, no direct answers |

> [!NOTE]
>
> Mode switching is explicit - the mentor always acknowledges which mode is active.
