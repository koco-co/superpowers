---
name: requesting-code-review
description: Use when completing tasks, implementing major features, or before merging to verify work meets requirements
---

# Requesting Code Review (Reasonix 适配版)

## Overview

Dispatch a code reviewer to catch issues before they cascade.

**Core principle:** Review early, review often.

## Reasonix Adaptation

- **No Task tool** → Use built-in review tool:
  ```
  review({task: "Review implementation for correctness and completeness"})
  ```
- **For security-sensitive changes** → Use security_review:
  ```
  security_review({task: "Focus on auth/file handling aspects"})
  ```

## When to Request Review

**Mandatory:**
- After each task in subagent-driven development
- After completing major feature
- Before merge

**Optional:**
- When stuck, before refactoring, after fixing complex bug

## How to Request

**1. Get git SHAs:**
```bash
run_command({command: "git rev-parse HEAD~1"})
run_command({command: "git rev-parse HEAD"})
```

**2. Dispatch review:**
```
review({task: "Review Task N implementation. Requirements: [...]. Check: correctness, completeness, edge cases."})
```

**3. Act on feedback:**
- Fix Critical issues immediately
- Fix Important issues before proceeding
- Push back with reasoning if reviewer is wrong

## Review Focus

- Correctness: Does it work correctly?
- Completeness: Meets all requirements?
- Code quality: Well-structured, tested?
- Security: Any vulnerabilities?
- Edge cases: Handled properly?

## Integration

**Subagent-Driven Development:** Review after EACH task
**Ad-Hoc:** Review before merge or when stuck
