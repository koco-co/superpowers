---
name: brainstorming
description: "You MUST use this before any creative work - creating features, building components, adding functionality, or modifying behavior."
---

# Brainstorming Ideas Into Designs (Reasonix 适配版)

Help turn ideas into fully formed designs and specs through natural collaborative dialogue.

<HARD-GATE>
Do NOT invoke any implementation skill, write any code, scaffold any project, or take any implementation action until you have presented a design and the user has approved it.
</HARD-GATE>

## Checklist

1. **Explore project context** — check files, docs, recent commits
2. **Offer visual companion** (if visual questions ahead) — own message, not combined
3. **Ask clarifying questions** — one at a time
4. **Propose 2-3 approaches** — with trade-offs and recommendation
5. **Present design** — in sections, get approval after each
6. **Write design doc** — save and commit
7. **Spec self-review** — check for placeholders, contradictions, ambiguity
8. **User reviews written spec** — ask user to review before proceeding
9. **Transition to implementation** — use run_skill({name: "writing-plans"})

## Key Differences from Claude Code version

- **No EnterPlanMode** → Use submit_plan for plan review
- **Skill invocation** → Use run_skill({name: "..."}) instead of Skill tool
- **Todo tracking** → Use todo_write for checklists

## The Process

**Understanding the idea:**
- Check project state first
- If project too large for single spec, decompose into sub-projects
- Ask one question at a time, prefer multiple choice

**Exploring approaches:**
- Propose 2-3 approaches with trade-offs
- Lead with recommendation

**Presenting the design:**
- Scale each section to complexity
- Cover: architecture, components, data flow, error handling, testing
- Get approval after each section

## After the Design

- Write validated spec to docs/superpowers/specs/YYYY-MM-DD-<topic>-design.md
- Commit design doc
- Spec self-review: placeholders, consistency, scope, ambiguity
- Ask user to review spec file
- Then invoke: run_skill({name: "writing-plans"})
