# CLAUDE.md

This file provides guidance to Claude Code when working with this repository.

## Project Identity

[PROJECT_NAME] is a [TYPE] that [ONE_SENTENCE_VALUE_PROP].

**Stack:** [LANGUAGE/FRAMEWORK], [KEY_DEPENDENCIES]

## Memory System

Before any task, consult `.ai/QUICK.md` which routes to authoritative files:

| File | Authority |
|------|-----------|
| `ARCHITECTURE.json` | System design, patterns, data flows |
| `FILES.json` | File locations and purposes |
| `PATTERNS.md` | Implementation templates |
| `BUSINESS.json` | Business rules and features |
| `OPS.md` | Build, test, debug, deploy |
| `CONSTRAINTS.md` | Platform limits, non-goals |

## Commands

| Command | Purpose |
|---------|---------|
| `/prd` | Generate PRD from feature idea |
| `/TaskGen` | Generate tasks from PRD |
| `/execute` | Execute task list |
| `/bugs` | Investigate bugs |
| `/commit` | Group and commit changes |
| `/update` | Update memory system |

## Universal Rules

<!-- Only include constraints that affect LITERALLY every task -->
<!-- Most constraints belong in .ai/CONSTRAINTS.md -->
<!-- Examples: -->
<!-- - Never commit .env files -->
<!-- - All PRs require tests -->
<!-- - Use TypeScript strict mode -->
