---
name: using-git-worktrees
description: Use when starting feature work that needs isolation from current workspace
---

# Using Git Worktrees (Reasonix 适配版)

## Overview

Ensure work happens in an isolated workspace. Reasonix has no native worktree tools — use pure git.

**Core principle:** Detect existing isolation first. Use git worktree. Never fight the sandbox.

## Reasonix Adaptations

- **No native worktree tools** (no EnterWorktree / WorktreeCreate) → pure git fallback
- **Sandbox awareness:** Reasonix filesystem is sandboxed to project root
- **Git commands:** Use run_command for all git operations

## Step 0: Detect Existing Isolation

```bash
run_command({command: "git rev-parse --git-dir"})
run_command({command: "git rev-parse --git-common-dir"})
```

**If GIT_DIR != GIT_COMMON:** Already in linked worktree. Skip creation.

## Step 1: Create Worktree (git only, no native tools)

1. Check for `.worktrees/` directory (create if needed)
2. Verify directory is git-ignored:
   ```bash
   run_command({command: "git check-ignore -q .worktrees"})
   ```
3. Create the worktree:
   ```bash
   run_command({command: "git worktree add .worktrees/<branch-name> -b <branch-name>"})
   ```

## Step 2: Project Setup
Auto-detect and run: npm install / cargo build / etc.

## Step 3: Verify Clean Baseline
Run tests. If failing, report and ask before proceeding.

## Sandbox Note

If git worktree add fails with permission error (sandbox denial), work in place.

## Quick Reference

| Situation | Action |
|-----------|--------|
| Already in linked worktree | Skip creation |
| Need isolation | git worktree add |
| .worktrees/ not ignored | Add to .gitignore first |
| Permission error | Work in place |

## Red Flags

Never create worktree when already isolated. Never skip baseline test verification.
