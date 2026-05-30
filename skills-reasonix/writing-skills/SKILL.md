---
name: writing-skills
description: Use when creating new skills, editing existing skills, or verifying skills work before deployment
---

# Writing Skills (Reasonix 适配版)

Same core methodology as original. Minor tool reference updates.

## Overview

Writing skills IS Test-Driven Development applied to process documentation.

**Core principle:** If you didn't watch an agent fail without the skill, you don't know if it teaches the right thing.

## Reasonix Adaptations

- **Installation:** Use run_skill({name: "skill-creator"}) or write to .reasonix/skills/
- **Skill storage:** ~/.reasonix/skills/ (global) or .reasonix/skills/ (project)
- **Invocation:** run_skill({name: "skill-name"})

## TDD for Skills

| TDD Concept | Skill Creation |
|-------------|----------------|
| Test case | Pressure scenario with subagent |
| Production code | Skill document |
| Test fails (RED) | Agent violates rule without skill |
| Test passes (GREEN) | Agent complies with skill present |

## When to Create

**Create when:** Technique wasn't intuitive, broadly applicable
**Don't create for:** One-off solutions, project-specific conventions

## SKILL.md Structure

Frontmatter: name + description (start with "Use when...")
Body: Overview, When to Use, Core Pattern, Quick Reference, Common Mistakes

## The Iron Law

NO SKILL WITHOUT A FAILING TEST FIRST.

Applies to NEW skills AND EDITS to existing skills.

## RED-GREEN-REFACTOR

1. RED: Run scenario WITHOUT skill — document baseline
2. GREEN: Write minimal skill addressing those failures
3. REFACTOR: Close loopholes, re-test

## Claude Search Optimization

Description = When to Use, NOT What the Skill Does.
✅ "Use when executing implementation plans with independent tasks"
❌ "Use when executing plans — dispatches subagent per task with code review"
