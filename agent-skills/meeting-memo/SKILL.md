---
name: meeting-memo
description: |
  Generate meeting memos capturing decisions, actions, and key discussions.
  Use after meetings to document outcomes and next steps.
  Triggers: "meeting memo", "meeting notes", "document meeting", "standup".
license: MIT
metadata:
  author: KemingHe
  version: "3.1.0"
---

# Meeting Memo Generation

Generate meeting memos that capture decisions, actions, and insights with precision following project templates.

**Temporary persona**: Senior engineering manager with expertise in meeting facilitation and documentation standards.

## When to Use This Skill

- Documenting meeting outcomes and decisions
- Creating action item lists with ownership
- Writing daily standup summaries
- Capturing key discussions for future reference

## Asset Resolution

1. Check `./assets/memo-template.md` for standard meeting memos
2. Check `./assets/standup-template.md` for daily standups
3. If not found, search `**/memo-template.md` or `**/standup-template.md` in repository
4. If still not found, ask user for template or use minimal structure

**Reference files** (search for context):

- `**/contacts.md` for attendee roles and background
- Previous memos in same directory for ongoing context
- Related meeting agendas for planned discussion topics

## Process

### Step 1: Gather Context

- Search for memo template in repository
- Review historical memos for ongoing context
- Check contacts.md for attendee information
- Request meeting transcripts, notes, or recordings from user

### Step 2: Create Memo

- Extract all decisions, action items, key discussions from source material
- Capture critical information completely - memos can be longer when needed
- Apply KISS and DRY: each bullet conveys unique information, no overlap
- Attribute points that rely on attendee/organization credibility
- Rank decisions by importance and impact, not chronological order
- Follow template structure with proper formatting

**Enrichment guidance**:

- Decisions: Include rationale and alternatives considered
- Actions: Specify owner, deadline, and success criteria when known
- Context: Link to related documents, issues, or previous discussions
- References (optional): Include when external docs, links, or prior work are discussed
- Glossary (optional): Include when meeting uses multiple acronyms or technical terms

### Step 3: Refine with User

Present draft and ask:

- Missing context or unclear decisions?
- Decision priorities and ranking correct?
- Action item ownership and deadlines accurate?
- Any corrections or additions?

Iterate based on feedback while maintaining structure.

## Output Format

Present memo in markdown code block following discovered template structure.

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
- **Completeness**: Capture all decisions, actions, discussions from source material
- **Information fidelity**: Preserve quotes, data points, technical terms exactly
- **Appropriate length**: Longer memos acceptable when content requires it
- **Decision hierarchy**: Rank by impact, not meeting sequence
- **Attribution**: Attribute credibility-dependent info, skip for established facts
- **Action clarity**: Include ownership and deadlines when specified
- **Characters exception**: `memo-template.md` uses 🔴🟠🟡🟢 as functional priority indicators in the ACTION ITEMS table - these are permitted per template

---

> Meeting Memo Generation Skill v3.1.0 - KemingHe/common-devx
