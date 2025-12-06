# Quick Reference Guide

*Commands, file locations, and debugging shortcuts*

---

## Memory Loading Guide

**Start here for any task.** Load additional files based on what you're doing:

| Task | Also Load |
|------|-----------|
| Quick lookup | This file only |
| New feature | ARCHITECTURE.json, PATTERNS.md |
| Bug fix | FILES.json |
| Business logic | BUSINESS.json |
| Full context | All .ai/ files |

---

## Build Commands

```bash
# Build
[BUILD_COMMAND]              # e.g., "npm run build", "./gradlew build", "cargo build"

# Test
[TEST_COMMAND]               # e.g., "npm test", "./gradlew test", "cargo test"

# Development/Watch mode
[DEV_COMMAND]                # e.g., "npm run dev", "./gradlew run", "cargo run"

# Lint/Format
[LINT_COMMAND]               # e.g., "npm run lint", "./gradlew lint"
```

---

## Critical File Locations

*Add file references with line numbers as your project grows*

```
[Feature]Service.ext:line    # Description of what's here
[Feature]Repository.ext:line # Description
config.ext:line              # Configuration file
routes.ext:line              # Route definitions
```

---

## Debugging Commands

```bash
# Debug mode
[DEBUG_COMMAND]              # e.g., "npm run debug", "cargo build --debug"

# Logs
[LOG_COMMAND]                # e.g., "tail -f logs/app.log"

# Test specific file
[TEST_FILE_COMMAND]          # e.g., "npm test -- path/to/test"
```

---

## Performance Monitoring

```bash
# Profile
[PROFILE_COMMAND]            # e.g., "npm run profile"

# Analyze bundle/build
[ANALYZE_COMMAND]            # e.g., "npm run analyze"
```

---

## Common Issues & Fixes

### Issue: [Common Problem]
**Symptoms**: [Description]
**Fix**: [Solution]
**File**: [Relevant file reference]

### Issue: [Another Problem]
**Symptoms**: [Description]
**Fix**: [Solution]
**Command**: [Specific command to run]

---

## Development Workflow

```bash
# Quick rebuild
[QUICK_BUILD]

# Install dependencies
[INSTALL_DEPS]               # e.g., "npm install", "./gradlew dependencies"

# Clean build
[CLEAN_BUILD]                # e.g., "npm run clean && npm run build"
```

---

## Slash Commands

```bash
/prd [idea]        # Generate PRD from feature idea
/tasks [prd-file]  # Generate tasks from PRD
/execute           # Execute task list
/bugs [issue]      # Investigate and fix bugs
/commit            # Group and commit changes
/update            # Update memory system
/review-memory     # Analyze and optimize memory structure
```

---

## Memory System Navigation

```
.ai/
├── QUICK.md          ← YOU ARE HERE (start point)
├── ARCHITECTURE.json   → System patterns, data flows
├── BUSINESS.json       → Features, rules, requirements
├── FILES.json          → File index, dependencies
├── PATTERNS.md         → Pattern index (lightweight)
├── patterns/           → Domain-specific patterns
│   └── _TEMPLATE.md    → How to add new patterns
├── TODO.md             → Current sprint tasks
└── SPRINT_UPDATE.md    → Update procedures
```

---

## Notes

- Update this file with commands as you discover them
- Add debugging techniques that work
- Document solutions to problems encountered
- Keep it concise - this is for quick reference
- Use `File.ext:line` format for file references
