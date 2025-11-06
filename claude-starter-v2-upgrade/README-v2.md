# Development System Starter Kit

## What This Is

A self-bootstrapping development system that sets up a complete AI-assisted development workflow for any project. This system provides:

- **Rule-Based Workflow**: Structured PRD → Tasks → Execution process
- **AI Memory System**: Persistent project knowledge that prevents context loss
- **Consistent Patterns**: Architectural patterns and templates for rapid development
- **Zero Configuration**: Completely customized to your project during bootstrap

## How to Use

### Quick Start

1. **Copy this folder** to your new project root:
   ```bash
   cp -r new_projects/* /path/to/your/new/project/
   ```

2. **Run the bootstrap** with Claude Code:
   - Open `BOOTSTRAP.md` in Claude Code
   - Answer 6-8 rounds of questions (1-3 questions at a time)
   - Claude will validate your answers and provide tech recommendations
   - Review the generated task plan (`bootstrap_tasks.md`)
   - Claude executes the plan and customizes everything

3. **Initialize Claude Code**:
   ```bash
   claude init
   ```
   This creates your `CLAUDE.md` file which Claude will populate over time.

4. **Start building**:
   - Your development system is ready!
   - Memory system is set up in `.ai/`
   - Rule files are customized in `.claude/`

## What Gets Created

### During Bootstrap

- **`.claude/` folder** - Slash commands and specialized agents:
  - **`commands/`** - Workflow commands (use `/command-name`):
    - `prd.md` - `/prd` - Generate Product Requirement Documents
    - `tasks.md` - `/tasks` - Break PRDs into implementation tasks
    - `execute.md` - `/execute` - Systematically execute task lists
    - `commit.md` - `/commit` - Intelligent git commits
    - `update.md` - `/update` - Update AI memory system
  - **`agents/`** - Specialized AI agents (invoked via Task tool):
    - `update-memory-agent.md` - Analyzes git diffs and updates memory
    - `cto-technical-advisor.md` - Strategic technical guidance
    - `security-auditor.md` - Comprehensive security audits
    - `ui-ux-expert.md` - UI/UX design expertise

- **`.ai/` folder** - Memory system for project knowledge:
  - `ARCHITECTURE.json` - Architecture patterns and data flows
  - `BUSINESS.json` - Business logic and feature specifications
  - `FILES.json` - File index with cross-references
  - `PATTERNS.md` - Implementation patterns and templates
  - `QUICK.md` - Quick reference commands and shortcuts
  - `SPRINT_UPDATE.md` - Process for updating memory
  - `TODO.md` - Current and completed tasks
  - `README.md` - Guide on using the memory system

- **`bootstrap_tasks.md`** - The task list used during setup (can delete after bootstrap)

### After `claude init`

- **`CLAUDE.md`** - Project-specific guidance for Claude Code

## What Typically Goes in CLAUDE.md

After running `claude init`, you'll want to add:

### Essential Sections

**Project Overview**
- Brief description of what the project does
- Tech stack summary
- Architecture approach

**AI Memory System**
- Link to `.ai/` folder
- Instruction to consult memory before any work
- Typical workflow (check QUICK.md → review PATTERNS.md → etc.)

**Build Commands**
- How to build the project
- How to run tests
- How to deploy/package

**Development Workflow**
- How to create new features (PRD → Tasks → Execution)
- Links to `.claude/` rule files
- Sprint process

**Architecture Guidelines**
- Key patterns used in the project
- Critical constraints
- Integration points

**Testing Strategy**
- Testing approach
- Test commands
- Coverage requirements

### Example Structure

```markdown
# CLAUDE.md

## Project Overview
[Your project description and tech stack]

## AI Memory System
**CRITICAL**: Before starting any task, consult `.ai/` memory:
- **QUICK.md** - File references and commands
- **ARCHITECTURE.json** - Architecture patterns
- **PATTERNS.md** - Implementation templates
- **BUSINESS.json** - Business logic

## Build Commands
[Your build commands]

## Development Workflow
1. Create PRD (`/prd` command)
2. Generate Tasks (`/tasks` command)
3. Execute (`/execute` command)
4. Commit changes (`/commit` command)
5. Update memory (`/update` command)

## Architecture
[Your architecture patterns]

## Testing
[Your testing approach]
```

Claude Code will help you expand and refine this over time as your project grows.

## After Bootstrap

### Recommended Next Steps

1. **Review the memory system**:
   - Read `.ai/README.md` to understand the memory structure
   - Start populating `.ai/` files as you learn about your project

2. **Create your first feature**:
   - See "Using the Development Workflow" section below
   - Follow the PRD → Tasks → Execution process

3. **Update memory regularly**:
   - After each sprint, update `.ai/` files
   - Follow guidance in `.ai/SPRINT_UPDATE.md`

4. **Delete bootstrap artifacts** (optional):
   - `bootstrap_tasks.md` (if you want to clean up)
   - Keep `BOOTSTRAP.md` for reference or delete if you prefer

### Git Setup

If you chose to set up git during bootstrap:
- `.gitignore` is configured based on your preferences
- Memory system (`.ai/`) is either tracked or ignored based on your choice
- Ready to commit

## Using the Development Workflow

Once bootstrap is complete, use this **slash command workflow** to build features:

### Step 1: Create a PRD

Use the `/prd` command with your feature idea:

```
/prd Add user authentication with email/password login
```

Claude will ask clarifying questions and generate a complete PRD file saved to `/tasks/prd-user-authentication.md`.

### Step 2: Generate Tasks

Use the `/tasks` command and reference the PRD:

```
/tasks @tasks/prd-user-authentication.md
```

Claude will create a detailed task list saved to `/tasks/tasks-user-authentication.md` with complexity ratings, file references, and pattern templates.

### Step 3: Execute Tasks

Use the `/execute` command with the tasks file:

```
/execute @tasks/tasks-user-authentication.md
```

Claude will systematically execute each task, mark progress in real-time, run builds, and verify completion.

### Step 4: Commit Changes

Use the `/commit` command when work is complete:

```
/commit
```

Claude will analyze changes, create logical grouped commits, and push to GitHub.

### Step 5: Update Memory System

Use the `/update` command to keep memory current:

```
/update
```

Claude will analyze git diffs and update the `.ai/` memory system with new patterns and changes.

### The Complete Flow

```
/prd → /tasks → /execute → /commit → /update
```

Each command leverages the memory system (`.ai/` files) for context, patterns, and file references - ensuring consistent, high-quality implementation.

### Specialized Agents

Beyond workflow commands, the system includes specialized agents for expert guidance:

- **CTO Technical Advisor**: Strategic technical decisions and feasibility assessments
- **Security Auditor**: Comprehensive security reviews before production releases
- **UI/UX Expert**: Design guidance for user interfaces and experience flows
- **Update Memory Agent**: Automatically analyzes git diffs to keep memory current

Agents are invoked automatically by Claude when their expertise is needed, or you can request them explicitly.

## Customization

All files are customized to your project during bootstrap based on:
- Project type (web app, mobile app, API, CLI, library, etc.)
- Technology stack (languages, frameworks, build tools)
- Architecture patterns (MVVM, Clean Architecture, etc.)
- Scale and complexity
- Development workflow preferences
- Special requirements (performance, security, etc.)

## Features

### Smart Question Flow

- **Grouped Questions**: 1-3 related questions at a time (never overwhelming)
- **Tech Validation**: Real-time feedback on compatibility
- **Recommendations**: Claude suggests tech choices if you're unsure
- **Rabbit Hole Prevention**: Internal checklist keeps bootstrap on track
- **Flexible Responses**: Works whether you know exactly what you want or need guidance

### Self-Referential System

- Bootstrap creates a task plan using TASK_GENERATION.md principles
- Execution follows TASK_EXECUTION.md rules
- The system uses its own methodology to set itself up
- Ensures consistency from day one

### Generic & Adaptable

- No preset templates or assumptions
- Works for any project type
- Fully customized to your specific needs
- Can be as simple or complex as your project requires

## System Philosophy

This development system is built on the principle that **AI works best with persistent, structured knowledge**. The memory system (`.ai/`) prevents Claude from "forgetting" your project context between sessions, while the rule files (`.claude/`) ensure consistent, high-quality development workflows.

### Key Benefits

- **Zero Context Loss**: Memory system preserves project knowledge
- **Consistent Quality**: Rule-based workflows prevent shortcuts
- **Rapid Development**: Templates and patterns enable fast implementation
- **Scalable**: Works for solo projects or large teams
- **Self-Improving**: Memory system grows with your project

## Support

This is a self-contained system. Everything you need is in:
- This README (getting started)
- `.ai/README.md` (memory system guide)
- `.claude/commands/*.md` (slash command documentation)
- `.claude/agents/*.md` (specialized agent expertise)
- `.claude/SLASH_COMMAND_MIGRATION.md` (migration guide from v1.0)

The system is designed to be self-documenting and self-explanatory.

### What's New in v2.0

- ✨ **Slash Commands**: Modern `/command` syntax replaces old `@.claude/FILE.md` approach
- 🤖 **Specialized Agents**: Expert AI agents for security, technical decisions, and UI/UX
- 📦 **Better Organization**: Separated commands and agents into dedicated directories
- 🚀 **Enhanced Workflow**: New `/commit` and `/update` commands automate common tasks
- 📖 **Improved Documentation**: Clearer structure and migration guide

## Version

This is a generic, project-agnostic version of a proven development system. It will be customized to your specific project during bootstrap.

## Credits & Inspiration

This project was originally inspired by the work of **Ryan Carson** and his approach to AI-assisted development workflows. I discovered Ryan's work through **How to AI with Claire Vo**.

### Related Resources

- [Ryan Carson's AI Dev Tasks Repository](https://github.com/snarktank/ai-dev-tasks)
- [How to AI with Claire Vo - YouTube](https://youtu.be/fD4ktSkNCw4?si=lhr5Rj3-JGIxVpWa)

---

**Ready to start?** Open `BOOTSTRAP.md` with Claude Code and begin the setup process!
