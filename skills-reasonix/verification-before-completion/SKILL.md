---
name: verification-before-completion
description: Use when about to claim work is complete, fixed, or passing, before committing or creating PRs
---

# Verification Before Completion (Reasonix 适配版)

Same as original. Pure behavioral rule — no platform-specific changes needed.

## Overview

Claiming work is complete without verification is dishonesty, not efficiency.

**Core principle:** Evidence before claims, always.

## The Iron Law

NO COMPLETION CLAIMS WITHOUT FRESH VERIFICATION EVIDENCE.

## The Gate Function

BEFORE claiming any status:
1. IDENTIFY: What command proves this?
2. RUN: Execute full command via run_command
3. READ: Full output, exit code, failure count
4. VERIFY: Does output confirm the claim?
5. ONLY THEN: Make the claim with evidence

## Key Patterns

**Tests:** [Run test command] [See: 0 failures] "All tests pass"
**Build:** [Run build] [See: exit 0] "Build passes"
**Requirements:** Re-read plan → checklist → verify each → report

## Red Flags

Using "should", "probably", "seems to". Expressing satisfaction before verification.
Trusting agent success reports. ANY wording implying success without running verification.

## The Bottom Line

Run the command. Read the output. THEN claim the result. Non-negotiable.
