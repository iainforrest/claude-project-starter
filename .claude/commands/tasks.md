---
description: Generate pattern-specific task list from PRD
---

# AI-Optimized Task Generation Command

**Objective:** Transform a PRD into a comprehensive, pattern-specific task list and save it to `/tasks/tasks-[prd-name].md`.

## Core Philosophy

Transform PRDs into **pattern-specific, file-targeted task lists** that leverage comprehensive architectural knowledge. Generate tasks that are immediately implementable using established patterns with zero additional research time.

## Output Requirements

**CRITICAL:** The task list MUST be saved to a file:
- **Location:** `/tasks/` directory
- **Filename:** `tasks-[prd-name].md` (match the PRD name)
- **Format:** Markdown (.md)
- **Action:** Use the Write tool to save the task list after generation

**Example filenames:**
- PRD: `prd-user-authentication.md` → `tasks-user-authentication.md`
- PRD: `prd-real-time-notifications.md` → `tasks-real-time-notifications.md`

## Memory-First Analysis

### 1. **Pre-Generation Memory Consultation** (Required)
Before generating any tasks, systematically consult:

```bash
# Memory consultation sequence
1. Read ARCHITECTURE.json → Understand integration patterns and constraints
2. Read FILES.json → Identify target files and dependencies
3. Read PATTERNS.md → Find applicable implementation templates
4. Read BUSINESS.json → Check performance targets and feature constraints
5. Read QUICK.md → Get development commands and debugging approaches
```

### 2. **PRD Pattern Mapping**
Map each PRD component to established patterns from PATTERNS.md:
- **Business Logic** → [BUSINESS_LAYER_PATTERN] (ServiceClass.ext:line)
- **UI Components** → [UI_PATTERN] (Component.ext:line)
- **Data Persistence** → [REPOSITORY_PATTERN] (Repository.ext:line)
- **API Integration** → [INTEGRATION_PATTERN] (ApiClient.ext:line)

## Streamlined Generation Process

### Phase 1: Memory-Informed Architecture Analysis
```
1. Analyze PRD feature components against ARCHITECTURE.json patterns
2. Map each component to specific files from FILES.json
3. Identify implementation templates from PATTERNS.md
4. Extract performance requirements from BUSINESS.json
5. Generate implementation-ready task structure
```

**No user confirmation needed** - memory system provides complete context

### Phase 2: Pattern-Based Task Generation
Generate tasks with:
- **Specific file paths** and line numbers from FILES.json
- **Pattern templates** from PATTERNS.md with copy-paste code
- **Performance targets** from BUSINESS.json benchmarks
- **Testing strategies** following established test patterns
- **Development commands** from QUICK.md

## AI-Optimized Task Structure

### Header with Memory Integration
```markdown
# Task List: [Feature Name]

**Generated from**: `[prd-file-name].md`
**Date**: [Current Date]
**Architecture Pattern**: [Primary pattern from PATTERNS.md]
**Target Files**: [Key files from FILES.json]
**Performance Target**: [Target from BUSINESS.json]
**Build Command**: [Command from QUICK.md]
```

### Memory-Enhanced Overview
```markdown
## Overview
[Feature description]

**Implementation Strategy**: Leverages [pattern] from [memory reference]
**Integration Points**: [Specific connections from ARCHITECTURE.json]
**File Modification Scope**: [Target files from FILES.json]
**Performance Impact**: [Expected impact on BUSINESS.json targets]
```

### Pattern-Specific Implementation Order
```markdown
## Implementation Order

**Foundation First**: [Pattern] implementation from PATTERNS.md
**Integration Second**: [STATE_MANAGER] and business layer updates
**UI Third**: [UI_PATTERN] pattern application
**Testing Throughout**: Continuous testing following established patterns

**Dependencies**: Based on ARCHITECTURE.json component relationships
```

### Memory-Referenced Commands
```markdown
## Build & Test Commands

# From QUICK.md - project-specific commands
[BUILD_COMMAND]           # e.g., "npm run build", "./gradlew build", "make build"
[TEST_COMMAND]            # e.g., "npm test", "./gradlew test", "make test"
[INTEGRATION_TEST]        # e.g., "npm run test:e2e", "./gradlew integrationTest"

# Performance monitoring
# [Include specific monitoring commands from QUICK.md]
```

## Task Generation Framework

### Task 1.0: Foundation (Business Logic Layer)
```markdown
### 1.0 [Business Logic Implementation] ([PATTERN_NAME])
**Goal**: Implement core business logic following [PATTERN_NAME] pattern
**Files**: [Specific files from FILES.json]
**Pattern**: [PATTERN_NAME] from PATTERNS.md
**Integration**: [STATE_MANAGER] updates from ARCHITECTURE.json

- [ ] 1.1 - complexity [X]/5 - Create [FeatureName][Component] class/module
  - **File**: [File from FILES.json:line]
  - **Pattern Reference**: [ExampleFile.ext:line]
  - **Template**:
    ```[language]
    # Copy pattern template from PATTERNS.md
    class [FeatureName][Component]:
        def __init__(self, dependencies):
            # Implementation following pattern
            pass
    ```
  - **Testing**: Unit tests following [Test file from FILES.json]

- [ ] 1.2 - complexity [X]/5 - Integrate with [STATE_MANAGER]
  - **File**: [StateManager file from FILES.json:line]
  - **Action**: Add new state types for feature
  - **Pattern**: State management pattern from ARCHITECTURE.json
  - **Validation**: Verify state updates trigger appropriate responses
```

### Task 2.0: Service/Integration Layer (If Applicable)
```markdown
### 2.0 [Service Integration] ([INTEGRATION_PATTERN])
**Goal**: Integrate feature with [SERVICE_LAYER] using [INTEGRATION_PATTERN]
**Files**: [Service files from FILES.json]
**Pattern**: [INTEGRATION_PATTERN] from PATTERNS.md
**Performance Target**: [Target from BUSINESS.json]

- [ ] 2.1 - complexity [X]/5 - Add service integration points
  - **File**: [Service file from FILES.json:line]
  - **Pattern Reference**: [ExampleService.ext:line]
  - **Implementation**: [Copy template from PATTERNS.md]
  - **Integration**: [Specific integration approach from ARCHITECTURE.json]
```

### Task 3.0: UI Implementation ([UI_PATTERN])
```markdown
### 3.0 [UI Implementation] ([UI_PATTERN])
**Goal**: Create UI components following [UI_PATTERN] pattern
**Files**: [UI files from FILES.json]
**Pattern**: [UI_PATTERN] from PATTERNS.md
**Testing**: UI tests following established patterns

- [ ] 3.1 - complexity [X]/5 - Create UI component
  - **File**: [UI component file from FILES.json:line]
  - **Pattern Reference**: [ExampleComponent.ext:line]
  - **Template**: [Copy from PATTERNS.md UI template]
  - **State Source**: [Integration from Task 1.0]
```

### Task 4.0: Data Layer (Repository Pattern)
```markdown
### 4.0 [Data Integration] (Repository Pattern)
**Goal**: Implement data persistence following Repository pattern
**Files**: [Repository files from FILES.json]
**Pattern**: Repository from PATTERNS.md
**Caching**: [Cache strategy from ARCHITECTURE.json]

- [ ] 4.1 - complexity [X]/5 - Create repository implementation
  - **File**: [Repository file from FILES.json:line]
  - **Pattern Reference**: [ExampleRepository.ext:line]
  - **Template**: [Repository template from PATTERNS.md]
  - **Error Handling**: [Error handling pattern from existing code]
```

### Task 5.0: Asset & Resource Tasks (When Required)
```markdown
### 5.0 Asset Requirements (Planning Task)
**When to include**: Feature requires new or modified visual/media assets
**Goal**: Identify and acquire all required assets for feature
**Decision Point**: User decides whether to create internally or outsource

- [ ] 5.1 - complexity 1/5 - Asset requirements analysis
  - **Required Assets**: [List all assets needed]
  - **Specifications**: [Sizes, formats, variations needed]
  - **Source Options**: [Internal creation / External designer / Existing library]
  - **Decision**: [User specifies approach]

- [ ] 5.2 - complexity [varies] - Asset acquisition/creation
  - **Approach**: [Based on user decision]
  - **Validation**: Assets meet specification requirements

- [ ] 5.3 - complexity 2/5 - Asset integration and verification
  - **Integration**: Place assets in correct project locations
  - **Build Verification**: Confirm assets load correctly
  - **Visual Verification**: Verify assets display as expected
```

### Task 6.0: Configuration & Secrets (When Required)
```markdown
### 6.0 Configuration Updates (Configuration Pattern)
**Goal**: Update all required configuration files for feature
**Security Check**: Verify no secrets committed to version control

- [ ] 6.1 - complexity 1/5 - Identify configuration changes
  - **Configuration Files**: [List all config files affected]
  - **Security Review**: Identify any sensitive values

- [ ] 6.2 - complexity 2/5 - Update configuration files
  - **Files**: [Specific config files to modify]
  - **Security**: Ensure secrets use proper secure storage
  - **Validation**: Verify configuration loads correctly
```

### Task 7.0: Breaking Changes & Migration (When Required)
```markdown
### 7.0 Breaking Change Implementation
**Goal**: Implement breaking change with migration path
**User Impact**: [HIGH/MEDIUM/LOW]
**Migration Required**: [YES/NO]

- [ ] 7.1 - complexity 3/5 - Implement breaking change
  - **What's Breaking**: [Explicit description]
  - **Old Behavior**: [What used to work]
  - **New Behavior**: [What works now]

- [ ] 7.2 - complexity 3/5 - Migration implementation
  - **Migration Path**: [How to transition]
  - **Data Migration**: [If applicable]

- [ ] 7.3 - complexity 2/5 - Migration testing
  - **Old State Test**: Verify old state detected correctly
  - **Migration Test**: Verify migration executes successfully
  - **New State Test**: Verify new state works correctly
```

### Task X.0: Memory System Update (MANDATORY FINAL TASK)
```markdown
### [X.0] Memory System Update (MANDATORY)
**CRITICAL RULE**: Do NOT create separate sprint completion files
**UPDATE RULE**: Integrate ALL sprint info into existing 8 core files only

- [ ] X.1 - complexity 1/5 - Verify no sprint completion files created
  - **Check**: .ai/ directory should contain ONLY these 8 files:
    - ARCHITECTURE.json, BUSINESS.json, FILES.json
    - PATTERNS.md, QUICK.md, README.md
    - SPRINT_UPDATE.md, TODO.md
  - **Action**: Delete any additional files (like SPRINT_X_COMPLETION.md)
  - **Goal**: Keep memory system at ~3000 lines across 8 core files

- [ ] X.2 - complexity 2/5 - Update BUSINESS.json
  - **File**: .ai/BUSINESS.json
  - **Update meta.lastUpdated**: Set to current date
  - **New features**: Add to appropriate section
  - **Integration points**: Add new services/APIs

- [ ] X.3 - complexity 2/5 - Update FILES.json
  - **File**: .ai/FILES.json
  - **Update meta.lastUpdated**: Set to current date
  - **New files**: Add to byPurpose categories
  - **Line number references**: Update if code moved

- [ ] X.4 - complexity 3/5 - Update PATTERNS.md (if new patterns)
  - **File**: .ai/PATTERNS.md
  - **Add new pattern**: Only if genuinely NEW pattern discovered
  - **Pattern template**: Include working code example
  - **Pattern reference**: Link to actual implementation file:line

- [ ] X.5 - complexity 2/5 - Update QUICK.md (if new commands)
  - **File**: .ai/QUICK.md
  - **New commands**: Add development/debugging commands
  - **File references**: Update if key file locations changed

- [ ] X.6 - complexity 2/5 - Update TODO.md
  - **File**: .ai/TODO.md
  - **Move completed sprint**: From Current to Completed section
  - **Add completion date**: Document when sprint finished
  - **Sprint summary**: 1-line summary of what was accomplished

- [ ] X.7 - complexity 1/5 - Validate memory system integrity
  - **Line count check**: Total should be ~3000 lines across 8 files
  - **File count check**: Exactly 8 files in .ai/ directory
  - **Meta dates check**: All meta.lastUpdated dates current
```

## Complexity Calibration

### Complexity Rating System
Use existing codebase patterns to calibrate complexity:

**1/5 - Simple**: Data structures, basic components, configuration
- Time: 5-15 minutes

**2/5 - Standard**: Service methods, straightforward UI, repository functions
- Time: 15-45 minutes

**3/5 - Moderate**: Service integration, complex UI, caching
- Time: 45-90 minutes

**4/5 - Complex**: Multi-component integration, new patterns
- Time: 1.5-3 hours

**5/5 - System-Wide**: Core architecture changes, new paradigms
- Time: 3+ hours

## Security Review Checklist (For Security-Sensitive Tasks)

**Applies to tasks involving:**
- Authentication or authorization
- User data handling
- API keys or credentials
- Database security rules
- Permissions

**Checklist:**
- [ ] No secrets committed to git
- [ ] API keys properly secured (environment variables, secret management)
- [ ] Database security rules updated appropriately
- [ ] User data access follows principle of least privilege
- [ ] Authentication flows tested with edge cases
- [ ] Permission requests justified and documented

## Success Metrics

### Task Quality
- **Specificity**: 100% of tasks include exact file and line references
- **Pattern Compliance**: All implementations follow templates from PATTERNS.md
- **Architecture Alignment**: Zero conflicts with ARCHITECTURE.json constraints
- **Implementation Readiness**: Zero additional research time needed

### Development Speed
- **Task Generation**: Under 5 minutes from PRD to saved task list
- **Implementation Start**: Immediate - no file searching or pattern research
- **Build Success**: 90%+ first-attempt success rate
- **Pattern Reuse**: 95%+ of implementations use existing patterns

---

## Final Step: Save the Task List

**MANDATORY FINAL ACTION:**

After generating the complete task list following all the rules above:

1. **Determine filename:** Use the same name as the source PRD
2. **Save to file:** Use the Write tool to save to `/tasks/tasks-[prd-name].md`
3. **Confirm to user:** Tell the user the task list has been saved and provide the file path

**Example:**
```
Source PRD: /tasks/prd-user-authentication.md
Generated task list saved to: /tasks/tasks-user-authentication.md
```

**DO NOT** just output the task list to the screen. It MUST be saved to a file.

---

**This system transforms generic task generation into memory-driven, pattern-specific implementation planning with instant architectural awareness.**
