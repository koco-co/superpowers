---
name: writing-plans
description: Use when you have a spec or requirements for a multi-step task, before touching code
---

# Writing Plans

## Overview

Write comprehensive implementation plans assuming the engineer has zero context for our codebase and questionable taste. Document everything they need to know: which files to touch for each task, code, testing, docs they might need to check, how to test it. Give them the whole plan as bite-sized tasks. DRY. YAGNI. TDD. Frequent commits.

Assume they are a skilled developer, but know almost nothing about our toolset or problem domain. Assume they don't know good test design very well.

**Announce at start:** "I'm using the writing-plans skill to create the implementation plan."

**Context:** This should be run in a dedicated worktree — use `run_skill({ name: "using-git-worktrees" })` first if not already in one.

**Save plans to:** `docs/plans/YYYY-MM-DD-<feature-name>.md`

## Bite-Sized Task Granularity

**Each step is one action (2-5 minutes):**
- "Write the failing test" — step
- "Run it to make sure it fails" — step (via `run_command`)
- "Implement the minimal code to make the test pass" — step (via `edit_file`)
- "Run the tests and make sure they pass" — step (via `run_command`)
- "Commit" — step (via `run_command`)

## Plan Document Header

**Every plan MUST start with this header:**

```markdown
# [Feature Name] Implementation Plan

> **For the agent:** REQUIRED SUB-SKILL: Use executing-plans or subagent-driven-development to implement this plan task-by-task.

**Goal:** [One sentence describing what this builds]

**Architecture:** [2-3 sentences about approach]

**Tech Stack:** [Key technologies/libraries]

**Model:** [deepseek-v4-flash for routine tasks; /pro for complex logic]

---
```

## Task Structure

````markdown
### Task N: [Component Name]

**Files:**
- Create: `exact/path/to/file.py`
- Modify: `exact/path/to/existing.py:123-145`
- Test: `tests/exact/path/to/test.py`

**Step 1: Write the failing test**

```python
def test_specific_behavior():
    result = function(input)
    assert result == expected
```

**Step 2: Run test to verify it fails**

Run: `pytest tests/path/test.py::test_name -v` (via `run_command`)
Expected: FAIL with "function not defined"

**Step 3: Write minimal implementation**

Use `edit_file` to add the minimal code.

```python
def function(input):
    return expected
```

**Step 4: Run test to verify it passes**

Run: `pytest tests/path/test.py::test_name -v` (via `run_command`)
Expected: PASS

**Step 5: Commit**

```bash
git add tests/path/test.py src/path/file.py
git commit -m "feat: add specific feature"
```
````

## Remember
- Exact file paths always
- Complete code in plan (not "add validation")
- Exact commands with expected output — specify `run_command` usage
- Reference relevant skills by name with `run_skill({ name: "..." })` syntax
- DRY, YAGNI, TDD, frequent commits

## Execution Handoff

After saving the plan, offer execution choice:

**"Plan complete and saved to `docs/plans/<filename>.md`. Two execution options:**

**1. Subagent-Driven (this session)** — I implement each task myself, dispatch code review via `review` tool after each task. Use `run_skill({ name: "subagent-driven-development" })`.

**2. Parallel Session (separate)** — Open new Reasonix session in the worktree with executing-plans, batch execution with checkpoints. Use `run_skill({ name: "executing-plans" })`.

**Which approach?"**

**If Subagent-Driven chosen:**
- Use `run_skill({ name: "subagent-driven-development" })`
- Stay in this session
- You implement, `review` tool reviews

**If Parallel Session chosen:**
- Guide them to open new session: `npx reasonix code .worktrees/<branch>`
- New session invokes `run_skill({ name: "executing-plans" })`
