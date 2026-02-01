# Use Authority-Based Memory System

**Status**: Accepted

**Date**: 2026-01-25

**Deciders**: CTO (via project vision)

**Tags**: memory-system, architecture, documentation

---

## Context

The original memory system allowed content duplication across files (file paths in QUICK.md, patterns in multiple places, etc.). This caused:
- Stale references when files moved
- Confusion about which file to update
- Token waste loading duplicate information
- Maintenance burden keeping copies in sync

We needed a single-source-of-truth approach where each type of content has exactly one authoritative home.

---

## Decision

We will implement an authority-based memory system where:
1. Each file has clear authority over specific content types
2. QUICK.md becomes a router with an authority map table
3. Content duplication is forbidden - other files use pointers/references
4. The Codex CLI validates authority rules during memory updates

**Authority Map**: See QUICK.md for the complete authority map table defining which file owns each content type.

---

## Consequences

### Positive Consequences

- Single source of truth eliminates staleness
- Faster agent loading (grep before full file read)
- Clear ownership for updates
- Codex validation catches violations automatically
- Token efficiency through elimination of duplication

### Negative Consequences

- Requires discipline to maintain (enforced by Codex validation)
- Initial migration effort to split existing content
- Agents must understand the authority map

### Neutral Consequences

- More files in .ai/ directory (but each focused)
- QUICK.md becomes much smaller (~150 lines vs ~200+)

---

## Implementation Notes

Implementation phases:
1. Create new template files (OPS.md, CONSTRAINTS.md, etc.)
2. Rewrite QUICK.md as router with authority map
3. Update JSON templates for new structure
4. Add Codex validation to update workflow
5. Embed automated capture in existing commands

---

## Related Decisions

- Builds on: Memory system foundation (implicit in project design)
- Enables: Automated tech debt tracking via code review
- Enables: Solution capture for faster future debugging

---

## References

- PRD: luminous-skipping-liskov.md
- Codex synthesis findings about grep-first retrieval
- CTO vision for "memory becomes tool through authority clarity"

---

## Revision History

| Date | Change | Author |
|------|--------|--------|
| 2026-01-25 | Created | Claude Sonnet |
| 2026-01-25 | Status set to Accepted | Execute Agent |
