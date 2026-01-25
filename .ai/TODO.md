# Project TODO

*Current and completed tasks*

## Current Sprint: None

No active sprint. Ready for new work.

---

## Upcoming Sprint

**Planned Features:**
- [ ] Bootstrap memory system for specific project
- [ ] Customize commands for project-specific patterns

---

## Backlog

- [ ] Add project-specific agent (e.g., database-expert.md)
- [ ] Customize BUSINESS.json for project features
- [ ] Add project-specific patterns to PATTERNS.md

---

## Completed Sprints

### Sprint 2 - Memory System Overhaul (Completed: 2026-01-25)
Implemented authority-based memory system with automated capture and Codex validation.

**Created:**
- [x] `.ai/OPS.md` - Operations, debugging, deploy runbooks (230 lines)
- [x] `.ai/CONSTRAINTS.md` - Platform limitations, non-goals (209 lines)
- [x] `.ai/DEPRECATIONS.md` - Deprecated APIs, patterns (222 lines)
- [x] `.ai/TECH_DEBT.md` - Unfixed code review findings (235 lines)
- [x] `.ai/decisions/` - ADR directory with template and first decision
- [x] `.ai/solutions/` - YAML solution capture directory with template
- [x] `.codex/prompts/code-review.md` - Codex validation prompt

**Enhanced:**
- [x] `.ai/QUICK.md` - Transformed to router with authority map (119 lines, down from 200+)
- [x] `.ai/README.md` - Updated with new file structure and authority matrix
- [x] `.claude/commands/update.md` - Authority-based routing with Codex validation
- [x] `.claude/commands/code-review.md` - Enhanced with Codex integration
- [x] `.claude/commands/prd.md` - Added decision capture
- [x] `.claude/commands/bugs.md` - Added solution capture
- [x] `.claude/commands/execute.md` - Added solution/decision/deprecation capture
- [x] `.claude/agents/update-memory-agent.md` - Rewritten for authority routing
- [x] `.claude/agents/code-review-agent.md` - Tech debt capture for MEDIUM/LOW findings

**Removed:**
- [x] `.claude/WORKFLOW.md` - Replaced by authority map in QUICK.md and README.md

**Architecture Decision:**
- [x] ADR 001: Use Authority-Based Memory System (accepted 2026-01-25)

**Key Improvements:**
- Single source of truth for all content types
- Grep-first retrieval strategy (check solutions/ before full memory load)
- Automated capture in all commands (no manual documentation)
- Codex validation prevents authority violations
- Token efficiency through elimination of duplication
- Three-tier execution model (Opus → Sonnet → Codex)

---

### Sprint 1 - Sync Command & Agent System (Completed: 2025-12-07)
Synchronized enhanced command and agent system from coach-ops battle-tested implementation.

**Created:**
- [x] `.claude/agents/prd-writer.md` - PRD generation agent with 17-section template
- [x] `.claude/agents/task-writer.md` - Task generation agent with complexity calibration
- [x] `.claude/commands/bugs.md` - 6-phase bug investigation command
- [x] `.claude/WORKFLOW.md` - Comprehensive workflow guide with decision trees

**Enhanced:**
- [x] `.claude/commands/prd.md` - Added decision frameworks, red flags, 3-phase questioning, agent handoff
- [x] `.claude/commands/TaskGen.md` - Renamed from tasks.md (avoids conflict with Claude's built-in /tasks), delegates to task-writer agent
- [x] `.claude/commands/execute.md` - Verified code documentation standards (8 example categories)

**Removed:**
- [x] `.claude/SLASH_COMMAND_MIGRATION.md` - Replaced by WORKFLOW.md

**Key Improvements:**
- Decision frameworks with explicit stopping criteria
- Red flag detection (14 indicators across 4 categories)
- Agent-based architecture for PRD and task generation
- 6-phase bug investigation methodology
- Command-agent hybrid pattern for context management

---

### Sprint 0 - Initial Setup (Completed: 2025-10-15)
- [x] Development system bootstrap
- [x] Initial project structure
- [x] Memory system initialization

---

## Notes

- Update this file at start and end of each sprint
- Move completed sprints to bottom section
- Keep backlog prioritized
- Use this for sprint planning and tracking
