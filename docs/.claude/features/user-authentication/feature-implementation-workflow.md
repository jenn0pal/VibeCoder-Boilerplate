# Feature Implementation Workflow: User Authentication System

> **Example: Multi-phase feature implementation with agent assignments**
>
> This is a real-world example demonstrating how to break down a complex feature
> into manageable phases with dedicated specialized agents.

## Overview

**Feature ID:** FEAT-001
**Date:** 2025-10-28
**Priority:** High
**Complexity:** Complex
**Estimated Effort:** 40-50 hours
**Status:** Planning

## Feature Summary

### Business Goal
Enable secure user authentication to protect sensitive user data and provide personalized experiences. This is a foundational feature required before launching user-specific functionality.

### User Story
**As a** new or returning user
**I want** to securely register and log in to the application
**So that** I can access my personalized dashboard and protected features

### Success Criteria
- [ ] Users can register with email and password
- [ ] Email verification is required before access
- [ ] Users can log in with email and password
- [ ] JWT tokens are used for session management
- [ ] Passwords are securely hashed (bcrypt/Argon2)
- [ ] Rate limiting prevents brute-force attacks
- [ ] Password reset flow via email is functional
- [ ] All authentication tests pass (unit, integration, E2E)
- [ ] Security audit passes with no critical issues

## Phase Breakdown

### Phase 1: Requirements & Security Design
**Agent:** Product Owner + Security Auditor
**Estimated Effort:** 6 hours
**Dependencies:** None

**Objective:** Define detailed requirements and security architecture

**Deliverables:**
- [ ] Detailed requirements document with all user stories
- [ ] Security requirements and threat model
- [ ] Authentication flow diagrams
- [ ] Password policy requirements
- [ ] Session management strategy

**Task File:** `docs/.claude/tasks/FEAT-001-PHASE-1-requirements.md`

---

### Phase 2: System Architecture & API Design
**Agent:** Systems Architect
**Estimated Effort:** 8 hours
**Dependencies:** Phase 1 complete

**Objective:** Design authentication system architecture and API contracts

**Deliverables:**
- [ ] System architecture diagram
- [ ] Database schema for users table
- [ ] API endpoint specifications (REST)
- [ ] JWT token structure and claims
- [ ] Integration points with existing system
- [ ] Error handling strategy

**Task File:** `docs/.claude/tasks/FEAT-001-PHASE-2-architecture.md`

---

### Phase 3: Backend Implementation
**Agent:** Backend Engineer
**Estimated Effort:** 16 hours
**Dependencies:** Phase 2 complete

**Objective:** Implement authentication API endpoints and business logic

**Deliverables:**
- [ ] User model and database migrations
- [ ] Registration endpoint with validation
- [ ] Login endpoint with JWT generation
- [ ] Password reset endpoints
- [ ] Email verification endpoints
- [ ] Middleware for JWT validation
- [ ] Unit tests for all endpoints (80%+ coverage)
- [ ] Integration tests for auth flows

**Task File:** `docs/.claude/tasks/FEAT-001-PHASE-3-backend.md`

---

### Phase 4: Frontend Implementation
**Agent:** Frontend Developer
**Estimated Effort:** 12 hours
**Dependencies:** Phase 3 complete

**Objective:** Build authentication UI components and integrate with backend

**Deliverables:**
- [ ] Registration form component
- [ ] Login form component
- [ ] Password reset request form
- [ ] Password reset confirmation form
- [ ] Email verification page
- [ ] Authentication state management (Pinia/Redux)
- [ ] Protected route guards
- [ ] Token refresh logic
- [ ] Component tests

**Task File:** `docs/.claude/tasks/FEAT-001-PHASE-4-frontend.md`

---

### Phase 5: Testing, Security & Performance
**Agent:** Test Engineer + Security Auditor + Performance Optimizer
**Estimated Effort:** 8 hours
**Dependencies:** Phase 4 complete

**Objective:** Comprehensive testing, security audit, and performance validation

**Deliverables:**
- [ ] E2E tests for complete auth flows
- [ ] Security penetration testing
- [ ] Rate limiting tests
- [ ] Load testing for auth endpoints
- [ ] Performance benchmarks (login < 200ms)
- [ ] Security audit report
- [ ] Performance optimization recommendations

**Task File:** `docs/.claude/tasks/FEAT-001-PHASE-5-testing.md`

---

## Agent Assignment Guide

### Why These Agents?

**Phase 1 - Product Owner + Security Auditor:**
- Product Owner defines functional requirements and user stories
- Security Auditor ensures security requirements are comprehensive from the start
- Combined expertise prevents security gaps in requirements

**Phase 2 - Systems Architect:**
- Designs scalable authentication architecture
- Defines API contracts and integration points
- Makes critical technology decisions (JWT vs sessions, storage strategy)

**Phase 3 - Backend Engineer:**
- Implements secure authentication logic
- Handles database operations and migrations
- Writes comprehensive backend tests

**Phase 4 - Frontend Developer:**
- Builds user-facing authentication components
- Implements client-side security best practices
- Manages authentication state

**Phase 5 - Test Engineer + Security Auditor + Performance Optimizer:**
- Test Engineer ensures comprehensive test coverage
- Security Auditor validates security implementation
- Performance Optimizer ensures authentication is fast and scalable

## Implementation Timeline

### Schedule

| Phase | Start Date | End Date | Duration | Status |
|-------|-----------|----------|----------|--------|
| Phase 1 | 2025-10-28 | 2025-10-28 | 1 day | ⏳ Pending |
| Phase 2 | 2025-10-29 | 2025-10-29 | 1 day | ⏳ Pending |
| Phase 3 | 2025-10-30 | 2025-11-01 | 3 days | ⏳ Pending |
| Phase 4 | 2025-11-04 | 2025-11-05 | 2 days | ⏳ Pending |
| Phase 5 | 2025-11-06 | 2025-11-06 | 1 day | ⏳ Pending |

### Milestones

- [ ] **M1:** Phase 1 Complete - Requirements & Security Design Approved (2025-10-28)
- [ ] **M2:** Phase 2 Complete - Architecture & API Design Approved (2025-10-29)
- [ ] **M3:** Phase 3 Complete - Backend Implementation & Tests Passing (2025-11-01)
- [ ] **M4:** Phase 4 Complete - Frontend Implementation Ready (2025-11-05)
- [ ] **M5:** Feature Complete - All Tests & Security Audit Passing (2025-11-06)

## Cross-Phase Dependencies

### Data Flow Between Phases

**Phase 1 Output → Phase 2 Input:**
- Security requirements document
- Password policy specifications
- Session management requirements
- User stories and acceptance criteria

**Phase 2 Output → Phase 3 Input:**
- API endpoint specifications
- Database schema design
- JWT token structure
- Error response formats

**Phase 3 Output → Phase 4 Input:**
- Working API endpoints
- API documentation
- JWT token format
- Error codes and messages

**Phase 4 Output → Phase 5 Input:**
- Complete authentication UI
- Client-side auth logic
- Protected routes implementation
- Test scenarios to validate

### Shared Resources

**Database Schema:** Defined in Phase 2, implemented in Phase 3
**API Contracts:** Defined in Phase 2, implemented in Phase 3, consumed in Phase 4
**JWT Token Format:** Defined in Phase 2, generated in Phase 3, validated in Phase 4
**Security Requirements:** Defined in Phase 1, implemented in Phase 3, validated in Phase 5

## Quality Assurance

### Per-Phase Quality Gates

**Phase 1 (Requirements):**
- [ ] All security requirements defined
- [ ] Threat model complete
- [ ] Stakeholder approval obtained
- [ ] No ambiguous requirements

**Phase 2 (Architecture):**
- [ ] Architecture review passed
- [ ] API design follows REST conventions
- [ ] Database schema normalized
- [ ] Security architecture approved

**Phase 3 (Backend):**
- [ ] Unit tests passing (80%+ coverage)
- [ ] Integration tests passing
- [ ] Code review approved
- [ ] No SQL injection vulnerabilities
- [ ] Passwords properly hashed

**Phase 4 (Frontend):**
- [ ] Component tests passing
- [ ] JWT tokens properly stored (httpOnly cookies)
- [ ] CSRF protection implemented
- [ ] Accessibility standards met (WCAG 2.1 AA)

**Phase 5 (Testing):**
- [ ] E2E tests passing
- [ ] Security scan clean
- [ ] Performance benchmarks met
- [ ] No critical or high vulnerabilities

### Overall Feature Quality Gates

- [ ] All phase deliverables completed
- [ ] All tests passing (unit, integration, E2E)
- [ ] Code review approved for all phases
- [ ] Security audit passed
- [ ] Performance targets met (< 200ms for login)
- [ ] Documentation complete
- [ ] Rate limiting configured and tested
- [ ] Email service integrated and tested

## Risk Management

### Phase-Specific Risks

**Phase 1 Risks:**
- Incomplete security requirements → Conduct thorough threat modeling session
- Scope creep (OAuth, 2FA) → Define clear MVP scope, defer advanced features to v2

**Phase 2 Risks:**
- Over-engineered architecture → Keep it simple for MVP, plan for future scalability
- Token storage debates → Choose httpOnly cookies for security

**Phase 3 Risks:**
- Password hashing performance → Use appropriate bcrypt work factor (10-12)
- Email delivery issues → Test with multiple providers, implement retry logic
- Database migration conflicts → Coordinate with team, use proper migration tools

**Phase 4 Risks:**
- XSS vulnerabilities in forms → Sanitize all inputs, use framework protection
- Token refresh complexity → Implement simple refresh token strategy
- State management bugs → Comprehensive testing of auth state transitions

**Phase 5 Risks:**
- Performance under load → Implement caching, rate limiting
- Security vulnerabilities found → Allocate buffer time for fixes

### Cross-Phase Risks

| Risk | Affected Phases | Impact | Mitigation |
|------|----------------|--------|------------|
| API contract changes | Phase 3, 4 | Medium | Lock API contract in Phase 2 |
| Database schema changes | Phase 3, 4 | High | Finalize schema before Phase 3 |
| Security issues discovered late | All | High | Security review in Phases 1, 2, 5 |
| Third-party email service issues | Phase 3, 4 | Medium | Use reliable provider, implement fallback |

### Contingency Plans

**If Phase 3 (Backend) takes longer than expected:**
- Frontend can work on UI mockups without API integration
- Use mock API responses for frontend development
- Parallelize work where possible

**If security issues found in Phase 5:**
- Allocate additional time for fixes (2-4 hours buffer built in)
- Prioritize critical issues, defer minor issues to backlog
- Re-run security tests after fixes

## Progress Tracking

### Completed Phases

None yet (feature in planning stage)

### Current Phase

- [ ] **Phase 1:** Requirements & Security Design - Not Started

### Upcoming Phases

- [ ] **Phase 2:** Architecture & API Design - Scheduled for 2025-10-29
- [ ] **Phase 3:** Backend Implementation - Scheduled for 2025-10-30
- [ ] **Phase 4:** Frontend Implementation - Scheduled for 2025-11-04
- [ ] **Phase 5:** Testing & Security - Scheduled for 2025-11-06

## Communication & Handoffs

### Phase Handoff Checklist

When completing a phase and transitioning to the next:

- [ ] Update phase status in this workflow document
- [ ] Mark phase task file as completed
- [ ] Document key decisions in decision log
- [ ] Create next phase task file (if not already created)
- [ ] Conduct handoff meeting or async handoff document
- [ ] Ensure all deliverables are accessible and documented
- [ ] Update timeline if needed

## Documentation

### Per-Phase Documentation

**Phase 1 Docs:**
- [ ] Requirements document with user stories
- [ ] Security requirements and threat model
- [ ] Authentication flow diagrams

**Phase 2 Docs:**
- [ ] Architecture diagrams (system, database, API)
- [ ] API specifications (OpenAPI/Swagger)
- [ ] Database ERD

**Phase 3 Docs:**
- [ ] API endpoint documentation
- [ ] Code comments and docstrings
- [ ] Database migration files
- [ ] Setup/configuration guide

**Phase 4 Docs:**
- [ ] Component documentation (Storybook)
- [ ] Auth state management guide
- [ ] Frontend integration guide

**Phase 5 Docs:**
- [ ] Test documentation and coverage reports
- [ ] Security audit report
- [ ] Performance benchmarking results
- [ ] End-user guide (how to register/login)

### Centralized Documentation

**Feature Overview:** `docs/features/user-authentication/README.md`
**API Docs:** `docs/api/authentication.md`
**Architecture:** `docs/architecture/authentication-system.md`
**Decision Log:** `docs/.claude/context/decision-log.md` (entries for key decisions)

## Post-Implementation Review

### Feature Metrics (To be filled after completion)

**Development Metrics:**
- Total Duration: [Actual] vs 8 days [Estimated]
- Total Effort: [Actual hours] vs 50 hours [Estimated hours]
- Phases Completed: [X of 5]
- Code Changes: [+X/-Y lines]

**Quality Metrics:**
- Test Coverage: [X%] (target: 80%+)
- Bug Count: [X bugs found during testing]
- Performance: Login time [X]ms (target: < 200ms)
- Security: [Critical/High/Medium/Low vulnerabilities found]

### Lessons Learned (To be filled after completion)

**What Worked Well:**
- [Point 1]
- [Point 2]

**What Could Be Improved:**
- [Point 1]
- [Point 2]

**Agent Effectiveness:**
- Product Owner: [Feedback]
- Systems Architect: [Feedback]
- Backend Engineer: [Feedback]
- Frontend Developer: [Feedback]
- Test Engineer: [Feedback]
- Security Auditor: [Feedback]

**Process Improvements:**
- [ ] [Improvement to implement for next feature]
- [ ] [Improvement to implement for next feature]

## Related

- **Phase Task Files:**
  - `docs/.claude/tasks/FEAT-001-PHASE-1-requirements.md`
  - `docs/.claude/tasks/FEAT-001-PHASE-2-architecture.md`
  - `docs/.claude/tasks/FEAT-001-PHASE-3-backend.md`
  - `docs/.claude/tasks/FEAT-001-PHASE-4-frontend.md`
  - `docs/.claude/tasks/FEAT-001-PHASE-5-testing.md`
- **Related Features:** None (foundational feature)
- **Related Bugs:** To be linked as discovered
- **Pull Requests:** To be linked when created
- **Discussion:** [Link to RFC or discussion thread]

---

**Status:** Planning
**Last Updated:** 2025-10-28
**Maintained By:** Development Team
**Total Phases:** 5
**Completed Phases:** 0 of 5

## How to Use This Example

This is a reference implementation showing how to structure a multi-phase feature. To start working on this feature:

1. **Begin Phase 1:**
```
Load CLAUDE.md
Load docs/.claude/context/project-overview.md
Load docs/.claude/_SYSTEM/agents/product-owner.md
Load docs/.claude/_SYSTEM/agents/security-auditor.md
Load docs/.claude/features/user-authentication/feature-implementation-workflow.md

Create Phase 1 task file for User Authentication feature.
Focus on requirements and security design.
```

2. **Work through each phase sequentially** using the phase-specific agent activation prompts

3. **Track progress** by updating this workflow file and individual phase task files

4. **Complete handoffs** between phases following the handoff checklist
