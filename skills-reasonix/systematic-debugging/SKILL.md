---
name: systematic-debugging
description: Use when encountering any bug, test failure, or unexpected behavior, before proposing fixes
---

# Systematic Debugging (Reasonix 适配版)

Same core methodology as original. No platform-specific changes needed.

## Overview

Random fixes waste time. Quick patches mask underlying issues.

**Core principle:** ALWAYS find root cause before attempting fixes.

## The Iron Law

NO FIXES WITHOUT ROOT CAUSE INVESTIGATION FIRST.

## The Four Phases

### Phase 1: Root Cause Investigation
1. Read error messages carefully (stack traces, line numbers)
2. Reproduce consistently
3. Check recent changes (git diff, commits)
4. Gather evidence at component boundaries
5. Trace data flow backward

### Phase 2: Pattern Analysis
Find working examples, compare, identify differences.

### Phase 3: Hypothesis and Testing
Single hypothesis → minimal test → verify → new hypothesis if needed.

### Phase 4: Implementation
Create failing test → single fix → verify → if 3+ fixes failed, question architecture.

## Tool Usage in Reasonix

- **Investigation:** read_file, search_content, explore, git diff via run_command
- **Fix verification:** run_command to run tests

## Quick Reference

| Phase | Key Activities |
|-------|---------------|
| 1. Root Cause | Read errors, reproduce, check changes, gather evidence |
| 2. Pattern | Find working examples, compare |
| 3. Hypothesis | Form theory, test minimally |
| 4. Implementation | Create test, fix, verify |

## Red Flags

"Quick fix for now", "Just try changing X" — STOP. Return to Phase 1.
