---
description: Update AI memory system with authority-based routing, Codex validation, then commit
---

**IMMEDIATE ACTION REQUIRED**: Launch the `update-memory-agent` NOW using the Task tool.

## Agent Instructions

Use the Task tool with `subagent_type=update-memory-agent` and provide this prompt:

```
Analyze recent git diffs and update the AI memory system in `.ai/` directory.

## Your Task

1. **Load Context**: Read all memory files starting with QUICK.md (the router)
2. **Analyze Diffs**: Examine uncommitted changes and last 10-20 commits
3. **Identify Gaps**: Compare diffs against memory to find what's missing or outdated
4. **Route to Authority**: Use AUTHORITY_MAP to determine which file owns each content type
5. **Apply Changes**: Use Edit tool to update authoritative files (NO approval needed)
6. **Update Timestamps**: Change meta.lastUpdated to current date
7. **Run Codex Review**: Validate no authority violations before committing
8. **Invoke Commit**: Run `/commit` command when done

## Authority-Based Routing

Each content type has ONE authoritative file. Add content to the right place:
- System topology → ARCHITECTURE.json
- File locations → FILES.json (use globs, NO line numbers)
- Coding patterns → PATTERNS.md
- Business rules/data models → BUSINESS.json
- Debug runbooks → OPS.md
- Decisions → decisions/*.md
- Solutions → solutions/*.yaml
- Deprecations → DEPRECATIONS.md
- Constraints → CONSTRAINTS.md
- Tech debt → TECH_DEBT.md
- Routing ONLY → QUICK.md (pointers, NOT content)

## Anti-Duplication Rules

NEVER add to QUICK.md:
- File paths (FILES.json owns this)
- Pattern details (PATTERNS.md owns this)
- Runbooks (OPS.md owns this)

If content exists in an authoritative file, add a POINTER in QUICK.md, not a COPY.

## Output Format

1. Show git diff analysis summary
2. Apply edits to authoritative files
3. Run Codex memory review (fix violations if found)
4. Invoke `/commit` when review passes
5. Report completion status

Work autonomously - do not ask for approval before making changes.
```

**DO NOT** explain what you're about to do. **DO NOT** show example workflows. **IMMEDIATELY** invoke the Task tool with the above prompt.
