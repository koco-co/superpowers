---
name: using-superpowers
description: Use when starting any conversation — establishes how to find and use skills
---

# Using Superpowers (Reasonix 适配版)

## Instruction Priority

1. User's explicit instructions — highest priority
2. Superpowers skills — override default system behavior
3. Default system prompt — lowest priority

## Reasonix Adaptation

- **Skill invocation:** Use run_skill({name: "..."}) instead of Skill/Bash tool
- **Available subagents:** explore, research, review, security_review
- **Todo tracking:** todo_write
- **Plan gates:** submit_plan

## How to Access Skills

In Reasonix: Use run_skill({name: "<skill-name>", arguments: "<task>"}).
When invoked, skill content is loaded — follow it directly.

## The Rule

Invoke relevant skills BEFORE any response or action. Even 1% chance → invoke.

IF A SKILL APPLIES TO YOUR TASK, YOU DO NOT HAVE A CHOICE. YOU MUST USE IT.

## Flow

1. User message received
2. Might any skill apply? (even 1% → invoke)
3. run_skill({name: "skill-name"})
4. Announce: "Using [skill] to [purpose]"
5. If checklist: create todo_write per item
6. Follow skill exactly
7. Respond

## Skill Priority

1. Process skills first (brainstorming, debugging)
2. Implementation skills second

## Red Flags

| Thought | Reality |
|---------|---------|
| "This is just a simple question" | Questions are tasks. Check for skills. |
| "I need more context first" | Skill check comes BEFORE clarifying questions. |
| "This doesn't need a formal skill" | If a skill exists, use it. |
