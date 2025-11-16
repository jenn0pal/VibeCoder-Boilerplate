# Features Directory

> **Purpose:** Organize feature specifications, implementation workflows, and working documentation for all product features.

## Overview

This directory contains detailed documentation for each feature in the project. Each feature gets its own subdirectory with comprehensive specifications and implementation tracking.

## Directory Structure

```
docs/.claude/features/
├── README.md                    # This file
├── [feature-name-1]/
│   ├── spec.md                  # Feature specification
│   ├── implementation-workflow.md # Multi-phase workflow (if complex)
│   ├── api-design.md            # API design (if applicable)
│   ├── ui-mockups/              # UI designs (if applicable)
│   └── notes.md                 # Implementation notes
├── [feature-name-2]/
│   └── spec.md
└── [feature-name-3]/
    ├── spec.md
    └── implementation-workflow.md
```

## When to Create a Feature Directory

**Create a feature directory when:**
- The feature requires detailed specification
- Multiple team members will work on it
- The feature spans multiple components/layers
- You need to track implementation progress
- The feature has complex business logic
- API or database design is needed

**Use inline/quick development for:**
- Small UI tweaks
- Simple bug fixes
- One-file changes
- Obvious implementations

## Feature Workflow

### 1. Planning Phase

**Create the feature directory:**
```bash
mkdir -p docs/.claude/features/user-authentication
```

**Create the specification:**
```bash
# Copy template
cp docs/.claude/_TEMPLATES/_BASE/feature-spec-detailed.md \
   docs/.claude/features/user-authentication/spec.md

# Edit the spec
# Fill in: objectives, user stories, requirements, acceptance criteria
```

**Review with team/stakeholders:**
- Get feedback on spec
- Refine requirements
- Prioritize features
- Estimate effort

### 2. Implementation Phase

#### Simple Feature (Single-Phase)

**For straightforward features that can be implemented in one go:**

```
Load CLAUDE.md
Load docs/.claude/context/project-overview.md
Load docs/.claude/features/user-authentication/spec.md

Implement the user authentication feature following our conventions.
```

Claude will:
- Read the spec
- Implement the feature
- Write tests
- Update documentation

#### Complex Feature (Multi-Phase)

**For features requiring multiple specializations:**

**Step 1: Create implementation workflow**
```bash
cp docs/.claude/_TEMPLATES/_BASE/feature-implementation-workflow.md \
   docs/.claude/features/user-authentication/implementation-workflow.md
```

**Step 2: Break down into phases**
Edit `implementation-workflow.md` and define phases:
- Phase 1: Backend API (Backend Engineer)
- Phase 2: Database Schema (Backend Engineer)
- Phase 3: Frontend UI (Frontend Developer)
- Phase 4: Integration Tests (Test Engineer)
- Phase 5: Security Audit (Security Auditor)

**Step 3: Create phase task files**
```bash
# For each phase, create a task file
cp docs/.claude/_TEMPLATES/_BASE/phase-task.md \
   docs/.claude/tasks/FEAT-001-PHASE-1-backend-api.md
```

**Step 4: Execute phases sequentially**
```
Load CLAUDE.md
Load docs/.claude/context/project-overview.md
Load docs/.claude/_SYSTEM/agents/backend-engineer.md
Load docs/.claude/tasks/FEAT-001-PHASE-1-backend-api.md

Execute Phase 1: Backend API development
```

Repeat for each phase with appropriate agent.

### 3. Completion Phase

**After implementation:**
- [ ] All acceptance criteria met
- [ ] Tests passing (unit, integration, E2E)
- [ ] Documentation updated
- [ ] Code reviewed
- [ ] Feature deployed to staging/production
- [ ] Stakeholder acceptance

**Archive the feature:**
```bash
# Move completed feature to archive
mv docs/.claude/features/user-authentication \
   docs/.claude/archive/features/user-authentication-2025-01
```

Or keep it for reference if it's a core feature.

## Feature Naming Conventions

### Directory Names
- Use kebab-case: `user-authentication`, `payment-processing`
- Be descriptive but concise
- Avoid version numbers (use git instead)

### File Names
- `spec.md` - Feature specification
- `implementation-workflow.md` - Multi-phase workflow
- `api-design.md` - API endpoint design
- `db-schema.md` - Database schema changes
- `notes.md` - Implementation notes and decisions

## Feature Specification Template

Every feature directory should have a `spec.md` file. Use the template:

```bash
docs/.claude/_TEMPLATES/_BASE/feature-spec-detailed.md
```

**Essential sections:**
- **Overview:** What is this feature?
- **Objectives:** What are we trying to achieve?
- **User Stories:** As a [user], I want [goal], so that [benefit]
- **Requirements:** Functional and non-functional requirements
- **Acceptance Criteria:** How do we know it's done?
- **Technical Design:** Architecture, APIs, database changes
- **Testing Strategy:** How to test this feature
- **Risks:** What could go wrong?

## Integration with Task Management

### Linking Features to Tasks

**Features spawn tasks:**
```
docs/.claude/features/payment-processing/
docs/.claude/tasks/FEAT-042-PHASE-1-stripe-integration.md
docs/.claude/tasks/FEAT-042-PHASE-2-payment-ui.md
docs/.claude/tasks/FEAT-042-PHASE-3-webhooks.md
```

**Reference tasks in spec.md:**
```markdown
## Implementation Tasks
- [FEAT-042-PHASE-1](../../tasks/FEAT-042-PHASE-1-stripe-integration.md)
- [FEAT-042-PHASE-2](../../tasks/FEAT-042-PHASE-2-payment-ui.md)
- [FEAT-042-PHASE-3](../../tasks/FEAT-042-PHASE-3-webhooks.md)
```

## Common Feature Types

### API Features
**Structure:**
```
features/api-v2-endpoints/
├── spec.md
├── api-design.md              # OpenAPI/Swagger spec
├── authentication.md          # Auth requirements
└── rate-limiting.md           # Rate limit strategy
```

### UI Features
**Structure:**
```
features/dashboard-redesign/
├── spec.md
├── ui-mockups/                # Figma exports, wireframes
│   ├── dashboard.png
│   └── mobile-view.png
├── components.md              # Component breakdown
└── accessibility.md           # A11y requirements
```

### Data Features
**Structure:**
```
features/analytics-engine/
├── spec.md
├── db-schema.md               # Schema changes
├── data-pipeline.md           # ETL workflow
└── performance.md             # Query optimization
```

## Best Practices

### 1. Keep Specs Updated
- Update spec.md as requirements change
- Document decisions in notes.md
- Keep implementation-workflow.md in sync

### 2. Use Consistent Structure
- Follow the template structure
- Use the same sections across features
- Make it easy for team to find information

### 3. Link Related Documentation
```markdown
## Related
- **Tech Debt:** [DEBT-005](../../tech-debt/DEBT-005-refactor-auth.md)
- **Decision Log:** See 2025-01-15 decision on OAuth provider
- **API Docs:** See `/docs/api/authentication.md`
```

### 4. Version Control
- Commit spec changes with meaningful messages
- Tag releases when features are deployed
- Keep feature branches aligned with feature docs

### 5. Collaboration
- Review specs before implementation
- Share with stakeholders early
- Get feedback iteratively
- Keep team informed of changes

## Example: Complete Feature Lifecycle

### 1. Feature Request
**Stakeholder:** "We need two-factor authentication"

### 2. Create Spec
```bash
mkdir -p docs/.claude/features/two-factor-auth
cp docs/.claude/_TEMPLATES/_BASE/feature-spec-detailed.md \
   docs/.claude/features/two-factor-auth/spec.md
```

Edit spec with:
- User stories (As a user, I want 2FA to secure my account)
- Requirements (TOTP, SMS, backup codes)
- Acceptance criteria
- Security considerations

### 3. Review & Approval
- Share spec with team
- Get security review
- Get stakeholder approval
- Refine based on feedback

### 4. Implementation
Create phases:
- Phase 1: Backend (TOTP generation, verification)
- Phase 2: Database (user settings, backup codes)
- Phase 3: Frontend (QR code, input form)
- Phase 4: Testing (security tests, E2E)

### 5. Execution
Execute each phase with appropriate agent, update workflow.md with progress.

### 6. Deployment
- Deploy to staging
- User acceptance testing
- Deploy to production
- Monitor for issues

### 7. Documentation
- Update user documentation
- Update API docs
- Add to decision log
- Archive feature spec (or keep for reference)

## FAQs

**Q: When should I create a feature directory vs just coding?**
A: If the feature takes more than 2 hours, affects multiple files, or requires coordination, create a directory.

**Q: Do I need an implementation-workflow.md for every feature?**
A: No, only for complex features with multiple phases. Simple features just need spec.md.

**Q: Can I have multiple features in progress?**
A: Yes, but limit work-in-progress to maintain focus. Finish features before starting new ones when possible.

**Q: Should I delete feature directories after completion?**
A: You can move to archive, but core features should stay for reference. Delete only obsolete or cancelled features.

**Q: How detailed should specs be?**
A: Detailed enough that someone unfamiliar with the feature can implement it. Include "why" not just "what."

## Related Documentation

- **Feature Spec Template:** `docs/.claude/_TEMPLATES/_BASE/feature-spec-detailed.md`
- **Implementation Workflow Template:** `docs/.claude/_TEMPLATES/_BASE/feature-implementation-workflow.md`
- **Phase Task Template:** `docs/.claude/_TEMPLATES/_BASE/phase-task.md`
- **Task Management:** `docs/.claude/tasks/README.md`
- **Agents Guide:** `docs/.claude/_SYSTEM/agents-guide.md`

---

**Maintained By:** [Team/Person]
**Last Updated:** [Date]
