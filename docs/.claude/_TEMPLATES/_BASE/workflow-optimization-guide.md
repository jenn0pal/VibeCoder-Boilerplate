# Workflow Optimization Guide

> **Master guide for maximizing productivity with ClaudeContext**

## Overview

This guide provides best practices, tips, and strategies for getting the most out of ClaudeContext across all development workflows.

## Core Principles

### 1. Context Loading Strategy

**The Right Context at the Right Time**

❌ **Don't load everything:**
```
Load CLAUDE.md
Load project-overview.md
Load conventions.md
Load tech-stack.md
Load decision-log.md
Load glossary.md
Load feature-spec.md
...
```

✅ **Load strategically:**
```
# For new sessions
Load CLAUDE.md
Load docs/.claude/context/project-overview.md

# Add context as needed
Load docs/.claude/context/conventions.md  # When writing code
Load docs/.claude/features/auth/spec.md   # When working on specific feature
```

**Context Loading Rules:**
- **Always load:** CLAUDE.md (master instructions)
- **Usually load:** project-overview.md (comprehensive context)
- **Load when coding:** conventions.md (coding standards)
- **Load when needed:** Feature specs, tech stack, specific agents

### 2. Session Management

**Effective Session Patterns**

**Short Sessions (< 1 hour):**
```
Load CLAUDE.md
Load docs/.claude/context/project-overview.md
Quick task: [Specific, focused task]
```

**Long Sessions (> 1 hour):**
```
Load CLAUDE.md
Load docs/.claude/context/project-overview.md
Load docs/.claude/features/[feature]/spec.md

Today's goal: Complete Phase 2 of user authentication
Context from last session: Completed backend API, now working on frontend
```

**Resuming Work:**
```
Load CLAUDE.md
Continuing: [Feature name]
Last completed: [What was done]
Current state: [Where you left off]
Today's goal: [What to accomplish]
```

###3. Agent Delegation

**When to Delegate vs Do It Yourself**

**Use Task tool + agents for:**
- Complex multi-step workflows
- Specialized work (security audit, performance optimization)
- Parallel execution of independent tasks
- Autonomous research/exploration

**Work directly for:**
- Quick fixes and small changes
- Iterative development with feedback
- Learning/teaching scenarios
- When you need tight control

**Delegation Examples:**

✅ **Good delegation:**
```
Task: Security audit of authentication system
Agent: Security Auditor
Reason: Specialized expertise, autonomous checklist execution
```

✅ **Good delegation:**
```
Task: Design system architecture for microservices migration
Agent: Systems Architect
Reason: Complex architectural thinking, needs deep analysis
```

❌ **Poor delegation:**
```
Task: Change button color from blue to green
Agent: Frontend Developer
Reason: Too simple, faster to do directly
```

### 4. Documentation Workflow

**Document While You Build, Not After**

**Progressive Documentation:**
1. **Before coding:** Create/update feature spec
2. **During coding:** Update notes.md with decisions
3. **After coding:** Update decision-log.md with significant choices
4. **At completion:** Archive or update project-overview.md

**Documentation Triggers:**
- New feature → Create feature spec
- Architecture change → Update decision-log.md
- New dependency → Update tech-stack.md
- Breaking change → Update BREAKING.md
- Gotcha/learning → Update glossary.md or notes.md

## Workflow-Specific Optimization

### Feature Development

**Optimal Flow:**

```mermaid
Feature Request
    ↓
Create Spec (15 min)
    ↓
Review Spec (async)
    ↓
Implement + Test (bulk of time)
    ↓
Code Review (automated + manual)
    ↓
Deploy
    ↓
Archive/Update Docs (5 min)
```

**Time Distribution:**
- 10% Planning (spec writing)
- 70% Implementation (coding + testing)
- 10% Review (code review + QA)
- 10% Deployment + Documentation

**Optimization Tips:**
- Write specs in bullet points, not essays
- Use templates (don't start from scratch)
- Implement with tests from the start
- Update docs while context is fresh

### Bug Fixing

**Optimal Flow:**

```mermaid
Bug Report
    ↓
Reproduce (write failing test)
    ↓
Identify Root Cause
    ↓
Fix + Verify Test Passes
    ↓
Add Regression Test
    ↓
Document if Needed
```

**Optimization Tips:**
- Start with test that reproduces bug
- Fix one bug at a time
- Don't optimize while fixing
- Only document if architectural issue

### Refactoring

**Optimal Flow:**

```mermaid
Identify Tech Debt
    ↓
Ensure Tests Exist (write if missing)
    ↓
Refactor Incrementally
    ↓
Run Tests After Each Change
    ↓
Verify No Behavior Change
```

**Optimization Tips:**
- Never refactor without tests
- Small incremental changes
- Commit frequently
- Measure before/after performance

## Token Efficiency

### Minimize Token Waste

**Template Reuse:**
```bash
# ✅ Good: Reference templates
"Use the bug report template from _TEMPLATES/task-management.md"

# ❌ Bad: Paste entire template in prompt
[Pasting 500 lines of template]
```

**Context Reuse:**
```bash
# ✅ Good: Load file once, reference multiple times
Load docs/.claude/context/conventions.md
[Ask multiple questions about conventions]

# ❌ Bad: Reload for each question
Load conventions.md
Question 1?
Load conventions.md
Question 2?
```

**Efficient Prompts:**
```bash
# ✅ Good: Specific and concise
"Add validation to User model email field following our Django conventions"

# ❌ Bad: Verbose and redundant
"I want you to please add some validation logic to the email field on the User model. This should validate that the email is in the correct format and follows all the conventions we have in our Django project..."
```

### Stack-Specific Loading

**v2.0 Optimization:**

✅ **Load only your stack:**
```
# Django project
Load docs/.claude/_TEMPLATES/django/conventions.md

# Laravel project
Load docs/.claude/_TEMPLATES/laravel/conventions.md

# Vue SPA project
Load docs/.claude/_TEMPLATES/vue/conventions-base.md
Load docs/.claude/_TEMPLATES/vue/conventions-spa.md
```

❌ **Don't load all stacks:**
```
Load docs/.claude/_TEMPLATES/conventions-django.md
Load docs/.claude/_TEMPLATES/conventions-laravel.md
Load docs/.claude/_TEMPLATES/conventions-vue-nuxt.md
...
```

## Time Management

### Batching Similar Tasks

**Efficient Batching:**
- Fix all linting errors in one session
- Write all unit tests for a module together
- Update all outdated dependencies together
- Review all pending PRs in one block

**Example:**
```
Load CLAUDE.md
Batch task: Fix all ESLint errors in src/components/

[Claude fixes all errors at once]
```

### Parallel vs Sequential

**Use Parallel for:**
- Independent feature development (different team members)
- Multiple tech debt items (if no dependencies)
- Simultaneous testing (unit + E2E + performance)

**Use Sequential for:**
- Dependent changes (API → Frontend → Tests)
- Learning workflows (understand then implement)
- Migration workflows (prepare → migrate → verify)

## Quality vs Speed Trade-offs

### When to Go Fast

**MVP/Prototype:**
- Skip comprehensive specs
- Minimal testing (smoke tests only)
- Defer documentation
- Accept tech debt (document it!)

**Quick Fixes:**
- Direct implementation
- Minimal testing
- Quick commit

### When to Go Slow

**Core Features:**
- Detailed specs with review
- Comprehensive testing (unit + integration + E2E)
- Full documentation
- Security review

**Breaking Changes:**
- Thorough impact analysis
- Migration strategy
- Team communication
- Rollback plan

## Common Anti-Patterns

### ❌ Anti-Pattern 1: Over-Documentation

**Problem:**
Spending 2 hours documenting a 30-minute fix.

**Solution:**
Document proportionally:
- Small fix: Git commit message only
- Medium feature: Feature spec (30 min)
- Large feature: Spec + workflow + decision log

### ❌ Anti-Pattern 2: Under-Specification

**Problem:**
Starting coding without clear requirements.

**Solution:**
- For uncertain features: Write spec first
- For clear features: Bullet point spec (5 min)
- For obvious changes: Skip spec, good commit message

### ❌ Anti-Pattern 3: Tool Overuse

**Problem:**
Creating tracking files for every small task.

**Solution:**
- Use tracking for multi-day features
- Use git commits for small changes
- Use GitHub issues for team visibility

### ❌ Anti-Pattern 4: Context Overload

**Problem:**
Loading every possible document "just in case".

**Solution:**
- Load CLAUDE.md + project-overview.md (always)
- Add context when you need it
- Trust Claude to ask for more context

## Measuring Success

### Productivity Metrics

**Good Indicators:**
- Features delivered per sprint ↑
- Time from spec to deployment ↓
- Bug rate ↓
- Test coverage ↑
- Documentation freshness ↑

**Track:**
- Velocity (story points per sprint)
- Lead time (idea to production)
- Cycle time (start to finish)
- Defect rate (bugs per feature)

### Quality Metrics

**Code Quality:**
- Test coverage > 80%
- Linting errors = 0
- Type coverage > 90% (if TypeScript/mypy)
- Code review approval rate

**Documentation Quality:**
- Spec completeness (all sections filled)
- Doc freshness (updated < 30 days ago)
- Team satisfaction (can new members onboard?)

## Workflow Customization

### Team Size Variations

**Solo Developer:**
- Lighter documentation
- Skip some review steps
- Combine roles (you're all agents!)
- Focus on clarity for "future you"

**Small Team (2-5):**
- Standard workflow
- Peer review required
- Shared conventions document
- Regular sync meetings

**Large Team (6+):**
- Stricter conventions
- Mandatory code review
- Detailed specs with stakeholder approval
- Architectural decision records

### Project Stage Variations

**Early Stage (MVP):**
- Lighter process
- Accept tech debt (document it!)
- Fast iteration
- Defer optimization

**Growth Stage:**
- Add rigor gradually
- Pay down tech debt
- Improve test coverage
- Refactor for scale

**Mature Stage:**
- Full process adherence
- High quality bar
- Comprehensive testing
- Performance optimization

## Advanced Techniques

### Workflow Chaining

**Example: Feature → Test → Deploy**
```
Session 1: Implement feature
Session 2: Load previous session context → Add tests
Session 3: Load test results → Fix issues → Deploy
```

### Template Customization

**Create project-specific templates:**
```
cp docs/.claude/_TEMPLATES/_BASE/feature-spec-detailed.md \
   docs/.claude/_TEMPLATES/custom/api-feature-spec.md

# Customize for API features specifically
```

### Agent Specialization

**Create custom agents:**
```
docs/.claude/_SYSTEM/agents/custom-agent-name.md

# Tailor to your domain (e.g., ML Engineer, Mobile Developer)
```

## Continuous Improvement

### Regular Reviews

**Weekly:**
- Review completed features
- Update tech debt backlog
- Refine conventions based on learnings

**Monthly:**
- Review workflow effectiveness
- Update templates if needed
- Team retrospective

**Quarterly:**
- Major documentation refresh
- Architecture review
- Process optimization

### Feedback Loops

**Collect Feedback:**
- What's working well?
- What's slowing us down?
- What's confusing?
- What's missing?

**Act on Feedback:**
- Update templates
- Refine workflows
- Add missing documentation
- Remove unused processes

## Quick Reference

### Optimal Session Start
```
Load CLAUDE.md
Load docs/.claude/context/project-overview.md
Working on: [clear, specific goal]
```

### Optimal Feature Implementation
```
1. Create feature spec (15 min)
2. Review spec
3. Implement with tests
4. Update docs while fresh
5. Archive or reference
```

### Optimal Bug Fix
```
1. Write failing test
2. Fix bug
3. Verify test passes
4. Add regression test
5. Document if architectural issue
```

### Optimal Refactoring
```
1. Ensure tests exist
2. Refactor incrementally
3. Run tests after each change
4. Verify no behavior change
5. Update documentation
```

---

**Remember:** The best workflow is the one your team actually follows. Start simple, add complexity only when needed, and continuously refine based on what works for your team.

---

*Last Updated: 2025*
*Version: 2.0*
