# Specialized AI Agents Usage Guide

> **Complete guide to using ClaudeContext's 14 specialized AI agents for optimal development workflow**

## Overview

ClaudeContext includes 14 specialized AI agents, each optimized for specific development tasks. Think of them as expert consultants you can activate for different phases of development.

**Key Benefit:** Instead of a generic Claude session, you get focused expertise with domain-specific knowledge and best practices.

## Available Agents

| Agent | Purpose | Best For |
|-------|---------|----------|
| **Product Owner** | Requirements & planning | Feature specs, user stories, acceptance criteria |
| **Systems Architect** | Architecture & design | System design, tech stack decisions, scalability |
| **Backend Engineer** | Server-side development | APIs, databases, business logic, performance |
| **Frontend Developer** | UI/UX implementation | Components, state management, responsive design |
| **Test Engineer** | Testing strategy | Test plans, TDD, coverage, debugging |
| **Code Reviewer** | Code quality assurance | PR reviews, security, best practices |
| **Security Auditor** | Security analysis | Vulnerability assessment, compliance, audits |
| **Performance Optimizer** | Performance tuning | Query optimization, caching, profiling |
| **DevOps Engineer** | Infrastructure & deployment | CI/CD, containers, monitoring, infrastructure |
| **Data Engineer** | Data pipelines & analytics | ETL, data warehousing, big data |
| **Documentation Specialist** | Technical writing | API docs, guides, diagrams |

## How to Activate Agents

### Method 1: Task Delegation (Recommended)

**This is the proper way to activate agents** - it creates a separate agent instance that works autonomously.

```markdown
Use the Task tool with the following prompt:

Load docs/.claude/_SYSTEM/agents/[agent-name].md
Load docs/.claude/context/conventions.md

Activate as [Agent Name] agent.

Task: [What you need done]
Type: [Task type specific to agent]
[Other agent-specific parameters]

Please complete this task following the agent's workflow and conventions.
```

**Example:**
```markdown
Task tool prompt:

Load docs/.claude/_SYSTEM/agents/backend-engineer.md
Load docs/.claude/context/conventions.md

Activate as Backend Developer agent.

Task: Create user authentication API
Type: REST API
Database: PostgreSQL
Authentication: JWT tokens
Scale: 50K concurrent users

Please implement the authentication system following our conventions.
```

**Why use Task delegation?**
- ✅ Creates a true specialized agent instance
- ✅ Agent works autonomously and independently
- ✅ Agent has full context and expertise
- ✅ Better separation of concerns
- ✅ Agent reports back with complete results

### Method 2: Direct Loading (Informational Only)

**Note:** This method loads the agent's persona but you're still the main Claude instance acting on the task. Use Method 1 for true delegation.

```markdown
Load docs/.claude/_SYSTEM/agents/[agent-name].md

[Provide context and task details]

Please help me with this task following our conventions.
```

### Quick Reference

```markdown
Activate [Agent Name] agent.

Task: [What you need done]
Context: [Relevant background]
Requirements: [Specific needs]

Please help me implement this.
```

## Agent-by-Agent Guide

---

### 1. Product Owner

**Use When:**
- Starting a new feature
- Writing user stories
- Defining acceptance criteria
- Planning sprints
- Gathering requirements

**Activation:**
```markdown
Load docs/.claude/_SYSTEM/agents/product-owner.md

Feature: [Feature name]
User problem: [Problem to solve]
Target users: [Who will use this]
Success criteria: [How to measure success]

Please help me:
1. Write user stories with acceptance criteria
2. Break down into tasks
3. Estimate complexity
4. Identify dependencies
```

**Outputs:**
- User stories in Gherkin format (Given/When/Then)
- Acceptance criteria checklist
- Sprint planning breakdown
- Feature specification outline

**Example:**
```markdown
Load docs/.claude/_SYSTEM/agents/product-owner.md

Feature: Password reset flow
User problem: Users forget passwords and can't log in
Target users: All registered users
Success criteria: <5% support tickets, 90% completion rate

Please help me define this feature completely.
```

---

### 2. Systems Architect

**Use When:**
- Designing new systems
- Making technology choices
- Planning architecture
- Solving scalability issues
- Refactoring architecture

**Activation:**
```markdown
Load docs/.claude/_SYSTEM/agents/systems-architect.md

System: [What you're building]
Requirements:
- Scale: [Expected load]
- Constraints: [Technical/budget limits]
- Integrations: [External systems]

Please design the architecture.
```

**Outputs:**
- Architecture diagrams (described)
- Technology recommendations
- Component breakdown
- Data flow design
- Scalability plan

**Example:**
```markdown
Load docs/.claude/_SYSTEM/agents/systems-architect.md

System: Real-time chat application
Requirements:
- Scale: 100K concurrent users
- Constraints: PostgreSQL database, existing Django backend
- Integrations: AWS S3 for file uploads

Please design a scalable architecture.
```

---

### 3. Backend Engineer

**Use When:**
- Implementing APIs
- Designing databases
- Writing business logic
- Optimizing queries
- Authentication/authorization

**Activation:**
```markdown
Load docs/.claude/_SYSTEM/agents/backend-engineer.md
Load docs/.claude/context/conventions.md

Task: [API/Service to implement]
Type: [REST/GraphQL/WebSocket]
Database: [PostgreSQL/MySQL/MongoDB]
Authentication: [JWT/OAuth/Session]
Scale: [Performance requirements]

Please implement backend solution.
```

**Outputs:**
- API endpoint implementations
- Database models and migrations
- Business logic services
- Test cases
- API documentation

**Example:**
```markdown
Load docs/.claude/_SYSTEM/agents/backend-engineer.md
Load docs/.claude/context/conventions.md

Task: Blog post CRUD API
Type: REST API
Database: PostgreSQL
Authentication: JWT tokens
Scale: 10K users, <200ms response

Please implement:
1. Database models with relationships
2. CRUD endpoints with validation
3. Pagination and filtering
4. Comprehensive tests
```

---

### 4. Frontend Developer

**Use When:**
- Building UI components
- Implementing designs
- State management
- Responsive layouts
- Client-side logic

**Activation:**
```markdown
Load docs/.claude/_SYSTEM/agents/frontend-developer.md
Load docs/.claude/context/conventions.md

Component: [What to build]
Framework: [React/Vue/Svelte]
Styling: [Tailwind/CSS Modules/Styled Components]
State: [Pinia/Redux/Zustand]
Requirements: [Specific UI needs]

Please implement this component.
```

**Outputs:**
- Vue/React components
- State management logic
- Responsive styles
- Accessibility features
- Component tests

**Example:**
```markdown
Load docs/.claude/_SYSTEM/agents/frontend-developer.md
Load docs/.claude/context/conventions.md

Component: Blog post editor with rich text
Framework: Vue 3 Composition API
Styling: Tailwind CSS
State: Pinia store
Requirements:
- Auto-save drafts
- Image upload
- WCAG AA compliant

Please implement complete component.
```

---

### 5. Test Engineer

**Use When:**
- Writing test strategies
- Implementing tests
- Debugging test failures
- Improving coverage
- TDD approach

**Activation:**
```markdown
Load docs/.claude/_SYSTEM/agents/test-engineer.md
Load docs/.claude/context/conventions.md

Component: [What to test]
Testing type: [Unit/Integration/E2E]
Framework: [pytest/Jest/Vitest]
Coverage goal: [Target percentage]
Current coverage: [Current state]

Please create comprehensive tests.
```

**Outputs:**
- Test suites (unit/integration/e2e)
- Test coverage reports
- Mock/stub strategies
- Edge case scenarios
- Performance tests

**Example:**
```markdown
Load docs/.claude/_SYSTEM/agents/test-engineer.md
Load docs/.claude/context/conventions.md

Component: User authentication system
Testing type: All (unit, integration, e2e)
Framework: pytest
Coverage goal: 90%
Current coverage: 45%

Please create comprehensive test suite covering:
1. Happy path scenarios
2. Edge cases (invalid tokens, expired sessions)
3. Security scenarios (XSS, CSRF)
4. Performance tests
```

---

### 6. Code Reviewer

**Use When:**
- Reviewing pull requests
- Pre-merge quality check
- Security review
- Performance audit
- Convention compliance

**Activation:**
```markdown
Load docs/.claude/_SYSTEM/agents/code-reviewer.md
Load docs/.claude/context/conventions.md

Review scope: [Files/PR/Module]
Focus areas: [Security/Performance/Maintainability]
Priority concerns: [Specific worries]

Please review this code thoroughly.
```

**Outputs:**
- Code quality assessment
- Security vulnerability findings
- Performance issues
- Convention violations
- Improvement suggestions

**Example:**
```markdown
Load docs/.claude/_SYSTEM/agents/code-reviewer.md
Load docs/.claude/context/conventions.md

Review scope: src/api/authentication.py (lines 45-150)
Focus areas: Security and error handling
Priority concerns: JWT token validation, SQL injection

Please review focusing on security vulnerabilities.
```

---

### 7. Security Auditor

**Use When:**
- Security assessments
- Compliance checks
- Vulnerability scanning
- Penetration testing
- Security architecture review

**Activation:**
```markdown
Load docs/.claude/_SYSTEM/agents/security-auditor.md
Load docs/.claude/context/conventions.md

Audit scope: [Authentication/API/Data/Infrastructure]
Compliance: [OWASP/GDPR/HIPAA/SOC2]
Priority concerns: [Specific security issues]

Please perform security audit.
```

**Outputs:**
- Vulnerability assessment
- OWASP Top 10 analysis
- Compliance checklist
- Security recommendations
- Risk prioritization

**Example:**
```markdown
Load docs/.claude/_SYSTEM/agents/security-auditor.md
Load docs/.claude/context/conventions.md

Audit scope: Complete authentication system
Compliance: OWASP Top 10, GDPR
Priority concerns:
- Password storage
- Session management
- XSS prevention

Please perform comprehensive security audit.
```

---

### 8. Performance Optimizer

**Use When:**
- Slow endpoints/queries
- High memory usage
- Optimization needed
- Scalability issues
- Profiling code

**Activation:**
```markdown
Load docs/.claude/_SYSTEM/agents/performance-optimizer.md
Load docs/.claude/context/conventions.md

Issue: [Performance problem]
Current metrics: [Speed/memory/etc]
Target metrics: [Performance goals]
Constraints: [Cannot change X, must maintain Y]

Please optimize performance.
```

**Outputs:**
- Performance analysis
- Optimization recommendations
- Refactored code
- Benchmarks before/after
- Caching strategies

**Example:**
```markdown
Load docs/.claude/_SYSTEM/agents/performance-optimizer.md
Load docs/.claude/context/conventions.md

Issue: Dashboard endpoint taking 3+ seconds
Current metrics:
- Response time: 3200ms (p95)
- Database queries: 45 queries (N+1 problem)
- Memory: 500MB per request

Target metrics: <200ms response, <10 queries, <100MB

Please optimize this endpoint.
```

---

### 9. DevOps Engineer

**Use When:**
- CI/CD setup
- Deployment automation
- Container configuration
- Infrastructure as code
- Monitoring setup

**Activation:**
```markdown
Load docs/.claude/_SYSTEM/agents/devops-engineer.md
Load docs/.claude/context/tech-stack.md

Task: [DevOps task]
Platform: [AWS/GCP/Azure/Docker]
Environment: [Dev/Staging/Production]
Requirements: [Specific needs]

Please help with DevOps implementation.
```

**Outputs:**
- CI/CD pipeline configs
- Dockerfile/docker-compose
- Infrastructure as Code (Terraform/CloudFormation)
- Monitoring setup
- Deployment scripts

**Example:**
```markdown
Load docs/.claude/_SYSTEM/agents/devops-engineer.md
Load docs/.claude/context/tech-stack.md

Task: Set up CI/CD for Django application
Platform: GitHub Actions + AWS ECS
Environment: Staging and Production
Requirements:
- Run tests before deploy
- Zero-downtime deployment
- Automatic rollback on failure

Please create complete CI/CD pipeline.
```

---

### 10. Data Engineer

**Use When:**
- ETL pipelines
- Data warehouse design
- Analytics setup
- Big data processing
- Data quality

**Activation:**
```markdown
Load docs/.claude/_SYSTEM/agents/data-engineer.md
Load docs/.claude/context/tech-stack.md

Task: [Data engineering task]
Data sources: [Sources]
Target: [Warehouse/Lake/Analytics]
Volume: [Expected data size]
Frequency: [Real-time/Batch]

Please design data pipeline.
```

**Outputs:**
- ETL pipeline design
- Data warehouse schema
- Transformation logic
- Data quality checks
- Orchestration workflows

**Example:**
```markdown
Load docs/.claude/_SYSTEM/agents/data-engineer.md
Load docs/.claude/context/tech-stack.md

Task: User behavior analytics pipeline
Data sources: PostgreSQL DB, Application logs, Third-party APIs
Target: Data warehouse for analytics
Volume: 1M events/day
Frequency: Real-time streaming

Please design complete data pipeline.
```

---

### 11. Documentation Specialist

**Use When:**
- Writing API docs
- User guides
- Architecture diagrams
- README files
- Migration guides

**Activation:**
```markdown
Load docs/.claude/_SYSTEM/agents/documentation-specialist.md

Documentation type: [API/User Guide/Technical]
Audience: [Developers/End users/DevOps]
Scope: [Features/modules to document]
Format: [OpenAPI/Markdown/etc]

Please create comprehensive documentation.
```

**Outputs:**
- API documentation (OpenAPI/Swagger)
- User guides and tutorials
- Architecture diagrams
- Code examples
- Migration guides

**Example:**
```markdown
Load docs/.claude/_SYSTEM/agents/documentation-specialist.md

Documentation type: API documentation
Audience: External developers (third-party integrators)
Scope: Complete authentication and blog post APIs
Format: OpenAPI 3.0

Please create:
1. OpenAPI specification
2. Authentication guide
3. Code examples in Python and JavaScript
4. Common error responses
```

---

## Agent Chaining Patterns

For complex features, chain multiple agents in sequence:

### Pattern 1: Full-Stack Feature Development

```
1. Product Owner → Define requirements
   ↓
2. Systems Architect → Design architecture
   ↓
3. Backend Engineer → Implement API
   ↓
4. Frontend Developer → Build UI
   ↓
5. Test Engineer → Comprehensive testing
   ↓
6. Code Reviewer → Quality assurance
   ↓
7. Documentation Specialist → Write docs
   ↓
8. DevOps Engineer → Deploy to production
```

### Pattern 2: Performance Optimization

```
1. Performance Optimizer → Identify bottlenecks
   ↓
2. Backend Engineer → Optimize queries
   ↓
3. Test Engineer → Performance testing
   ↓
4. Code Reviewer → Review changes
```

### Pattern 3: Security Hardening

```
1. Security Auditor → Identify vulnerabilities
   ↓
2. Backend Engineer → Fix security issues
   ↓
3. Test Engineer → Security testing
   ↓
4. Code Reviewer → Verify fixes
```

## Multi-Phase Feature Workflow

For large features, use the phase-based approach:

### Step 1: Create Workflow Plan
```markdown
Load CLAUDE.md and docs/.claude/context/project-overview.md

Feature: [Feature name]
Complexity: Complex
Description: [Brief description]

This feature requires multiple phases with different specializations.

Please help me:
1. Create a feature implementation workflow
2. Break down into logical phases
3. Assign appropriate agents to each phase
4. Create individual phase task files
```

### Step 2: Execute Each Phase

**Phase 1: Requirements (Product Owner)**
```markdown
Load docs/.claude/_SYSTEM/agents/product-owner.md
Load docs/.claude/tasks/FEAT-042-PHASE-1-requirements.md

Complete Phase 1: Define requirements and acceptance criteria
```

**Phase 2: Architecture (Systems Architect)**
```markdown
Load docs/.claude/_SYSTEM/agents/systems-architect.md
Load docs/.claude/tasks/FEAT-042-PHASE-2-architecture.md

Complete Phase 2: Design system architecture
```

**Phase 3: Backend (Backend Engineer)**
```markdown
Load docs/.claude/_SYSTEM/agents/backend-engineer.md
Load docs/.claude/tasks/FEAT-042-PHASE-3-backend.md

Complete Phase 3: Implement API endpoints
```

**Phase 4: Frontend (Frontend Developer)**
```markdown
Load docs/.claude/_SYSTEM/agents/frontend-developer.md
Load docs/.claude/tasks/FEAT-042-PHASE-4-frontend.md

Complete Phase 4: Build UI components
```

**Phase 5: Testing (Test Engineer)**
```markdown
Load docs/.claude/_SYSTEM/agents/test-engineer.md
Load docs/.claude/tasks/FEAT-042-PHASE-5-testing.md

Complete Phase 5: Comprehensive testing
```

## Best Practices

### 1. Always Load Context
```markdown
Load docs/.claude/_SYSTEM/agents/[agent-name].md
Load docs/.claude/context/conventions.md  # Your project conventions
```

### 2. Be Specific with Requirements
**Bad:**
```
Help me with authentication.
```

**Good:**
```
Load docs/.claude/_SYSTEM/agents/backend-engineer.md

Task: JWT authentication for REST API
Type: Bearer token authentication
Database: PostgreSQL for user storage
Requirements:
- Access tokens (15 min expiry)
- Refresh tokens (7 day expiry)
- Token rotation on refresh
- Rate limiting: 5 attempts per minute
- OWASP compliance

Please implement complete authentication system.
```

### 3. Provide Current State
```markdown
Current situation: [What exists now]
Problem: [What's not working]
Goal: [What you want to achieve]
Constraints: [Limitations]
```

### 4. Chain Agents Appropriately
Don't jump straight to implementation:
- Start with Product Owner or Systems Architect
- Then move to implementation agents
- End with Test Engineer and Code Reviewer

### 5. Use Phase-Based Approach for Complex Features
- Features with > 4 hours of work
- Multi-component features
- Features requiring multiple skill sets

## Common Workflows

### New Feature (Simple)
```
Product Owner → Backend Engineer → Test Engineer
```

### New Feature (Complex)
```
Product Owner → Systems Architect → Backend Engineer →
Frontend Developer → Test Engineer → Documentation Specialist
```

### Bug Fix
```
Test Engineer (reproduce) → Backend/Frontend Engineer (fix) →
Code Reviewer (verify)
```

### Performance Issue
```
Performance Optimizer (identify) → Backend Engineer (implement) →
Test Engineer (validate)
```

### Security Issue
```
Security Auditor (identify) → Backend Engineer (fix) →
Test Engineer (verify) → Code Reviewer (approve)
```

### Tech Debt
```
Systems Architect (assess) → Backend/Frontend Engineer (refactor) →
Test Engineer (validate) → Code Reviewer (approve)
```

## Tips for Success

1. **Read the agent file first** - Each agent has specific activation patterns
2. **Provide complete context** - More details = better results
3. **Use conventions** - Always load your project conventions
4. **Chain appropriately** - Don't skip planning phases
5. **Track decisions** - Update decision-log.md with agent recommendations
6. **Iterate** - Agents can refine their work based on feedback

## Troubleshooting

**Q: Agent suggestions don't match my project style**
**A:** Always load `docs/.claude/context/conventions.md` with the agent

**Q: Too generic recommendations**
**A:** Provide more specific requirements and constraints

**Q: Agent suggests wrong technology**
**A:** Load `docs/.claude/context/tech-stack.md` to show current stack

**Q: Conflicting advice from different agents**
**A:** Use Systems Architect to make final decision, document in decision-log.md

---

## Quick Reference

| Need | Agent | Prompt |
|------|-------|--------|
| Define feature | Product Owner | `Load agents/product-owner.md` |
| Design system | Systems Architect | `Load agents/systems-architect.md` |
| Build API | Backend Engineer | `Load agents/backend-engineer.md` |
| Create UI | Frontend Developer | `Load agents/frontend-developer.md` |
| Write tests | Test Engineer | `Load agents/test-engineer.md` |
| Review code | Code Reviewer | `Load agents/code-reviewer.md` |
| Security audit | Security Auditor | `Load agents/security-auditor.md` |
| Optimize | Performance Optimizer | `Load agents/performance-optimizer.md` |
| Deploy | DevOps Engineer | `Load agents/devops-engineer.md` |
| Data pipeline | Data Engineer | `Load agents/data-engineer.md` |
| Write docs | Documentation Specialist | `Load agents/documentation-specialist.md` |

---

**Last Updated:** 2024-11-16
**Version:** 1.0
