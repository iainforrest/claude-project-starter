# Constraints

*Platform limitations, technical constraints, and explicit non-goals*

**Authority**: This is the single source of truth for what we CAN'T do. If it's a limitation, constraint, or deliberate non-goal, it lives here.

---

## Purpose

This file documents:
- **Platform Limitations**: Technical boundaries imposed by our stack
- **Non-Goals**: Features we explicitly choose NOT to build
- **Technical Constraints**: Hard limits and resource boundaries

**Why this matters**: Knowing what we can't do prevents wasted effort and guides architectural decisions.

---

## Platform Limitations

### API Rate Limits

| Service | Endpoint | Limit | Reset Window |
|---------|----------|-------|--------------|
| [Service 1] | [endpoint] | [N requests/time] | [time window] |
| [Service 2] | [endpoint] | [N requests/time] | [time window] |

### Storage Constraints

| Resource | Limit | Impact |
|----------|-------|--------|
| [Storage type] | [size limit] | [what breaks at limit] |
| [Database] | [connection limit] | [what breaks at limit] |

### Compute Constraints

| Resource | Limit | Impact |
|----------|-------|--------|
| [Resource type] | [limit] | [what breaks at limit] |

### Browser/Client Limitations

| Limitation | Affected Browsers | Workaround |
|------------|-------------------|------------|
| [Feature limitation] | [browser list] | [alternative approach] |

---

## Non-Goals

*Features we explicitly choose NOT to build*

### [Non-Goal Category 1]

**What we're not building**: [Description]

**Why**: [Rationale for not building this]

**Alternative**: [What users should do instead]

**Documented**: [Date decided] | [Decision maker/ADR reference]

---

### [Non-Goal Category 2]

**What we're not building**: [Description]

**Why**: [Rationale]

**Alternative**: [Alternative approach]

**Documented**: [Date decided] | [Decision maker/ADR reference]

---

## Technical Constraints

### Technology Stack Boundaries

| Technology | Constraint | Reason |
|------------|------------|--------|
| [Tech 1] | [Version/feature limit] | [Why this constraint exists] |
| [Tech 2] | [Version/feature limit] | [Why this constraint exists] |

### Security Constraints

**Required**:
- [Security requirement 1]
- [Security requirement 2]

**Forbidden**:
- [Security anti-pattern to avoid]
- [Another forbidden approach]

### Data Constraints

| Data Type | Constraint | Enforcement |
|-----------|------------|-------------|
| [Data type] | [Size/format limit] | [How enforced] |
| [Data type] | [Size/format limit] | [How enforced] |

### Performance Constraints

| Metric | Target | Hard Limit | Consequence |
|--------|--------|------------|-------------|
| [Metric 1] | [target value] | [max value] | [what happens at limit] |
| [Metric 2] | [target value] | [max value] | [what happens at limit] |

---

## Compatibility Constraints

### Minimum Supported Versions

| Platform | Minimum Version | Reason |
|----------|----------------|--------|
| [Platform 1] | [version] | [why this is minimum] |
| [Platform 2] | [version] | [why this is minimum] |

### Browser Support Matrix

| Browser | Minimum Version | Notes |
|---------|----------------|-------|
| Chrome | [version] | [any special notes] |
| Firefox | [version] | [any special notes] |
| Safari | [version] | [any special notes] |
| Edge | [version] | [any special notes] |

---

## Dependency Constraints

### Required Dependencies

| Dependency | Version Constraint | Reason |
|------------|-------------------|--------|
| [Package 1] | [version range] | [why this constraint] |
| [Package 2] | [version range] | [why this constraint] |

### Forbidden Dependencies

| Dependency | Reason |
|------------|--------|
| [Package name] | [why we can't/won't use this] |

---

## Resource Constraints

### Development Environment

| Resource | Minimum | Recommended | Hard Limit |
|----------|---------|-------------|------------|
| Memory | [size] | [size] | [size] |
| Disk | [size] | [size] | [size] |
| CPU | [spec] | [spec] | N/A |

### Production Environment

| Resource | Allocated | Maximum | Scale Strategy |
|----------|-----------|---------|----------------|
| [Resource 1] | [amount] | [max amount] | [how to scale] |
| [Resource 2] | [amount] | [max amount] | [how to scale] |

---

## Adding New Constraints

When you discover a new constraint:

1. **Categorize it** (Platform, Non-Goal, Technical, etc.)
2. **Document clearly**:
   - What is the constraint?
   - Why does it exist?
   - What breaks if ignored?
   - Workaround (if any)
3. **Link to ADR** if decision-based
4. **Update this file** immediately (constraints drive architecture)

---

## Template for New Constraint

```markdown
### [Constraint Name]

**Type**: [Platform/Non-Goal/Technical/etc.]

**Constraint**: [Clear description of the limitation]

**Reason**: [Why this constraint exists]

**Impact**: [What breaks if ignored]

**Workaround**: [Alternative approach, or "None"]

**Documented**: [Date] | [ADR reference if applicable]
```

---

## Notes

- Constraints are not failures - they're boundaries that guide good architecture
- Update this file when you hit limits or make non-goal decisions
- Reference this during PRD creation to avoid building impossible features
- Link from ADRs when constraints drive architectural decisions
