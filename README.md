# Claude Project Starter v2.0

A self-bootstrapping development system that sets up a complete AI-assisted workflow for any project.

## What This Is

- **Generic Commands & Agents**: Reusable workflow tools that work across any project
- **AI Memory System**: Persistent project knowledge in `.ai/` that prevents context loss
- **Sync System**: Keep your projects up-to-date with `/pull-cps` and `/push-cps`

## Key Architecture (v2.0)

```
.claude/                    # Generic (syncs across projects)
├── commands/               # Workflow commands (/prd, /tasks, /execute, etc.)
├── agents/                 # Specialized AI agents (CTO, Security, UI/UX, etc.)
└── WORKFLOW.md             # Command/agent documentation

.ai/                        # Project-specific (never syncs)
├── ARCHITECTURE.json       # Your project's patterns and data flows
├── BUSINESS.json           # Your features and requirements
├── FILES.json              # Your file index with cross-references
├── PATTERNS.md             # Your implementation patterns
├── QUICK.md                # Your build commands and shortcuts
└── ...                     # Other memory files
```

**The key insight**: Commands and agents are fully generic - they read from `.ai/` for all project-specific context. This means:
- Commands work identically across all projects
- Updates can be synced without customization
- Project knowledge lives in one place (`.ai/`)

## Quick Start

### For New Projects

1. **Clone this repo** into your project:
   ```bash
   git clone https://github.com/iainforrest/claude-project-starter.git
   cp -r claude-project-starter/.claude your-project/
   cp -r claude-project-starter/.ai your-project/
   ```

2. **Run bootstrap** with Claude Code:
   - Open your project in Claude Code
   - Run: `@BOOTSTRAP.md` or paste its contents
   - Answer 6-8 rounds of questions
   - Claude customizes your `.ai/` memory files

3. **Start building**:
   ```
   /prd → /tasks → /execute → /commit → /update
   ```

### For Existing Projects (Upgrade to v2.0)

See the upgrade guide: Copy `upgrade-to-cps-v2.md` into your project and run it.

## Development Workflow

### The Command Flow

```
/prd [feature idea]     → Generate Product Requirements Document
/tasks [prd-file]       → Break PRD into implementation tasks
/execute [tasks-file]   → Systematically execute tasks
/commit                 → Intelligent grouped git commits
/update                 → Update .ai/ memory from git diffs
```

### Sync Commands (New in v2.0)

```
/pull-cps               → Pull latest commands/agents from this repo
/push-cps               → Push improvements back as PR
```

## Commands Reference

| Command | Purpose | Output |
|---------|---------|--------|
| `/prd` | Generate requirements from feature idea | `/tasks/prd-[name].md` |
| `/tasks` | Convert PRD to implementation tasks | `/tasks/tasks-[name].md` |
| `/execute` | Execute tasks with build verification | Implemented code |
| `/commit` | Group and commit changes intelligently | Git commits |
| `/update` | Update memory system from git diffs | Updated `.ai/` files |
| `/pull-cps` | Sync latest from starter repo | Updated commands/agents |
| `/push-cps` | Contribute improvements back | GitHub PR |

## Specialized Agents

Agents provide domain expertise and are invoked automatically or on request:

| Agent | Expertise |
|-------|-----------|
| `cto-technical-advisor` | Architecture decisions, feasibility assessment |
| `security-auditor` | Security reviews, vulnerability detection |
| `ui-ux-expert` | Interface design, accessibility, user flows |
| `prd-writer` | Requirements documentation |
| `task-writer` | Task breakdown with complexity ratings |
| `update-memory-agent` | Git diff analysis, memory updates |

## Memory System (`.ai/`)

The memory system is your project's brain. It's created during bootstrap and grows with your project.

| File | Purpose |
|------|---------|
| `ARCHITECTURE.json` | Patterns, data flows, integration points |
| `BUSINESS.json` | Features, requirements, performance targets |
| `FILES.json` | File index with dependencies and cross-refs |
| `PATTERNS.md` | Implementation templates and examples |
| `QUICK.md` | Build commands, debugging tips, shortcuts |
| `TODO.md` | Current and completed tasks |
| `SPRINT_UPDATE.md` | Process for updating memory |
| `README.md` | Guide to the memory system |

**Key rule**: Commands reference `.ai/` for context. Keep it updated.

## Keeping in Sync

### Pull Updates

When new commands or agents are added to this repo:

```
/pull-cps
```

This compares your `.claude/` with the latest, shows diffs, and lets you selectively update.

### Push Improvements

When you improve a command or agent:

```
/push-cps
```

This validates your changes are generic (no project-specific content), then creates a PR.

### What Syncs vs What Doesn't

| Syncs | Never Syncs |
|-------|-------------|
| `.claude/commands/*.md` | `.ai/*` (project-specific) |
| `.claude/agents/*.md` | `.claude/settings.local.json` |
| `.claude/WORKFLOW.md` | Project-specific commands |

## What's New in v2.0

- **Sync System**: `/pull-cps` and `/push-cps` commands for keeping projects updated
- **Cleaner Architecture**: Commands/agents are now fully generic
- **Memory-First Design**: All project context lives in `.ai/`
- **Simplified Bootstrap**: Focuses on populating `.ai/` files
- **Better Agents**: Enhanced prd-writer and task-writer with structured output

## Project Structure After Bootstrap

```
your-project/
├── .claude/
│   ├── commands/           # Workflow commands
│   │   ├── prd.md
│   │   ├── tasks.md
│   │   ├── execute.md
│   │   ├── commit.md
│   │   ├── update.md
│   │   ├── pull-cps.md
│   │   └── push-cps.md
│   ├── agents/             # Specialized agents
│   │   ├── prd-writer.md
│   │   ├── task-writer.md
│   │   ├── update-memory-agent.md
│   │   ├── cto-technical-advisor.md
│   │   ├── security-auditor.md
│   │   └── ui-ux-expert.md
│   └── WORKFLOW.md
├── .ai/
│   ├── ARCHITECTURE.json   # Your patterns
│   ├── BUSINESS.json       # Your features
│   ├── FILES.json          # Your files
│   ├── PATTERNS.md         # Your templates
│   ├── QUICK.md            # Your commands
│   └── ...
├── tasks/                  # Generated PRDs and task lists
└── CLAUDE.md               # Project overview (create with `claude init`)
```

## Philosophy

**AI works best with persistent, structured knowledge.**

The memory system prevents Claude from "forgetting" your project between sessions. The generic commands ensure consistent workflows. Together, they enable rapid, high-quality development.

### Key Benefits

- **Zero Context Loss**: Memory system preserves project knowledge
- **Consistent Quality**: Commands enforce best practices
- **Rapid Development**: Templates and patterns enable fast implementation
- **Stay Current**: Sync commands keep all projects updated
- **Contribute Back**: Improvements benefit everyone

## Credits

Originally inspired by **Ryan Carson** and his approach to AI-assisted development, discovered through **How to AI with Claire Vo**.

- [Ryan Carson's AI Dev Tasks](https://github.com/snarktank/ai-dev-tasks)
- [How to AI with Claire Vo - YouTube](https://youtu.be/fD4ktSkNCw4)

---

**Ready to start?** Run `BOOTSTRAP.md` with Claude Code to customize for your project.
