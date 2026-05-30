---
name: executing-plans
description: Use when you have a written implementation plan to execute with review checkpoints
---

# Executing Plans (Reasonix 适配版)

## Overview

Load plan, review critically, execute all tasks, report when complete.

## Reasonix Adaptations

- **No EnterPlanMode** → Use submit_plan for approval gates
- **No Task subagent** → Execute tasks inline or dispatch via run_skill subagent
- **Todo tracking** → Use todo_write
- **Review** → Use built-in review tool
- **Git worktrees** → Use run_command with git commands

## The Process

### Step 1: Load and Review Plan
1. Read plan file
2. Review critically — identify questions or concerns
3. If concerns: raise with your human partner
4. Create todo_write and proceed

### Step 2: Execute Tasks

For each task:
1. Mark as in_progress in todo_write
2. Follow each step exactly
3. Run verifications as specified (use run_command)
4. Mark as completed

### Step 3: Complete Development

After all tasks:
- REQUIRED SUB-SKILL: run_skill({name: "finishing-a-development-branch"})
- Verify tests, present options, execute choice

## When to Stop

STOP when: hit blocker, plan has critical gaps, instruction unclear, verification fails.

**Ask for clarification rather than guessing.**

## Tool Mapping (Claude Code → Reasonix)

| Claude Code | Reasonix |
|-------------|----------|
| Task(subagent) | run_skill subagent mode / inline |
| TodoWrite | todo_write |
| EnterPlanMode | submit_plan |
| Bash | run_command / run_background |
| Skill | run_skill |
| Read | read_file / search_content |

## Remember

- Review plan critically first
- Follow plan steps exactly
- Don't skip verifications
- Stop when blocked
