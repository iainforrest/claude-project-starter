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
| Authority routing | Authority-Based Memory | (below) |
| Automated capture | Knowledge Capture Pattern | (below) |
| Codex validation | Three-Tier Execution | (below) |

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

## Built-in Pattern: Authority-Based Memory

This pattern ensures single source of truth for all content types.

### When to Use
- Updating memory system
- Adding new content to .ai/ files
- Preventing content duplication
- Routing updates to correct authoritative file

### Authority Map
```
Content Type          → Authoritative File
──────────────────────────────────────────
System topology       → ARCHITECTURE.json
File locations        → FILES.json
Coding patterns       → PATTERNS.md
Business rules        → BUSINESS.json
Operations/runbooks   → OPS.md
Decisions (ADR)       → decisions/*.md
Solutions/learnings   → solutions/*.yaml
Deprecations          → DEPRECATIONS.md
Constraints           → CONSTRAINTS.md
Tech debt             → TECH_DEBT.md
Routing only          → QUICK.md (NO content)
```

### Implementation Checklist
- [ ] Identify content type using authority map
- [ ] Check if content already exists in authoritative file
- [ ] Add content to authoritative file (or update existing)
- [ ] If needed, add pointer in QUICK.md (not copy)
- [ ] Validate: no content duplication across files

**Reference**: `.ai/decisions/001-use-authority-based-memory.md`

---

## Built-in Pattern: Automated Knowledge Capture

Commands automatically capture decisions, solutions, deprecations, and tech debt.

### When to Use
- During /prd → capture architectural decisions
- During /bugs → capture solutions (YAML)
- During /execute → capture solutions, decisions, deprecations
- During /code-review → capture MEDIUM/LOW findings to TECH_DEBT.md

### Capture Formats
```yaml
# solutions/*.yaml (grep-friendly)
problem: "Brief problem description"
symptoms: ["Observable symptom 1", "Symptom 2"]
rootCause: "Why this happened"
solution: "What fixed it"
preventionSteps: ["How to prevent recurrence"]

# decisions/*.md (ADR format)
# Use template at .ai/decisions/000-template.md

# TECH_DEBT.md entries
### [TD-NNN] [Component]: [Brief Description]
**Severity**: MEDIUM | LOW
**Location**: `file or glob`
**Description**: [Details]
**Why Deferred**: [Reason]
```

### Implementation Checklist
- [ ] Identify capture opportunity in command workflow
- [ ] Choose correct format (YAML for solutions, ADR for decisions)
- [ ] Capture without interrupting user workflow
- [ ] Use grep-friendly structure (YAML keys, ADR headings)
- [ ] Reference captured knowledge in memory files

**Reference**: `.claude/commands/execute.md` (solution capture), `.claude/commands/code-review.md` (tech debt capture)

---

## Built-in Pattern: Three-Tier Execution

Route tasks to appropriate model tier based on complexity.

### When to Use
- Tier 1 (Codex Max gpt-5.1-codex-max): Complex tasks (4-5), deep reasoning
- Tier 2 (Sonnet): Moderate tasks (3), balanced cost/capability
- Tier 3 (Codex gpt-5.2-codex): Simple tasks (1-2), saves Claude tokens

### Execution Strategy
```
Task arrives
    ↓
Complexity assessment
    ↓
┌─────────────────────┬──────────────────┬───────────────────────┐
│ COMPLEX (4-5)       │ STANDARD (3)     │ SIMPLE (1-2)          │
│ Codex Max           │ Sonnet 4.5       │ Codex (gpt-5.2-codex) │
│ (gpt-5.1-codex-max) │                  │                       │
├─────────────────────┼──────────────────┼───────────────────────┤
│ - Architecture      │ - Implementation │ - Validation          │
│ - Complex refactor  │ - Bug fixes      │ - Simple edits        │
│ - System-wide tasks │ - Code review    │ - Config changes      │
└─────────────────────┴──────────────────┴───────────────────────┘
```

### Implementation Checklist
- [ ] Assess task complexity (lines of code, decision points, context needed)
- [ ] Route to appropriate tier
- [ ] Use Codex for simple tasks (1-2) via Bash
- [ ] Use Sonnet for moderate tasks (3) via Task tool
- [ ] Use Codex Max for complex tasks (4-5) via Bash with `-m gpt-5.1-codex-max`

**Reference**: `.claude/commands/execute.md` (model selection), `.claude/commands/code-review.md` (uses Codex)

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
