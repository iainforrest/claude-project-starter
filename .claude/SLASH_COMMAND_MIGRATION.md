# Slash Command Migration Guide

This project has been upgraded from the older `@mention` system to the modern **slash command** system for better UX and discoverability.

## What Changed

**Old System (v1.0):**
- `@.claude/PRD_GENERATION.md [idea]` → Generate PRD
- `@.claude/TASK_GENERATION.md @path/to/PRD.md` → Generate tasks
- `@.claude/TASK_EXECUTION.md @path/to/tasks.md` → Execute tasks

**New System (v2.0):**
- `/prd [idea]` → Generate PRD
- `/tasks @path/to/PRD.md` → Generate tasks
- `/execute @path/to/tasks.md` → Execute tasks
- `/commit` → Intelligent git commits
- `/update` → Update AI memory system

## New Directory Structure

```
.claude/
  ├── commands/          # Slash commands (invoke with /command-name)
  │   ├── prd.md        # /prd - Generate PRD
  │   ├── tasks.md      # /tasks - Generate task list
  │   ├── execute.md    # /execute - Execute tasks
  │   ├── commit.md     # /commit - Intelligent commits
  │   └── update.md     # /update - Update memory system
  │
  ├── agents/           # Specialized agents (invoked via Task tool)
  │   ├── update-memory-agent.md      # Memory system updates
  │   ├── cto-technical-advisor.md    # Technical feasibility
  │   ├── security-auditor.md         # Security reviews
  │   └── ui-ux-expert.md             # UI/UX guidance
  │
  └── [OLD FILES - can be deleted after migration]
      ├── PRD_GENERATION.md
      ├── TASK_GENERATION.md
      └── TASK_EXECUTION.md
```

## Benefits of Slash Commands

✅ **Faster workflow** - Less typing, more natural syntax
✅ **Discoverable** - Commands appear in slash command autocomplete
✅ **Cleaner** - `/prd` instead of `@.claude/PRD_GENERATION.md`
✅ **Extensible** - Easy to add new commands as needed

## Migration Steps

If you're upgrading from v1.0 to v2.0:

1. **Verify new structure exists:**
   ```bash
   ls .claude/commands/  # Should show: prd.md, tasks.md, execute.md, commit.md, update.md
   ls .claude/agents/    # Should show agent files
   ```

2. **Test new commands:**
   ```
   /prd Test feature idea
   ```

3. **Delete old files (optional but recommended):**
   ```bash
   cd .claude
   rm PRD_GENERATION.md TASK_GENERATION.md TASK_EXECUTION.md
   ```

4. **Update any documentation** that references the old `@.claude/` syntax

## New Commands

### Core Workflow Commands

**`/prd [feature idea]`**
- Generates implementation-ready PRD
- Saves to `/tasks/prd-[feature-name].md`
- Uses AI memory system for architectural context

**`/tasks @path/to/prd.md`**
- Generates pattern-specific task list from PRD
- Saves to `/tasks/tasks-[feature-name].md`
- Includes file references, patterns, and complexity ratings

**`/execute @path/to/tasks.md`**
- Executes task list systematically
- Marks subtasks complete in real-time
- Runs builds and tests per task

### Utility Commands

**`/commit`**
- Analyzes uncommitted changes
- Creates logical, grouped commits
- Pushes to GitHub automatically
- Can be invoked by agents

**`/update`**
- Launches `update-memory-agent`
- Analyzes git diffs
- Updates `.ai/` memory system
- Commits and pushes changes

## Agents vs Commands

**Commands** are workflows you invoke directly:
- Use slash syntax: `/command-name`
- Run immediately in current context
- Examples: `/prd`, `/tasks`, `/execute`, `/commit`

**Agents** are specialized AI assistants:
- Invoked via Task tool by Claude
- Run autonomously with specific expertise
- Examples: security audits, technical feasibility, UI/UX review

## Getting Help

- **Command usage**: Type `/` and see autocomplete
- **Command details**: Read `.claude/commands/[command-name].md`
- **Agent details**: Read `.claude/agents/[agent-name].md`
- **Memory system**: Consult `.ai/README.md`

## Backward Compatibility

The old `@.claude/PRD_GENERATION.md` syntax still works if those files exist, but we recommend migrating to slash commands for:
- Better discoverability
- Cleaner syntax
- Easier maintenance
- Future extensibility

---

**Version**: 2.0
**Migration Date**: [Current Date]
**Status**: Slash commands active, old files can be removed
