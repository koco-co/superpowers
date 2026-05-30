---
name: requesting-code-review
description: Use when completing tasks, implementing major features, or before merging to verify work meets requirements
---

# Requesting Code Review

Dispatch review subagents to catch issues before they cascade.

**Core principle:** Review early, review often.

## Reasonix Review Tools

Reasonix provides two built-in review subagent tools, both read-only and running on `deepseek-v4-flash`:

| Tool | Purpose | Checks |
|------|---------|--------|
| `review` | General code review | Correctness, security, missing tests, hidden behavior |
| `security_review` | Security-focused review | Injection, authz, secrets, deserialization, path-traversal, crypto |

Both tools **automatically check the current branch diff** — you don't need to compute or pass SHAs. Just describe what to focus on.

## When to Request Review

**Mandatory:**
- After each task in subagent-driven development
- After completing major feature
- Before merge to main

**Optional but valuable:**
- When stuck (fresh perspective)
- Before refactoring (baseline check)
- After fixing complex bug

## How to Request

### General Code Review

```
review({ task: "Review [what was implemented].
Requirements: [what it should do].
Focus on: [specific concerns or 'general']." })
```

The `review` tool reads the current branch diff, checks against your description, and returns:
- **Strengths** — what's well done
- **Issues** — by severity (Critical / Important / Minor) with file:line references
- **Assessment** — ready to merge or needs fixes

### Security Review

```
security_review({ task: "focus on [area of concern, e.g. 'token handling in src/auth/']" })
```

Use for changes touching: authentication, input parsing, file I/O, external requests, secrets management.

### After Fixing Issues

Always re-review after implementing fixes:

```
review({ task: "Re-review [what was fixed]. Confirm issues from previous review are resolved." })
```

## Example

```
[Just completed Task 2: Add verification function]

You: Let me request code review before proceeding.

review({ task: "Review verification and repair functions for conversation index.
Requirements: Task 2 from docs/plans/deployment-plan.md — verifyIndex() and repairIndex() with 4 issue types.
Focus on: correctness, edge cases, test coverage." })

[review returns]:
  Strengths: Clean architecture, real tests (not mocks), good error handling
  Issues:
    Important: Missing progress indicators for long-running repair operations
    Minor: Magic number (100) for reporting interval — extract constant
  Assessment: Ready to proceed after fixing Important issue

You: [Fix progress indicators via edit_file]
review({ task: "Re-review Task 2 after fix. Confirm progress indicators added." })
review: ✅ All issues resolved. Approved.

[Continue to Task 3]
```

## Integration with Workflows

**Subagent-Driven Development:**
- Review after EACH task
- Catch issues before they compound
- Fix before moving to next task

**Executing Plans:**
- Review after each batch (3 tasks)
- Get feedback, apply, continue

**Ad-Hoc Development:**
- Review before merge
- Review when stuck

## Red Flags

**Never:**
- Skip review because "it's simple"
- Ignore Critical issues
- Proceed with unfixed Important issues
- Argue with valid technical feedback

**If reviewer wrong:**
- Push back with technical reasoning
- Show code/tests that prove it works
- Request clarification from user if needed

## Cost Note

`review` and `security_review` subagents run on `deepseek-v4-flash` (~$0.14/M input tokens). A typical review costs a fraction of a cent. The cost of NOT reviewing (bugs in production, debugging later) is orders of magnitude higher.
