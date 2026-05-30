---
name: writing-skills
description: Use when creating new skills, editing existing skills, or verifying skills work before deployment
---

# Writing Skills

## Overview

**Writing skills IS Test-Driven Development applied to process documentation.**

**Skills live in Reasonix-specific directories:**
- `<project>/.reasonix/skills/<name>.md` — project-local skills
- `~/.reasonix/skills/<name>.md` — global skills (cross-project)
- Reasonix also reads Claude-format: `<project>/.claude/skills/<name>/SKILL.md`

You write test cases (pressure scenarios with subagents), watch them fail (baseline behavior), write the skill (documentation), watch tests pass (agents comply), and refactor (close loopholes).

**Core principle:** If you didn't watch an agent fail without the skill, you don't know if the skill teaches the right thing.

**REQUIRED BACKGROUND:** You MUST understand test-driven-development before using this skill. Use `run_skill({ name: "test-driven-development" })` if needed.

## What is a Skill?

A **skill** is a Markdown playbook that future Reasonix instances can invoke. Skills help future agents find and apply effective approaches.

**Skills are:** Reusable techniques, patterns, tools, reference guides

**Skills are NOT:** Narratives about how you solved a problem once

## Reasonix Skill Format

Skills are single `.md` files with YAML frontmatter:

```markdown
---
name: my-skill-name
description: Use when [specific triggering conditions]
runAs: subagent          # optional — "inline" (default) or "subagent"
model: deepseek-v4-pro   # optional — model override for subagent skills
allowed-tools: read_file, search_content  # optional — restrict subagent tools
---

# Skill Title

## Overview
...
```

**Key frontmatter fields:**
| Field | Required | Description |
|-------|----------|-------------|
| `name` | Yes | Identifier — letters/digits/hyphens only |
| `description` | Yes | ≤120 chars, starts with "Use when...", triggering conditions only |
| `runAs` | No | `inline` (default) or `subagent` (isolated child loop) |
| `model` | No | `deepseek-v4-pro` override for subagent skills (flash is default) |
| `allowed-tools` | No | Comma-separated tool names for subagent skill tool restriction |

**Creating skills:**
- Via slash command: `/skill new my-skill` (project) or `/skill new my-skill --global`
- Via tool: `install_skill({ name: "...", description: "...", body: "..." })`

## TDD Mapping for Skills

| TDD Concept | Skill Creation |
|-------------|----------------|
| **Test case** | Pressure scenario with subagent |
| **Production code** | Skill document (SKILL.md) |
| **Test fails (RED)** | Agent violates rule without skill (baseline) |
| **Test passes (GREEN)** | Agent complies with skill present |
| **Refactor** | Close loopholes while maintaining compliance |
| **Write test first** | Run baseline scenario BEFORE writing skill |
| **Watch it fail** | Document exact rationalizations agent uses |
| **Minimal code** | Write skill addressing those specific violations |
| **Watch it pass** | Verify agent now complies |
| **Refactor cycle** | Find new rationalizations → plug → re-verify |

## When to Create a Skill

**Create when:**
- Technique wasn't intuitively obvious to you
- You'd reference this again across projects
- Pattern applies broadly (not project-specific)
- Others would benefit

**Don't create for:**
- One-off solutions
- Standard practices well-documented elsewhere
- Project-specific conventions (put in REASONIX.md)
- Mechanical constraints (if it's enforceable with regex/validation, automate it)

## Skill Types and Their runAs Mode

### Inline Skills (`runAs: inline` or omitted)
Body is appended to parent context. Best for:
- **Technique skills** — concrete methods with steps (TDD cycle, debugging process)
- **Pattern skills** — ways of thinking about problems
- **Reference skills** — API docs, syntax guides

### Subagent Skills (`runAs: subagent`)
Spawns isolated child loop on `deepseek-v4-flash` (or `pro` if specified). Best for:
- **Investigation skills** — "explore the codebase and return findings"
- **Review skills** — "review this diff and flag issues"
- **Research skills** — "search the web and codebase and synthesize"

**Subagents are read-only by design.** They cannot edit files or run commands. Use them for investigation, verification, and review — not for implementation.

## SKILL.md Structure

```markdown
---
name: Skill-Name-With-Hyphens
description: Use when [specific triggering conditions and symptoms]
---

# Skill Name

## Overview
What is this? Core principle in 1-2 sentences.

## When to Use
[Small inline flowchart IF decision non-obvious]

Bullet list with SYMPTOMS and use cases
When NOT to use

## Core Pattern (for techniques/patterns)
Before/after code comparison

## Quick Reference
Table or bullets for scanning common operations

## Implementation
Inline code for simple patterns
Link to file for heavy reference or reusable tools

## Common Mistakes
What goes wrong + fixes
```

## Agent Search Optimization (ASO)

**Critical for discovery:** Future Reasonix instances need to FIND your skill.

### 1. Rich Description Field

**CRITICAL: Description = When to Use, NOT What the Skill Does**

The description should ONLY describe triggering conditions. Do NOT summarize the skill's process or workflow.

**Why this matters:** When a description summarizes the skill's workflow, the agent may follow the description instead of reading the full skill content. The skill body becomes documentation the agent skips.

```yaml
# ❌ BAD: Summarizes workflow
description: Use when executing plans — dispatches subagent per task with code review

# ✅ GOOD: Just triggering conditions
description: Use when executing implementation plans with independent tasks in the current session
```

### 2. Keyword Coverage

Use words the agent would search for:
- Error messages: "Hook timed out", "ENOTEMPTY"
- Symptoms: "flaky", "hanging", "zombie"
- Synonyms: "timeout/hang/freeze"
- Tools: Actual command names, library names

### 3. Token Efficiency

Skills load into the prefix cache. Every token counts.
- Frequently-loaded skills: <200 words
- Other skills: <500 words
- Use cross-references instead of repeating content

## Testing Skills (RED-GREEN-REFACTOR)

### RED: Baseline Test
Run pressure scenario with an agent WITHOUT the skill. Document:
- What choices did they make?
- What rationalizations did they use (verbatim)?
- Which pressures triggered violations?

### GREEN: Write Minimal Skill
Write skill addressing those specific rationalizations. Don't add content for hypothetical cases.

### REFACTOR: Close Loopholes
Agent found new rationalization? Add explicit counter. Re-test until bulletproof.

## Bulletproofing Against Rationalization

Skills that enforce discipline need to resist rationalization.

### Close Every Loophole Explicitly

<Bad>
```markdown
Write code before test? Delete it.
```
</Bad>

<Good>
```markdown
Write code before test? Delete it. Start over.

**No exceptions:**
- Don't keep it as "reference"
- Don't "adapt" it while writing tests
- Don't look at it
- Delete means delete
```
</Good>

### Address "Spirit vs Letter" Arguments

```markdown
**Violating the letter of the rules is violating the spirit of the rules.**
```

### Build Rationalization Table

```markdown
| Excuse | Reality |
|--------|---------|
| "Too simple to test" | Simple code breaks. Test takes 30 seconds. |
```

### Create Red Flags List

```markdown
## Red Flags — STOP and Start Over

- Code before test
- "This is different because..."
**All of these mean: Delete code. Start over.**
```

## Reasonix-Specific Tips

### Use Reasonix Tools in Skill Instructions

When writing skills, reference Reasonix tools by their exact names:
- `run_skill({ name: "other-skill" })` — invoke another skill
- `edit_file` — SEARCH/REPLACE edits (exact match required)
- `run_command` — shell commands (gated)
- `explore` / `research` / `review` / `security_review` — subagent tools
- `ask_choice` — present options to user
- `todo_write` — track tasks
- `submit_plan` — submit plan for review

### Leverage DeepSeek Features

- Mention when thinking mode helps: "For complex [task], let DeepSeek thinking mode engage"
- Note cost trade-offs: "Routine work on flash; switch to `/pro` for complex logic"
- Reference prefix-cache: "Skills load into the prefix; subsequent invocations are cheap"

### Cross-Referencing Skills

```markdown
# ✅ Good
**REQUIRED SUB-SKILL:** Use `run_skill({ name: "test-driven-development" })`
**REQUIRED BACKGROUND:** You MUST understand systematic-debugging

# ❌ Bad
See skills/testing/test-driven-development (unclear if required)
@skills/testing/test-driven-development/SKILL.md (force-loads, burns context)
```

## Deployment

After writing a skill:
1. Save via `install_skill` tool or `/skill new` command
2. Skill is immediately callable: `run_skill({ name: "my-skill" })`
3. Appears in Skills index on next `/new` or launch
4. For subagent skills, test with a focused task before wider use

## The Bottom Line

**Creating skills IS TDD for process documentation.**

Same Iron Law: No skill without failing test first.
Same cycle: RED (baseline) → GREEN (write skill) → REFACTOR (close loopholes).
Same benefits: Better quality, fewer surprises, bulletproof results.
