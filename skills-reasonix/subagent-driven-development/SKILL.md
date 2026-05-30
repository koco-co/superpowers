---
name: subagent-driven-development
description: Use when executing implementation plans with independent tasks in the current session
---

# Subagent-Driven Development (Reasonix 适配版)

Execute implementation plan by dispatching tasks per-step, with integrated review after each.

**Core principle:** One task at a time + spec review after each step = high quality, fast iteration

**Continuous execution:** Do not pause to check in with your human partner between tasks.

## The Process

1. Read plan, extract all tasks with full text, create todo_write
2. For each task:
   a. Implement (subagent dispatch via run_skill, or inline execution)
   b. Run tests, commit
   c. Self-review
   d. Spec compliance check (read actual code vs requirements)
   e. Code quality review (use built-in review tool)
   f. Fix any issues, re-review
   g. Mark task complete
3. After all tasks: use finishing-a-development-branch

## How to Execute Tasks

### Option A: Subagent mode (complex tasks)
Use run_skill to dispatch an isolated implementer subagent:
run_skill({name: "subagent-implementer", arguments: "Task N: [name]

Requirements: ..."})

### Option B: Inline execution (simple tasks)
Execute directly in this session - write test first, then implement.

### Post-Implementation Review (MANDATORY)
1. Spec compliance: Read actual code, compare against requirements line by line
2. Code quality: Use built-in review tool to validate

## Handling Subagent Status
- DONE: Proceed to review
- DONE_WITH_CONCERNS: Read concerns before proceeding
- NEEDS_CONTEXT: Provide context, re-dispatch
- BLOCKED: Assess and escalate if needed

## Red Flags
Never skip reviews. Never start on main/master without consent.
