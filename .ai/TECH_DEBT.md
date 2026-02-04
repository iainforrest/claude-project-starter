# Technical Debt

*Code review findings and known issues not immediately fixed*

**Authority**: This is the single source of truth for known unfixed issues. All MEDIUM and LOW code review findings that don't get fixed immediately are tracked here.

---

## Purpose

This file captures:
- **MEDIUM and LOW findings** from code review that aren't fixed immediately
- **Known issues** that are accepted but should be addressed later
- **Refactoring opportunities** identified but deferred
- **Documentation gaps** that need filling

**Why this matters**: Tech debt is inevitable. Tracking it prevents:
- Rediscovering the same issues repeatedly
- Losing context on why issues were deferred
- Accumulating invisible debt that slows development

---

## Severity Levels

| Level | Definition | Typical Response |
|-------|------------|------------------|
| **CRITICAL** | Security issue, data loss risk | Fix immediately (NOT tracked here) |
| **HIGH** | Functional bug, major degradation | Fix in current sprint (NOT tracked here) |
| **MEDIUM** | Minor bug, code smell, pattern violation | Fix when touching related code |
| **LOW** | Cosmetic issue, optimization opportunity | Fix when convenient |

**Note**: CRITICAL and HIGH findings should be fixed immediately, not added to this file.

---

## Known Issues

### MEDIUM Severity

_No MEDIUM items currently tracked._

---

### LOW Severity

#### [TD-001] prd.md: Checkbox format for automated validation

**Severity**: LOW

**Location**: `.claude/commands/prd.md` (Phase 5 validation section)

**Description**: Validation step uses markdown checkboxes for automated validation steps instead of describing as code logic. Other automated phases describe validation as numbered steps with failure behaviors.

**Why Deferred**: Cosmetic issue. Current checkbox format is actually more scannable and readable.

**Impact**: Minor documentation style inconsistency.

**Suggested Fix**: Convert checkboxes to numbered automated check descriptions with explicit failure handling.

**Added**: 2026-02-04

**Source**: CR-2026-02-04 (Both)

---

#### [TD-002] prd.md: Pseudo-code uses wrong block type

**Severity**: LOW

**Location**: `.claude/commands/prd.md` (Phase 5 reconciliation steps)

**Description**: Uses ```bash code blocks for pseudo-code that isn't valid bash syntax (e.g., "ORIGINAL_CONTEXT = read /tasks/...").

**Why Deferred**: Purely cosmetic. Anyone reading understands this is pseudocode. The syntax highlighting improves readability.

**Impact**: Minimal - no functional impact.

**Suggested Fix**: Change to ```yaml or unlabeled code blocks for pseudo-code.

**Added**: 2026-02-04

**Source**: CR-2026-02-04 (Codex only)

---

#### [TD-003] prd.md: Post-Agent Response option change unexplained

**Severity**: LOW

**Location**: `.claude/commands/prd.md` (Post-Agent Response section)

**Description**: Option 4 in Post-Agent Response may have changed from previous versions without documenting the reason. Phase 6 covers ADR capture separately.

**Why Deferred**: Historical context issue. Current options are functional.

**Impact**: Minimal - users may wonder about option changes if familiar with older version.

**Suggested Fix**: Add comment explaining option rationale or restore as option 5 if needed.

**Added**: 2026-02-04

**Source**: CR-2026-02-04 (Claude only)

---

## Refactoring Opportunities

### [RO-001] [Refactoring Name]

**Opportunity**: [What could be refactored]

**Location**: `[files/modules affected]`

**Benefit**: [Why this refactoring would help]

**Effort**: [Estimated effort - Small/Medium/Large]

**Trigger**: [When to do this - e.g., "When adding new auth methods"]

**Added**: [YYYY-MM-DD]

**Source**: [Where this was identified]

---

## Documentation Gaps

### [DOC-001] [What's Undocumented]

**Gap**: [What documentation is missing]

**Location**: `[files/modules that need docs]`

**Impact**: [Why this matters]

**Suggested**: [What documentation should be added]

**Added**: [YYYY-MM-DD]

**Source**: [CR-YYYY-MM-DD]

---

## Tech Debt Summary

| ID | Type | Severity | Component | Added | Status |
|----|------|----------|-----------|-------|--------|
| TD-001 | Issue | LOW | prd.md | 2026-02-04 | Open |
| TD-002 | Issue | LOW | prd.md | 2026-02-04 | Open |
| TD-003 | Issue | LOW | prd.md | 2026-02-04 | Open |

---

## Resolved Tech Debt

*Items resolved are moved here for historical tracking*

### [TD-XXX] [Resolved Item]

**Resolution Date**: [YYYY-MM-DD]

**Resolution**: [How it was fixed]

**Commit**: [commit SHA]

**Original Issue**: [Original description]

---

## Tech Debt Workflow

### When Code Review Finds Issues

1. **CRITICAL/HIGH**: Fix immediately, don't add to this file
2. **MEDIUM**:
   - Add to this file if not fixed in current work
   - Include context for future fix
3. **LOW**:
   - Add to this file
   - Tag with trigger conditions for when to fix

### When Fixing Tech Debt

1. **Update Status**: Mark as in-progress while working
2. **Complete**: Move to "Resolved Tech Debt" section when done
3. **Reference**: Include TD-XXX ID in commit message
4. **Clean Up**: Periodically archive old resolved items

### When to Address Tech Debt

**Triggers for fixing**:
- You're touching related code anyway
- Issue severity increases (MEDIUM → HIGH)
- Multiple LOW issues in same component (batch fix)
- Sprint planning allocates time for tech debt
- Issue blocks new feature development

---

## Template for New Tech Debt Item

```markdown
#### [TD-XXX] [Component/File]: [Brief Description]

**Severity**: [MEDIUM/LOW]

**Location**: [file path or stable glob]

**Description**: [Detailed explanation of what's wrong]

**Why Deferred**: [Clear reason for not fixing now]

**Impact**: [What this affects or could affect]

**Suggested Fix**: [Recommended approach]

**Added**: YYYY-MM-DD

**Source**: [CR-YYYY-MM-DD] [Claude only|Codex only|Both]

**Related**: [Links to related items/ADRs]
```

---

## Template for Refactoring Opportunity

```markdown
### [RO-XXX] [Refactoring Name]

**Opportunity**: [What could be improved]

**Location**: [files/modules]

**Benefit**: [Why this would help]

**Effort**: [Small/Medium/Large estimate]

**Trigger**: [When to do this]

**Added**: YYYY-MM-DD

**Source**: [Where identified]
```

---

## Notes

- Tech debt is not shame - it's pragmatic trade-offs documented
- Update this file immediately when code review identifies deferred issues
- Review this file during sprint planning to allocate cleanup time
- Batch similar LOW items for efficient fixing
- Archive resolved items older than 6 months to keep file manageable
- Link to `.ai/solutions/` when fixes reveal reusable patterns
