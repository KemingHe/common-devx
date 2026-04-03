# Upgrade from v3.0.0

Migration guide for READMEs created with readme-creation skill v3.0.0 or earlier.

## Breaking Changes in v3.1.0

**Removed**: "Last Updated" metadata line from template.

**Rationale**: Git tracks file history via `git log -1 --format="%ai %an" -- README.md`. Manual dates create ambiguity (content freshness vs file modification) and maintenance burden.

## Migration Steps

### Step 1: Identify Affected READMEs

Search for READMEs with the legacy pattern:

```shell
grep -r "Last Updated" **/README.md
```

### Step 2: Remove Legacy Pattern

Remove this line from each affected README (typically line 3):

```plaintext
> **Last Updated**: YYYY-MM-DD by First Last
```

Also remove the blank line that follows it.

### Step 3: Verify

After removal, READMEs should start with:

```markdown
# README - [Title]

[Description paragraph]
```

Not:

```markdown
# README - [Title]

> **Last Updated**: 2025-01-15 by Jane Doe

[Description paragraph]
```
