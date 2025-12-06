# PRD: Sync Command & Agent System from Coach-Ops

**Generated:** 2025-12-07
**Source Project:** coach-ops (battle-tested implementation)
**Target Project:** claude-project-starter (generic template)
**Priority:** High - Core workflow infrastructure

---

## Overview

Synchronize the enhanced command and agent system developed in coach-ops to claude-project-starter. Coach-ops has evolved significantly more sophisticated workflows for PRD generation, task creation, and bug investigation that should become the standard template for all projects.

**Key Improvements:**
- Decision frameworks with explicit stopping criteria
- Red flag detection during requirement gathering
- Agent-based architecture for PRD and task generation
- Comprehensive bug investigation methodology
- Enhanced code documentation standards

---

## Current State Comparison

| Component | coach-ops | claude-project-starter | Gap |
|-----------|-----------|------------------------|-----|
| `/prd` command | Decision frameworks, red flags, 3-phase questioning | Basic memory consultation | **Major upgrade needed** |
| `prd-writer` agent | Full PRD generation with project context | **Missing** | **Create new** |
| `/tasks` command | `/TaskGen` delegates to agent | Direct inline task generation | **Restructure** |
| `task-writer` agent | Memory-driven, complexity calibration | **Missing** | **Create new** |
| `/bugs` command | 6-phase investigation, root cause | **Missing** | **Copy entire** |
| `/execute` command | Detailed comment standards | Good but less detailed | **Enhance** |
| `WORKFLOW.md` | Comprehensive (500+ lines) | Migration guide only | **Replace** |

---

## Implementation Plan

### Phase 1: Create Missing Agents (Priority: Critical)

#### 1.1 Create `prd-writer.md` Agent
**Source:** `/root/projects/realnz/coach-ops/.claude/agents/prd-writer.md`
**Target:** `/root/projects/claude-project-starter/.claude/agents/prd-writer.md`

**Action:** Copy from coach-ops with these modifications:
- Remove project-specific references (Firebase, Firestore, Pacific/Auckland timezone)
- Keep generic placeholders like `[PROJECT_DATABASE]`, `[PROJECT_FRAMEWORK]`
- Preserve all decision frameworks and PRD structure

**Key Features to Preserve:**
- PRD Template (17 sections)
- Memory system integration patterns
- Quality gates and validation checklist
- Architecture-mapped component structure

#### 1.2 Create `task-writer.md` Agent
**Source:** `/root/projects/realnz/coach-ops/.claude/agents/task-writer.md`
**Target:** `/root/projects/claude-project-starter/.claude/agents/task-writer.md`

**Action:** Copy from coach-ops with these modifications:
- Remove project-specific file references
- Keep complexity calibration system (1-5 scale with time estimates)
- Preserve memory system update as mandatory final task
- Keep architecture layer organization (1.0-7.0 task categories)

**Key Features to Preserve:**
- Complexity Calibration (1/5 to 5/5 with time estimates)
- Task Output Structure with header, overview, implementation order
- Quality Gates (pattern compliance, file accuracy, integration correctness)
- Memory Update as MANDATORY final task

---

### Phase 2: Upgrade Existing Commands (Priority: High)

#### 2.1 Upgrade `/prd.md` Command
**Source:** `/root/projects/realnz/coach-ops/.claude/commands/prd.md`
**Target:** `/root/projects/claude-project-starter/.claude/commands/prd.md`

**Changes Required:**

1. **Add Decision Frameworks Section** (from coach-ops lines ~57-100):
   ```markdown
   ## Decision Frameworks

   ### Stopping Criteria (Requirement Gathering Completeness)
   - Problem statement clarity: 0-100%
   - User journey definition: 0-100%
   - Integration points identified: 0-100%
   - Success metrics defined: 0-100%
   - Edge cases documented: 0-100%

   **Threshold:** When average score ≥ 85%, requirements are sufficient
   ```

2. **Add Red Flag Framework** (from coach-ops lines ~107-132):
   ```markdown
   ## Red Flag Framework

   During questioning, proactively alert user if detecting:

   ### Scope Creep Indicators
   - Feature requests expanding beyond original problem
   - "While we're at it..." additions
   - Multiple unrelated features bundled

   ### Technical Risk Indicators
   - Requests conflicting with existing architecture
   - Performance-critical features without clear requirements
   - Security-sensitive features mentioned casually
   ```

3. **Add 3-Phase Questioning Process** (from coach-ops lines ~135-194):
   - Round 1: Core Understanding (problem, users, success criteria)
   - Round 2: Scope & UX (boundaries, flows, integrations)
   - Round 3+: Deep Dive & Integration (edge cases, technical constraints)
   - Max 7 rounds with explicit stopping criteria

4. **Add Agent Handoff Section**:
   ```markdown
   ## Agent Handoff

   After user confirms requirements summary:
   1. Compile all gathered context into structured YAML
   2. Invoke prd-writer agent with context
   3. Agent generates and saves PRD to `/tasks/prd-[feature-name].md`
   ```

#### 2.2 Replace `/tasks.md` with TaskGen Pattern
**Source:** `/root/projects/realnz/coach-ops/.claude/commands/TaskGen.md`
**Target:** Modify `/root/projects/claude-project-starter/.claude/commands/tasks.md`

**Changes Required:**

1. Update command to delegate to task-writer agent:
   ```markdown
   ## Command Structure

   `/tasks [prd-name]`

   Immediately invokes task-writer agent with:
   - PRD filename (from argument)
   - Memory system context
   - Project-specific patterns
   ```

2. Add Complexity Calibration section:
   ```markdown
   ## Complexity Calibration

   | Level | Time Estimate | Examples |
   |-------|---------------|----------|
   | 1/5 | 5-15 min | Simple data/UI changes |
   | 2/5 | 15-45 min | Business logic methods |
   | 3/5 | 45-90 min | Service integration |
   | 4/5 | 1.5-3 hrs | Multi-component features |
   | 5/5 | 3+ hrs | System-wide changes |
   ```

3. Ensure Memory Update is MANDATORY final task

#### 2.3 Create `/bugs.md` Command (New)
**Source:** `/root/projects/realnz/coach-ops/.claude/commands/bugs.md`
**Target:** `/root/projects/claude-project-starter/.claude/commands/bugs.md`

**Action:** Copy entire file with these modifications:
- Remove project-specific investigation areas (keep as template placeholders)
- Preserve 6-phase investigation methodology
- Keep decision rules (complexity ≤6 → tasks, complexity ≥7 → PRD)
- Preserve example investigation flow structure

**Key Sections to Preserve:**
- Phase 1: Clarification (targeted questions only)
- Phase 2: Memory System Consultation
- Phase 3: Autonomous Code Exploration
- Phase 4: Root Cause Analysis
- Phase 5: Solution Options (2-4 with trade-offs)
- Phase 6: Recommendation & Next Steps

---

### Phase 3: Enhance Supporting Files (Priority: Medium)

#### 3.1 Enhance `/execute.md` Command
**Source:** `/root/projects/realnz/coach-ops/.claude/commands/execute.md`
**Target:** Enhance `/root/projects/claude-project-starter/.claude/commands/execute.md`

**Additions Required:**

1. **Code Documentation Standards Section** (~50 lines):
   - Mandatory high-quality comments guideline
   - 1 comment per 5-15 lines recommendation
   - 7 detailed examples showing what NOT to do

2. **Strengthen Subtask Marking**:
   - IMMEDIATE [x] marking after each subtask (non-negotiable)
   - Build verification mandatory after parent tasks
   - Failure protocol with memory-informed error resolution

#### 3.2 Replace `SLASH_COMMAND_MIGRATION.md` with `WORKFLOW.md`
**Source:** `/root/projects/realnz/coach-ops/.claude/WORKFLOW.md`
**Target:** Replace `/root/projects/claude-project-starter/.claude/SLASH_COMMAND_MIGRATION.md` with `/root/projects/claude-project-starter/.claude/WORKFLOW.md`

**Key Sections to Include:**
- Command Flow table (which command → what output → next step)
- 4 Workflow Patterns (new feature, simple bug, complex bug, small tweak)
- Decision Tree for command selection
- Detailed command descriptions
- Example full workflows

---

### Phase 4: Copy Additional Agents (Priority: Low)

#### 4.1 Consider `firebase-expert.md` Agent
**Source:** `/root/projects/realnz/coach-ops/.claude/agents/firebase-expert.md`

**Decision:** This is project-specific. Consider creating a generic `database-expert.md` template that projects can customize.

---

## File Operations Summary

### Files to CREATE:
1. `.claude/agents/prd-writer.md` - Copy from coach-ops, generalize
2. `.claude/agents/task-writer.md` - Copy from coach-ops, generalize
3. `.claude/commands/bugs.md` - Copy from coach-ops, generalize
4. `.claude/WORKFLOW.md` - Copy from coach-ops, generalize

### Files to MODIFY:
1. `.claude/commands/prd.md` - Add decision frameworks, red flags, 3-phase questioning
2. `.claude/commands/tasks.md` - Restructure to delegate to task-writer agent
3. `.claude/commands/execute.md` - Add code documentation standards

### Files to DELETE:
1. `.claude/SLASH_COMMAND_MIGRATION.md` - Replaced by WORKFLOW.md

---

## Acceptance Criteria

### Functional Requirements
- [ ] `/prd` command includes decision frameworks and red flag detection
- [ ] `/prd` command delegates to prd-writer agent for document generation
- [ ] `/tasks` command delegates to task-writer agent
- [ ] `/tasks` includes complexity calibration with time estimates
- [ ] `/bugs` command provides 6-phase investigation methodology
- [ ] Memory update is mandatory final task in all task lists
- [ ] WORKFLOW.md documents all command flows and decision trees

### Quality Requirements
- [ ] All project-specific references removed from starter templates
- [ ] Placeholder patterns used (e.g., `[PROJECT_DATABASE]`, `[PROJECT_FRAMEWORK]`)
- [ ] Commands can be used immediately in new projects without modification
- [ ] Agent prompts are comprehensive but generic

### Documentation Requirements
- [ ] WORKFLOW.md includes all 4 workflow patterns
- [ ] Each command has clear input/output documentation
- [ ] Agent handoff protocols are explicit

---

## Risk Assessment

**Risk Level:** Low

- Changes are to template/configuration files only
- No code changes to project functionality
- Improvements are additive (enhance existing patterns)
- Source material is battle-tested in coach-ops

**Mitigation:**
- Test commands in a fresh project after sync
- Verify agent invocations work correctly
- Ensure memory system references are generic

---

## Implementation Notes

### Generalization Guidelines

When copying from coach-ops, replace:
- `Firebase`, `Firestore` → `[PROJECT_DATABASE]`
- `Pacific/Auckland` → `[PROJECT_TIMEZONE]`
- `@realnz.com` → `[PROJECT_DOMAIN]`
- Specific file paths → `[path/to/relevant/file.ext]`
- Coach-ops specific patterns → Generic pattern placeholders

### Testing Strategy

After sync, verify in claude-project-starter:
1. Run `/prd "test feature"` - should invoke questioning, then agent
2. Run `/tasks test-feature` - should generate task list with complexity ratings
3. Run `/bugs "test bug"` - should show 6-phase investigation framework
4. Verify all commands reference memory system correctly
