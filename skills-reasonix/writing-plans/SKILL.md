---
name: writing-plans
description: Use when you have a spec or requirements for a multi-step task, before touching code
---

# Writing Plans (Reasonix 适配版)

## Overview

Write comprehensive implementation plans with bite-sized tasks. Assume engineer has zero context.

## Reasonix Adaptations

- **Plan header:** References subagent-driven-development / executing-plans via run_skill
- **Task tracking:** Use todo_write instead of TaskCreate/TaskUpdate
- **Tool references:** Use Reasonix-native tool names

## Plan Document Header

```markdown
# [Feature Name] Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use run_skill({name: "subagent-driven-development"}) (recommended) or run_skill({name: "executing-plans"}).

**Goal:** [One sentence]
**Architecture:** [2-3 sentences]
**Tech Stack:** [Key technologies]
---
```

## Task Structure

Each step is one action (2-5 minutes). Include exact commands for verification.

```markdown
### Task N: [Component Name]

**Files:**
- Create: path/to/file.py
- Modify: path/to/existing.py:123-145

- [ ] **Step 1: Write failing test**
  [code block with test]

- [ ] **Step 2: Run to verify failure**
  Run: pytest path/test.py -v

- [ ] **Step 3: Write minimal implementation**
  [code block]

- [ ] **Step 4: Run to verify pass**
  Run: pytest path/test.py -v

- [ ] **Step 5: Commit**
  git add ... && git commit -m "..."
```

**In Reasonix:** Use todo_write to track checkbox progress. Use run_command for verification commands.

## No Placeholders

Every step must contain actual code. No "TBD", "TODO", "implement later".

## Self-Review

After writing, check: spec coverage, no placeholders, type consistency across tasks.

## Execution Handoff

Offer choice:
1. Subagent-Driven: run_skill({name: "subagent-driven-development"})
2. Inline Execution: run_skill({name: "executing-plans"})
