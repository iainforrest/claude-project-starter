---
description: Pull latest commands and agents from claude-project-starter
---

# Pull Claude Project Starter Updates

Pull the latest generic commands and agents from the central starter repository.

## Key Principle

**Commands and agents are fully generic** - they reference `.ai/` memory files for project-specific context. No customization or templating is needed when pulling updates.

## What Gets Synced

| Syncs | Never Syncs |
|-------|-------------|
| `.claude/commands/*.md` | `.ai/*` (project-specific memory) |
| `.claude/agents/*.md` | `.claude/settings.local.json` (machine-specific) |
| `.claude/WORKFLOW.md` | `pull-cps.md`, `push-cps.md` (sync commands) |

## Steps

### 1. Clone starter repo

```bash
TEMP_DIR=$(mktemp -d)
git clone --depth 1 https://github.com/iainforrest/claude-project-starter.git "$TEMP_DIR"
echo "Cloned to $TEMP_DIR"
```

### 2. Compare files

Compare these directories:
- `.claude/commands/` (excluding pull-cps.md and push-cps.md)
- `.claude/agents/`
- `.claude/WORKFLOW.md` (if exists)

For each file, determine:
- **New**: Exists in starter but not locally
- **Updated**: Exists in both, content differs
- **Same**: No changes needed

Use `diff` to show what changed in updated files.

### 3. Present changes

Show the user:
```
Files to update:
- commands/prd.md (updated - 15 lines changed)
- commands/execute.md (updated - 8 lines changed)
- agents/new-agent.md (new)

Files unchanged:
- commands/commit.md
- commands/update.md
```

For updated files, show the diff.

### 4. Confirm

Ask the user:
- "Apply all changes?"
- "Apply selectively?" (then confirm each file)
- "Cancel"

### 5. Apply changes

Copy approved files from temp directory to this project's `.claude/` directory.

### 6. Cleanup

```bash
rm -rf "$TEMP_DIR"
```

### 7. Report

```
Updated:
- commands/prd.md
- commands/execute.md

Added:
- agents/new-agent.md

Your commands and agents are now in sync with claude-project-starter.
```

---

**Execute this workflow now.**
