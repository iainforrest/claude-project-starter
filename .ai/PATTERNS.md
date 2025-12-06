# Pattern Index

*Quick reference for finding implementation patterns*

## How to Use This Index

1. **Find your need** in the Quick Pattern Lookup table below
2. **Load the domain file** from `patterns/[DOMAIN].md`
3. **Copy the template** and adapt to your use case
4. **Reference the codebase** location for working examples

## Pattern Domains

Create domain-specific pattern files as your project grows:

| Domain | File | Description | Status |
|--------|------|-------------|--------|
| Template | `patterns/_TEMPLATE.md` | How to create new domain files | Ready |
| [YOUR_DOMAIN] | `patterns/[NAME].md` | Add as needed | - |

**Common domains to create:**
- `WEB.md` - Frontend patterns (components, state, routing)
- `API.md` - Backend patterns (endpoints, middleware, auth)
- `DATABASE.md` - Data access patterns (queries, repos, migrations)
- `TESTING.md` - Test patterns (unit, integration, e2e)
- `INFRASTRUCTURE.md` - DevOps patterns (deploy, logging, monitoring)

---

## Quick Pattern Lookup

Find the right pattern for your task:

| Need | Pattern | Domain File |
|------|---------|-------------|
| Service with business logic | Service Layer Pattern | patterns/API.md |
| API endpoint | Controller Pattern | patterns/API.md |
| Database queries | Repository Pattern | patterns/DATABASE.md |
| Error handling | Result Type Pattern | patterns/API.md |
| Input validation | Validation Pattern | patterns/API.md |
| Component structure | Component Pattern | patterns/WEB.md |
| State management | State Pattern | patterns/WEB.md |
| Unit tests | Unit Test Pattern | patterns/TESTING.md |
| Integration tests | Integration Test Pattern | patterns/TESTING.md |
| Authentication | Auth Pattern | patterns/AUTH.md |
| Logging | Logging Pattern | patterns/INFRASTRUCTURE.md |
| Agent delegation | Command-Agent Pattern | (below) |

*Table expands as you add patterns. Update when adding new domain files.*

---

## Built-in Pattern: Command-Agent Delegation

This pattern is core to the claude-project-starter workflow.

### When to Use
- Heavy document generation (PRDs, task lists)
- Work requiring isolated context
- Autonomous processing without interactive Q&A
- Pattern matching across entire codebase

### Command Structure
```yaml
---
description: Short description for command list
---

# Command Role and Instructions

[Command gathers context through batched Q&A]
[Confirms summary with user]
[Invokes agent with structured context]
```

### Agent Structure
```yaml
---
name: agent-name
description: When to invoke with examples
model: sonnet
color: blue
---

# Agent Role and Instructions

[Reads memory system for context]
[Processes input autonomously]
[Generates output to /tasks/]
[Returns confirmation summary]
```

### Context Handoff Format
```yaml
FEATURE_NAME: kebab-case-name
PROBLEM: One sentence problem statement
MUST_HAVE:
- Requirement 1
- Requirement 2
NICE_TO_HAVE:
- Optional requirement
USER_FLOWS:
  HAPPY_PATH:
    - Step 1
    - Step 2
  ERROR_FLOWS:
    - Error scenario
SUCCESS_CRITERIA: How we know it's done
COMPLEXITY: Low/Medium/High
```

**Reference**: `.claude/commands/prd.md` → `.claude/agents/prd-writer.md`

---

## Adding New Patterns

### 1. Create Domain File
```bash
cp .ai/patterns/_TEMPLATE.md .ai/patterns/[DOMAIN].md
```

### 2. Update This Index
- Add row to Pattern Domains table
- Add entries to Quick Pattern Lookup table

### 3. Pattern Format
Each pattern in domain files should have:
- **When to Use** - Trigger conditions
- **Template** - Copy-paste code
- **Checklist** - Implementation steps
- **Reference** - `FileName.ext:lineNumber`

---

## Token Efficiency

| Load | Tokens |
|------|--------|
| This index only | ~1,000 |
| Index + 1 domain file | ~3,500 |
| Index + 2 domain files | ~6,000 |

**Strategy**: Load index first, then only the domain file(s) you need.

---

## Maintenance

### After Each Sprint
- Add patterns discovered during implementation
- Update file:line references if code moved
- Remove patterns that didn't work well

### When Patterns Exceed ~400 Lines
- Split into more specific domain files
- Keep each domain file focused

---

*This is an index. Detailed patterns live in `patterns/[DOMAIN].md` files.*
