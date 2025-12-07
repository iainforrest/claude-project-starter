# PRD: Starter Kit Sync System

**Generated:** 2025-12-07
**Status:** Approved
**Version:** v2.0 (Simplified)

## Overview

Enable seamless syncing of claude-project-starter updates across multiple repositories.

**Problem:** When improvements are made to commands/agents in one project, there's no easy way to push them back to the starter repo and pull them into other projects.

**Solution:** Two simple commands (`/pull-cps` and `/push-cps`) that sync the `.claude/` directory.

---

## Key Insight: Separation of Concerns

After auditing MyVoi, CoachOps, and the starter repo, we discovered a clean separation:

| Directory | Purpose | Syncs? | Customization |
|-----------|---------|--------|---------------|
| `.claude/commands/` | Workflow instructions | ✅ Yes | None needed - already generic |
| `.claude/agents/` | Domain expertise | ✅ Yes | None needed - already generic |
| `.ai/` | Project-specific memory | ❌ Never | Created by bootstrap, evolves with project |

**Commands and agents are already fully generic.** They reference the `.ai/` memory system for all project-specific context:
- "Read ARCHITECTURE.json for patterns..."
- "Check BUSINESS.json for features..."
- "Use commands from QUICK.md..."

**The `.ai/` files are never synced.** They're created once during bootstrap and grow organically with the project.

---

## The Simplified System

### `/pull-cps` - Pull Updates

```
1. Clone starter repo to temp directory
2. Compare .claude/commands/ and .claude/agents/
3. Show diff of what changed
4. Copy approved files (no transformation needed)
5. Cleanup
```

**No templating, no placeholders, no customization.** Files come in as-is because they're already generic.

### `/push-cps` - Push Improvements

```
1. Ask user what files to push
2. Verify files are generic (no project-specific content)
3. Clone starter repo
4. Copy files to temp clone
5. Create PR
```

**The only check is ensuring no project-specific content leaked in.** If the commands/agents are written correctly (referencing `.ai/` for context), they should already be generic.

---

## What Gets Synced

### Always Sync
- `.claude/commands/*.md` - All command files
- `.claude/agents/*.md` - All agent files
- `.claude/settings.json` - Shared settings (if exists)
- `.claude/WORKFLOW.md` - Workflow documentation

### Never Sync
- `.ai/*` - All memory files (project-specific)
- `.claude/settings.local.json` - Local permissions (machine-specific)
- Project-specific commands (e.g., `test-voice-engine.md` in MyVoi)

### Exclusions for Pull
- `pull-cps.md` and `push-cps.md` themselves (avoid overwriting local copies)

---

## Validation Rules

### For `/push-cps` - Before Creating PR

Scan files for project-specific content:

**Red Flags (block push):**
- Project names (MyVoi, CoachOps, etc.)
- Absolute paths (`/root/projects/...`)
- Service account emails
- API keys or secrets
- Hardcoded tech stack (should say "from QUICK.md" not "./gradlew")

**Acceptable:**
- References to `.ai/` files
- Placeholders like `[BUILD_COMMAND]`
- Generic examples in code blocks
- Pattern descriptions without specific implementations

### For `/pull-cps` - Before Applying

Show user:
1. List of files that will be updated
2. Diff for each changed file
3. Any files that would be added (new commands/agents)

---

## Implementation

### Phase 1: Update Commands (Now)
1. Simplify `/pull-cps` - remove templating logic
2. Simplify `/push-cps` - add validation, remove generalization logic
3. Test with actual sync

### Phase 2: Documentation
1. Update README with sync workflow
2. Document how to keep commands/agents generic

---

## Success Metrics

- **Pull time:** < 30 seconds to sync updates
- **Push time:** < 1 minute to create PR
- **Zero transformation:** Files copied as-is in both directions
- **Validation catches:** 100% of project-specific leaks blocked

---

## What This Replaces

The original PRD proposed:
- `project-profile.json` with all project values
- `{{PLACEHOLDER}}` syntax in files
- Automatic customization on pull
- Automatic generalization on push

**This is no longer needed** because:
1. Commands/agents are already generic
2. They read from `.ai/` for project context
3. `.ai/` files are never synced

The system is simpler than we thought.
