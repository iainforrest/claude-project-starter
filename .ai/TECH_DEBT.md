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

#### [TD-001] [Component/File]: [Brief Description]

**Severity**: MEDIUM

**Location**: `[file path or glob pattern]`

**Description**: [Detailed explanation of the issue]

**Why Deferred**: [Reason for not fixing immediately]

**Impact**: [What problems this causes or could cause]

**Suggested Fix**: [Recommended approach to resolve]

**Added**: [YYYY-MM-DD]

**Source**: [CR-YYYY-MM-DD or other source reference]

**Related**: [Links to ADRs, issues, or other tech debt items]

---

### LOW Severity

#### [TD-002] [Component/File]: [Brief Description]

**Severity**: LOW

**Location**: `[file path or glob pattern]`

**Description**: [Detailed explanation]

**Why Deferred**: [Reason]

**Impact**: [Minimal impact description]

**Suggested Fix**: [Approach]

**Added**: [YYYY-MM-DD]

**Source**: [CR-YYYY-MM-DD]

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
| TD-001 | Issue | MEDIUM | [component] | [date] | Open |
| TD-002 | Issue | LOW | [component] | [date] | Open |
| RO-001 | Refactor | - | [component] | [date] | Open |
| DOC-001 | Docs | - | [component] | [date] | Open |

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

**Source**: [CR-YYYY-MM-DD or other reference]

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
