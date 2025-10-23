# Modifications Directory

**Purpose:** Track significant code modifications requiring planning and documentation.

## When to Create Files Here

**Create modification file:**
- Medium/large changes (1+ hours)
- Multiple files affected
- Risk assessment needed

**Use CLAUDE.md prompt directly:**
- Small changes (< 1 hour)
- Single file modifications

## File Naming

```
MOD-[ID]-brief-description.md
```

Examples: `MOD-001-theme-orange.md`, `MOD-002-add-validation.md`

## Workflow

1. Copy template: `cp docs/.claude/_TEMPLATES/code-modification.md docs/.claude/modifications/MOD-XXX.md`
2. Fill out template
3. Load in Claude session
4. After completion: `mv` to `docs/.claude/archive/modifications/`

## Template Location

`docs/.claude/_TEMPLATES/code-modification.md`
