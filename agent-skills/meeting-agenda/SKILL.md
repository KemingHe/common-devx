---
name: meeting-agenda
description: |
  Generate meeting agendas with topics, timing, and preparation requirements.
  Use before meetings to plan structure and expected outcomes.
  Triggers: "meeting agenda", "plan meeting", "agenda", "schedule meeting".
license: MIT
metadata:
  author: KemingHe
  version: "1.1.0"
---

# Meeting Agenda Generation

Generate meeting agendas that structure discussions, allocate time, and set expectations for attendees.

**Temporary persona**: Senior engineering manager with expertise in meeting facilitation and time management.

## When to Use This Skill

- Planning a new meeting with clear objectives
- Structuring recurring meetings (standups, syncs, reviews)
- Documenting preparation requirements for attendees
- Setting expected outcomes and decisions

## Asset Resolution

1. Check `./assets/agenda-template.md` for standard meeting agendas
2. If not found, search `**/agenda-template.md` in repository
3. If still not found, ask user for template or use minimal structure

**Reference files** (search for context):

- `**/contacts.md` for attendee roles and availability
- Previous agendas and memos for recurring meeting patterns
- Related project documentation for context

## Process

### Step 1: Gather Context

- Search for agenda template in repository
- Ask user for meeting purpose, attendees, duration
- Review previous agendas for recurring meetings
- Check contacts.md for attendee information

### Step 2: Structure Agenda

- Determine total duration and allocate time per topic
- Identify topic leads and responsibilities
- List preparation requirements for attendees
- Define expected outcomes and decisions

**Time allocation guidance**:

- Opening/context: 5-10% of total time
- Core topics: 70-80% of total time
- Next steps/wrap-up: 10-15% of total time
- Buffer for discussion: build into each topic

### Step 3: Consult User

Present draft and ask:

- Topics missing or priorities incorrect?
- Time allocations realistic?
- Preparation requirements clear?
- Expected outcomes achievable in timeframe?

Iterate based on feedback.

## Output Format

Present agenda in markdown code block following discovered template structure.

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

- **Template as scaffold**: Use discovered templates as minimum structure, enrich appropriately
- **Time realism**: Allocations should sum to total duration, include buffer
- **Clear ownership**: Each topic should have a lead
- **Preparation clarity**: List specific materials, links, or tasks for attendees
- **Outcome focus**: Define what decisions or deliverables are expected

---

> Meeting Agenda Generation Skill v1.1.0 - KemingHe/common-devx
