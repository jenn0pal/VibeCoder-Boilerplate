# Feature Implementation Workflow: [Feature Name]

> **Multi-phase feature implementation with agent assignments**
>
> Use this template to break down complex features into manageable phases,
> each with a dedicated task file and assigned specialized agent.

## Overview

**Feature ID:** FEAT-[ID]
**Date:** [YYYY-MM-DD]
**Priority:** [Critical/High/Medium/Low]
**Complexity:** [Simple/Medium/Complex]
**Estimated Effort:** [Total hours/days]
**Status:** [Planning/In Progress/Review/Completed]

## Feature Summary

### Business Goal
[Why are we building this? What business problem does it solve?]

### User Story
**As a** [type of user]
**I want** [capability]
**So that** [benefit]

### Success Criteria
- [ ] [Measurable criterion 1]
- [ ] [Measurable criterion 2]
- [ ] [Measurable criterion 3]

## Phase Breakdown

> **Important:** Each phase should have its own task file in `docs/.claude/tasks/`
> with format: `FEAT-[ID]-PHASE-[N]-[brief-description].md`

### Phase 1: [Phase Name]
**Agent:** [Agent Name]
**Estimated Effort:** [Hours]
**Dependencies:** [None or list prerequisites]

**Objective:** [What this phase accomplishes]

**Deliverables:**
- [ ] [Deliverable 1]
- [ ] [Deliverable 2]

**Task File:** `docs/.claude/tasks/FEAT-[ID]-PHASE-1-[brief-name].md`

---

### Phase 2: [Phase Name]
**Agent:** [Agent Name]
**Estimated Effort:** [Hours]
**Dependencies:** [Phase 1 or other requirements]

**Objective:** [What this phase accomplishes]

**Deliverables:**
- [ ] [Deliverable 1]
- [ ] [Deliverable 2]

**Task File:** `docs/.claude/tasks/FEAT-[ID]-PHASE-2-[brief-name].md`

---

### Phase 3: [Phase Name]
**Agent:** [Agent Name]
**Estimated Effort:** [Hours]
**Dependencies:** [Phase 2 or other requirements]

**Objective:** [What this phase accomplishes]

**Deliverables:**
- [ ] [Deliverable 1]
- [ ] [Deliverable 2]

**Task File:** `docs/.claude/tasks/FEAT-[ID]-PHASE-3-[brief-name].md`

---

## Agent Assignment Guide

### When to Use Which Agent

| Phase Type | Recommended Agent | When to Use |
|------------|------------------|-------------|
| **Planning & Requirements** | Product Owner | Defining specs, user stories, acceptance criteria |
| **Architecture Design** | Systems Architect | System design, tech stack decisions, API design |
| **Data Modeling** | Backend Engineer or Data Engineer | Database schema, models, migrations |
| **API Development** | Backend Engineer | REST/GraphQL APIs, business logic |
| **UI/UX Implementation** | Frontend Developer | React/Vue components, styling, user interactions |
| **Database Optimization** | Backend Engineer or Data Engineer | Query optimization, indexing, performance |
| **Testing Strategy** | Test Engineer | Test planning, test data, test automation |
| **Security Review** | Security Auditor | Security audit, vulnerability assessment |
| **Performance Tuning** | Performance Optimizer | Load testing, optimization, caching |
| **CI/CD Setup** | DevOps Engineer | Deployment, infrastructure, monitoring |
| **Code Review** | Code Reviewer | Quality review, standards compliance |
| **Documentation** | Documentation Specialist | API docs, user guides, technical writing |

### Agent Activation Examples

**Product Owner:**
```
Load CLAUDE.md
Load docs/.claude/context/project-overview.md
Load docs/.claude/_SYSTEM/agents/product-owner.md
Load docs/.claude/tasks/FEAT-[ID]-PHASE-1-requirements.md

I need to complete Phase 1 of this feature.
Please help me define the detailed requirements and acceptance criteria.
```

**Systems Architect:**
```
Load CLAUDE.md
Load docs/.claude/context/project-overview.md
Load docs/.claude/_SYSTEM/agents/systems-architect.md
Load docs/.claude/tasks/FEAT-[ID]-PHASE-2-architecture.md

I need to complete Phase 2 of this feature.
Please help me design the system architecture and technical approach.
```

**Backend Engineer:**
```
Load CLAUDE.md
Load docs/.claude/context/project-overview.md
Load docs/.claude/_SYSTEM/agents/backend-engineer.md
Load docs/.claude/tasks/FEAT-[ID]-PHASE-3-api-implementation.md

I need to complete Phase 3 of this feature.
Please help me implement the API endpoints and business logic.
```

**Frontend Developer:**
```
Load CLAUDE.md
Load docs/.claude/context/project-overview.md
Load docs/.claude/_SYSTEM/agents/frontend-developer.md
Load docs/.claude/tasks/FEAT-[ID]-PHASE-4-ui-implementation.md

I need to complete Phase 4 of this feature.
Please help me build the UI components and integrate with the API.
```

## Common Phase Patterns

### Pattern 1: Full-Stack Feature (5 Phases)
```
Phase 1: Requirements Definition (Product Owner)
Phase 2: System Architecture (Systems Architect)
Phase 3: Backend Implementation (Backend Engineer)
Phase 4: Frontend Implementation (Frontend Developer)
Phase 5: Testing & QA (Test Engineer)
```

### Pattern 2: Backend-Heavy Feature (4 Phases)
```
Phase 1: Requirements & Design (Product Owner + Systems Architect)
Phase 2: Data Modeling (Backend Engineer or Data Engineer)
Phase 3: API Implementation (Backend Engineer)
Phase 4: Testing & Documentation (Test Engineer + Documentation Specialist)
```

### Pattern 3: Frontend-Heavy Feature (3 Phases)
```
Phase 1: UI/UX Design (Product Owner + Frontend Developer)
Phase 2: Component Implementation (Frontend Developer)
Phase 3: Integration & Testing (Frontend Developer + Test Engineer)
```

### Pattern 4: Infrastructure Feature (3 Phases)
```
Phase 1: Infrastructure Planning (Systems Architect + DevOps Engineer)
Phase 2: Implementation & Configuration (DevOps Engineer)
Phase 3: Security & Monitoring (Security Auditor + DevOps Engineer)
```

### Pattern 5: Data Pipeline Feature (4 Phases)
```
Phase 1: Pipeline Design (Systems Architect + Data Engineer)
Phase 2: Data Ingestion (Data Engineer)
Phase 3: Data Processing (Data Engineer)
Phase 4: Monitoring & Optimization (Data Engineer + Performance Optimizer)
```

## Implementation Timeline

### Schedule

| Phase | Start Date | End Date | Duration | Status |
|-------|-----------|----------|----------|--------|
| Phase 1 | [Date] | [Date] | [Days] | ⏳ Pending |
| Phase 2 | [Date] | [Date] | [Days] | ⏳ Pending |
| Phase 3 | [Date] | [Date] | [Days] | ⏳ Pending |
| Phase 4 | [Date] | [Date] | [Days] | ⏳ Pending |
| Phase 5 | [Date] | [Date] | [Days] | ⏳ Pending |

### Milestones

- [ ] **M1:** Phase 1 Complete - Requirements Approved ([Date])
- [ ] **M2:** Phase 2 Complete - Architecture Approved ([Date])
- [ ] **M3:** Phase 3 Complete - Backend Ready ([Date])
- [ ] **M4:** Phase 4 Complete - Frontend Ready ([Date])
- [ ] **M5:** Feature Complete - All Tests Passing ([Date])

## Cross-Phase Dependencies

### Data Flow Between Phases

**Phase 1 Output → Phase 2 Input:**
- [What Phase 1 produces that Phase 2 needs]

**Phase 2 Output → Phase 3 Input:**
- [What Phase 2 produces that Phase 3 needs]

**Phase 3 Output → Phase 4 Input:**
- [What Phase 3 produces that Phase 4 needs]

### Shared Resources

**Database Schema:** [Where defined, when finalized]
**API Contracts:** [Where documented, who owns]
**UI Components:** [Where stored, reusability]

## Quality Assurance

### Per-Phase Quality Gates

**Phase 1 (Requirements):**
- [ ] All acceptance criteria defined
- [ ] Stakeholder approval obtained
- [ ] Technical feasibility confirmed

**Phase 2 (Architecture):**
- [ ] Architecture review passed
- [ ] Technical debt assessed
- [ ] Performance targets defined

**Phase 3 (Backend):**
- [ ] Unit tests passing (80%+ coverage)
- [ ] API tests passing
- [ ] Code review approved

**Phase 4 (Frontend):**
- [ ] Component tests passing
- [ ] Integration tests passing
- [ ] Accessibility compliance verified

**Phase 5 (Testing):**
- [ ] E2E tests passing
- [ ] Performance benchmarks met
- [ ] Security scan clean

### Overall Feature Quality Gates

- [ ] All phase deliverables completed
- [ ] All tests passing (unit, integration, e2e)
- [ ] Code review approved for all phases
- [ ] Documentation complete
- [ ] Performance targets met
- [ ] Security requirements satisfied
- [ ] Accessibility standards met

## Risk Management

### Phase-Specific Risks

**Phase 1 Risks:**
- [Risk] - Impact: [H/M/L] - Mitigation: [Strategy]

**Phase 2 Risks:**
- [Risk] - Impact: [H/M/L] - Mitigation: [Strategy]

**Phase 3 Risks:**
- [Risk] - Impact: [H/M/L] - Mitigation: [Strategy]

### Cross-Phase Risks

| Risk | Affected Phases | Impact | Mitigation |
|------|----------------|--------|------------|
| [Risk description] | [Phase 1, Phase 3] | High | [Strategy] |

### Contingency Plans

**If Phase N fails:**
- [Fallback strategy]
- [Alternative approach]
- [Rollback plan]

## Progress Tracking

### Completed Phases

- [x] **Phase 1:** [Name] - Completed [Date] by [Person]
  - Deliverables: [List]
  - Agent Used: [Agent Name]
  - Duration: [Actual hours]

### Current Phase

- [ ] **Phase 2:** [Name] - In Progress
  - Started: [Date]
  - Assigned Agent: [Agent Name]
  - Progress: [X%]
  - Blockers: [List or None]

### Upcoming Phases

- [ ] **Phase 3:** [Name] - Scheduled for [Date]
- [ ] **Phase 4:** [Name] - Scheduled for [Date]

## Communication & Handoffs

### Phase Handoff Checklist

When completing a phase and transitioning to the next:

- [ ] Update phase status in this workflow document
- [ ] Mark phase task file as completed
- [ ] Document key decisions in decision log
- [ ] Create next phase task file
- [ ] Notify next phase agent/team member
- [ ] Ensure all deliverables are accessible
- [ ] Conduct handoff meeting (if applicable)

### Phase Handoff Template

```markdown
## Phase [N] → Phase [N+1] Handoff

**From:** [Phase N Name] ([Agent])
**To:** [Phase N+1 Name] ([Agent])
**Date:** [YYYY-MM-DD]

### Completed Deliverables
- [Deliverable 1] - Location: [Path/URL]
- [Deliverable 2] - Location: [Path/URL]

### Key Decisions Made
- [Decision 1] - Rationale: [Why]
- [Decision 2] - Rationale: [Why]

### Important Context for Next Phase
- [Context 1]
- [Context 2]

### Open Questions
- [Question 1]
- [Question 2]

### Files Modified
- [File path] - [What changed]

### Next Steps for Phase [N+1]
1. [Step 1]
2. [Step 2]
3. [Step 3]
```

## Documentation

### Per-Phase Documentation

**Phase 1 Docs:**
- [ ] Requirements document
- [ ] User stories
- [ ] Acceptance criteria

**Phase 2 Docs:**
- [ ] Architecture diagrams
- [ ] API specifications
- [ ] Data models

**Phase 3 Docs:**
- [ ] API documentation
- [ ] Code comments
- [ ] Database migrations

**Phase 4 Docs:**
- [ ] Component documentation
- [ ] Style guide updates
- [ ] Integration guides

**Phase 5 Docs:**
- [ ] Test documentation
- [ ] User guides
- [ ] Deployment notes

### Centralized Documentation

**Feature Overview:** `docs/features/[feature-name]/README.md`
**API Docs:** `docs/api/[feature-name].md`
**Architecture:** `docs/architecture/[feature-name].md`
**Decision Log:** `docs/.claude/context/decision-log.md`

## Post-Implementation Review

### Feature Metrics

**Development Metrics:**
- Total Duration: [Actual] vs [Estimated]
- Total Effort: [Actual hours] vs [Estimated hours]
- Phases Completed: [X of Y]
- Code Changes: [+X/-Y lines]

**Quality Metrics:**
- Test Coverage: [X%]
- Bug Count: [X bugs found]
- Performance: [Meets/Exceeds/Below targets]
- Code Review Score: [Rating]

### Lessons Learned

**What Worked Well:**
- [Point 1]
- [Point 2]

**What Could Be Improved:**
- [Point 1]
- [Point 2]

**Agent Effectiveness:**
- [Agent Name]: [Feedback on effectiveness]
- [Agent Name]: [Feedback on effectiveness]

**Process Improvements:**
- [ ] [Improvement to implement for next feature]
- [ ] [Improvement to implement for next feature]

## Related

- **Feature Spec:** `docs/.claude/features/[feature-name]/spec.md`
- **Phase Task Files:** `docs/.claude/tasks/FEAT-[ID]-PHASE-*.md`
- **Related Features:** [FEAT-XXX]
- **Related Bugs:** [BUG-XXX]
- **Pull Requests:** [#PR-numbers]
- **Discussion:** [Links to discussions]

---

**Status:** [Planning/In Progress/Review/Completed]
**Last Updated:** [YYYY-MM-DD]
**Maintained By:** [Name/Team]
**Total Phases:** [N]
**Completed Phases:** [X of N]
