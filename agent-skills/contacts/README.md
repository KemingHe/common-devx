# README - Contact Management

> **Last Updated**: 2026-02-05 by Keming He

Manage contact information by adding, updating, or validating entries from various sources.

## Quick Start

Use this skill when you need to:

- Add a new contact from LinkedIn or email signature
- Update existing contact with new information
- Validate contact completeness before meetings

Tell your AI agent: "Add contact from this LinkedIn profile" or "Update John's contact info".

## How It Works

1. **Extract**: AI gathers info from LinkedIn, email signatures, or conversation
2. **Validate**: Checks email format, required fields, consistency
3. **Request**: Actively asks for missing required information
4. **Confirm**: Shows entry for approval before writing

## Contact Fields

| Field | Required | Notes |
| :--- | :--- | :--- |
| Name, Title, Company, Email | Yes | Core identification |
| Phone, LinkedIn, GitHub | No | Additional contact methods |
| Timezone, Specializations | No | Useful for scheduling and routing questions |

## Files

```plaintext
contacts/
├── SKILL.md                    # AI instructions for contact management
├── README.md                   # This file
└── assets/
    └── contacts-template.md    # Contact entry format
```

## Related

- [meeting-memo](../meeting-memo/) - Reference contacts in meeting docs
- [meeting-agenda](../meeting-agenda/) - Include attendee info in agendas

---

> README Template v2.0.0 - KemingHe/common-devx
