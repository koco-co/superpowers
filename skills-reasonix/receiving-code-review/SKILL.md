---
name: receiving-code-review
description: Use when receiving code review feedback, before implementing suggestions, especially if feedback seems unclear or technically questionable
---

# Code Review Reception (Reasonix 适配版)

Same as original. Pure behavioral methodology — no platform-specific changes needed.

## Overview

Code review requires technical evaluation, not emotional performance.

**Core principle:** Verify before implementing. Ask before assuming.

## The Response Pattern

```
WHEN receiving review feedback:
1. READ: Complete feedback without reacting
2. UNDERSTAND: Restate requirement (or ask)
3. VERIFY: Check against codebase reality
4. EVALUATE: Technically sound for THIS codebase?
5. RESPOND: Technical acknowledgment or reasoned pushback
6. IMPLEMENT: One item at a time, test each
```

## Forbidden Responses

NEVER: "You're absolutely right!", "Great point!" (performative)
INSTEAD: Restate requirement, ask clarifying questions, push back with technical reasoning.

## When To Push Back

- Suggestion breaks existing functionality
- Reviewer lacks full context
- Violates YAGNI
- Technically incorrect for this stack

## Common Mistakes

| Mistake | Fix |
|---------|-----|
| Performative agreement | State requirement or just act |
| Blind implementation | Verify first |
| Assuming reviewer is right | Check if breaks things |

## The Bottom Line

External feedback = suggestions to evaluate, not orders to follow.
