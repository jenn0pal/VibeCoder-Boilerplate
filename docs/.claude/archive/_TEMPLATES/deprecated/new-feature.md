# Feature: [Name]

## User Story
As a [role], I want [capability], so that [benefit]

## Acceptance Criteria
- [ ] Criterion 1
- [ ] Criterion 2

## Technical Approach
[High-level design]

## Tasks
See tasks.md

## Open Questions
- Question 1?
- Question 2?
```

### 5. **Smart Context Loading**

When starting a conversation:
```
"I'm working on [feature]. Here's the context:
1. Project overview: [paste/upload .claude/context/project-overview.md]
2. Feature spec: [paste/upload specific feature spec]
3. Current conventions: [paste relevant conventions]

Please acknowledge you understand the context before we begin."
```

### 6. **Version Control Integration**

**.gitignore additions:**
```
# Claude working files (if ephemeral)
.claude/tasks/in-progress.md
.claude/prompts/scratch.md

# Keep these in git:
!.claude/features/
!.claude/context/
!.claude/archive/
```

### 7. **Iterative Spec Refinement**
```
"Claude, review this feature spec and tell me:
1. What's unclear or ambiguous?
2. What edge cases are missing?
3. What technical risks do you see?
4. Suggest acceptance criteria I might have missed"