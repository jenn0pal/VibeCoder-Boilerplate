# Agent Configuration Template

> **Complete guide to creating and configuring custom AI agents for ClaudeContext**

## Overview

This template provides the structure for creating specialized AI agents that can be delegated specific development tasks. Each agent should have focused expertise and follow a consistent workflow pattern.

## Agent Configuration Structure

### 1. Agent Identity

Every agent configuration should start with:

```markdown
# [Agent Name]

## Purpose
[One-sentence description of the agent's primary responsibility]

## Expertise
- [Expertise area 1]
- [Expertise area 2]
- [Expertise area 3]
- [Core skill 4]
- [Core skill 5]
```

**Example:**
```markdown
# Backend Developer Agent

## Purpose
Specialize in backend development, API design, database architecture, and server-side implementation.

## Expertise
- API design (REST, GraphQL, WebSockets)
- Database design and optimization
- Authentication and authorization
- Message queues and background jobs
- Microservices architecture
```

---

### 2. Activation Parameters

Define clear parameters that users must provide when activating the agent:

```markdown
## Activation

When activating this agent, provide:
- **[Parameter 1]**: [Description and examples]
- **[Parameter 2]**: [Description and examples]
- **[Parameter 3]**: [Description and examples]
- **[Parameter N]**: [Description and examples]

### Example Activation
\`\`\`
Activate [Agent Name] agent.

[Parameter 1]: [Example value]
[Parameter 2]: [Example value]
[Parameter 3]: [Example value]

Please [action to perform].
\`\`\`
```

**Example:**
```markdown
## Activation

When activating this agent, provide:
- **Task**: API/Service/Feature to implement
- **Type**: REST/GraphQL/WebSocket
- **Database**: PostgreSQL/MySQL/MongoDB
- **Authentication**: JWT/OAuth/Session
- **Scale**: Expected load and performance requirements

### Example Activation
\`\`\`
Activate Backend Developer agent.

Task: Blog post creation API with rich text support
Type: REST API
Database: PostgreSQL
Authentication: JWT tokens
Scale: 10K concurrent users, <200ms response time

Please implement backend solution.
\`\`\`
```

---

### 3. Agent Workflow

Define the step-by-step workflow the agent should follow:

```markdown
## Workflow

1. **[Phase 1 Name]**
   - [Sub-task 1]
   - [Sub-task 2]
   - [Sub-task 3]

2. **[Phase 2 Name]**
   - [Sub-task 1]
   - [Sub-task 2]
   - [Sub-task 3]

3. **[Phase N Name]**
   - [Sub-task 1]
   - [Sub-task 2]
   - [Final verification]
```

**Example:**
```markdown
## Workflow

1. **Design API Structure**
   - Define endpoints and HTTP methods
   - Design request/response schemas
   - Plan error handling
   - Version API appropriately

2. **Implement Data Models**
   - Create database schemas
   - Define relationships
   - Add indexes for performance
   - Handle migrations

3. **Write Tests**
   - Unit tests for business logic
   - Integration tests for API endpoints
   - Database transaction tests
   - Edge case validation
```

---

### 4. Required Context Files

Specify which context files the agent should always load:

```markdown
## Required Context Files

Always load these files when activating this agent:
- `docs/.claude/context/conventions.md` - Project coding standards
- `docs/.claude/context/tech-stack.md` - Technology stack documentation
- `docs/.claude/context/project-overview.md` - Project context
- `[Other agent-specific files]`
```

---

### 5. Deliverables

Define what the agent should produce:

```markdown
## Deliverables

This agent produces:
1. **[Deliverable 1]**
   - [Format or location]
   - [Quality criteria]

2. **[Deliverable 2]**
   - [Format or location]
   - [Quality criteria]

3. **[Deliverable N]**
   - [Format or location]
   - [Quality criteria]
```

**Example:**
```markdown
## Deliverables

This agent produces:
1. **API Implementation**
   - Endpoint handlers following REST conventions
   - Request/response validation
   - Error handling with proper HTTP codes

2. **Database Models**
   - Django/SQLAlchemy models with relationships
   - Migration files
   - Database indexes

3. **Test Suite**
   - Unit tests with >80% coverage
   - Integration tests for all endpoints
   - Test fixtures and factories

4. **Documentation**
   - API endpoint documentation
   - Request/response examples
   - Error response catalog
```

---

### 6. Quality Standards

Define quality expectations:

```markdown
## Quality Standards

### Code Quality
- [ ] Follows project conventions (conventions.md)
- [ ] Proper error handling and validation
- [ ] Comprehensive inline documentation
- [ ] No security vulnerabilities (OWASP Top 10)

### Testing
- [ ] Unit test coverage >80%
- [ ] All edge cases covered
- [ ] Integration tests for critical paths
- [ ] Tests pass in CI/CD pipeline

### Performance
- [ ] Database queries optimized (N+1 prevention)
- [ ] Appropriate caching strategies
- [ ] Response time meets requirements
- [ ] Resource usage within limits

### Documentation
- [ ] API endpoints documented
- [ ] Complex logic explained
- [ ] Setup instructions provided
- [ ] Examples included
```

---

### 7. Best Practices

Include agent-specific best practices:

```markdown
## Best Practices

### [Category 1]
- [Best practice 1]
- [Best practice 2]
- [Best practice 3]

### [Category 2]
- [Best practice 1]
- [Best practice 2]

### Common Pitfalls to Avoid
- ❌ [Anti-pattern 1]
- ❌ [Anti-pattern 2]
- ✅ Instead: [Better approach]
```

**Example:**
```markdown
## Best Practices

### API Design
- Use RESTful resource naming (plural nouns)
- Version APIs from the start (v1, v2)
- Implement proper HTTP status codes
- Include pagination for list endpoints

### Database
- Always use migrations for schema changes
- Index foreign keys and frequently queried fields
- Use database constraints for data integrity
- Implement soft deletes where appropriate

### Common Pitfalls to Avoid
- ❌ Returning raw database objects in responses
- ❌ Ignoring transaction boundaries
- ❌ Missing input validation
- ✅ Instead: Use serializers/DTOs for responses, wrap operations in transactions, validate all inputs
```

---

### 8. Tools and Commands

Provide agent-specific tools and commands:

```markdown
## Tools and Commands

### [Tool Category 1]
\`\`\`bash
# [Command description]
[command example]

# [Another command]
[command example]
\`\`\`

### [Tool Category 2]
\`\`\`bash
[relevant commands]
\`\`\`
```

---

### 9. Decision Framework

Help the agent make consistent decisions:

```markdown
## Decision Framework

### When to [Decision Type 1]
- Condition 1: Use approach A
- Condition 2: Use approach B
- Default: Use approach C

### When to [Decision Type 2]
- Scenario 1: [Recommendation]
- Scenario 2: [Recommendation]
```

**Example:**
```markdown
## Decision Framework

### When to Use REST vs GraphQL
- Simple CRUD operations: Use REST
- Complex data relationships: Consider GraphQL
- Mobile apps with bandwidth constraints: Consider GraphQL
- Public API with wide adoption: Use REST

### When to Add Caching
- Read-heavy operations (>80% reads): Add caching
- Data rarely changes: Add long-term caching
- Real-time requirements: Skip caching
- Expensive computations: Add memoization
```

---

### 10. Communication Protocol

Define how the agent should communicate results:

```markdown
## Communication Protocol

### Starting Work
"I'll implement [task] following these steps:
1. [Step 1]
2. [Step 2]
3. [Step 3]"

### During Implementation
- Report progress after each major step
- Flag blockers or questions immediately
- Explain non-obvious decisions

### Completion Report
"Implementation complete:

**What was built:**
- [Deliverable 1]
- [Deliverable 2]

**Tests:**
- [Test results summary]

**Next steps:**
- [Recommended follow-up actions]

**Files modified:**
- [List of files]"
```

---

## Agent Delegation via Task Tool

### Proper Delegation Pattern

When delegating to an agent, always use the Task tool:

```markdown
Task tool prompt:

Load docs/.claude/_SYSTEM/agents/[agent-name].md
Load docs/.claude/context/conventions.md

Activate as [Agent Name] agent.

Task: [Specific task description]
Type: [Task type]
[Additional parameters...]

Please complete this task following the agent's workflow and conventions.
```

### Why Task Tool Delegation?

- ✅ Creates independent agent instance
- ✅ Agent works autonomously
- ✅ Better context separation
- ✅ Clean completion reporting
- ✅ Easier to track and debug

---

## Example: Complete Agent Configuration

See the following reference agents for complete examples:
- `docs/.claude/_SYSTEM/agents/backend-engineer.md` - Full-stack backend agent
- `docs/.claude/_SYSTEM/agents/test-engineer.md` - Testing specialist
- `docs/.claude/_SYSTEM/agents/systems-architect.md` - Architecture planning

---

## Creating Custom Agents

### When to Create a Custom Agent

Create a custom agent when:
- ✅ Task requires specialized expertise
- ✅ Workflow is repeatable and well-defined
- ✅ Domain knowledge is consistent
- ✅ Multiple team members need same capability

Don't create an agent when:
- ❌ Task is one-time only
- ❌ Workflow is still evolving
- ❌ Too specific to single feature
- ❌ Overlaps significantly with existing agent

### Agent Creation Checklist

- [ ] Agent has clear, focused purpose
- [ ] Expertise areas are well-defined
- [ ] Activation parameters are documented
- [ ] Workflow is step-by-step
- [ ] Quality standards are explicit
- [ ] Deliverables are specified
- [ ] Examples are provided
- [ ] Tested with real tasks

---

## Maintenance

### Updating Agent Configurations

When updating agents:
1. Document changes in decision log
2. Test with representative tasks
3. Update examples if needed
4. Notify team of changes
5. Version control agent files

### Deprecating Agents

When an agent is no longer needed:
1. Move to `docs/.claude/archive/agents/`
2. Document deprecation reason
3. Suggest replacement agent if applicable
4. Update all references in documentation

---

*For comprehensive agent usage guide, see: `docs/.claude/_SYSTEM/agents-guide.md`*
