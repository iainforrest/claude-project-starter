# Technical Debt Registry

*Authority: This is source of truth for known technical debt and unfixed code review findings*

## Overview

| Severity | Count | Oldest |
|----------|-------|--------|
| HIGH | 0 | - |
| MEDIUM | 0 | - |
| LOW | 0 | - |

---

## HIGH Severity

*Should be addressed in next sprint*

*(No items)*

---

## MEDIUM Severity

*Address when working in affected area*

*(No items)*

---

## LOW Severity

*Address opportunistically*

*(No items)*

---

## Tech Debt Entry Template

```markdown
### [TD-NNN] [Component]: [Brief Description]
**Severity**: HIGH | MEDIUM | LOW
**Added**: YYYY-MM-DD
**Location**: `file/path/or/glob`
**Description**: [What the issue is]
**Why Deferred**: [Reason for not fixing immediately]
**Suggested Fix**: [How to address]
**Effort Estimate**: [Small/Medium/Large]
```

---

## Resolution Process

1. When fixing debt, remove the entry from this file
2. If debt becomes invalid (code removed), delete the entry
3. Update severity if situation changes
4. Link to PR/commit when resolved

---

## Sources

Tech debt entries come from:
- `/code-review` command (MEDIUM/LOW findings)
- Manual addition during development
- Architecture reviews

---

*Auto-populated by `/code-review` agent for MEDIUM and LOW severity findings.*
