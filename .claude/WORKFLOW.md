# Claude Code Workflow Guide

Quick reference for the custom command workflow in this project.

## Command Overview

| Command | Purpose | Output | Next Step |
|---------|---------|--------|-----------|
| `/prd` | Plan new features | PRD document | → `/tasks` |
| `/bugs` | Explore & fix bugs | Tasks OR PRD | → `/execute` OR `/tasks` |
| `/tasks` | Generate task list | Task document | → `/execute` |
| `/execute` | Implement tasks | Code changes | → `/commit` |
| `/commit` | Commit & push | Git commits | Done |
| `/update` | Update memory system | Updated .ai/ files | → `/commit` |

---

## Architecture: Commands vs Agents

This project uses a **hybrid command/agent architecture**:

### Commands (Interactive)
Commands run in the main conversation context and can ask questions:
- `/prd` - Interactive requirements gathering with batched Q&A
- `/bugs` - Investigation with optional clarification questions
- `/execute` - Implementation with progress updates
- `/commit` - Commit grouping with approval

### Agents (Autonomous)
Agents run in isolated context windows for heavy generation work:
- **prd-writer** - Generates PRD documents (invoked by `/prd` after Q&A)
- **task-writer** - Generates task lists (invoked by `/tasks`)
- **update-memory-agent** - Updates .ai/ files (invoked by `/update`)

**Why this split?**
- Commands handle user interaction (questions, confirmations)
- Agents handle heavy document generation (isolated context, full tools access)
- Better context management - heavy work doesn't consume main conversation context

---

## Workflow Patterns

### Pattern 1: New Feature Development

```
User describes feature idea
    ↓
/prd → Interactive requirements gathering
    ↓
[User confirms requirements summary]
    ↓
prd-writer agent → PRD saved to /tasks/prd-[name].md
    ↓
/tasks prd-[name] → task-writer agent → Tasks saved
    ↓
/execute → Implementation → Code complete
    ↓
/commit → Git commit & push → Feature shipped
```

**When to use:** Building something new that doesn't exist yet

**Example:**
```
You: "I want to add email notifications when a report is finalized"
/prd
[Answers questions about requirements]
[Confirms summary]
→ PRD saved to /tasks/prd-email-notifications.md

/tasks prd-email-notifications
→ Tasks saved to /tasks/tasks-email-notifications.md

/execute
→ Implements all tasks

/commit
→ Commits and pushes changes
```

---

### Pattern 2: Simple Bug Fix

```
User reports bug
    ↓
/bugs → Investigation → Root cause found → Fix options
    ↓
User picks option (simple)
    ↓
Tasks generated directly → /execute → /commit
```

**When to use:** Bug in existing code, straightforward fix (complexity ≤6)

**Example:**
```
You: "Date picker doesn't refresh the data"
/bugs "Date picker doesn't refresh the data"
→ Investigates, finds root cause, proposes options
→ Creates tasks-date-refresh-fix.md directly

/execute
→ Implements fix

/commit
→ Ships fix
```

---

### Pattern 3: Complex Bug Fix (Requires Refactoring)

```
User reports bug
    ↓
/bugs → Investigation → Root cause needs architectural changes
    ↓
Bug PRD generated (complexity ≥7)
    ↓
/tasks [bug-prd-name] → /execute → /commit
```

**When to use:** Bug requires significant refactoring or architectural changes

**Example:**
```
You: "The algorithm assigns items incorrectly"
/bugs "The algorithm assigns items incorrectly"
→ Investigates, finds core logic is fundamentally broken
→ Creates PRD for algorithm refactor (complex fix)
→ Saves to /tasks/prd-fix-algorithm.md

/tasks prd-fix-algorithm
→ Creates detailed task breakdown

/execute
→ Implements refactor

/commit
→ Ships fix
```

---

### Pattern 4: Small Improvement/Tweak

```
User requests small change
    ↓
Just describe it directly → Claude implements
    ↓
/commit
```

**When to use:** Tiny changes that don't need planning (typo fix, style tweak, config change)

**Example:**
```
You: "Change the header font size to 18px"
→ Claude makes the change

/commit
→ Done
```

---

## Decision Tree: Which Command?

```
Is this a new feature or bug fix?
├─ NEW FEATURE
│  └─ /prd → /tasks → /execute → /commit
│
├─ BUG or EXISTING CODE FIX
│  └─ /bugs
│     ├─ Simple fix (≤6 complexity)
│     │  └─ Creates tasks → /execute → /commit
│     │
│     └─ Complex fix (≥7 complexity)
│        └─ Creates PRD → /tasks → /execute → /commit
│
└─ TINY CHANGE (1-2 lines)
   └─ Just ask → /commit
```

---

## Command Details

### `/prd` - Product Requirements Document

**Purpose:** Plan new features with comprehensive requirements gathering

**Process:**
1. Asks clarifying questions (batched, 3 max per round)
2. Reviews memory system (.ai/ files) for context
3. Identifies integration points and patterns
4. Confirms summary with user
5. **Hands off to prd-writer agent** for document generation
6. Agent saves to `/tasks/prd-[feature-name].md`

**When to use:**
- Building something new
- Adding significant functionality
- Need stakeholder alignment
- Want comprehensive documentation

**Output:** Enterprise-grade PRD ready for task generation

---

### `/bugs` - Bug Exploration & Fix Planning

**Purpose:** Investigate bugs, find root cause, propose fix options

**Process:**
1. Asks 1-3 clarifying questions (only if needed)
2. Reviews memory system for architectural context
3. Autonomously explores codebase
4. Identifies root cause with specific file:line
5. Presents 2-4 fix options with trade-offs
6. Makes recommendation
7. Generates tasks (simple) OR PRD (complex)

**When to use:**
- Something's broken
- Unexpected behavior
- Performance issues
- Data inconsistencies
- Need root cause analysis

**Output:**
- Tasks file (complexity ≤6) → ready for /execute
- Bug PRD (complexity ≥7) → needs /tasks first

**Complexity threshold:**
- ≤6: Single file/component, clear fix, <6 hours
- ≥7: Multiple components, refactoring, ≥6 hours, architectural changes

---

### `/tasks` - Task Generation from PRD

**Purpose:** Break down PRD into implementation-ready tasks

**Input:** PRD file name (without path/extension)

**Process:**
1. **Immediately invokes task-writer agent**
2. Agent reads PRD and memory system
3. Maps components to patterns from PATTERNS.md
4. Identifies target files from FILES.json
5. Generates tasks with specific file:line references
6. Includes pattern templates for copy-paste
7. Saves to `/tasks/tasks-[prd-name].md`

**When to use:**
- After PRD is approved
- After complex bug PRD generated
- Ready to start implementation

**Output:** Implementation-ready task list with specific file targets

> **Note:** This command runs entirely through the task-writer agent - no interactive Q&A.

---

### `/execute` - Task Implementation

**Purpose:** Execute tasks from task list

**Process:**
1. Reads task file and memory system
2. Implements each task following patterns
3. Marks subtasks [x] as completed
4. Runs build verification after each parent task
5. Updates memory system with learnings

**When to use:**
- Task list ready
- Ready to write code

**Output:** Working code implementing all tasks

---

### `/commit` - Intelligent Git Commit

**Purpose:** Group changes into logical commits and push

**Process:**
1. Analyzes all uncommitted changes
2. Groups by related work
3. Proposes commit groupings
4. Creates commits with proper messages
5. Pushes to GitHub

**When to use:**
- Work is complete and tested
- Ready to commit changes

**Output:** Commits pushed to GitHub

---

### `/update` - Memory System Update

**Purpose:** Update .ai/ memory files with recent work

**Process:**
1. **Invokes update-memory-agent**
2. Agent analyzes git diffs
3. Identifies gaps in memory files
4. Updates relevant .ai/ files
5. Validates JSON syntax
6. Invokes /commit

**When to use:**
- After completing a sprint
- After significant feature work
- When memory files are stale

**Output:** Updated .ai/ files committed

---

## Memory System (.ai/ files)

The commands leverage these files for context:

- **ARCHITECTURE.json** - System structure, integration points
- **FILES.json** - File locations, dependencies
- **PATTERNS.md** - Code templates, implementation patterns
- **BUSINESS.json** - Features, performance targets
- **QUICK.md** - Common commands, debugging tips
- **TODO.md** - Sprint tracking
- **SPRINT_UPDATE.md** - Memory update guidelines
- **README.md** - Memory system overview

Commands and agents automatically:
- Read these for context
- Apply patterns from PATTERNS.md
- Target files from FILES.json
- Follow architecture from ARCHITECTURE.json
- Update them when discovering new patterns

---

## Tips & Best Practices

### For `/prd`:
- Provide as much context as possible upfront
- Answer questions thoroughly
- Review the summary carefully before confirming
- The prd-writer agent handles document generation

### For `/bugs`:
- Describe observed behavior clearly
- Include reproduction steps if known
- Mention where/when it happens
- Trust the investigation process
- Pick the fix option that fits your timeline/risk tolerance

### For `/tasks`:
- Just provide the PRD name
- The task-writer agent does everything else
- Review task breakdown before /execute
- Ensure complexity estimates seem reasonable

### For `/execute`:
- Let it run through all tasks
- Watch for build failures
- Review changes before /commit

### For `/commit`:
- Review proposed commit groupings
- Approve before it commits
- Check that commits are logical units

---

## Example Full Workflow

```bash
# Scenario: Want to add SMS notifications for users

# Step 1: Plan the feature
/prd
> "I want to send SMS notifications to users when their report is ready"
> [Answer questions about SMS provider, timing, opt-in, etc.]
> [Confirm summary]
→ prd-writer agent generates PRD
→ PRD saved: /tasks/prd-sms-notifications.md

# Step 2: Generate tasks
/tasks prd-sms-notifications
→ task-writer agent generates tasks
→ Tasks saved: /tasks/tasks-sms-notifications.md

# Step 3: Implement
/execute
→ Implements all tasks, runs builds, marks progress

# Step 4: Commit and push
/commit
→ Groups changes into logical commits
→ Pushes to GitHub

# Done! Feature shipped.
```

```bash
# Scenario: Import fails with special characters

# Step 1: Investigate
/bugs "Import fails when data has special characters"
→ Investigates code
→ Finds parsing issue in parser.ts:67
→ Proposes 3 fix options
→ Recommends Option A (escape characters properly)
→ Complexity: 2/10
→ Creates tasks-special-char-fix.md directly

# Step 2: Implement
/execute
→ Implements fix

# Step 3: Commit
/commit
→ Ships fix

# Done! Bug fixed.
```

---

## When NOT to Use Commands

**Don't use commands for:**
- Asking questions about code
- Getting explanations
- Code reviews
- Quick 1-line changes
- Running tests
- Debugging sessions

**Just chat normally for:**
- "How does this algorithm work?"
- "Why did you implement it that way?"
- "Can you review this code?"
- "Change this constant to 50"
- "Run the tests"
- "Why is this test failing?"

---

## Command Cheat Sheet

```bash
# Plan new feature
/prd

# Fix a bug
/bugs "description of bug"

# Generate tasks from PRD
/tasks prd-name

# Implement tasks
/execute

# Commit changes
/commit

# Update memory with sprint completion
/update
```

---

## Available Agents

| Agent | Purpose | Invoked By |
|-------|---------|------------|
| `prd-writer` | Generate PRD documents | `/prd` (after Q&A) |
| `task-writer` | Generate task lists | `/tasks` |
| `update-memory-agent` | Update .ai/ files | `/update` |
| `cto-technical-advisor` | Technical guidance | Manual invocation |
| `security-auditor` | Security reviews | Manual invocation |
| `ui-ux-expert` | UI/UX guidance | Manual invocation |

---

**Pro Tip:** The commands are designed to work together as a flow. Start with `/prd` or `/bugs`, flow through `/tasks` (if needed), then `/execute`, then `/commit`. Each command sets up the next one perfectly. The agent-based architecture keeps heavy generation work in isolated contexts while commands handle user interaction.
