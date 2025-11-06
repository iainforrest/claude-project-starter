---
description: Update AI memory system with recent work using git diff analysis, then commit changes
---

**IMMEDIATE ACTION REQUIRED**: Launch the `update-memory-agent` NOW using the Task tool.

## Agent Instructions

Use the Task tool with `subagent_type=update-memory-agent` and provide this prompt:

```
Analyze recent git diffs and update the AI memory system in `.ai/` directory.

## Your Task

1. **Load Context**: You have access to all 8 memory files as primary context
2. **Analyze Diffs**: Examine uncommitted changes and last 10-20 commits
3. **Identify Gaps**: Compare diffs against memory to find what's missing or outdated
4. **Propose Updates**: Suggest specific edits to relevant `.ai/` files with file:line references
5. **Apply Changes**: Use Edit tool to update files (NO approval needed - proceed autonomously)
6. **Update Timestamps**: Change meta.lastUpdated to current date
7. **Invoke Commit**: Run `/commit` command when done to create grouped commits and push

## What to Update

Examine the git diffs and determine which `.ai/` files need updates:
- New features or patterns → PATTERNS.md or ARCHITECTURE.json
- File changes → FILES.json
- New commands/workflows → QUICK.md
- Business logic changes → BUSINESS.json

Focus on high-value updates that will help future development. Keep updates concise and actionable.

## Output Format

1. Show git diff analysis summary
2. Apply edits directly (no approval needed)
3. Invoke `/commit` when done
4. Report completion status

Work autonomously - do not ask for approval before making changes.
```

**DO NOT** explain what you're about to do. **DO NOT** show example workflows. **IMMEDIATELY** invoke the Task tool with the above prompt.
