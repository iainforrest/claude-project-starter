# AI Memory System Guide

## What This Is

The `.ai/` folder is your project's **persistent memory system** for AI-assisted development. It prevents context loss between Claude sessions by storing structured knowledge about your project.

## Core Philosophy

**Context Efficiency**: Load only what you need, when you need it.

This system is designed to:
- Keep total memory under ~3,000 lines for single-app projects
- Allow selective loading based on task type
- Scale gracefully to mono-repos when needed
- Provide instant access without re-analyzing the codebase

## Quick Navigation

| Working On | Files to Load | Est. Tokens |
|------------|---------------|-------------|
| **Quick lookup** | QUICK.md | ~1,000-2,000 |
| **New feature** | QUICK.md + ARCHITECTURE.json + PATTERNS.md | ~4,000-6,000 |
| **Bug fix** | QUICK.md + FILES.json | ~3,000-4,000 |
| **Business logic** | BUSINESS.json + ARCHITECTURE.json | ~5,000-8,000 |
| **Full context** | All core files | ~15,000-20,000 |

**Rule**: Always start with QUICK.md - it's your entry point.

---

## The Files

### QUICK.md (Start Here)
**Purpose**: Fast reference for commands, file locations, and debugging.

Load first for: Any task. Contains build commands, critical file locations, common issues.

### ARCHITECTURE.json
**Purpose**: Architectural patterns, data flows, component relationships.

Load for: Understanding system structure, planning new features, integration work.

### BUSINESS.json
**Purpose**: Business rules, feature specs, user flows, performance targets.

Load for: Understanding requirements, business logic, data models.

### FILES.json
**Purpose**: Smart file index organized by purpose and layer.

Load for: Finding files, understanding dependencies, navigation.

### PATTERNS.md (Index)
**Purpose**: Lightweight index pointing to domain-specific pattern files.

Load for: Finding implementation templates. Then load specific `patterns/[DOMAIN].md` file.

### patterns/ folder
**Purpose**: Domain-specific implementation patterns and copy-paste templates.

Structure: Create files like `patterns/WEB.md`, `patterns/API.md`, `patterns/DATABASE.md` as your project grows.

### TODO.md
**Purpose**: Current sprint tasks and completed work.

Load for: Understanding current priorities and recent history.

### SPRINT_UPDATE.md
**Purpose**: Process guide for updating the memory system.

Load for: End-of-sprint maintenance procedures.

---

## Token Budget Guidelines

### Single-App Project (Target: ~3,000 lines total)

```
File              Lines       Tokens (approx)
─────────────────────────────────────────────
QUICK.md          100-400     1,000-4,000
ARCHITECTURE.json 200-500     2,000-5,000
BUSINESS.json     300-800     3,000-8,000
FILES.json        200-600     2,000-6,000
PATTERNS.md       ~200        ~1,000 (index only)
patterns/[DOMAIN] ~400 each   ~2,500 each
TODO.md           50-200      500-2,000
SPRINT_UPDATE.md  ~200        ~1,000 (static)
─────────────────────────────────────────────
TOTAL TARGET      ~3,000      ~15,000-25,000
```

### Typical Task Load

Most tasks need only 2-3 files (~3,000-6,000 tokens), not the full system.

---

## Usage Workflow

### Before Any Feature

1. **Read QUICK.md** - Get oriented (30 seconds)
2. **Read relevant memory** - Based on task type (see navigation table)
3. **Implement** - Using knowledge from memory
4. **Update memory** - Add what you learned

### When to Update

| Trigger | Action |
|---------|--------|
| New file created | Add to FILES.json |
| New pattern discovered | Add to patterns/ folder, update PATTERNS.md index |
| Sprint complete | Follow SPRINT_UPDATE.md process |
| Bug fix with learning | Add to QUICK.md common issues |
| Architecture change | Update ARCHITECTURE.json |

---

## Critical Rules

1. **No separate sprint files** - Integrate learnings into core files
2. **Keep it under 3,000 lines** - Split into domains or apps if exceeding
3. **Use line number references** - `FileName.ext:123` for instant navigation
4. **JSON for structured data** - Machine-parseable, greppable
5. **Markdown for patterns** - Human-readable, copy-paste ready

---

## Scaling to Mono-Repo

When your project grows to multiple apps or exceeds 3,000 lines:

See **MONOREPO_GUIDE.md** for:
- When to upgrade
- How to create app-specific memory folders
- MONOREPO.json template
- Context loading strategies for multi-app projects

---

## File Structure

### Single-App (Default)

```
.ai/
├── README.md           # This file
├── QUICK.md            # Quick reference (START HERE)
├── ARCHITECTURE.json   # Architecture patterns
├── BUSINESS.json       # Business logic
├── FILES.json          # File index
├── PATTERNS.md         # Pattern index
├── patterns/           # Domain-specific patterns
│   └── _TEMPLATE.md    # Template for new domains
├── TODO.md             # Task tracking
└── SPRINT_UPDATE.md    # Update process
```

### Mono-Repo (When Scaled)

```
.ai/
├── README.md           # This file
├── QUICK.md            # Monorepo navigation
├── MONOREPO.json       # Workspace architecture
├── app1/               # App-specific memory
│   ├── QUICK.md
│   ├── ARCHITECTURE.json
│   ├── BUSINESS.json
│   ├── FILES.json
│   ├── PATTERNS.md
│   └── TODO.md
└── app2/               # Another app's memory
    └── ...
```

---

## Common Mistakes

| Mistake | Instead Do |
|---------|------------|
| Creating SPRINT_X.md files | Update core files with sprint learnings |
| Loading all files for every task | Use navigation table, load selectively |
| Letting memory exceed 3,000 lines | Split into domains or app-specific folders |
| Skipping memory before features | Always start with QUICK.md |
| Not updating after sprints | Follow SPRINT_UPDATE.md process |

---

## Getting Started

1. **Review QUICK.md** - Understand current project state
2. **Customize templates** - Replace placeholders with real data
3. **Use memory immediately** - Reference before implementing
4. **Update as you work** - Memory grows with your project
5. **Run /update** - Use the update command after significant work

---

*The memory system is your project's brain. Keep it lean, keep it current.*
