---
name: finishing-a-development-branch
description: Use when implementation is complete, all tests pass, and you need to decide how to integrate the work
---

# Finishing a Development Branch (Reasonix 适配版)

## Overview

Guide completion of development work by presenting clear options.

**Core principle:** Verify tests → Detect environment → Present options → Execute choice → Clean up.

## Reasonix Adaptations

- **No native worktree tools** → Use pure git commands via run_command
- **No gh CLI assumed** → Use GitHub MCP tools for PR creation
- **Git operations** → Use run_command for git commands

## The Process

### Step 1: Verify Tests
Run project's test suite via run_command.
If tests fail: report, don't proceed.

### Step 2: Detect Environment
```bash
run_command({command: "git rev-parse --git-dir"})
run_command({command: "git rev-parse --git-common-dir"})
```

Determine: normal repo, named-branch worktree, or detached HEAD.

### Step 3: Determine Base Branch
```bash
run_command({command: "git merge-base HEAD main"})
```

### Step 4: Present Options

**Normal repo / named-branch worktree:**
1. Merge back to <base-branch> locally
2. Push and create a Pull Request
3. Keep the branch as-is
4. Discard this work

### Step 5: Execute Choice

**Option 1 — Merge Locally:**
Use run_command for git operations. Clean up worktree after.

**Option 2 — Push and Create PR:**
Use run_command for git push. Use github_create_pull_request tool for PR.

**Option 3 — Keep As-Is:**
Report branch and worktree preserved.

**Option 4 — Discard:**
Require typed "discard" confirmation before proceeding.

### Step 6: Cleanup
Only for Options 1 and 4. Use run_command with git worktree remove.

## Key Differences from Claude Code

| Operation | Claude Code | Reasonix |
|-----------|-------------|----------|
| git commands | Bash tool | run_command |
| PR creation | gh CLI | github_create_pull_request |
| Worktree create | native tool | git worktree add |
| File ops | Edit tool | edit_file / write_file |
