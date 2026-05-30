---
name: dispatching-parallel-agents
description: Use when facing 2+ independent tasks that can be worked on without shared state or sequential dependencies
---

# Dispatching Parallel Agents (Reasonix 适配版)

## Overview

Dispatch multiple isolated subagents concurrently for independent tasks.

**Core principle:** Dispatch one agent per independent problem domain. Let them work concurrently.

## Reasonix Adaptations

- **No Task tool** → Use explore/research for read-only, or run_skill subagent for complex tasks
- **Parallel dispatch** → The tools themselves are sync; you dispatch one, get result, dispatch next.
  For true parallelism, the subagent's work happens in its own context.

## When to Use

**Use when:** 3+ independent test failures, multiple unrelated subsystems, no shared state
**Don't use when:** Failures are related, need full system context, agents would interfere

## The Pattern

### 1. Identify Independent Domains
Group by what's broken — each domain is independent.

### 2. Dispatch Individual Agents

**For investigations:** Use explore tool (read-only subagent)
```
explore({task: "Investigate failing tests in file X: error messages Y"})
```

**For implementations:** Use run_skill subagent mode
```
run_skill({name: "custom-task", arguments: "Implement feature X in file Y"})
```

### 3. Review and Integrate
- Read each summary
- Verify fixes don't conflict
- Run full test suite

## Agent Prompt Structure

Good agent prompts are:
1. **Focused** — one clear problem domain
2. **Self-contained** — all context needed
3. **Specific about output** — what should agent return?

## Common Mistakes

❌ Too broad: "Fix all tests" → agent gets lost
✅ Specific: "Fix agent-tool-abort.test.ts" → focused scope

❌ No context → provide error messages and test names
❌ No constraints → "Do NOT change production code"
❌ Vague output → "Return summary of root cause and changes"
