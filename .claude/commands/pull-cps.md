---
description: Pull latest changes from claude-project-starter into this project
---

# Pull Claude Project Starter Updates

You are pulling the latest updates from the claude-project-starter repository into this project.

## Configuration

- **Source repo**: `iainforrest/claude-project-starter` (GitHub)
- **Branch**: `master`
- **Target directory**: `.claude/` in current project

## Steps

### 1. Fetch the latest from the starter repo

```bash
# Create a temp directory and clone the starter repo (shallow clone for speed)
TEMP_DIR=$(mktemp -d)
git clone --depth 1 https://github.com/iainforrest/claude-project-starter.git "$TEMP_DIR"
```

### 2. Compare and show differences

Compare the following directories between the cloned starter and this project:
- `.claude/commands/` - slash commands
- `.claude/settings.json` - settings (if exists)
- `.ai/` - memory system templates (structure only, not project data)

Use `diff -rq` or similar to identify changed files, then show the actual diff content for each changed file.

**Important exclusions** - Do NOT overwrite these project-specific files:
- `.ai/*.json` files containing project-specific data
- Any file that has been customized for this specific project
- The pull-cps.md and push-cps.md commands themselves (to avoid overwriting local copies)

**Safe to update**:
- `.claude/commands/*.md` - command templates (except sync commands)
- `.ai/PATTERNS.md` - generic patterns
- `.ai/QUICK.md` - quick reference

### 3. Present changes for review

Show the user:
1. List of files that would be updated
2. For each file, show a readable diff of what would change
3. Highlight any files that might have project-specific customizations

### 4. Ask for confirmation

Before applying any changes, ask:
- "Apply all changes?"
- "Apply selectively?" (then ask about each file)
- "Cancel"

### 5. Apply approved changes

Copy the approved files from the temp directory to this project.

### 6. Cleanup

```bash
rm -rf "$TEMP_DIR"
```

### 7. Report

Summarize what was updated and note any new commands or features added.

---

**Execute this workflow now.** Start by cloning the starter repo to a temp directory.
