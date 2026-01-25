# AI Memory System

*Persistent context for AI-assisted development*

## Quick Start

1. **First time?** Run the bootstrap guide: `INSTALL-NEW.md` or `INSTALL-EXISTING.md`
2. **Need something?** Check `QUICK.md` for the authority map
3. **Making changes?** Use `/update` command to sync memory with git diffs

## File Authority Map

Each file is the **single source of truth** for specific content types:

| Content Type | Authoritative File |
|--------------|-------------------|
| System architecture, patterns | `ARCHITECTURE.json` |
| Business rules, features | `BUSINESS.json` |
| File locations, structure | `FILES.json` |
| Coding patterns, conventions | `PATTERNS.md` |
| Operations, debugging | `OPS.md` |
| Platform constraints | `CONSTRAINTS.md` |
| Deprecated APIs/patterns | `DEPRECATIONS.md` |
| Known tech debt | `TECH_DEBT.md` |
| Architecture decisions | `decisions/*.md` |
| Solved problems | `solutions/*.yaml` |
| Quick navigation | `QUICK.md` (router only) |

**Rule**: Content lives in ONE place. `QUICK.md` routes to content, never duplicates it.

## Retrieval Strategy

1. **Grep first**: `grep -r "keyword" .ai/solutions/` before loading full files
2. **Load specific files**: Only load what you need for the task
3. **Full context**: Load all files only for major architectural work

## Commands That Update Memory

| Command | What It Captures |
|---------|-----------------|
| `/prd` | Decisions to `decisions/*.md` |
| `/bugs` | Solutions to `solutions/*.yaml` |
| `/execute` | Decisions, solutions, deprecations |
| `/code-review` | Tech debt to `TECH_DEBT.md` |
| `/update` | Syncs all files from git diffs |

## Directory Structure

```
.ai/
├── README.md           # This file
├── QUICK.md            # Router + authority map
├── ARCHITECTURE.json   # System design
├── BUSINESS.json       # Business logic
├── FILES.json          # File index
├── PATTERNS.md         # Pattern index
├── OPS.md              # Operations
├── CONSTRAINTS.md      # Limitations
├── DEPRECATIONS.md     # Deprecated items
├── TECH_DEBT.md        # Known debt
├── TODO.md             # Sprint tracking
├── SPRINT_UPDATE.md    # Update process
├── decisions/          # ADRs
├── solutions/          # Solved problems
└── patterns/           # Domain patterns
```

## Token Efficiency

| Load | Approximate Tokens |
|------|-------------------|
| QUICK.md only | ~500 |
| QUICK + 1 JSON | ~2,000 |
| All core files | ~8,000 |

Load incrementally based on task needs.
