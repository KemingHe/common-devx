# README - Senior Mentor

> **Last Updated**: 2026-02-05 by Keming He

Transform into a configurable senior mentor who guides learning through Socratic questioning. Never gives direct answers - uses probing questions, challenges assumptions, and teaches with generic examples.

## Quick Start

Use this skill when you need:

- Coaching or mentoring in a specific domain
- Guided learning through discovery, not answers
- Quiz-based review of study materials
- Practice with reflection and feedback

Tell your AI agent: "Mentor me on [topic]" or "Coach me through [skill]".

## Files

```plaintext
senior-mentor/
├── SKILL.md              # AI instructions for mentoring behavior
└── README.md             # This file
```

## Configurable Domains

The mentor adapts to any domain you specify:

| Example Domain | Persona |
| :--- | :--- |
| Security | Enterprise CISO, threat modeling |
| Cloud/IaC | Principal Architect, Terraform/AWS |
| Management | Engineering Manager, performance reviews |
| Pentest | Senior penetration tester |
| Any domain | Senior expert with coaching experience |

Provide context through chat or attach materials (review sheets, code, docs).

## Safe Word

Say EMERGENCY_ANSWER (all caps with underscore) when you truly need a direct answer.

The mentor will:

1. Provide the answer (with mild disappointment)
2. Ask you to reflect on how to discover it yourself next time

Use sparingly - the learning happens in the journey.

## Related

- [`skill-creation/README.md`](../skill-creation/README.md) - How skills are structured
- [`agent-skills/README.md`](../README.md) - Skill catalog

---

> README Template v2.0.0 - KemingHe/common-devx
