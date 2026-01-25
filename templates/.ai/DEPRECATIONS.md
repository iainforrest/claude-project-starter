# Deprecations

*Authority: This is source of truth for deprecated APIs, patterns, and migrations*

## Active Deprecations

*Items currently deprecated but not yet removed*

### [DEP-001] [Name of Deprecated Item]
**Deprecated**: YYYY-MM-DD
**Removal Target**: YYYY-MM-DD (or version)
**Replacement**: [What to use instead]
**Migration Guide**:
```
[Steps to migrate]
```
**Files Affected**: `path/to/files`

---

## Completed Migrations

*Deprecations that have been fully removed*

### [DEP-000] Example Completed Migration
**Deprecated**: 2025-01-01
**Removed**: 2025-03-01
**What Changed**: [Description]
**Notes**: [Any relevant notes]

---

## Deprecation Process

### When Deprecating
1. Add entry to Active Deprecations above
2. Add `@deprecated` annotation/comment in code
3. Log warning when deprecated code is used (if applicable)
4. Set removal target date
5. Create migration guide

### When Removing
1. Verify no usage remains
2. Remove code
3. Move entry to Completed Migrations
4. Update removal date

---

## Deprecation Template

```markdown
### [DEP-NNN] [Name]
**Deprecated**: YYYY-MM-DD
**Removal Target**: YYYY-MM-DD
**Replacement**: [Alternative]
**Migration Guide**:
```
[Steps]
```
**Files Affected**: `glob/pattern`
```

---

*Auto-populated by `/execute` command when patterns are deprecated.*
