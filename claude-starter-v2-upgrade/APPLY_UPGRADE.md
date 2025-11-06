# Claude Project Starter v2.0 Upgrade Package

This folder contains all the files needed to upgrade claude-project-starter from v1.0 to v2.0.

## What's Included

- `.claude/commands/` - 5 slash commands (prd, tasks, execute, commit, update)
- `.claude/agents/` - 4 specialized agents (update-memory, cto-advisor, security-auditor, ui-ux)
- `.claude/SLASH_COMMAND_MIGRATION.md` - Migration guide
- `README-v2.md` - Updated README with v2.0 documentation

## How to Apply

1. **Navigate to your claude-project-starter repository:**
   ```bash
   cd /path/to/claude-project-starter
   ```

2. **Remove old rule files:**
   ```bash
   rm .claude/PRD_GENERATION.md
   rm .claude/TASK_GENERATION.md
   rm .claude/TASK_EXECUTION.md
   ```

3. **Copy new structure:**
   ```bash
   cp -r /path/to/MyVoi/claude-starter-v2-upgrade/.claude .
   cp /path/to/MyVoi/claude-starter-v2-upgrade/README-v2.md README.md
   ```

4. **Verify structure:**
   ```bash
   ls .claude/commands/  # Should show: prd.md, tasks.md, execute.md, commit.md, update.md
   ls .claude/agents/    # Should show: 4 agent files
   ```

5. **Commit and push:**
   ```bash
   git add -A
   git commit -m "feat: Upgrade to v2.0 with slash commands and specialized agents"
   git push
   ```

## What Changed

**From v1.0:**
- Old `@.claude/FILE.md` syntax
- 3 rule files only
- No specialized agents
- No automation commands

**To v2.0:**
- Modern `/command` syntax
- 5 workflow commands + 4 expert agents
- Automated `/commit` and `/update` commands
- Enhanced PRD/task generation with security, assets, breaking changes

## File Manifest

```
.claude/
├── commands/
│   ├── prd.md (3.5 KB)
│   ├── tasks.md (9.2 KB)
│   ├── execute.md (7.1 KB)
│   ├── commit.md (2.1 KB)
│   └── update.md (0.8 KB)
├── agents/
│   ├── update-memory-agent.md (6.9 KB)
│   ├── cto-technical-advisor.md (4.8 KB)
│   ├── security-auditor.md (6.2 KB)
│   └── ui-ux-expert.md (5.4 KB)
└── SLASH_COMMAND_MIGRATION.md (3.1 KB)
```

## Improvements from MyVoi

These files incorporate learnings from several iterations of the MyVoi project:

- ✅ Subtask marking enforcement in `/execute`
- ✅ Breaking changes analysis in `/prd`
- ✅ Security considerations sections
- ✅ Asset & resource planning
- ✅ Build verification frequency guidance
- ✅ Memory system as mandatory final task
- ✅ All patterns generalized for any project type

## Support

After applying the upgrade, see `.claude/SLASH_COMMAND_MIGRATION.md` for complete migration documentation.

---

**Package Created:** November 4, 2025
**Source:** MyVoi development system improvements
**Target:** claude-project-starter v2.0
