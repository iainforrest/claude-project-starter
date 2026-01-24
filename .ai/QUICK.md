# Quick Reference

*Agent entry point and router to authoritative memory files*

---

## Authority Map

**Single source of truth for each content type. Content lives in ONE file only.**

| File | Purpose | Source of Truth For |
|------|---------|---------------------|
| `QUICK.md` | Router + Authority Map | Agent entry point |
| `ARCHITECTURE.json` | System topology | System design, data flows |
| `FILES.json` | File map (globs, NO line numbers) | File locations |
| `PATTERNS.md` | Implementation patterns | Coding conventions |
| `BUSINESS.json` | Business rules + data models | Domain logic, schemas |
| `OPS.md` | Debug, deploy, runbooks | Operations |
| `decisions/` | ADR files | Architecture decisions |
| `solutions/` | Solution capture YAML | Resolved investigation patterns |
| `DEPRECATIONS.md` | Deprecated modules | Deprecation tracking |
| `CONSTRAINTS.md` | Platform limits, non-goals | What we CAN'T do |
| `TECH_DEBT.md` | Unfixed code review findings | Known issues backlog |

---

## Retrieval Strategy

**Before loading full files, grep for matches first.**

```bash
# 1. Check solutions/ for error text or symptoms
grep -r "error message or symptom" .ai/solutions/

# 2. If found, read matching solution file
# 3. If not found, proceed with normal memory loading below
```

---

## Memory Loading Guide

**Load files based on your task:**

| Task | Load |
|------|------|
| Quick lookup | This file only |
| New feature | ARCHITECTURE.json, PATTERNS.md |
| Bug fix | FILES.json, solutions/ (grep first) |
| Business logic | BUSINESS.json |
| Operations/debugging | OPS.md |
| Full context | All .ai/ files |

---

## Build Commands

```bash
# Build
[BUILD_COMMAND]

# Test
[TEST_COMMAND]

# Dev mode
[DEV_COMMAND]

# Lint
[LINT_COMMAND]
```

*For debugging, deploy, monitoring: see OPS.md*

---

## Slash Commands

```bash
/prd [idea]        # Generate PRD from feature idea
/TaskGen [file]    # Generate tasks from PRD
/execute           # Execute task list
/code-review       # Run code review on changes
/bugs [issue]      # Investigate and fix bugs
/commit            # Group and commit changes
/update            # Update memory system
/review-memory     # Analyze memory structure
```

---

## Anti-Duplication Rules

**NEVER add to QUICK.md:**
- File paths (FILES.json owns this)
- Pattern details (PATTERNS.md owns this)
- Runbooks (OPS.md owns this)
- Debug commands (OPS.md owns this)

**This file is a router. Add content to the authoritative file instead.**

---

## Memory System Navigation

```
.ai/
├── QUICK.md            <- YOU ARE HERE (router)
├── ARCHITECTURE.json   -> System patterns, data flows
├── BUSINESS.json       -> Features, rules, data models
├── FILES.json          -> File index (globs, no line numbers)
├── PATTERNS.md         -> Pattern index
├── OPS.md              -> Debug, deploy, runbooks
├── CONSTRAINTS.md      -> Platform limits, non-goals
├── DEPRECATIONS.md     -> Deprecated modules
├── TECH_DEBT.md        -> Unfixed code review findings
├── decisions/          -> ADR files (NNN-title.md)
├── solutions/          -> Solution capture (YYYY-MM-DD-desc.yaml)
└── patterns/           -> Domain-specific patterns
```
