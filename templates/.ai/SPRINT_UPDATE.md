# Sprint Update Process

*Guide for keeping memory system in sync with development*

## When to Update

Run `/update` command:
- **End of sprint** - Capture all changes before planning next sprint
- **After major feature** - When significant new code is merged
- **Before long break** - Preserve context before stepping away
- **Weekly minimum** - Keep memory fresh even during slow periods

## What Gets Updated

The `/update` command analyzes git diffs and updates:

| File | Updated When |
|------|--------------|
| `ARCHITECTURE.json` | New patterns, data flows, integrations |
| `BUSINESS.json` | New features, business rules, user flows |
| `FILES.json` | New files, reorganization, deleted files |
| `PATTERNS.md` | New coding patterns discovered |
| `OPS.md` | Build/deploy changes, new debug commands |
| `DEPRECATIONS.md` | Deprecated APIs or patterns |
| `TODO.md` | Sprint completion, new tasks |

## Update Workflow

```
1. Complete development work
2. Run `/code-review` (optional but recommended)
3. Run `/update` to sync memory
4. Run `/commit` to push changes
```

## Authority Rules

The update agent follows strict authority rules:
- Each content type has ONE authoritative file
- No duplication across files
- `QUICK.md` is a router only (no content storage)
- Solutions go to `solutions/*.yaml`
- Decisions go to `decisions/*.md`

## Manual Updates

For changes the agent might miss:
1. Edit the authoritative file directly
2. Run `/update` to validate changes
3. Commit with descriptive message

## Troubleshooting

**Memory seems stale?**
- Run `/update` with recent git history
- Check if files were modified outside normal workflow

**Duplicate content?**
- Check authority map in `QUICK.md`
- Move content to authoritative file
- Remove duplicate

**Missing content?**
- Check `solutions/` and `decisions/` directories
- May need manual addition to appropriate file
