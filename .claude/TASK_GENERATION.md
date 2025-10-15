# AI-Optimized Task Generation Rules

*Memory-driven task breakdown for instant implementation readiness*

## Core Philosophy

Transform PRDs into **pattern-specific, file-targeted task lists** that leverage comprehensive architectural knowledge. Generate tasks that are immediately implementable using established patterns with zero additional research time.

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
Map each PRD component to established patterns:
- **Business Logic** → [PRIMARY_PATTERN] # e.g., "Service pattern (UserService.ext:148)"
- **UI Components** → [UI_PATTERN] # e.g., "MVVM pattern (ViewModel.ext:45)" or "Component pattern (HeaderComponent.ext:23)"
- **Data Persistence** → [REPOSITORY_PATTERN] # e.g., "Repository pattern (UserRepository.ext:67)"
- **API Integration** → [INTEGRATION_PATTERN] # e.g., "HTTP client pattern (ApiClient.ext:171)" or "Caching pattern (CacheService.ext:89)"

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
**Integration Second**: [STATE_MANAGER] and [BUSINESS_LAYER] updates # e.g., "State management and service layer updates"
**UI Third**: [UI_PATTERN] pattern application # e.g., "MVVM pattern" or "Component-based UI"
**Testing Throughout**: Continuous testing following established patterns

**Dependencies**: Based on ARCHITECTURE.json component relationships
```

### Memory-Referenced Commands
```markdown
## Build & Test Commands

# From QUICK.md - project-specific commands
[BUILD_COMMAND]           # e.g., "./gradlew build" or "npm run build"
[TEST_COMMAND]            # e.g., "./gradlew test" or "npm test"
[INTEGRATION_TEST]        # e.g., "./gradlew integrationTest" or "npm run test:e2e"

# Performance monitoring
# [Include specific monitoring commands from QUICK.md]
```

## Task Generation Framework

### Task 1.0: Foundation (Business Logic Layer)
```markdown
### 1.0 [Business Logic Implementation] ([PATTERN_NAME])
**Goal**: Implement core business logic following [PATTERN_NAME] pattern # e.g., "Service pattern", "Manager pattern", "Use case pattern"
**Files**: [Specific files from FILES.json]
**Pattern**: [PATTERN_NAME] from PATTERNS.md
**Integration**: [STATE_MANAGER] updates from ARCHITECTURE.json # e.g., "Redux store updates", "State coordinator updates"

- [ ] 1.1 - complexity [X]/5 - Create [FeatureName][Component] interface/class # e.g., "UserService", "AuthManager", "OrderProcessor"
  - **File**: [File from FILES.json:line]
  - **Pattern Reference**: [ExampleFile.ext:line] # e.g., "UserService.ts:148"
  - **Template**:
    ```[language]
    [DEPENDENCY_INJECTION_DECORATOR]  # e.g., "@Injectable()" or "@Singleton" or "class with constructor"
    class [FeatureName][Component] [IMPLEMENTS] [Interface] {
        constructor(
            [dependencies from ARCHITECTURE.json]
        ) {}
        // [Implementation following pattern from PATTERNS.md]
    }
    ```
  - **Testing**: Unit tests following [Test file from FILES.json]

- [ ] 1.2 - complexity [X]/5 - Integrate with [STATE_MANAGER]
  - **File**: [StateManager file from FILES.json:line] # e.g., "store/index.ts:67" or "StateCoordinator.ts:45"
  - **Action**: Add new state types for feature
  - **Pattern**: State management pattern from ARCHITECTURE.json
  - **Validation**: Verify state updates trigger UI changes correctly
```

### Task 2.0: Service/Integration Layer (If Applicable)
```markdown
### 2.0 [Service Integration] ([INTEGRATION_PATTERN])
**Goal**: Integrate feature with [SERVICE_LAYER] using [INTEGRATION_PATTERN] # e.g., "background service", "middleware", "API layer"
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
**Goal**: Create UI components following [UI_PATTERN] # e.g., "MVVM", "Component-based", "MVC"
**Files**: [UI files from FILES.json]
**Pattern**: [UI_PATTERN] from PATTERNS.md
**Testing**: UI tests following established patterns

- [ ] 3.1 - complexity [X]/5 - Create [UI_COMPONENT_TYPE] # e.g., "component", "view", "screen", "composable"
  - **File**: [UI component file from FILES.json:line]
  - **Pattern Reference**: [ExampleComponent.ext:line]
  - **Template**: [Copy from PATTERNS.md [UI_PATTERN] template]
  - **State Source**: [Business logic integration from Task 1.0]
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
  - **Error Handling**: [ERROR_PATTERN] # e.g., "Result<T> pattern", "try/catch with custom errors"
```

## Advanced AI Optimization Features

### 1. **Complexity Calibration**
Use existing codebase patterns to calibrate complexity ratings:
- **1/5**: Simple data class or basic UI component
- **2/5**: Business logic method or repository function
- **3/5**: Service integration or complex UI logic
- **4/5**: New architectural pattern or multi-component integration
- **5/5**: System-wide changes or novel algorithm implementation

### 2. **Pattern-Specific Error Handling**
```markdown
**Error Handling Strategy**: [Pattern] from PATTERNS.md
- **Type**: [ERROR_PATTERN] for business logic # e.g., "Result<T>", "Either<Error, Success>", "OperationResult<T>"
- **UI**: State-based error display (from UI patterns)
- **Network**: Retry logic following [Network pattern from memory]
- **Testing**: Error scenario tests (from test patterns)
```

### 3. **Performance Integration**
Every task includes performance consideration:
```markdown
**Performance Impact**: [Specific impact on BUSINESS.json targets]
**Monitoring**: [Analytics/monitoring integration following established pattern]
**Optimization**: [Specific optimization approach from memory system]
```

### 4. **Memory-Referenced Testing**
```markdown
**Testing Strategy**: Following [Test pattern from PATTERNS.md]
**Test Files**: [Specific test files from FILES.json]
**Coverage Target**: [Target from BUSINESS.json requirements]
**Integration Tests**: [Pattern from existing integration tests]
```

## Task Generation Quality Gates

### Pre-Generation Validation
- [ ] **Pattern Mapping**: Every component maps to pattern in PATTERNS.md
- [ ] **File Targeting**: All tasks reference specific files from FILES.json
- [ ] **Architecture Compliance**: Follows constraints from ARCHITECTURE.json
- [ ] **Performance Alignment**: Meets targets from BUSINESS.json

### Task Quality Checklist
- [ ] **File Specificity**: Includes exact file paths and line numbers
- [ ] **Pattern Reference**: References template from PATTERNS.md
- [ ] **Integration Clarity**: Specifies connections from ARCHITECTURE.json
- [ ] **Complexity Accuracy**: Ratings calibrated to existing codebase
- [ ] **Test Coverage**: Clear testing approach with pattern reference

## Memory-Enhanced Output Template

```markdown
# Task List: [Feature Name]

**Generated from**: `[prd-file-name].md`
**Architecture Pattern**: [Pattern from PATTERNS.md]
**Core Integration**: [STATE_MANAGER updates from ARCHITECTURE.json]
**Target Performance**: [Target from BUSINESS.json]
**File Scope**: [Primary files from FILES.json]

## Memory System Analysis

**Architectural Context**: [Summary from ARCHITECTURE.json]
**Implementation Patterns**: [Relevant patterns from PATTERNS.md]
**File Dependencies**: [Relationships from FILES.json]
**Performance Baseline**: [Current targets from BUSINESS.json]

## Implementation Strategy

**Phase 1**: [Business logic layer using [PATTERN_NAME]]
**Phase 2**: [Service integration using [INTEGRATION_PATTERN]]
**Phase 3**: [UI implementation using [UI_PATTERN]]
**Phase 4**: [Data layer using Repository pattern]

**Build Verification**: After each phase using commands from QUICK.md

## Development Commands

# From QUICK.md - project-specific
[BUILD_COMMAND]           # e.g., "npm run build", "./gradlew build", "cargo build"
[TEST_COMMAND]            # e.g., "npm test", "./gradlew test", "cargo test"
[INTEGRATION_TEST]        # e.g., "npm run test:e2e", "./gradlew integrationTest"

# Performance monitoring
# [Specific commands from QUICK.md]

## Tasks

### 1.0 [Business Logic Implementation] ([PATTERN_NAME])
**Goal**: [Specific goal aligned with PRD]
**Files**: [Exact files from FILES.json with line references]
**Pattern**: [PATTERN_NAME] ([ExampleFile.ext:line])
**Integration**: [STATE_MANAGER] updates ([StateFile.ext:line])

- [ ] 1.1 - complexity [X]/5 - [Specific task]
  - **File**: [Exact file from FILES.json:line]
  - **Pattern Template**: [Copy-paste code from PATTERNS.md]
  - **Integration Method**: [Approach from ARCHITECTURE.json]
  - **Testing**: [Test pattern from existing tests]
  - **Verification**: [Specific success criteria]

[Continue with pattern-specific tasks...]

### [X.0] Documentation Generation (Analysis-Based)
**Goal**: Create comprehensive feature documentation using implementation analysis
**Pattern**: Documentation pattern from PATTERNS.md
**Analysis Source**: Completed implementation and PRD comparison

- [ ] [X.1] - complexity 2/5 - Analyze implementation against PRD
  - **Source**: [PRD file] and completed task list
  - **Template**: [Documentation analysis template from PATTERNS.md]
  - **Extract**: Goals achieved, technical decisions, deviations

- [ ] [X.2] - complexity 3/5 - Generate technical architecture documentation
  - **File**: `docs/[feature-name]-technical-architecture.md`
  - **Pattern**: [Architecture documentation pattern from PATTERNS.md]
  - **Include**: Component relationships, data flows, integration points

[Continue with documentation tasks...]
```

## AI Assistant Instructions

### 1. **Memory-First Task Generation**
```
BEFORE generating tasks:
1. Read ARCHITECTURE.json → Map PRD components to architectural patterns
2. Read FILES.json → Identify target files and dependencies
3. Read PATTERNS.md → Select implementation templates
4. Read BUSINESS.json → Extract performance and feature constraints
5. Read QUICK.md → Get development and testing commands
```

### 2. **Pattern-Specific Task Creation**
```
For each PRD component:
1. Map to pattern from PATTERNS.md
2. Find target files from FILES.json with line numbers
3. Include pattern template with specific implementation
4. Add integration points from ARCHITECTURE.json
5. Include testing approach from established patterns
```

### 3. **Implementation-Ready Output**
```
Every task must include:
- **File Reference**: [ActualFile.ext:lineNumber] from FILES.json
- **Pattern Template**: Copy-paste code from PATTERNS.md
- **Integration Method**: Specific approach from ARCHITECTURE.json
- **Testing Strategy**: Following existing test patterns
- **Performance Impact**: Against targets from BUSINESS.json
```

### 4. **Quality Assurance**
```
Generated tasks pass these checks:
- [ ] 100% of tasks reference real files from memory system
- [ ] All patterns map to templates in PATTERNS.md
- [ ] Integration points match ARCHITECTURE.json relationships
- [ ] Performance considerations align with BUSINESS.json targets
- [ ] Development commands sourced from QUICK.md
```

### 5. **Security Review Checklist** (For Security-Sensitive Tasks)

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
- [ ] Security implications documented in task notes

## Success Metrics

### Task Quality
- **Specificity**: 100% of tasks include exact file and line references
- **Pattern Compliance**: All implementations follow templates from PATTERNS.md
- **Architecture Alignment**: Zero conflicts with ARCHITECTURE.json constraints
- **Implementation Readiness**: Zero additional research time needed

### Development Speed
- **Task Generation**: Under 3 minutes from PRD to saved task list
- **Implementation Start**: Immediate - no file searching or pattern research
- **Build Success**: 90%+ first-attempt success rate using memory-referenced commands
- **Pattern Reuse**: 95%+ of implementations use existing patterns

## Example: Memory-Enhanced Task Generation

**Input PRD**: [FEATURE_REQUEST] # e.g., "User preference settings with API integration"

**Memory Consultation Results**:
- `ARCHITECTURE.json` → [ARCHITECTURE_INFO] # e.g., "Layered architecture with service layer and repository pattern"
- `FILES.json` → [KEY_FILES] # e.g., "UserService.ts:148, PreferencesRepository.ts:23, ApiClient.ts:171"
- `PATTERNS.md` → [APPLICABLE_PATTERNS] # e.g., "Service pattern + Repository pattern"
- `BUSINESS.json` → [BUSINESS_REQUIREMENTS] # e.g., "User settings feature, sub-500ms response target"
- `QUICK.md` → Build commands and debugging approaches

**Generated Tasks** (sample):
```markdown
### 1.0 Service Implementation (Service Pattern)
**Files**: UserService.ts:148, PreferencesModel.ts:23
**Pattern**: Service pattern (PATTERNS.md template)
**Performance Target**: Sub-500ms response (BUSINESS.json)

- [ ] 1.1 - complexity 3/5 - Add preference management to UserService
  - **File**: UserService.ts:148
  - **Template**: [Service pattern from PATTERNS.md]
  - **Integration**: StateManager.ts:67 for preference state updates
  - **Cache Strategy**: [Caching pattern from CacheService.ts:89]
```

**Result**: Implementation-ready tasks with exact file references, pattern templates, and integration approaches - generated in under 2 minutes.

## Task Categories by Architecture Layer

### 1. **Business Logic Layer Tasks**
```markdown
**Pattern**: [PRIMARY_PATTERN] (PATTERNS.md template) # e.g., "Service pattern", "Manager pattern", "Use case pattern"
**Files**: [Business logic files from FILES.json]
**Integration**: [STATE_MANAGER] updates (ARCHITECTURE.json)
**Testing**: Unit tests (existing pattern)
```

### 2. **Service/Integration Layer Tasks** (If Applicable)
```markdown
**Pattern**: [INTEGRATION_PATTERN] (PATTERNS.md template) # e.g., "Middleware", "Background service", "API integration"
**Files**: [Service files from FILES.json]
**Integration**: [SERVICE_INTEGRATION] (ARCHITECTURE.json)
**Performance**: Service optimization (BUSINESS.json)
```

### 3. **Network/API Layer Tasks** (If Applicable)
```markdown
**Pattern**: [API_PATTERN] or Repository (PATTERNS.md) # e.g., "HTTP client", "GraphQL client", "REST API"
**Files**: [Network files from FILES.json]
**Integration**: Cache coordination (ARCHITECTURE.json)
**Performance**: API response targets (BUSINESS.json)
```

### 4. **UI Layer Tasks**
```markdown
**Pattern**: [UI_PATTERN] (PATTERNS.md) # e.g., "MVVM", "Component-based", "MVC"
**Files**: [UI files from FILES.json]
**Integration**: State observation (ARCHITECTURE.json)
**Testing**: UI integration tests (existing pattern)
```

### 5. **Data Layer Tasks**
```markdown
**Pattern**: Repository (PATTERNS.md)
**Files**: [Data files from FILES.json]
**Integration**: Database/storage sync (ARCHITECTURE.json)
**Error Handling**: [ERROR_PATTERN] # e.g., "Result<T> pattern"
```

### 6. **Asset & Resource Tasks** (When Required)
```markdown
**When to include**: Feature requires new or modified visual/media assets
**Approach**: Identify requirements, user decides implementation method
**Options**: Internal (AI tools), external (designer), or hybrid

### X.0 Asset Requirements (Planning Task)
**Goal**: Identify and acquire all required assets for feature
**Decision Point**: User decides whether to create internally or outsource
**Validation**: Assets meet requirements and integrate successfully

- [ ] X.1 - complexity 1/5 - Asset requirements analysis
  - **Required Assets**: [List all assets needed]
  - **Specifications**: [Sizes, formats, variations needed]
  - **Source Options**: [Internal creation / External designer / Existing library]
  - **Decision**: [User specifies approach]

- [ ] X.2 - complexity [varies] - Asset acquisition/creation
  - **Approach**: [Based on user decision]
  - **Internal**: User may ask AI to assist with tool scripts/generation
  - **External**: User handles outsourcing, provides assets
  - **Validation**: Assets meet specification requirements

- [ ] X.3 - complexity 2/5 - Asset integration and verification
  - **Integration**: Place assets in correct project locations
  - **Build Verification**: Confirm assets load correctly
  - **Visual Verification**: Verify assets display as expected
  - **Cleanup**: Remove any conflicting or obsolete assets
```

### 7. **Configuration & Secrets Tasks** (When Required)
```markdown
**Pattern**: Configuration management pattern
**Files**: Config files, resource values, environment configs, build configs
**Security**: Never commit secrets or credentials

### X.0 Configuration Updates (Configuration Pattern)
**Goal**: Update all required configuration files for feature
**Security Check**: Verify no secrets committed to version control
**Validation**: Build success + functional test

- [ ] X.1 - complexity 1/5 - Identify configuration changes
  - **Configuration Files**: [List all config files affected]
  - **External Configs**: [API configs, service configs, etc.]
  - **Resource Values**: [String resources, constants, etc.]
  - **Security Review**: Identify any sensitive values

- [ ] X.2 - complexity 2/5 - Update configuration files
  - **Files**: [Specific config files to modify]
  - **Changes**: [List configuration changes needed]
  - **Security**: Ensure secrets use proper secure storage
  - **Validation**: Verify configuration loads correctly

- [ ] X.3 - complexity 2/5 - Build system configuration
  - **Build Files**: [Build configuration files if needed]
  - **Dependencies**: [New dependencies or version changes]
  - **Environment**: [Environment-specific configuration]
  - **Security**: BuildConfig/environment secrets properly managed
```

### 8. **Breaking Changes & Migration Tasks** (When Required)
```markdown
**Pattern**: Migration pattern
**Impact**: High - affects existing users
**Testing**: Extra validation required

### X.0 Breaking Change Implementation
**Goal**: Implement breaking change with migration path
**User Impact**: [HIGH/MEDIUM/LOW]
**Migration Required**: [YES/NO]
**Rollback Plan**: [Brief description]

- [ ] X.1 - complexity 3/5 - Implement breaking change
  - **What's Breaking**: [Explicit description]
  - **Old Behavior**: [What used to work]
  - **New Behavior**: [What works now]
  - **Affected Users**: [All users / Subset]

- [ ] X.2 - complexity 3/5 - Migration implementation
  - **Migration Path**: [How to transition]
  - **Data Migration**: [If applicable]
  - **User Communication**: [How users learn about change]

- [ ] X.3 - complexity 2/5 - Migration testing
  - **Old State Test**: Verify old state detected correctly
  - **Migration Test**: Verify migration executes successfully
  - **New State Test**: Verify new state works correctly
```

## Advanced AI Features

### 1. **Dependency Auto-Resolution**
```json
// From FILES.json dependencies
"NewFeatureComponent.ext": {
  "depends_on": ["StateManager.ext:67", "AuthService.ext:45"],
  "modifies": ["MainService.ext:123"],
  "tests": "NewFeatureComponent.test.ext"
}
```

### 2. **Performance Impact Analysis**
```markdown
**Performance Analysis**: [Feature impact on BUSINESS.json targets]
- **API Calls**: [Expected increase/decrease in API usage]
- **Memory**: [Memory/state management impact]
- **Cache**: [Caching strategy effectiveness]
- **UI**: [UI rendering impact]
```

### 3. **Pattern Compliance Verification**
```markdown
**Pattern Verification Checklist**:
- [ ] [PRIMARY_PATTERN]: [Key pattern requirements] # e.g., "Service: @Injectable annotation, dependency injection"
- [ ] [UI_PATTERN]: [Key pattern requirements] # e.g., "MVVM: ViewModel separation, data binding"
- [ ] Repository: [ERROR_PATTERN] return types, error handling # e.g., "Result<T>"
- [ ] [CACHING_PATTERN]: [Caching requirements if applicable]
```

### 4. **Integration Point Mapping**
```markdown
**Integration Requirements**: [From ARCHITECTURE.json]
- **[STATE_MANAGER]**: [Specific state updates needed]
- **[DATABASE/API]**: [Data structure and endpoints]
- **[EXTERNAL_SERVICE]**: [Integration requirements and patterns]
- **UI**: [UI state observation patterns]
```

## Memory-Driven Complexity Calibration

### Complexity Rating System (Project-Specific)
Based on existing codebase analysis:

**1/5 - Simple**: Data classes, basic UI components, configuration updates
- Example: Adding new enum value or simple data model
- Time: 5-15 minutes

**2/5 - Standard**: Business logic methods, repository functions, straightforward UI
- Example: New method following existing pattern
- Time: 15-45 minutes

**3/5 - Moderate**: Service integration, complex UI, cache modifications
- Example: Adding new integration point or complex UI logic
- Time: 45-90 minutes

**4/5 - Complex**: Multi-component integration, new architectural patterns
- Example: New feature with full integration across layers
- Time: 1.5-3 hours

**5/5 - System-Wide**: Core architecture changes, new service patterns
- Example: New architectural pattern implementation
- Time: 3+ hours

## Documentation Task Enhancement

### Final Documentation Task Structure
```markdown
### [X.0] Implementation Documentation (Analysis-Based)
**Goal**: Generate comprehensive documentation from implementation analysis
**Pattern**: Documentation generation from PATTERNS.md
**Source**: Completed implementation + PRD comparison

- [ ] [X.1] - complexity 2/5 - Implementation analysis against PRD
  - **Source Files**: [All modified files from task list]
  - **Analysis Template**: [Documentation pattern from PATTERNS.md]
  - **Output**: Implementation summary with deviations noted

- [ ] [X.2] - complexity 3/5 - Technical architecture documentation
  - **File**: `docs/[feature-name]-technical-architecture.md`
  - **Template**: [Architecture doc template from PATTERNS.md]
  - **Content**: Component relationships, data flows, integration points

- [ ] [X.3] - complexity 2/5 - API and interface documentation
  - **Analysis**: All public methods and interfaces from implementation
  - **Pattern**: [API documentation pattern from PATTERNS.md]
  - **Reference**: Existing API docs in project

- [ ] [X.4] - complexity 2/5 - Usage examples and integration guide
  - **Template**: [Usage documentation from PATTERNS.md]
  - **Examples**: Based on actual implementation patterns
  - **Integration**: How to use with existing features

- [ ] [X.5] - complexity 2/5 - Update AI memory system (MANDATORY)
  - **CRITICAL RULE**: Do NOT create separate sprint completion files
  - **UPDATE RULE**: Integrate ALL sprint info into existing core files only
  - **Template**: Follow SPRINT_UPDATE.md exactly
  - **Goal**: Keep .ai/ folder at ~3000 lines across 8 core files

### [X.6] Memory System Update Details (MANDATORY SUB-TASKS)

- [ ] X.6.1 - complexity 1/5 - Verify no sprint completion files created
  - **Check**: ls .ai/ should show ONLY these 8 files:
    - ARCHITECTURE.json, BUSINESS.json, FILES.json
    - PATTERNS.md, QUICK.md, README.md
    - SPRINT_UPDATE.md, TODO.md
  - **Action**: If ANY other files exist (like SPRINT_X_COMPLETION.md), DELETE them
  - **Reason**: Memory system must be condensed (8 files, ~3000 lines total)

- [ ] X.6.2 - complexity 2/5 - Update BUSINESS.json
  - **File**: .ai/BUSINESS.json
  - **Update meta.lastUpdated**: Set to current date
  - **Update meta.version**: Increment version
  - **Update meta.description**: Include sprint name if major feature
  - **New features**: Add to appropriate section
  - **User flows**: Update if workflows changed
  - **Security**: Update authentication/security sections if changed
  - **Integration points**: Add new database/API services

- [ ] X.6.3 - complexity 2/5 - Update FILES.json
  - **File**: .ai/FILES.json
  - **Update meta.lastUpdated**: Set to current date
  - **Update meta.totalFiles**: Increment count
  - **New files**: Add to byPurpose categories
  - **New purpose categories**: Add if new functional area
  - **Authentication**: Ensure auth section current if auth changes

- [ ] X.6.4 - complexity 3/5 - Update PATTERNS.md (if new patterns)
  - **File**: .ai/PATTERNS.md
  - **Add new pattern**: Only if genuinely NEW pattern discovered
  - **Pattern template**: Include working code example
  - **When to use**: Clear guidance on pattern application
  - **Pattern reference**: Link to actual implementation file:line

- [ ] X.6.5 - complexity 2/5 - Update QUICK.md (if new commands)
  - **File**: .ai/QUICK.md
  - **New commands**: Add development/debugging commands
  - **File references**: Update if key file locations changed
  - **Performance tips**: Add optimization techniques discovered

- [ ] X.6.6 - complexity 2/5 - Update TODO.md
  - **File**: .ai/TODO.md
  - **Move completed sprint**: From Current to Completed section
  - **Add completion date**: Document when sprint finished
  - **Sprint summary**: 1-line summary of what was accomplished
  - **Next sprint preview**: Add upcoming sprint to "Upcoming Sprint" section

- [ ] X.6.7 - complexity 1/5 - Validate memory system integrity
  - **Line count check**: Total should be ~3000 lines across 8 files
  - **File count check**: Exactly 8 files in .ai/ directory
  - **Meta dates check**: All meta.lastUpdated dates current
  - **Reference validation**: Spot-check that file:line references are accurate
```

## Output Specifications

### File Requirements
- **Format**: Markdown (.md)
- **Location**: `/tasks/`
- **Filename**: `tasks-[prd-file-name].md` (kebab-case)
- **Memory References**: Include file paths and line numbers from FILES.json
- **Pattern Templates**: Copy-paste ready code from PATTERNS.md

### Quality Standards
- **Implementation Ready**: Zero additional research required
- **Pattern Compliant**: 100% alignment with established patterns
- **Architecture Aware**: Full integration with existing system
- **Performance Conscious**: Aligned with current targets and constraints

---

**This system transforms generic task generation into memory-driven, pattern-specific implementation planning with instant architectural awareness and zero research overhead.**
