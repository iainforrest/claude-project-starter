# Task List: Sync Command & Agent System from Coach-Ops

**Generated from**: `prd-sync-command-agent-system.md`
**Date**: 2025-12-07
**Architecture Pattern**: Command-Agent Hybrid (Interactive Commands + Autonomous Agents)
**Target Files**: `.claude/commands/*.md`, `.claude/agents/*.md`, `.claude/WORKFLOW.md`
**Risk Level**: Low (template/configuration files only)
**Build Command**: N/A (Markdown configuration files)

---

## Overview

Synchronize the enhanced command and agent system developed in coach-ops to claude-project-starter. This upgrade brings battle-tested workflows including decision frameworks, red flag detection, 3-phase questioning, and agent-based document generation.

**Implementation Strategy**: Copy proven patterns from coach-ops, generalize project-specific references to placeholders
**Integration Points**: `.claude/commands/`, `.claude/agents/` directories
**File Modification Scope**: 4 new files, 3 modified files, 1 deleted file
**Impact**: Core workflow infrastructure for all projects using this starter

---

## Implementation Order

**Phase 1**: Create missing agents (prd-writer, task-writer) - Foundation for command handoffs
**Phase 2**: Upgrade existing commands (prd, tasks, bugs, execute) - Enhanced workflows
**Phase 3**: Replace documentation (WORKFLOW.md) - User guidance
**Phase 4**: Cleanup - Remove obsolete files

**Dependencies**: Agents must exist before commands can delegate to them

---

## Build & Test Commands

```bash
# Validation (no build required - markdown files)
# Verify file syntax and links manually
# Test by running commands in a fresh conversation

# Testing Strategy:
# 1. Run /prd "test feature" - verify questioning + agent handoff
# 2. Run /tasks test-feature - verify task generation
# 3. Run /bugs "test bug" - verify 6-phase investigation
# 4. Verify memory system references are generic
```

---

## Phase 1: Create Missing Agents (Priority: Critical)

### 1.0 Create prd-writer Agent
**Goal**: Create autonomous PRD generation agent that receives context from /prd command
**Files**: `.claude/agents/prd-writer.md` (NEW)
**Pattern**: Agent definition with frontmatter, input contract, and generation template
**Source Reference**: `/root/projects/realnz/coach-ops/.claude/agents/prd-writer.md`

- [x] 1.1 - complexity 3/5 - Create prd-writer.md agent file
  - **File**: `.claude/agents/prd-writer.md` (CREATE NEW)
  - **Source**: `/root/projects/realnz/coach-ops/.claude/agents/prd-writer.md`
  - **Action**: Copy from coach-ops with generalizations
  - **Generalizations Required**:
    - Replace `Firebase`, `Firestore` → `[PROJECT_DATABASE]`
    - Replace `Pacific/Auckland` → `[PROJECT_TIMEZONE]`
    - Replace `@realnz.com` → `[PROJECT_DOMAIN]`
    - Replace specific file paths → `[path/to/relevant/file.ext]`
    - Replace `/sprints/` → `/tasks/` (starter uses tasks folder)
    - Replace coach-ops specific patterns → generic placeholders
    - Remove service account paths and credentials references
  - **Key Sections to Preserve**:
    - Agent frontmatter (name, description, model, color)
    - Input contract (YAML structure for context handoff)
    - Memory system loading instructions
    - 17-section PRD template structure
    - Writing guidelines and anti-patterns
    - Validation checklist
  - **Verification**: Agent file follows frontmatter format, references generic patterns

- [x] 1.2 - complexity 1/5 - Verify prd-writer agent frontmatter
  - **File**: `.claude/agents/prd-writer.md`
  - **Check**: Frontmatter includes: name, description, model (sonnet), color
  - **Check**: Description explains when to invoke agent
  - **Check**: Examples provided for invocation scenarios

---

### 2.0 Create task-writer Agent
**Goal**: Create autonomous task generation agent that receives PRD reference from /tasks command
**Files**: `.claude/agents/task-writer.md` (NEW)
**Pattern**: Agent definition with memory consultation and task template
**Source Reference**: `/root/projects/realnz/coach-ops/.claude/agents/task-writer.md`

- [x] 2.1 - complexity 3/5 - Create task-writer.md agent file
  - **File**: `.claude/agents/task-writer.md` (CREATE NEW)
  - **Source**: `/root/projects/realnz/coach-ops/.claude/agents/task-writer.md`
  - **Action**: Copy from coach-ops with generalizations
  - **Generalizations Required**:
    - Replace `npm run build/test/dev` → `[BUILD_COMMAND]`, `[TEST_COMMAND]`, `[DEV_COMMAND]`
    - Replace Vite/Firebase specifics → generic build tool references
    - Replace `/sprints/` → `/tasks/`
    - Replace `.ai/allocations/` → `.ai/` (standard memory location)
    - Replace project-specific patterns → generic pattern placeholders
    - Remove coach-ops file path references
  - **Key Sections to Preserve**:
    - Agent frontmatter with description
    - Input contract (PRD filename)
    - Memory system loading sequence
    - Task categories by architecture layer (1.0-7.0)
    - Complexity calibration table (1/5 to 5/5 with time estimates)
    - Quality gates and security checklist
    - Memory update as MANDATORY final task
  - **Verification**: Agent generates tasks referencing memory system patterns

- [x] 2.2 - complexity 1/5 - Verify task-writer agent structure
  - **File**: `.claude/agents/task-writer.md`
  - **Check**: Complexity calibration table present with 5 levels
  - **Check**: Memory update section marked as MANDATORY
  - **Check**: Output saves to `/tasks/tasks-[prd-name].md`

---

## Phase 2: Upgrade Existing Commands (Priority: High)

### 3.0 Upgrade /prd Command with Decision Frameworks
**Goal**: Add decision frameworks, red flags, 3-phase questioning, and agent handoff
**Files**: `.claude/commands/prd.md` (MODIFY)
**Pattern**: Interactive command with batched questioning and agent delegation
**Source Reference**: `/root/projects/realnz/coach-ops/.claude/commands/prd.md`

- [x] 3.1 - complexity 4/5 - Replace prd.md with enhanced version
  - **File**: `.claude/commands/prd.md`
  - **Source**: `/root/projects/realnz/coach-ops/.claude/commands/prd.md`
  - **Action**: Replace entire file, then generalize
  - **Sections to Add**:
    - Role & Authority definition
    - Input Architecture (Three-Layer Structure)
    - Decision Frameworks:
      - Framework 1: Stopping Criteria (8-point checklist scoring to 100%)
      - Framework 2: Complexity Assessment (formula-based scoring)
      - Framework 3: Priority Scoring (for components)
      - Framework 4: Assumptions Validation
    - Red Flag Framework (14 indicators across 4 categories):
      - Scope & Complexity Risks
      - Communication & Clarity Risks
      - Technical & Timeline Risks
      - Organizational Risks
    - Questioning Process (3-phase with max 7 rounds)
    - Agent Handoff Section (prd-writer invocation)
    - Post-Agent Response options
    - Anti-Patterns to avoid
  - **Generalizations Required**:
    - Remove project-specific context section entirely
    - Replace Firebase references → `[PROJECT_DATABASE]`
    - Replace timezone → `[PROJECT_TIMEZONE]`
    - Replace domain restrictions → `[PROJECT_DOMAIN]`
    - Replace `/sprints/` → `/tasks/`
  - **Verification**: Command includes all 4 decision frameworks, 14 red flags, agent handoff

- [x] 3.2 - complexity 1/5 - Verify prd command agent handoff
  - **File**: `.claude/commands/prd.md`
  - **Check**: Agent handoff section references `subagent_type=prd-writer`
  - **Check**: YAML context structure documented for handoff
  - **Check**: Post-agent response offers 4 options to user

---

### 4.0 Restructure /tasks Command with Agent Delegation
**Goal**: Update /tasks to delegate immediately to task-writer agent
**Files**: `.claude/commands/tasks.md` (MODIFY)
**Pattern**: Thin command that delegates to agent
**Source Reference**: `/root/projects/realnz/coach-ops/.claude/commands/TaskGen.md`

- [x] 4.1 - complexity 2/5 - Update tasks.md to delegate to agent
  - **File**: `.claude/commands/tasks.md`
  - **Source**: `/root/projects/realnz/coach-ops/.claude/commands/TaskGen.md`
  - **Action**: Replace content with agent-delegation pattern
  - **New Structure**:
    ```markdown
    # Task Generation Command

    Generate implementation-ready task lists from PRD documents.

    ## Usage
    `/tasks [prd-name]`

    ## Process
    This command immediately delegates to the **task-writer agent**.

    ## Agent Invocation
    Use Task tool with `subagent_type=task-writer`:
    - PRD_FILE: $ARGUMENTS
    - Agent reads PRD from /tasks/[PRD_FILE].md
    - Agent generates and saves tasks

    ## Next Steps
    After tasks generated:
    - Review task breakdown
    - Run /execute to implement
    - Use /commit when complete
    ```
  - **Key Changes**:
    - Remove inline task generation logic (now in agent)
    - Add agent invocation instructions
    - Keep complexity calibration reference (agent handles detail)
    - Reference `/tasks/` folder (not `/sprints/`)
  - **Verification**: Command is under 100 lines, delegates to agent

---

### 5.0 Create /bugs Command (NEW)
**Goal**: Add comprehensive bug investigation and fix planning command
**Files**: `.claude/commands/bugs.md` (CREATE NEW)
**Pattern**: 6-phase investigation with fix options and decision tree
**Source Reference**: `/root/projects/realnz/coach-ops/.claude/commands/bugs.md`

- [x] 5.1 - complexity 4/5 - Create bugs.md command file
  - **File**: `.claude/commands/bugs.md` (CREATE NEW)
  - **Source**: `/root/projects/realnz/coach-ops/.claude/commands/bugs.md`
  - **Action**: Copy from coach-ops with generalizations
  - **Key Sections to Preserve**:
    - Role & Authority (Senior Software Debugging Specialist)
    - 6-Phase Investigation Process:
      - Phase 1: Clarification (targeted questions only)
      - Phase 2: Memory System Consultation
      - Phase 3: Autonomous Code Exploration
      - Phase 4: Root Cause Analysis
      - Phase 5: Solution Options (2-4 with trade-offs)
      - Phase 6: Recommendation & Next Steps
    - Decision Rules:
      - Complexity ≤6 → Create tasks directly
      - Complexity ≥7 → Create bug PRD first
    - Task List Template (for simple fixes)
    - Bug PRD Template (for complex fixes)
    - Quality Assurance checklists
    - Communication Guidelines
    - Example Investigation Flow
  - **Generalizations Required**:
    - Remove "Project Context" section with Firebase specifics
    - Remove "Project-Specific Investigation Areas" section entirely
    - Replace `/sprints/` → `/tasks/`
    - Remove coach-ops file paths and patterns
  - **Verification**: 6 phases documented, decision tree for tasks vs PRD

- [x] 5.2 - complexity 1/5 - Add bugs command frontmatter
  - **File**: `.claude/commands/bugs.md`
  - **Add**: Frontmatter at top of file:
    ```yaml
    ---
    description: Explore bugs, analyze root causes, and propose fix options
    ---
    ```
  - **Verification**: Frontmatter present with description

---

### 6.0 Enhance /execute Command with Code Documentation Standards
**Goal**: Add detailed code documentation standards from coach-ops
**Files**: `.claude/commands/execute.md` (MODIFY)
**Pattern**: Execution rules with comprehensive comment guidelines
**Source Reference**: `/root/projects/realnz/coach-ops/.claude/commands/execute.md`

- [x] 6.1 - complexity 2/5 - Add code documentation standards section
  - **File**: `.claude/commands/execute.md`
  - **Source**: coach-ops execute.md lines ~32-250 (Code Documentation Standards)
  - **Action**: Current execute.md already has good structure; verify and enhance
  - **Sections to Verify Present**:
    - CRITICAL: SUBTASK MARKING IS MANDATORY (with examples)
    - CRITICAL: NO SHORTCUTS ALLOWED (forbidden shortcuts list)
    - Code Documentation Standards section with:
      - Comment quality guidelines (HIGH-QUALITY vs LOW-QUALITY)
      - Where to comment (8 categories with examples)
      - Comment frequency guidelines (1 per 5-15 lines)
  - **If Missing, Add**:
    - 7 detailed examples of where to comment (from coach-ops)
    - File-level, function-level, logic block examples
    - Business logic, integration, error handling, performance comments
  - **Verification**: Code documentation section has 8 example categories

- [x] 6.2 - complexity 1/5 - Verify execute command build requirements
  - **File**: `.claude/commands/execute.md`
  - **Check**: Build verification frequency section present
  - **Check**: Build failure protocol defined (5 DO/DON'T rules)
  - **Check**: Testing verification requirements (Unit/Integration/Manual)
  - **Generalize**: Replace `npm run build/test` → `[BUILD_COMMAND]`, `[TEST_COMMAND]`

---

## Phase 3: Replace Documentation (Priority: Medium)

### 7.0 Create WORKFLOW.md and Remove Obsolete File
**Goal**: Replace SLASH_COMMAND_MIGRATION.md with comprehensive WORKFLOW.md
**Files**: `.claude/WORKFLOW.md` (CREATE NEW), `.claude/SLASH_COMMAND_MIGRATION.md` (DELETE)
**Pattern**: User guide with command flow, decision trees, and examples
**Source Reference**: `/root/projects/realnz/coach-ops/.claude/WORKFLOW.md`

- [x] 7.1 - complexity 3/5 - Create WORKFLOW.md guide
  - **File**: `.claude/WORKFLOW.md` (CREATE NEW)
  - **Source**: `/root/projects/realnz/coach-ops/.claude/WORKFLOW.md`
  - **Action**: Copy from coach-ops with generalizations
  - **Key Sections to Preserve**:
    - Command Overview table (6 commands with purpose/output/next step)
    - Architecture: Commands vs Agents explanation
    - 4 Workflow Patterns:
      - Pattern 1: New Feature Development
      - Pattern 2: Simple Bug Fix
      - Pattern 3: Complex Bug Fix (Requires Refactoring)
      - Pattern 4: Small Improvement/Tweak
    - Decision Tree (ASCII diagram)
    - Command Details (6 detailed sections)
    - Memory System (.ai/ files) overview
    - Tips & Best Practices
    - Example Full Workflow (2 scenarios)
    - When NOT to Use Commands
    - Command Cheat Sheet
    - Available Agents table
  - **Generalizations Required**:
    - Replace `/sprints/` → `/tasks/`
    - Replace `/TaskGen` → `/tasks` (use standard name)
    - Remove coach-ops specific examples
    - Replace Firebase/Firestore references → generic examples
    - Remove firebase-expert agent (project-specific)
  - **Verification**: 4 workflow patterns, decision tree, cheat sheet present

- [x] 7.2 - complexity 1/5 - Delete obsolete SLASH_COMMAND_MIGRATION.md
  - **File**: `.claude/SLASH_COMMAND_MIGRATION.md` (DELETE)
  - **Action**: Remove file (replaced by WORKFLOW.md)
  - **Verification**: File no longer exists in .claude/ directory

---

## Phase 4: Validation & Memory Update (MANDATORY)

### 8.0 Validate Complete System
**Goal**: Verify all files are correctly created/modified and work together
**Files**: All `.claude/commands/*.md`, `.claude/agents/*.md`, `.claude/WORKFLOW.md`

- [x] 8.1 - complexity 2/5 - Validate file structure
  - **Check**: `.claude/agents/` contains:
    - prd-writer.md (NEW)
    - task-writer.md (NEW)
    - cto-technical-advisor.md (EXISTING)
    - security-auditor.md (EXISTING)
    - ui-ux-expert.md (EXISTING)
    - update-memory-agent.md (EXISTING)
  - **Check**: `.claude/commands/` contains:
    - prd.md (ENHANCED)
    - tasks.md (RESTRUCTURED)
    - bugs.md (NEW)
    - execute.md (ENHANCED)
    - commit.md (EXISTING)
    - update.md (EXISTING)
    - feature.md (EXISTING)
  - **Check**: `.claude/WORKFLOW.md` exists (NEW)
  - **Check**: `.claude/SLASH_COMMAND_MIGRATION.md` deleted

- [x] 8.2 - complexity 2/5 - Verify cross-references
  - **Check**: /prd command references prd-writer agent correctly
  - **Check**: /tasks command references task-writer agent correctly
  - **Check**: WORKFLOW.md lists all commands and agents
  - **Check**: All agents reference `/tasks/` folder (not `/sprints/`)
  - **Check**: No coach-ops specific file paths remain

- [x] 8.3 - complexity 1/5 - Verify generalization completeness
  - **Search all new/modified files for**:
    - `coach-ops` → Should not appear
    - `@realnz.com` → Should not appear
    - `Pacific/Auckland` → Should not appear (unless as example with placeholder)
    - `Firebase` → Should not appear (unless as example with placeholder)
    - `/sprints/` → Should be `/tasks/`
    - Specific file paths from coach-ops → Should not appear
  - **All should use placeholders like**:
    - `[PROJECT_DATABASE]`
    - `[PROJECT_TIMEZONE]`
    - `[PROJECT_DOMAIN]`
    - `[BUILD_COMMAND]`
    - `[TEST_COMMAND]`

---

### 9.0 Memory System Update (MANDATORY FINAL TASK)
**CRITICAL RULE**: Do NOT create separate sprint completion files
**UPDATE RULE**: Integrate ALL sprint info into existing core files only

- [x] 9.1 - complexity 1/5 - Verify no sprint completion files created
  - **Check**: .ai/ directory should contain ONLY these 8 files:
    - ARCHITECTURE.json, BUSINESS.json, FILES.json
    - PATTERNS.md, QUICK.md, README.md
    - SPRINT_UPDATE.md, TODO.md
  - **Action**: Delete any additional files (like SPRINT_X_COMPLETION.md)
  - **Goal**: Keep memory system at ~3000 lines across 8 core files

- [x] 9.2 - complexity 2/5 - Update FILES.json
  - **File**: .ai/FILES.json
  - **Update meta.lastUpdated**: Set to current date
  - **Add new files**:
    - `.claude/agents/prd-writer.md` - PRD generation agent
    - `.claude/agents/task-writer.md` - Task generation agent
    - `.claude/commands/bugs.md` - Bug investigation command
    - `.claude/WORKFLOW.md` - Command workflow guide
  - **Mark removed**:
    - `.claude/SLASH_COMMAND_MIGRATION.md` - Replaced by WORKFLOW.md

- [x] 9.3 - complexity 2/5 - Update PATTERNS.md (if new patterns)
  - **File**: .ai/PATTERNS.md
  - **Add pattern if not exists**: Agent delegation pattern
    - Command frontmatter structure
    - Agent handoff with Task tool
    - Context passing via YAML structure
  - **Pattern template**: Include working examples from prd.md

- [x] 9.4 - complexity 2/5 - Update TODO.md
  - **File**: .ai/TODO.md
  - **Add to completed**: "Sync Command & Agent System from Coach-Ops"
  - **Add completion date**: Current date
  - **Sprint summary**: "Added prd-writer and task-writer agents, enhanced /prd and /tasks commands with decision frameworks and agent delegation, created /bugs command, added WORKFLOW.md guide"

- [x] 9.5 - complexity 1/5 - Validate memory system integrity
  - **Line count check**: Total should be ~3000 lines across 8 files
  - **File count check**: Exactly 8 files in .ai/ directory
  - **Meta dates check**: All meta.lastUpdated dates current

---

## Complexity Summary

| Rating | Count | Tasks |
|--------|-------|-------|
| **1/5** | 9 | Frontmatter, validation, simple checks |
| **2/5** | 6 | File updates, memory updates |
| **3/5** | 3 | Agent creation, WORKFLOW.md |
| **4/5** | 2 | prd.md upgrade, bugs.md creation |
| **5/5** | 0 | None |

**Total Subtasks**: 20
**Estimated Total Effort**: ~6-8 hours

---

## Risk Mitigation

**Low Risk Overall**:
- Changes are to template/configuration files only
- No code changes to project functionality
- Improvements are additive (enhance existing patterns)
- Source material is battle-tested in coach-ops

**Testing Strategy**:
1. After sync, verify in claude-project-starter:
   - Run `/prd "test feature"` - should invoke questioning, then agent
   - Run `/tasks test-feature` - should generate task list with complexity ratings
   - Run `/bugs "test bug"` - should show 6-phase investigation framework
2. Verify all commands reference memory system correctly
3. Ensure no project-specific references remain

**Rollback Plan**:
- Git revert if any issues discovered
- Keep coach-ops as reference for correct behavior
