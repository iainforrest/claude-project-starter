---
description: Generate pattern-specific task list from PRD
---

# Task Generation Command

Generate implementation-ready task lists from PRD documents.

## Usage

```
/TaskGen [prd-name]
```

**Example:**
```
/TaskGen prd-email-notifications
```

## Process

This command immediately delegates to the **task-writer agent** for autonomous task generation.

**Input:** PRD file name (without path or `.md` extension)

**The task-writer agent will:**
1. Read the PRD from `/tasks/[feature-name]/prd.md`
2. Detect memory structure:
   - Check if `.ai/MONOREPO.json` exists
   - If mono-repo: Identify target app from PRD or ask user
   - Load appropriate memory (root + app-specific for mono-repo)
3. Load memory system files for architectural context:
   - `.ai/ARCHITECTURE.json` - Patterns, integration points
   - `.ai/FILES.json` - File locations, dependencies
   - `.ai/PATTERNS.md` - Pattern index (+ relevant `patterns/[DOMAIN].md`)
   - `.ai/BUSINESS.json` - Performance targets
   - `.ai/QUICK.md` - Development commands
   - For mono-repo: Also load `.ai/[app]/*` files
4. Map PRD components to patterns and files
5. Generate implementation-ready tasks with:
   - Specific file:line references
   - Pattern templates from PATTERNS.md
   - Complexity ratings calibrated to codebase
   - Testing strategies
6. Save to `/tasks/[feature-name]/task.xml`
7. Return confirmation with summary

## Agent Invocation

Use the Task tool with `subagent_type=task-writer`:

```
PRD_FILE: $ARGUMENTS

Read the PRD from /tasks/[feature-name]/prd.md (extract feature-name from PRD_FILE argument, e.g., 'prd-email-notifications' becomes 'email-notifications') and generate implementation-ready tasks using the memory system for architectural context. Save output to /tasks/[feature-name]/task.xml.
```

## Complexity Calibration

The agent uses this calibration system:

| Rating | Description | Time |
|--------|-------------|------|
| **1/5** | Simple data class or basic component | 5-15 min |
| **2/5** | Business logic method or repository function | 15-45 min |
| **3/5** | Service integration or complex logic | 45-90 min |
| **4/5** | Multi-component integration, new patterns | 1.5-3 hours |
| **5/5** | System-wide changes or novel algorithms | 3+ hours |

## Next Steps

After tasks are generated:
- Review the task breakdown
- Run `/execute` to implement all tasks
- Use `/commit` when complete

## Why an Agent?

Task generation benefits from running in an isolated context window because:
- Heavy document generation (~600+ lines of templates)
- Requires reading multiple memory files
- Pattern matching across entire codebase
- No interactive questioning needed - pure generation

The task-writer agent has full access to tools (Read, Glob, Grep, Write) and generates tasks autonomously based on the PRD and memory system.

## Code Review & Memory Update Requirements

**IMPORTANT:** Every generated task list includes TWO mandatory final tasks:

### Step 5: Code Review (Before Memory Update)
- Run code review agent on all changes
- Fix any CRITICAL or HIGH severity findings
- Re-run code review if significant fixes were made

### Step 6: Memory Update (Final Task)
- Update FILES.json with new files
- Update PATTERNS.md with new patterns discovered
- Update BUSINESS.json with feature status
- Update TODO.md with sprint completion

This ensures code quality is verified before updating the memory system.
