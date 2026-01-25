# Quick Reference

*Router and authority map - NO content duplication*

## Authority Map

| Need | Go To |
|------|-------|
| System architecture | `ARCHITECTURE.json` |
| Business rules, features | `BUSINESS.json` |
| File locations | `FILES.json` |
| Coding patterns | `PATTERNS.md` |
| Build, test, deploy | `OPS.md` |
| Platform limitations | `CONSTRAINTS.md` |
| Deprecated patterns | `DEPRECATIONS.md` |
| Known tech debt | `TECH_DEBT.md` |
| Release notes | `CHANGELOG.md` |
| Past decisions (ADR) | `decisions/*.md` |
| Solved problems | `solutions/*.yaml` |

## Retrieval Strategy

```bash
# Step 1: Grep solutions first
grep -r "error keyword" .ai/solutions/

# Step 2: If not found, load relevant file
# Step 3: Full context only for architecture work
```

## Key Commands

| Command | Purpose |
|---------|---------|
| `/prd` | Generate PRD from feature idea |
| `/TaskGen` | Break PRD into tasks |
| `/execute` | Run task list |
| `/bugs` | Investigate bugs |
| `/commit` | Group and commit changes |
| `/update` | Sync memory from git diffs |
| `/code-review` | Review recent changes |

## Project Quick Facts

**Project**: [YOUR_PROJECT_NAME]
**Stack**: [YOUR_TECH_STACK]
**Build**: [YOUR_BUILD_COMMAND]
**Test**: [YOUR_TEST_COMMAND]

## Critical Files

| Purpose | Location |
|---------|----------|
| Entry point | [YOUR_ENTRY_FILE] |
| Config | [YOUR_CONFIG_FILE] |
| Main logic | [YOUR_MAIN_DIR] |

---

*This file routes to content. It never stores content itself.*
