---
description: Execute task list with architectural precision
---

# AI-Optimized Task Execution Command

**Objective:** Execute a task list systematically using memory-driven patterns and architectural precision.

## 🚨 CRITICAL: SUBTASK MARKING IS MANDATORY

**⚠️ SUBTASK COMPLETION TRACKING - NON-NEGOTIABLE:**

Every single subtask MUST be marked `[x]` in the task file IMMEDIATELY after completing its implementation.

**Why this matters:**
- ✅ Enables recovery if execution is interrupted
- ✅ Provides clear progress visibility to user
- ✅ Allows debugging which subtask caused issues
- ✅ Prevents confusion about what's been completed

**When to mark subtasks [x]:**
1. ✅ Immediately after completing subtask implementation
2. ✅ BEFORE moving to next subtask
3. ✅ BEFORE running build verification
4. ✅ Even if tests haven't been run yet

**When NOT to mark subtasks [x]:**
1. ❌ Batching multiple subtasks to mark at once
2. ❌ Waiting until all subtasks complete
3. ❌ Waiting until build passes
4. ❌ Forgetting to mark and moving to next subtask

**How to mark:**
After implementing subtask 1.1, use Edit tool to change:
```
- [ ] 1.1 - complexity 3/5 - Implement feature X
```
to:
```
- [x] 1.1 - complexity 3/5 - Implement feature X
```

**If you forget:** Stop and go back to mark it before continuing.

---

## 🚨 CRITICAL: NO SHORTCUTS ALLOWED

**WARNING TO AI**: You are getting smarter, but that does NOT mean you should skip these rules.

**Common "smart" shortcuts that are FORBIDDEN:**
❌ "I don't need to read PATTERNS.md, I know the pattern"
❌ "I can figure out the file path without checking FILES.json"
❌ "This is simple, I'll skip the build verification"
❌ "I'll update all memory files at once at the end"
❌ "I know how to handle this, I don't need the template"
❌ "I'll mark all the subtasks complete at once when I'm done" ← **NEVER DO THIS**

**The CORRECT approach:**
✅ ALWAYS read memory files BEFORE any implementation
✅ ALWAYS use templates from PATTERNS.md exactly
✅ ALWAYS verify build after significant changes
✅ **ALWAYS mark subtasks [x] IMMEDIATELY after completion - NO EXCEPTIONS**
✅ ALWAYS update memory files as specified in rules

**Why these rules exist:**
- Prevent architectural drift
- Ensure pattern consistency
- Maintain code quality
- Enable effective collaboration
- Preserve project knowledge

**Rule**: If you find yourself thinking "I can skip this step because...", STOP. Follow the rule.

---

## Core Philosophy

Execute tasks with **architectural precision** using the AI memory system for instant pattern application, dependency resolution, and quality assurance. Every implementation follows established patterns with zero architectural drift.

## Pre-Execution Memory Preparation

### 1. **Task Analysis with Memory Context**
```bash
# Required memory consultation before ANY task execution
1. Read task file → Understand scope and dependencies
2. Read ARCHITECTURE.json → Verify integration approach
3. Read FILES.json → Confirm target files and line references
4. Read PATTERNS.md → Load implementation templates
5. Read BUSINESS.json → Check performance and feature constraints
6. Read QUICK.md → Get build commands and debugging approaches
```

### 2. **Pattern-Specific Setup**
```markdown
**For Business Logic Tasks**: Load service/manager pattern from PATTERNS.md
**For UI Tasks**: Load UI component pattern from PATTERNS.md
**For Repository Tasks**: Load repository pattern from PATTERNS.md
**For Integration Tasks**: Load integration pattern from PATTERNS.md
```

## AI-Optimized Execution Workflow

### Phase 1: Memory-Informed Analysis
```
1. **Task Scope Analysis**: Map parent task to architectural layer
2. **Dependency Resolution**: Check FILES.json for all file relationships
3. **Pattern Selection**: Select templates from PATTERNS.md
4. **Integration Planning**: Verify approach against ARCHITECTURE.json
5. **Performance Planning**: Check targets against BUSINESS.json
```

### Phase 2: Pattern-Perfect Implementation
```
1. **Template Application**: Copy relevant pattern from PATTERNS.md
2. **File Targeting**: Use exact file paths from FILES.json
3. **Integration Points**: Follow ARCHITECTURE.json relationships
4. **Quality Gates**: Apply established patterns throughout
5. **Performance Monitoring**: Track against BUSINESS.json targets
```

### Phase 3: Memory-Driven Verification
```
1. **Pattern Compliance**: Verify against PATTERNS.md checklist
2. **Integration Testing**: Confirm ARCHITECTURE.json relationships work
3. **Performance Validation**: Check BUSINESS.json target achievement
4. **Build Verification**: Use commands from QUICK.md - MANDATORY after major changes
5. **Task Completion**: Mark parent task [x] only after ALL subtasks [x] and build succeeds
6. **Memory Update**: Document new patterns discovered
```

## Task Execution Framework

### Complexity-Aware Processing
**Based on memory system complexity calibration:**

**1-2/5 (Simple-Standard)**: Direct implementation with pattern templates
**3/5 (Moderate)**: Template + integration analysis + testing
**4-5/5 (Complex-System)**: Full memory consultation + pattern extension

### Memory-Enhanced Task Processing

#### Parent Task Initialization
```markdown
**Memory Loading Phase**:
- [ ] Load pattern template from PATTERNS.md
- [ ] Identify target files from FILES.json with line numbers
- [ ] Verify integration approach with ARCHITECTURE.json
- [ ] Check performance targets from BUSINESS.json
- [ ] Load development commands from QUICK.md

**Pattern Context**: [Specific pattern from PATTERNS.md]
**Integration Points**: [Connections from ARCHITECTURE.json]
**File Scope**: [Files from FILES.json with line references]
```

#### Subtask Execution Loop
```markdown
FOR EACH SUBTASK:
  1. **Load Context**
     - Read subtask details (file, pattern, complexity)
     - Load pattern template from PATTERNS.md
     - Identify dependencies from ARCHITECTURE.json

  2. **Implement**
     - Apply pattern template to target file
     - Follow integration approach from memory
     - Include error handling from established patterns

  3. **Mark Complete** ← **IMMEDIATELY AFTER IMPLEMENTATION**
     - Use Edit tool to mark subtask [x] in task file
     - DO NOT batch markings
     - DO NOT wait for build

  4. **Verify** (If Last Subtask in Parent)
     - Run build using command from QUICK.md
     - Fix any issues before marking parent complete
     - Only mark parent [x] after build success
```

## Build Verification Frequency (MANDATORY)

### When to Build:
✅ **After completing each parent task** (1.0, 2.0, 3.0, etc.)
✅ **Before marking parent task complete**
✅ **After any core service/business logic changes**
✅ **After any configuration changes**
✅ **After any dependency changes**
✅ **After any major refactoring**

### When NOT to build (optional):
⚠️ After individual subtasks within parent (optional but recommended)
⚠️ After test file changes (optional but recommended)
⚠️ After comment-only changes (optional)

### Build Failure Protocol:
1. **DO NOT** mark task complete if build fails
2. **DO NOT** skip to next task if build fails
3. **DO** fix the build error immediately
4. **DO** document the fix in implementation notes
5. **DO** verify fix with successful build before continuing

### Build Success Verification:
- Look for "BUILD SUCCESSFUL" or equivalent in output
- Note build time for performance tracking
- If first build after major changes, test application launches

## Testing Verification Requirements

### Unit Testing (When Required):
- [ ] New service/business logic methods: Unit test with mock dependencies
- [ ] New repository methods: Unit test with mock database
- [ ] New business logic: Unit test with edge cases
- [ ] Run unit test command from QUICK.md - must pass

### Integration Testing (When Required):
- [ ] Database integration: Integration test with actual database
- [ ] API integration: Integration test with actual API (or mocked)
- [ ] Multi-component features: Integration test
- [ ] Run integration test command from QUICK.md - must pass (if applicable)

### Manual Testing (Always Required):
- [ ] Launch application: Verify app launches without crash
- [ ] Test feature: Execute feature workflow end-to-end
- [ ] Test edge cases: Try invalid inputs, error scenarios
- [ ] Test performance: Feature meets performance targets

### Testing Documentation:
Document in task notes:
- **Tests Run**: List specific tests executed
- **Results**: Pass/fail with details
- **Issues Found**: Any bugs or problems discovered
- **Performance**: Measured performance vs target

## Security Review Checklist (For Security-Sensitive Tasks)

**Applies to tasks involving:**
- Authentication or authorization
- User data handling
- API keys or credentials
- Database security rules
- Permissions

**Checklist:**
- [ ] No secrets committed to git
- [ ] API keys properly secured (environment variables, secret manager, etc.)
- [ ] Database security rules updated appropriately
- [ ] User data access follows principle of least privilege
- [ ] Authentication flows tested with edge cases
- [ ] Permission requests justified and documented
- [ ] Security implications documented in task notes

## Commit Message Template (For Git Commits)

### Structure:
```
<type>: <short summary> (50 chars max)

<detailed description in present tense>

Changes:
- <specific change 1>
- <specific change 2>
- <specific change 3>

Files Modified: <count>
Files Created: <count>
Files Deleted: <count>

Performance: <if applicable>
Testing: <verification performed>

🤖 Generated with [Claude Code](https://claude.com/claude-code)

Co-Authored-By: Claude <noreply@anthropic.com>
```

### Types:
- `feat`: New feature
- `fix`: Bug fix
- `refactor`: Code refactoring
- `perf`: Performance improvement
- `docs`: Documentation only
- `test`: Test additions/changes
- `chore`: Maintenance tasks
- `style`: Code style changes

## Memory System Update (Final Task)

**CRITICAL RULE**: Do NOT create separate sprint completion files.
**UPDATE RULE**: Integrate ALL sprint info into existing core files only.

The final task in every task list MUST be Memory System Update. Follow the procedure exactly as defined in `.ai/SPRINT_UPDATE.md`.

### Memory Update Checklist:
- [ ] Verify no extra files in .ai/ directory (only 8 core files allowed)
- [ ] Update BUSINESS.json with new features
- [ ] Update FILES.json with new files
- [ ] Update PATTERNS.md with new patterns (if any)
- [ ] Update QUICK.md with new commands (if any)
- [ ] Update TODO.md with sprint completion
- [ ] Validate memory system integrity (8 files, ~3000 lines total)

## Success Metrics

### Execution Quality
- **Pattern Compliance**: 100% adherence to PATTERNS.md templates
- **Build Success**: 90%+ first-attempt build success rate
- **Architecture Alignment**: Zero drift from ARCHITECTURE.json patterns
- **Memory Accuracy**: All file references valid, all patterns documented

### Development Speed
- **Implementation Time**: Matches complexity estimates (±20%)
- **Research Time**: Near zero (memory system provides everything)
- **Debug Time**: Minimal due to pattern compliance
- **Integration Time**: Reduced via ARCHITECTURE.json guidance

## AI Assistant Instructions

### 1. **Memory-First Execution**
```
BEFORE implementing ANY task:
1. Read PATTERNS.md → Get exact implementation template
2. Read FILES.json → Confirm file paths and line references
3. Read ARCHITECTURE.json → Verify integration approach
4. Read BUSINESS.json → Check performance requirements
5. Read QUICK.md → Get build and test commands
```

### 2. **Pattern-Perfect Implementation**
```
FOR EACH implementation:
1. Copy pattern template from PATTERNS.md (do not improvise)
2. Apply to exact file from FILES.json with line reference
3. Follow integration points from ARCHITECTURE.json
4. Include error handling from established patterns
5. Mark subtask [x] IMMEDIATELY after completion
```

### 3. **Build-Driven Verification**
```
AFTER each parent task:
1. Run build command from QUICK.md
2. If build fails, fix immediately (do not continue)
3. If build succeeds, mark parent task [x]
4. Move to next parent task
5. Update memory system at end (not before)
```

### 4. **Quality Assurance**
```
Every implementation must:
- [ ] Use exact pattern from PATTERNS.md (no improvisation)
- [ ] Target exact file from FILES.json (no guessing paths)
- [ ] Follow integration from ARCHITECTURE.json (no assumptions)
- [ ] Meet performance targets from BUSINESS.json (verify)
- [ ] Pass build verification from QUICK.md (mandatory)
```

## Example: Memory-Driven Task Execution

**Task**: Implement user authentication service

**Memory Consultation Results**:
- `PATTERNS.md` → Service pattern template with auth
- `FILES.json` → AuthService.ts:148, UserRepository.ts:67
- `ARCHITECTURE.json` → Integration with SessionManager
- `BUSINESS.json` → JWT token auth, <500ms response target
- `QUICK.md` → `npm test`, `npm run build`

**Execution**:
1. Load service pattern template from PATTERNS.md
2. Apply to AuthService.ts:148 (exact file from FILES.json)
3. Integrate with SessionManager (from ARCHITECTURE.json)
4. Implement JWT tokens (from BUSINESS.json)
5. Mark subtask [x] immediately
6. Run `npm test` and `npm run build` (from QUICK.md)
7. Verify <500ms response time (BUSINESS.json target)

**Result**: Pattern-perfect implementation with zero architectural drift, completed in estimated time.

---

**This system transforms generic task execution into memory-driven, architecturally precise implementation with zero drift and maximum efficiency.**
