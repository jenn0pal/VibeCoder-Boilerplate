# Task Directory

> **Location for active phase-based feature implementation tasks**

## Overview

This directory contains **active task files** for multi-phase feature implementations. Each task file represents a single phase of a feature with a dedicated agent assignment.

## File Naming Convention

```
FEAT-[ID]-PHASE-[N]-[brief-description].md
```

**Examples:**
- `FEAT-001-PHASE-1-requirements.md` (Product Owner)
- `FEAT-001-PHASE-2-architecture.md` (Systems Architect)
- `FEAT-001-PHASE-3-api-implementation.md` (Backend Engineer)
- `FEAT-001-PHASE-4-ui-implementation.md` (Frontend Developer)
- `FEAT-001-PHASE-5-testing.md` (Test Engineer)

## Directory Structure

```
docs/.claude/tasks/
├── README.md                                    # This file
├── FEAT-001-PHASE-1-requirements.md            # Active task
├── FEAT-001-PHASE-2-architecture.md            # Active task
├── FEAT-002-PHASE-1-data-modeling.md           # Active task
└── ...
```

## Usage Workflow

### 1. Creating a New Multi-Phase Feature

When starting a new complex feature:

```
Load CLAUDE.md
Load docs/.claude/context/project-overview.md

I'm starting a new feature: [Feature Name]
This feature requires multiple phases with different specializations.

Please help me:
1. Create a feature implementation workflow using the template at:
   docs/.claude/_TEMPLATES/_BASE/feature-implementation-workflow.md
2. Break down the feature into logical phases
3. Assign appropriate agents to each phase
4. Create individual phase task files using the template at:
   docs/.claude/_TEMPLATES/_BASE/phase-task.md
```

### 2. Working on a Specific Phase

When you're ready to work on a phase:

```
Load CLAUDE.md
Load docs/.claude/context/project-overview.md
Load docs/.claude/_SYSTEM/agents/[agent-name].md
Load docs/.claude/tasks/FEAT-[ID]-PHASE-[N]-[brief-name].md

I need to complete Phase [N] of feature [Feature Name].
Please help me execute this phase following our conventions.
```

### 3. Completing a Phase

When a phase is complete:

1. ✅ Mark all checklist items as complete in the phase task file
2. ✅ Update the status to "Completed" with completion date
3. ✅ Complete the "Handoff to Next Phase" section
4. ✅ Update the parent feature workflow document
5. ✅ Archive the completed phase task (optional, or keep for reference)

### 4. Handling Dependencies

If a phase is blocked:

1. ⚠️ Update the task status to "Blocked"
2. ⚠️ Document the blocker in the "Blockers" section
3. ⚠️ Create an issue or discussion for the blocker
4. ⚠️ Work on other non-blocked phases (if available)

## Phase Task Lifecycle

```
┌─────────────┐
│ Not Started │
└──────┬──────┘
       │
       ▼
┌─────────────┐
│ In Progress │◄─────┐
└──────┬──────┘      │
       │             │
       ▼             │
┌─────────────┐      │
│   Blocked   │──────┘
└──────┬──────┘
       │
       ▼
┌─────────────┐
│   Review    │
└──────┬──────┘
       │
       ▼
┌─────────────┐
│  Completed  │
└─────────────┘
```

## Agent Assignment Quick Reference

| Phase Type | Agent | Template Section |
|------------|-------|------------------|
| Requirements & Planning | Product Owner | Phase 1 typical |
| Architecture & Design | Systems Architect | Phase 2 typical |
| Data Modeling | Backend Engineer / Data Engineer | Phase 2-3 |
| API Implementation | Backend Engineer | Phase 3 typical |
| UI/UX Implementation | Frontend Developer | Phase 4 typical |
| Database Optimization | Backend Engineer / Data Engineer | Any phase |
| Testing & QA | Test Engineer | Phase 5 typical |
| Security Review | Security Auditor | Any phase |
| Performance Tuning | Performance Optimizer | Any phase |
| CI/CD & Infrastructure | DevOps Engineer | Any phase |
| Code Review | Code Reviewer | Any phase |
| Documentation | Documentation Specialist | Final phase |

## Best Practices

### ✅ DO:

1. **Break features into logical phases** - Each phase should be independently completable
2. **Assign the right agent** - Match agent expertise to phase requirements
3. **Document dependencies** - Clearly specify what each phase needs from previous phases
4. **Include handoff information** - Make phase transitions smooth
5. **Update status regularly** - Keep task files current
6. **Test incrementally** - Don't wait until the end to test

### ❌ DON'T:

1. **Create monolithic tasks** - If a task takes > 2 days, break it into phases
2. **Skip agent assignments** - Each phase should have a designated agent
3. **Ignore dependencies** - Document and respect phase order
4. **Forget handoffs** - Always document what the next phase needs
5. **Leave tasks stale** - Archive or update old tasks
6. **Mix concerns** - Keep each phase focused on its specific objective

## Common Phase Patterns

### Full-Stack Feature (5 Phases)
```
FEAT-XXX-PHASE-1-requirements.md       (Product Owner)
FEAT-XXX-PHASE-2-architecture.md       (Systems Architect)
FEAT-XXX-PHASE-3-backend.md            (Backend Engineer)
FEAT-XXX-PHASE-4-frontend.md           (Frontend Developer)
FEAT-XXX-PHASE-5-testing.md            (Test Engineer)
```

### API-Only Feature (3 Phases)
```
FEAT-XXX-PHASE-1-design.md             (Systems Architect)
FEAT-XXX-PHASE-2-implementation.md     (Backend Engineer)
FEAT-XXX-PHASE-3-testing.md            (Test Engineer)
```

### Infrastructure Feature (3 Phases)
```
FEAT-XXX-PHASE-1-planning.md           (Systems Architect + DevOps)
FEAT-XXX-PHASE-2-implementation.md     (DevOps Engineer)
FEAT-XXX-PHASE-3-security.md           (Security Auditor + DevOps)
```

### Data Pipeline (4 Phases)
```
FEAT-XXX-PHASE-1-design.md             (Data Engineer)
FEAT-XXX-PHASE-2-ingestion.md          (Data Engineer)
FEAT-XXX-PHASE-3-processing.md         (Data Engineer)
FEAT-XXX-PHASE-4-monitoring.md         (Data Engineer + Performance Optimizer)
```

## Task Organization Tips

### Active Tasks
- Keep in `docs/.claude/tasks/`
- Update regularly
- Archive when complete (optional)

### Completed Tasks
- Either keep for reference
- Or move to `docs/.claude/archive/tasks/[feature-name]/`
- Update parent feature workflow to mark phase as complete

### Blocked Tasks
- Update status to "Blocked"
- Document blocker clearly
- Link to blocker ticket/issue
- Set up notifications for blocker resolution

## Integration with Other Workflows

### Feature Workflow
- Parent document: `docs/.claude/features/[feature-name]/feature-implementation-workflow.md`
- Contains overview of all phases
- Tracks overall feature progress

### Decision Log
- Document significant technical decisions
- Reference from task files
- Location: `docs/.claude/context/decision-log.md`

### Bug Tracking
- If bugs are found during implementation
- Create: `docs/.claude/bugs/BUG-[ID].md`
- Link from task file

### Code Modifications
- If phase requires refactoring
- Consider: `docs/.claude/modifications/MOD-[ID].md`
- Or: `docs/.claude/refactoring/REFACTOR-[ID].md`

## Examples

### Example 1: User Authentication Feature

```
Feature: User Authentication (FEAT-042)
Parent Workflow: docs/.claude/features/user-auth/feature-implementation-workflow.md

Phase 1: Requirements Definition
File: FEAT-042-PHASE-1-requirements.md
Agent: Product Owner
Status: Completed
Duration: 4 hours

Phase 2: Security Architecture
File: FEAT-042-PHASE-2-architecture.md
Agent: Systems Architect + Security Auditor
Status: Completed
Duration: 6 hours

Phase 3: Backend Implementation
File: FEAT-042-PHASE-3-backend.md
Agent: Backend Engineer
Status: In Progress
Duration: Est. 16 hours

Phase 4: Frontend Integration
File: FEAT-042-PHASE-4-frontend.md
Agent: Frontend Developer
Status: Not Started
Duration: Est. 12 hours

Phase 5: Security & Testing
File: FEAT-042-PHASE-5-security-testing.md
Agent: Security Auditor + Test Engineer
Status: Not Started
Duration: Est. 8 hours
```

### Example 2: Data Export Feature

```
Feature: CSV/Excel Export (FEAT-087)
Parent Workflow: docs/.claude/features/data-export/feature-implementation-workflow.md

Phase 1: Design & Requirements
File: FEAT-087-PHASE-1-design.md
Agent: Product Owner + Backend Engineer
Status: Completed

Phase 2: Backend Implementation
File: FEAT-087-PHASE-2-backend.md
Agent: Backend Engineer
Status: Completed

Phase 3: Frontend UI
File: FEAT-087-PHASE-3-frontend.md
Agent: Frontend Developer
Status: In Progress

Phase 4: Performance Testing
File: FEAT-087-PHASE-4-performance.md
Agent: Performance Optimizer
Status: Not Started
```

## Troubleshooting

### Issue: Phase is too large
**Solution:** Break it into sub-phases or multiple tasks

### Issue: Unclear agent assignment
**Solution:** Review the agent assignment guide in the feature workflow template

### Issue: Dependencies are blocking progress
**Solution:**
1. Document the blocker
2. Work on non-blocked phases
3. Escalate if blocker persists

### Issue: Phase scope is changing
**Solution:**
1. Update the phase task file
2. Update the parent feature workflow
3. Notify stakeholders
4. Consider if scope change requires new phase

## Related Documentation

- **Feature Workflow Template:** `docs/.claude/_TEMPLATES/_BASE/feature-implementation-workflow.md`
- **Phase Task Template:** `docs/.claude/_TEMPLATES/_BASE/phase-task.md`
- **Agent Guides:** `docs/.claude/_SYSTEM/agents/`
- **Project Conventions:** `docs/.claude/context/conventions.md`
- **Decision Log:** `docs/.claude/context/decision-log.md`

## Quick Commands

### Create new feature with phases:
```
Load docs/.claude/_TEMPLATES/_BASE/feature-implementation-workflow.md
Create new feature: [name]
```

### Start working on a phase:
```
Load docs/.claude/tasks/FEAT-[ID]-PHASE-[N]-[name].md
Load docs/.claude/_SYSTEM/agents/[agent].md
Begin phase [N]
```

### Complete a phase:
```
Load docs/.claude/tasks/FEAT-[ID]-PHASE-[N]-[name].md
Mark phase complete and prepare handoff
```

---

**Need Help?**
- Review templates in `docs/.claude/_TEMPLATES/`
- Check agent guides in `docs/.claude/_SYSTEM/agents/`
- See CLAUDE.md for overall workflow guidance
