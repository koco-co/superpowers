---
name: test-driven-development
description: Use when implementing any feature or bugfix, before writing implementation code
---

# Test-Driven Development (TDD) (Reasonix 适配版)

Same as original. Pure methodology — no platform-specific changes needed.

## Overview

Write the test first. Watch it fail. Write minimal code to pass.

**Core principle:** If you didn't watch the test fail, you don't know if it tests the right thing.

## The Iron Law

NO PRODUCTION CODE WITHOUT A FAILING TEST FIRST.

Write code before the test? Delete it. Start over.

## Red-Green-Refactor

### RED — Write Failing Test
One behavior per test. Clear name. Real code.

### Verify RED (MANDATORY)
Run the test via run_command. Confirm it fails for the right reason.

### GREEN — Minimal Code
Simplest code to pass. No YAGNI additions.

### Verify GREEN (MANDATORY)
Run test via run_command. Confirm it passes AND other tests still pass.

### REFACTOR — Clean Up
Remove duplication, improve names, keep tests green.

## Verification in Reasonix

Use run_command to run tests:
```
run_command({command: "npm test path/to/test.test.ts"})
```

## Common Rationalizations

| Excuse | Reality |
|--------|---------|
| "Too simple to test" | Simple code breaks. Test takes 30 seconds. |
| "I'll test after" | Tests passing immediately prove nothing. |
| "Deleting is wasteful" | Sunk cost. Keeping unverified code = tech debt. |

## Red Flags

Code before test, test passes immediately, "I already tested manually" — ALL mean: Delete code. Start over.
