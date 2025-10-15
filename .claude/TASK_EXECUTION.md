# AI-Optimized Task Execution Rules

*Memory-driven implementation workflow for pattern-perfect code execution*

## 🚨 CRITICAL: NO SHORTCUTS ALLOWED

**WARNING TO AI**: You are getting smarter, but that does NOT mean you should skip these rules.

**Common "smart" shortcuts that are FORBIDDEN:**
❌ "I don't need to read PATTERNS.md, I know the pattern"
❌ "I can figure out the file path without checking FILES.json"
❌ "This is simple, I'll skip the build verification"
❌ "I'll update all memory files at once at the end"
❌ "I know how to handle this, I don't need the template"

**The CORRECT approach:**
✅ ALWAYS read memory files BEFORE any implementation
✅ ALWAYS use templates from PATTERNS.md exactly
✅ ALWAYS verify build after significant changes
✅ ALWAYS mark subtasks [x] immediately after completion
✅ ALWAYS update memory files as specified in rules

**Why these rules exist:**
- Prevent architectural drift
- Ensure pattern consistency
- Maintain code quality
- Enable effective collaboration
- Preserve project knowledge

**Rule**: If you find yourself thinking "I can skip this step because...", STOP. Follow the rule.

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
**For Business Logic Tasks**: Load [PRIMARY_PATTERN] template from PATTERNS.md # e.g., "Service pattern", "Manager pattern"
**For Integration Tasks**: Load [INTEGRATION_PATTERN] template from PATTERNS.md # e.g., "API integration pattern", "Middleware pattern"
**For UI Tasks**: Load [UI_PATTERN] template from PATTERNS.md # e.g., "MVVM", "Component pattern"
**For Repository Tasks**: Load Repository pattern template from PATTERNS.md
**For Caching Tasks**: Load [CACHING_PATTERN] template from PATTERNS.md # e.g., "Cache service pattern"
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
4. **Build Verification**: Use commands from QUICK.md - MANDATORY ([BUILD_COMMAND])
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

#### 1.0 Parent Task Initialization
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

#### 1.X Subtask Execution (Memory-Driven)
```markdown
- [ ] 1.1 - complexity [X]/5 - [Task description]
  **Memory-Enhanced Implementation**:
  - **File**: [Exact file from FILES.json:line]
  - **Pattern**: [Template from PATTERNS.md]
  - **Template**:
    ```[language]
    // Copy-paste template from PATTERNS.md
    [DEPENDENCY_INJECTION_DECORATOR] # e.g., "@Injectable()", "@Singleton", etc.
    class [FeatureName][Component] [implements/extends] [Interface] {
        constructor(
            // Dependencies from ARCHITECTURE.json
        ) {}
        // Implementation following established pattern
    }
    ```
  - **Integration**: [Specific approach from ARCHITECTURE.json]
  - **Testing**: [Test pattern from existing tests]
  - **Performance**: [Impact on BUSINESS.json targets]
  - **Verification**: [Pattern compliance checklist from PATTERNS.md]

  **CRITICAL**: Mark subtask `[x]` IMMEDIATELY after completing implementation
  **INTERRUPTION RECOVERY**: If interrupted, task progress preserved for recovery
```

## Advanced AI Features

### 1. **Pattern Compliance Automation**
```markdown
**Automatic Pattern Verification**:
- [ ] [PRIMARY_PATTERN]: [Key pattern requirements verified] # e.g., "Service: @Injectable annotation, DI verified"
- [ ] [UI_PATTERN]: [Key pattern requirements verified] # e.g., "MVVM: ViewModel separation confirmed"
- [ ] Repository: [ERROR_PATTERN] return types, error handling implemented # e.g., "Result<T>"
- [ ] [CACHING_PATTERN]: [Caching structure verified if applicable]
- [ ] State: [STATE_MANAGER] integration following established flow
```

### 2. **Dependency Auto-Resolution**
```markdown
**From FILES.json dependencies**:
- **Required Imports**: [Auto-detected from file relationships]
- **Integration Points**: [Auto-mapped from ARCHITECTURE.json]
- **Test Dependencies**: [Auto-identified from test patterns]
- **Build Requirements**: [Auto-sourced from QUICK.md]
```

### 3. **Performance-Aware Implementation**
```markdown
**Performance Integration** (from BUSINESS.json):
- **Target**: [Specific performance target for this feature]
- **Monitoring**: [Analytics integration pattern]
- **Optimization**: [Specific optimization approach from memory]
- **Validation**: [Performance test approach]
```

### 4. **Quality Assurance Automation**
```markdown
**Memory-Driven Quality Gates**:
- [ ] **Pattern Compliance**: Matches template from PATTERNS.md
- [ ] **File Accuracy**: Uses exact paths from FILES.json
- [ ] **Integration Correctness**: Follows ARCHITECTURE.json relationships
- [ ] **Performance Alignment**: Meets BUSINESS.json targets
- [ ] **Testing Coverage**: Implements test patterns from memory
```

## Build and Verification Workflow

### Memory-Enhanced Build Process
```bash
# Commands from QUICK.md - Project specific
[BUILD_COMMAND]              # e.g., "./gradlew build", "npm run build", "cargo build"
[TEST_COMMAND]               # e.g., "./gradlew test", "npm test", "cargo test"
[INTEGRATION_TEST_COMMAND]   # e.g., "./gradlew integrationTest", "npm run test:e2e"

# Performance monitoring (from QUICK.md)
# [Project-specific monitoring commands]

# Memory system validation
# Check that implementation follows patterns correctly
```

### Build Verification Frequency (MANDATORY)

**When to Build:**
✅ **After completing each parent task** (1.0, 2.0, 3.0, etc.)
✅ **Before marking parent task complete**
✅ **After any business logic/service/repository changes**
✅ **After any manifest or configuration changes**
✅ **After any dependency changes**
✅ **After any resource file changes** (assets, configs, etc.)

**When NOT to build (optional):**
⚠️ After individual subtasks within parent (optional but recommended)
⚠️ After test file changes (optional but recommended)
⚠️ After comment-only changes (optional)

**Build Failure Protocol:**
1. **DO NOT** mark task complete if build fails
2. **DO NOT** skip to next task if build fails
3. **DO** fix the build error immediately
4. **DO** document the fix in implementation notes
5. **DO** verify fix with successful build before continuing

**Build Success Verification:**
- Look for "BUILD SUCCESSFUL" or equivalent in output
- Note build time for performance tracking
- If first build after major changes, also test application launch

### Testing Verification Requirements

**Unit Testing (When Required):**
- [ ] New business logic methods: Unit test with mock dependencies
- [ ] New repository methods: Unit test with mocked data layer
- [ ] New business logic: Unit test with edge cases
- [ ] Run tests: Verify all unit tests pass

**Integration Testing (When Required):**
- [ ] Database integration: Integration test with actual database
- [ ] API integration: Integration test with actual API (or mocked)
- [ ] Multi-component features: Integration test
- [ ] Run integration tests: Verify all tests pass

**Manual Testing (Always Required):**
- [ ] Launch application: Deploy to target environment
- [ ] Test feature: Execute feature workflow end-to-end
- [ ] Test edge cases: Try invalid inputs, error scenarios
- [ ] Test performance: Feature meets performance targets

**Testing Documentation:**
Document in task notes:
- **Tests Run**: List specific tests executed
- **Results**: Pass/fail with details
- **Issues Found**: Any bugs or problems discovered
- **Performance**: Measured performance vs target

### Pattern-Specific Verification
```markdown
**[PRIMARY_PATTERN] Verification**: # e.g., "Service Pattern Verification"
- [ ] [Dependency injection working correctly]
- [ ] [STATE_MANAGER] integration functional
- [ ] [ERROR_PATTERN] return types implemented # e.g., "Result<T>"

**[UI_PATTERN] Verification**: # e.g., "MVVM Verification"
- [ ] [Pattern-specific requirements verified]
- [ ] [State management working]
- [ ] [UI integration functional]
- [ ] [Lifecycle management correct]

**Repository Pattern Verification**:
- [ ] Database/API integration working
- [ ] Error handling with [ERROR_PATTERN] # e.g., "Result<T>", "Either<Error, Success>"
- [ ] Data sync operational
- [ ] Data validation applied
```

## Documentation and Memory Updates

### Implementation Documentation
```markdown
**Implementation Notes Template**:
- **Pattern Applied**: [Specific pattern from PATTERNS.md]
- **Files Modified**: [List with line number references]
- **Integration Approach**: [Method from ARCHITECTURE.json]
- **Performance Impact**: [Measured impact on BUSINESS.json targets]
- **Deviations**: [Any changes from original plan with reasons]
- **New Patterns**: [Any new patterns discovered during implementation]
- **Error Solutions**: [Specific fixes applied with context]
```

### Commit Message Template (For Git Commits)

**Structure:**
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

**Types:**
- `feat`: New feature
- `fix`: Bug fix
- `refactor`: Code refactoring
- `perf`: Performance improvement
- `docs`: Documentation only
- `test`: Test additions/changes
- `chore`: Maintenance tasks
- `style`: Code style changes

**Example:**
```
feat: Add user preference settings with API integration

Implemented user preference settings feature with integration to existing
state management system and repository pattern. Feature allows users
to customize application settings with automatic cloud sync.

Changes:
- Added PreferenceService with dependency injection
- Integrated with StateManager for preference state updates
- Implemented repository pattern for preference persistence
- Added UI controls for preference selection

Files Modified: 8 core files
Files Created: PreferenceService.ext, PreferenceRepository.ext, SettingsUI.ext
Files Deleted: None

Performance: Preference loading <100ms, sync <200ms
Testing: ✅ Unit tests, ✅ Integration tests, ✅ Manual testing

🤖 Generated with [Claude Code](https://claude.com/claude-code)

Co-Authored-By: Claude <noreply@anthropic.com>
```

### Memory System Updates (Final Phase)
```markdown
### [Final Task]: Update AI Memory System
**Goal**: Update memory system with implementation learnings
**Files**: .ai/ directory files
**Pattern**: Memory update template from SPRINT_UPDATE.md

- [ ] X.1 - complexity 2/5 - Update PATTERNS.md with new templates
  - **File**: .ai/PATTERNS.md
  - **Action**: Add any new patterns discovered during implementation
  - **Template**: Follow SPRINT_UPDATE.md guidelines
  - **Verification**: Patterns include working code examples

- [ ] X.2 - complexity 2/5 - Update FILES.json with new file references
  - **File**: .ai/FILES.json
  - **Action**: Add new files and update dependencies
  - **Include**: Line number references for key implementations
  - **Verification**: All file paths are accurate

- [ ] X.3 - complexity 2/5 - Update ARCHITECTURE.json with integration points
  - **File**: .ai/ARCHITECTURE.json
  - **Action**: Document new component relationships and data flows
  - **Include**: Integration points and constraints discovered
  - **Verification**: Architecture map reflects actual implementation

- [ ] X.4 - complexity 1/5 - Update BUSINESS.json with feature status
  - **File**: .ai/BUSINESS.json
  - **Action**: Mark feature as complete and update performance data
  - **Include**: Actual performance measurements vs targets
  - **Verification**: Feature status accurately reflects implementation

- [ ] X.5 - complexity 1/5 - Update QUICK.md with new debugging approaches
  - **File**: .ai/QUICK.md
  - **Action**: Add any new debugging patterns or commands discovered
  - **Include**: File locations and debugging approaches that worked
  - **Verification**: Commands are tested and functional
```

## Error Recovery with Memory Intelligence

### Memory-Informed Error Resolution
```markdown
**Error Analysis Protocol**:
1. **Pattern Check**: Verify implementation matches PATTERNS.md template
2. **File Verification**: Confirm file paths match FILES.json references
3. **Integration Review**: Check ARCHITECTURE.json relationships are correct
4. **Dependency Analysis**: Verify all dependencies from memory system
5. **Performance Impact**: Consider BUSINESS.json constraint violations
```

### Common Error Solutions (Memory-Enhanced)
```markdown
**Build Errors**:
- **Import Issues**: Check FILES.json dependencies for correct imports
- **Type Mismatches**: Verify pattern templates from PATTERNS.md
- **Injection Errors**: Confirm dependency injection pattern application
- **State Issues**: Check [STATE_MANAGER] integration from ARCHITECTURE.json

**Runtime Errors**:
- **Cache Issues**: Verify [CACHING_PATTERN] from memory
- **Service Issues**: Check [INTEGRATION_PATTERN] implementation
- **UI Issues**: Confirm [UI_PATTERN] application
- **Performance Issues**: Review BUSINESS.json targets and optimization approaches
```

## AI Assistant Instructions

### 1. **Memory-First Implementation**
```
BEFORE implementing any task:
1. Load pattern template from PATTERNS.md
2. Verify file targets in FILES.json with line numbers
3. Check integration requirements in ARCHITECTURE.json
4. Confirm performance targets in BUSINESS.json
5. Load development commands from QUICK.md
```

### 2. **Pattern-Perfect Execution**
```
During implementation:
1. Apply pattern template exactly from PATTERNS.md
2. Use file references from FILES.json for all dependencies
3. Follow integration approach from ARCHITECTURE.json
4. Monitor performance against BUSINESS.json targets
5. Use debugging commands from QUICK.md when needed
6. MARK PROGRESS: Update subtasks [x] immediately after completing each one
7. HANDLE INTERRUPTIONS: Preserve task state for recovery scenarios
```

### 3. **Quality Assurance with Memory**
```
Before marking task complete:
1. Verify pattern compliance against PATTERNS.md checklist
2. Confirm all file modifications align with FILES.json structure
3. Test integration points specified in ARCHITECTURE.json
4. Validate performance meets BUSINESS.json requirements
5. BUILD VERIFICATION: Run [BUILD_COMMAND] - must succeed
6. TASK MARKING: Mark parent task [x] only after all subtasks [x] and build success
7. Document new learnings for memory system update
```

### 4. **Memory Update Responsibility**
```
After task completion:
1. Identify new patterns for PATTERNS.md
2. Update file references in FILES.json
3. Document integration learnings in ARCHITECTURE.json
4. Update performance data in BUSINESS.json
5. Add debugging approaches to QUICK.md
```

## Security Review Checklist (For Security-Sensitive Tasks)

**Applies to tasks involving:**
- Authentication or authorization
- User data handling
- API keys or credentials
- Database security rules
- Permissions

**Checklist:**
- [ ] No secrets committed to git
- [ ] API keys properly secured (environment variables, secret management, etc.)
- [ ] Database security rules updated appropriately
- [ ] User data access follows principle of least privilege
- [ ] Authentication flows tested with edge cases
- [ ] Permission requests justified and documented
- [ ] Security implications documented in implementation notes

## Success Criteria (Memory-Enhanced)

### Task Completion Requirements
- ✅ **Pattern Compliance**: Implementation matches PATTERNS.md template
- ✅ **File Accuracy**: Uses exact paths from FILES.json
- ✅ **Integration Success**: ARCHITECTURE.json relationships working
- ✅ **Performance Achievement**: Meets BUSINESS.json targets
- ✅ **Build Success**: [BUILD_COMMAND] executes successfully (MANDATORY)
- ✅ **Test Coverage**: Following test patterns from memory
- ✅ **Task Progress**: ALL subtasks marked [x] immediately after completion
- ✅ **Parent Task**: Only marked [x] after all subtasks [x] AND build success
- ✅ **Interruption Ready**: Task state preserved for recovery scenarios
- ✅ **Memory Update**: New learnings documented in .ai/ files

### Memory System Validation
- ✅ **Pattern Templates**: All patterns include working code examples
- ✅ **File References**: All file paths and line numbers are accurate
- ✅ **Architecture Map**: Integration points reflect actual implementation
- ✅ **Performance Data**: Targets updated with actual measurements
- ✅ **Quick Commands**: All commands tested and functional

## Workflow Optimization

### Parallel Processing
```markdown
**Batch Operations** (when possible):
- Read multiple memory files simultaneously
- Apply multiple pattern templates in parallel
- Verify multiple integration points concurrently
- Update multiple memory files together
```

### Context Preservation
```markdown
**Memory Context Maintenance**:
- Keep pattern templates loaded throughout parent task
- Maintain file reference context across subtasks
- Preserve integration approach throughout implementation
- Monitor performance continuously against targets
```

### Efficiency Targets
- **Memory Consultation**: Under 30 seconds per parent task
- **Pattern Application**: Immediate template usage from memory
- **Error Resolution**: Memory-informed debugging approaches
- **Quality Verification**: Automated pattern compliance checking

## Quick Reference Flow

```
Memory Load → Pattern Apply → File Target → Integrate → Mark [x] → Test → Build ✓ → Document → Memory Update → Mark Parent [x] → Next Task
```

**Memory System Integration**: Every step leverages comprehensive architectural knowledge for pattern-perfect implementation with zero research overhead.

## Critical Task Management Rules

### Interruption Recovery Protocol
1. **Task State Preservation**: All subtask progress marked [x] preserved
2. **Build State Tracking**: Build success/failure status maintained
3. **Implementation Notes**: Document actual vs planned approach
4. **Recovery Point**: Resume from last completed subtask
5. **Verification Required**: Re-run build after interruption recovery

### Build Requirements
- **Mandatory Command**: [BUILD_COMMAND] from QUICK.md
- **Failure Handling**: Fix errors immediately, don't skip
- **Success Verification**: No parent task [x] until build succeeds
- **Error Documentation**: Record fixes in implementation notes

---

**This system transforms task execution from generic programming into memory-driven, pattern-specific implementation with continuous architectural awareness and automatic quality assurance.**
