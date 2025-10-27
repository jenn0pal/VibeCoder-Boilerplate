# Phase Task: [Phase Name]

> **Single-phase implementation task with dedicated agent**
>
> This task is part of a multi-phase feature implementation.
> Complete this phase before moving to the next phase.

## Task Identification

**Task ID:** FEAT-[ID]-PHASE-[N]-[brief-description]
**Feature:** [Parent Feature Name] (FEAT-[ID])
**Phase Number:** [N of M]
**Date Created:** [YYYY-MM-DD]
**Assigned Agent:** [Agent Name]
**Estimated Effort:** [Hours/Days]
**Priority:** [Critical/High/Medium/Low]

## Context

### Parent Feature
**Feature:** [Feature Name]
**Feature File:** `docs/.claude/features/[feature-name]/feature-implementation-workflow.md`
**Overall Goal:** [Brief description of the complete feature]

### This Phase's Role
[Explain how this phase fits into the overall feature implementation]

### Dependencies
**Requires:**
- [ ] [Previous phase or external dependency]
- [ ] [Previous phase or external dependency]

**Blocks:**
- [ ] [Next phase that depends on this phase]
- [ ] [Next phase that depends on this phase]

## Agent Assignment

### Why This Agent?

**Assigned Agent:** [Agent Name]

**Reason for Assignment:**
[Explain why this specific agent was chosen for this phase]

**Agent Strengths for This Phase:**
- [Relevant skill 1]
- [Relevant skill 2]
- [Relevant skill 3]

### Agent Activation Prompt

```
Load CLAUDE.md
Load docs/.claude/context/project-overview.md
Load docs/.claude/_SYSTEM/agents/[agent-name].md
Load docs/.claude/tasks/FEAT-[ID]-PHASE-[N]-[brief-description].md

I need to complete Phase [N] of feature [Feature Name].
This phase focuses on [phase objective].

Please help me [specific request based on phase type]:
- [Action 1]
- [Action 2]
- [Action 3]
```

## Phase Objective

### Primary Goal
[What this phase must accomplish - clear, measurable objective]

### Success Criteria
- [ ] [Specific, measurable criterion 1]
- [ ] [Specific, measurable criterion 2]
- [ ] [Specific, measurable criterion 3]

### Out of Scope
[What this phase explicitly does NOT include - to prevent scope creep]

## Deliverables

### Required Deliverables

1. **[Deliverable 1 Name]**
   - **Format:** [File type/format]
   - **Location:** [Where it will be saved]
   - **Acceptance Criteria:** [How to verify it's complete]

2. **[Deliverable 2 Name]**
   - **Format:** [File type/format]
   - **Location:** [Where it will be saved]
   - **Acceptance Criteria:** [How to verify it's complete]

3. **[Deliverable 3 Name]**
   - **Format:** [File type/format]
   - **Location:** [Where it will be saved]
   - **Acceptance Criteria:** [How to verify it's complete]

### Optional Deliverables
- [Optional deliverable 1]
- [Optional deliverable 2]

## Detailed Requirements

### Functional Requirements

**FR-1:** [Requirement Name]
- **Description:** [Detailed description]
- **Acceptance:** [How to verify]
- **Priority:** [Must-have/Should-have/Nice-to-have]

**FR-2:** [Requirement Name]
- **Description:** [Detailed description]
- **Acceptance:** [How to verify]
- **Priority:** [Must-have/Should-have/Nice-to-have]

### Technical Requirements

**TR-1:** [Technical Constraint or Requirement]
- **Details:** [Specific technical details]
- **Rationale:** [Why this is required]

**TR-2:** [Technical Constraint or Requirement]
- **Details:** [Specific technical details]
- **Rationale:** [Why this is required]

### Quality Requirements

- **Test Coverage:** [Target percentage]
- **Performance:** [Specific metrics]
- **Security:** [Security requirements]
- **Accessibility:** [Accessibility standards]

## Implementation Plan

### Step 1: [First Step]
**Goal:** [What this step accomplishes]

**Actions:**
- [ ] [Specific action 1]
- [ ] [Specific action 2]
- [ ] [Specific action 3]

**Validation:** [How to verify this step is complete]

---

### Step 2: [Second Step]
**Goal:** [What this step accomplishes]

**Actions:**
- [ ] [Specific action 1]
- [ ] [Specific action 2]
- [ ] [Specific action 3]

**Validation:** [How to verify this step is complete]

---

### Step 3: [Third Step]
**Goal:** [What this step accomplishes]

**Actions:**
- [ ] [Specific action 1]
- [ ] [Specific action 2]
- [ ] [Specific action 3]

**Validation:** [How to verify this step is complete]

---

### Step 4: [Fourth Step]
**Goal:** [What this step accomplishes]

**Actions:**
- [ ] [Specific action 1]
- [ ] [Specific action 2]
- [ ] [Specific action 3]

**Validation:** [How to verify this step is complete]

## Input from Previous Phase

### Artifacts Received
[What was delivered from the previous phase that this phase will use]

1. **[Artifact 1]**
   - Location: [Path/URL]
   - Format: [Type]
   - Key Information: [What's important in this artifact]

2. **[Artifact 2]**
   - Location: [Path/URL]
   - Format: [Type]
   - Key Information: [What's important in this artifact]

### Key Decisions from Previous Phase
- [Decision 1] - Rationale: [Why]
- [Decision 2] - Rationale: [Why]

### Constraints from Previous Phase
- [Constraint 1]
- [Constraint 2]

## Output for Next Phase

### Artifacts to Produce
[What this phase will deliver to the next phase]

1. **[Artifact 1]**
   - Format: [Type]
   - Will contain: [Description]
   - Used by next phase for: [Purpose]

2. **[Artifact 2]**
   - Format: [Type]
   - Will contain: [Description]
   - Used by next phase for: [Purpose]

### Decisions to Document
- [Decision area 1 that next phase needs to know]
- [Decision area 2 that next phase needs to know]

### Handoff Requirements
- [ ] [What must be communicated to the next phase]
- [ ] [What must be documented for the next phase]

## Testing Strategy

### Test Types for This Phase

**Unit Tests:**
- [ ] [Test scenario 1]
- [ ] [Test scenario 2]
- [ ] [Test scenario 3]

**Integration Tests:**
- [ ] [Test scenario 1]
- [ ] [Test scenario 2]

**Manual Tests:**
- [ ] [Test scenario 1]
- [ ] [Test scenario 2]

### Test Coverage Target
- **Target:** [X%]
- **Measurement:** [How to measure]
- **Tools:** [Testing framework/tools to use]

### Test Data Requirements
- [Test data set 1 needed]
- [Test data set 2 needed]

## Technical Specifications

### Architecture Constraints
[Any architectural decisions or constraints that apply to this phase]

### Technology Stack
- **Language/Framework:** [Specific tech for this phase]
- **Libraries/Packages:** [Dependencies to use]
- **Tools:** [Development tools]

### Code Structure
```
[Expected file/directory structure]
src/
  [component]/
    [file1.ext]
    [file2.ext]
```

### Design Patterns
- **Pattern 1:** [Name] - [Where/How to apply]
- **Pattern 2:** [Name] - [Where/How to apply]

### API Contracts (if applicable)

**Endpoints/Methods to Implement:**

```
[HTTP Method] /api/[path]
Request:
{
  "field": "type"
}

Response:
{
  "field": "type"
}
```

### Database Schema (if applicable)

**Tables/Models to Create/Modify:**

```sql
CREATE TABLE [table_name] (
  id UUID PRIMARY KEY,
  [field] [type],
  ...
);
```

## Quality Gates

### Phase Completion Checklist

**Code Quality:**
- [ ] All code follows project conventions
- [ ] No linting errors
- [ ] No security vulnerabilities
- [ ] Code reviewed and approved
- [ ] Comments and documentation added

**Testing:**
- [ ] All tests passing
- [ ] Test coverage meets target ([X%])
- [ ] Edge cases covered
- [ ] Performance tests passing (if applicable)

**Documentation:**
- [ ] Code documented
- [ ] README/guides updated
- [ ] API documentation updated (if applicable)
- [ ] Decision log updated

**Integration:**
- [ ] Builds successfully
- [ ] No breaking changes (or documented)
- [ ] Dependencies updated
- [ ] Environment variables documented

### Review Requirements

**Code Review:**
- **Reviewer:** [Name or Role]
- **Focus Areas:** [What to review carefully]
- **Approval Required:** [Yes/No]

**Technical Review:**
- **Reviewer:** [Name or Role]
- **Focus Areas:** [Architecture, performance, security]
- **Approval Required:** [Yes/No]

## Risk Management

### Risks Specific to This Phase

| Risk | Likelihood | Impact | Mitigation Strategy |
|------|------------|--------|-------------------|
| [Risk 1] | Low/Med/High | Low/Med/High | [How to mitigate] |
| [Risk 2] | Low/Med/High | Low/Med/High | [How to mitigate] |

### Blockers

**Current Blockers:**
- [None or list current blockers]

**Potential Blockers:**
- [Potential blocker 1] - Contingency: [Plan]
- [Potential blocker 2] - Contingency: [Plan]

### Fallback Plan
[What to do if this phase cannot be completed as planned]

## Progress Tracking

### Status: [Not Started/In Progress/Blocked/Review/Completed]

### Timeline

**Planned:**
- Start: [Date]
- End: [Date]
- Duration: [X days]

**Actual:**
- Started: [Date]
- Completed: [Date]
- Duration: [X days]

### Completion Percentage: [X%]

### Daily Progress Log

**[Date]:**
- Completed: [What was done]
- Next: [What's next]
- Blockers: [Any issues]

**[Date]:**
- Completed: [What was done]
- Next: [What's next]
- Blockers: [Any issues]

## Communication

### Stakeholders
- **Primary:** [Name/Role] - [What they care about]
- **Secondary:** [Name/Role] - [What they care about]

### Updates Required
- **Frequency:** [Daily/Weekly/On milestone]
- **Method:** [Slack/Email/Meeting]
- **Content:** [What to communicate]

### Escalation Path
[Who to contact if there are critical issues]

## Resources

### Documentation to Reference
- [Document 1] - `[path]`
- [Document 2] - `[path]`

### Similar Implementations
- [Example 1] - [Where to find it]
- [Example 2] - [Where to find it]

### External Resources
- [Tutorial/Guide 1] - [URL]
- [Library documentation] - [URL]

## Files Affected

### Files to Create
- `[path/to/file1]` - [Purpose]
- `[path/to/file2]` - [Purpose]

### Files to Modify
- `[path/to/file1]` - [What changes]
- `[path/to/file2]` - [What changes]

### Files to Delete
- `[path/to/file1]` - [Reason for deletion]

## Phase Completion

### Completion Checklist

- [ ] All deliverables produced
- [ ] All success criteria met
- [ ] All tests passing
- [ ] Code reviewed and approved
- [ ] Documentation complete
- [ ] Handoff document prepared
- [ ] Next phase task file created
- [ ] Feature workflow document updated
- [ ] Decision log updated (if significant decisions made)

### Sign-off

**Developer:** [Name] - Date: [YYYY-MM-DD]
**Reviewer:** [Name] - Date: [YYYY-MM-DD]
**Approver:** [Name] - Date: [YYYY-MM-DD]

### Handoff to Next Phase

**Next Phase:** FEAT-[ID]-PHASE-[N+1]-[brief-description]
**Next Agent:** [Agent Name]
**Handoff Date:** [YYYY-MM-DD]
**Handoff Document:** [Link to handoff document in feature workflow]

## Lessons Learned

### What Went Well
- [Point 1]
- [Point 2]

### What Could Be Improved
- [Point 1]
- [Point 2]

### Recommendations for Similar Tasks
- [Recommendation 1]
- [Recommendation 2]

### Agent Effectiveness
**How well did the assigned agent perform?**
- [Feedback on agent effectiveness]
- [Suggestions for improvement]

## Related

- **Parent Feature:** `docs/.claude/features/[feature-name]/feature-implementation-workflow.md`
- **Previous Phase:** `FEAT-[ID]-PHASE-[N-1]-[name].md`
- **Next Phase:** `FEAT-[ID]-PHASE-[N+1]-[name].md`
- **Related Decisions:** Decision log entries [#XXX, #YYY]
- **Pull Request:** [#PR-number]
- **Branch:** `feature/FEAT-[ID]-phase-[N]-[brief-name]`

---

**Status:** [Not Started/In Progress/Blocked/Review/Completed]
**Last Updated:** [YYYY-MM-DD]
**Assigned To:** [Person Name]
**Completed:** [YYYY-MM-DD or N/A]
