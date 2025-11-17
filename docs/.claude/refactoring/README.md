# Refactoring Directory

**Purpose:** Track significant refactoring efforts requiring phased approach and testing.

## When to Create Files Here

**Create refactoring plan:**
- Significant refactoring (2+ hours)
- Performance optimization
- Must preserve external behavior
- Multiple phases needed

**Use CLAUDE.md prompt directly:**
- Simple refactoring (< 2 hours)
- Single method/function cleanup

## File Naming

```
REFACTOR-[ID]-component-or-goal.md
```

Examples: `REFACTOR-001-user-dashboard.md`, `REFACTOR-002-auth-service.md`

## Critical Requirements

**BEFORE refactoring:**
- Tests must exist (80%+ coverage)
- All tests must pass
- Baseline metrics recorded

**DURING refactoring:**
- Small, incremental changes
- Run tests after each change
- Commit when tests green

## Workflow

1. Copy template: `cp docs/.claude/_TEMPLATES/_BASE/refactoring-plan.md docs/.claude/refactoring/REFACTOR-XXX.md`
2. Fill out current state and goals
3. Ensure tests exist and pass
4. Load in Claude session
5. Execute phase by phase
6. After completion: `mv` to `docs/.claude/archive/refactoring/`

## Template Location

`docs/.claude/_TEMPLATES/_BASE/refactoring-plan.md`
