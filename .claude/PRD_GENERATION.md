# AI-Optimized PRD Generation Rules

*Leveraging AI Memory System for Rapid, Accurate Product Requirements*

## Core Philosophy

Generate PRDs that are **instantly implementable** by leveraging the comprehensive AI memory system. Focus on **architectural integration** and **pattern-based implementation** rather than generic requirements.

## Pre-Generation Memory Consultation

### 1. **Memory System Freshness Check** (MANDATORY)
Before starting PRD generation:
- [ ] Check meta.lastUpdated dates in ARCHITECTURE.json, BUSINESS.json, FILES.json
- [ ] If dates > 1 sprint old, STOP and update memory system first
- [ ] Memory system must be current to ensure accurate pattern references

**Why**: Stale memory leads to incorrect file references and outdated patterns.

### 2. **Architecture Analysis** (Required)
Before asking any questions, consult:
- **`ARCHITECTURE.json`** → Understand integration points and constraints
- **`BUSINESS.json`** → Check existing features and performance targets
- **`FILES.json`** → Identify relevant files and dependencies
- **`PATTERNS.md`** → Find applicable implementation patterns

### 3. **Context-Aware Questioning**
Ask questions informed by memory system:
- Reference existing patterns: "Should this follow the [PATTERN_NAME] pattern like [EXAMPLE_COMPONENT]?" # e.g., "Service pattern like UserService"
- Leverage architecture knowledge: "Given the [ARCHITECTURE_PATTERN], will this need [INTEGRATION_POINT]?" # e.g., "Given the layered architecture, will this need database integration?"
- Use performance baselines: "The current [METRIC] target is [TARGET_VALUE] - does this need similar performance?" # e.g., "API response target is <200ms"

## Streamlined Question Process

### Round 1: Memory-Informed Questions (3-5 questions max)
Based on memory system analysis, ask only the **gap-filling questions**:

**Architecture Integration:**
- "Looking at the current [ARCHITECTURE_PATTERN], should this integrate with [EXISTING_COMPONENT] or be [ALTERNATIVE_APPROACH]?" # e.g., "layered architecture, should this integrate with the service layer or be controller-only?"
- "Given the [STATE_MANAGEMENT] architecture, what new state types will this feature need?" # e.g., "Redux/Vuex/Context architecture"

**Pattern Application:**
- "Should this follow the [specific pattern from PATTERNS.md] like [existing component]?" # e.g., "Repository pattern like UserRepository"
- "Does this need [DATABASE/API] integration following the [PATTERN_NAME] pattern?" # e.g., "database integration following the Repository pattern"

**Business Logic Integration:**
- "How does this relate to the existing [CORE_FEATURE] system and [ARCHITECTURE]?" # e.g., "user authentication system and role-based access control"
- "Should this integrate with the [CACHING/PERFORMANCE] system for [OPTIMIZATION]?" # e.g., "caching system for API calls"

### Round 2: Clarification Only (if needed)
Only ask follow-up questions if Round 1 reveals:
- **New architectural patterns** not covered in memory system
- **Integration complexity** beyond existing patterns
- **Performance requirements** different from established targets

## AI-Optimized PRD Structure

### Header with Memory References
```markdown
# PRD: [Feature Name]

**Generated:** [Date]
**Architecture Pattern:** [Pattern from PATTERNS.md]
**Integration Points:** [References from ARCHITECTURE.json]
**Implementation Files:** [Key files from FILES.json]
```

### Memory-Enhanced Sections

#### 1. Overview
```markdown
## Overview
[Brief description]

**Architecture Integration:** Leverages [existing pattern] from [memory reference]
**Performance Target:** [Target based on BUSINESS.json benchmarks]
**Implementation Strategy:** [Pattern application from memory system]
```

#### 2. Feature Components (Architecture-Mapped)
Instead of generic components, map directly to architecture layers:

```markdown
## Feature Components

### Component 1: [Business Logic Layer Integration]
**Pattern:** [PATTERN_NAME] (following [EXAMPLE_FILE.ext:lineNumber]) # e.g., "Service pattern (following UserService.ts:45)"
**Files:** [Specific files from FILES.json]
**Dependencies:** [Known dependencies from ARCHITECTURE.json]

### Component 2: [Presentation Layer Integration]
**Pattern:** [ARCHITECTURE_PATTERN] based on context # e.g., "MVVM", "Component-based", "MVC"
**Files:** [UI files from FILES.json]
**State Management:** [STATE_MANAGEMENT integration approach] # e.g., "Redux store integration", "Context API", "ViewModel binding"
```

#### 3. Implementation-Ready Requirements
```markdown
## Functional Requirements

### [Component] Requirements

**FR1.1:** The system must [requirement]
- **Implementation File:** [Specific file from FILES.json:line]
- **Pattern Reference:** [Template from PATTERNS.md]
- **Integration Point:** [Connection from ARCHITECTURE.json]
- **Error Handling:** Follow OperationResult<T> pattern
- **Testing:** Unit tests following [existing test pattern]
```

#### 4. Memory-Referenced Technical Considerations
```markdown
## Technical Considerations

### Architecture Alignment
- **[ARCHITECTURE_PATTERN]:** [If applicable - reference integration points] # e.g., "Layered architecture: service layer integration"
- **State Management:** [STATE_MANAGER updates and new state types] # e.g., "Redux store updates", "Context updates"
- **Performance Strategy:** [If applicable - caching/optimization approach] # e.g., "API caching strategy", "database query optimization"

### Pattern Compliance
- **Follow:** [Specific pattern from PATTERNS.md] 
- **Files to Modify:** [Exact files from FILES.json with line references]
- **Dependencies:** [Known constraints from ARCHITECTURE.json]

### Performance Integration
- **Target:** [Specific target from BUSINESS.json performance requirements]
- **Monitoring:** [Analytics integration following CacheAnalyticsService pattern]
```

#### 5. Breaking Changes Analysis (REQUIRED SECTION)
```markdown
## Breaking Changes Analysis

### User Impact Assessment
- [ ] Does this change existing user workflows?
- [ ] Will existing users need to take action (re-auth, migrate data, etc.)?
- [ ] Are there data migrations required?
- [ ] What is the communication plan for users?

### API/Interface Changes
- [ ] Are we removing or changing existing APIs?
- [ ] Will this break existing integrations?
- [ ] Is backward compatibility maintained or possible?

### Data Model Changes
- [ ] Are we changing database schema or data structures?
- [ ] Is data migration required?
- [ ] Can old and new versions coexist during transition?

**Rule**: If ANY breaking change identified, PRD must include migration strategy.
```

#### 6. Security Considerations (REQUIRED SECTION)
```markdown
## Security Considerations

### Authentication & Authorization
- [ ] Does this change authentication flow?
- [ ] Are new permissions required?
- [ ] Is user data access modified?
- [ ] Are database access rules or security policies affected?

### Data Privacy
- [ ] Does this collect new user data?
- [ ] Is PII (Personally Identifiable Information) involved?
- [ ] Are privacy policies affected?

### API Security
- [ ] Are new API keys or credentials needed?
- [ ] Is rate limiting affected?
- [ ] Are there new attack vectors?

**Rule**: Authentication/authorization changes require explicit security review section.
```

#### 7. Asset & Resource Requirements (NEW SECTION)
```markdown
## Asset & Resource Requirements

### Visual Assets
- [ ] New visual assets required? (icons, images, logos, etc.)
- [ ] Asset specifications? (sizes, formats, variations)
- [ ] Asset source? (designer, existing library, AI-generated, etc.)
- [ ] Delivery method? (user decides: internal creation or external sourcing)

### Configuration Assets
- [ ] New configuration files required?
- [ ] Environment-specific configuration needed?
- [ ] Secret management changes?

### Asset Checklist Template
For each asset:
- **Type**: Icon/Image/Logo/Config/Media
- **Specifications**: Sizes/formats/variations required
- **Source**: Where asset comes from
- **Delivery Method**: Internal/external/AI-assisted
- **Location**: Final destination in project
```

#### 8. Implementation Roadmap
```markdown
## Implementation Roadmap

### Phase 1: Foundation ([Pattern] Application)
**Files:** [List from FILES.json]
**Pattern:** [Template from PATTERNS.md]
**Integration:** [Points from ARCHITECTURE.json]

### Phase 2: Integration
**Dependencies:** [Cross-references from memory system]
**Testing:** [Strategy based on existing test patterns]

### Phase 3: Optimization
**Performance:** [Targets from BUSINESS.json]
**Analytics:** [Monitoring approach]
```

## Memory-Driven Validation

### Pre-PRD Validation Checklist
- [ ] **Architecture Alignment:** Follows established patterns from memory system
- [ ] **File References:** Includes specific files and line numbers from FILES.json
- [ ] **Pattern Application:** Maps to templates in PATTERNS.md
- [ ] **Integration Points:** Addresses connections from ARCHITECTURE.json
- [ ] **Performance Targets:** Aligns with benchmarks in BUSINESS.json

### Quality Gates
- **Pattern Compliance:** Every component maps to a pattern from PATTERNS.md
- **File Specificity:** Requirements reference actual files with line numbers
- **Integration Clarity:** All dependencies identified in ARCHITECTURE.json
- **Implementation Ready:** No additional architecture research needed

### Security Review Checklist (For Security-Sensitive Features)

**Applies to features involving:**
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
- [ ] Security implications documented in PRD

## AI Assistant Instructions

### 1. **Memory First Approach**
```
BEFORE asking any questions:
1. Read ARCHITECTURE.json → Understand existing patterns and integration points
2. Read BUSINESS.json → Check current features and constraints  
3. Read FILES.json → Identify relevant files and dependencies
4. Read PATTERNS.md → Find applicable implementation templates
```

### 2. **Context-Aware Questioning**
```
Instead of: "What problem does this solve?"
Ask: "Given the existing [CORE_FEATURE] system, how should this feature integrate with the current [SYSTEM_COMPONENT]?" # e.g., "user authentication system, permission model"

Instead of: "How should this work?"
Ask: "Should this follow the [PATTERN_NAME] pattern like [EXAMPLE_COMPONENT]?" # e.g., "Repository pattern like UserRepository, or Service pattern like AuthService"
```

### 3. **Implementation-Ready Output**
```
Every requirement should include:
- **File Reference:** [Actual file from FILES.json:line]
- **Pattern Template:** [Specific template from PATTERNS.md]
- **Integration Method:** [Approach from ARCHITECTURE.json]
- **Testing Strategy:** [Based on existing test patterns]
```

### 4. **Efficiency Targets**
- **Questions:** Maximum 5 questions total (3-5 Round 1, 0-2 Round 2)
- **PRD Generation:** Under 2 minutes using memory system
- **Implementation Ready:** No additional research needed to start coding

## Success Metrics

### PRD Quality
- **Completeness:** 100% of components map to memory system patterns
- **Specificity:** All requirements include file and line references
- **Implementability:** Developer can start coding immediately after PRD
- **Test Coverage:** Clear testing approach for each component

### Development Speed
- **Time to PRD:** Under 5 minutes from initial prompt to saved document
- **Implementation Start:** Zero additional research time needed
- **Pattern Reuse:** 90%+ of implementation uses existing patterns

## Example: Memory-Enhanced PRD Generation

**User Prompt:** "Add [FEATURE_REQUEST]" # e.g., "Add user preference settings"

**Memory Consultation Results:**
- `BUSINESS.json` → [EXISTING_FEATURES] # e.g., "User management system with UserProfile model"
- `ARCHITECTURE.json` → [ARCHITECTURE_PATTERNS] # e.g., "Service layer pattern and repository pattern"
- `FILES.json` → [RELEVANT_FILES] # e.g., "UserService.ts:45, UserRepository.ts:23, SettingsModel.ts"
- `PATTERNS.md` → [APPLICABLE_PATTERN] # e.g., "Service layer pattern template"

**Informed Questions (2-3 max):**
1. "Should [FEATURE] integrate with the existing [MANAGER/SERVICE] (following the pattern at [FILE:LINE]), or create a new [COMPONENT_NAME]?" # e.g., "preference saving integrate with UserService (UserService.ts:45), or create PreferenceService?"
2. "Given the [EXISTING_SYSTEM], should this support [OPTION_A] or [OPTION_B]?" # e.g., "existing auth system, should this be per-user or global settings?"
3. "Should this follow [PERFORMANCE_PATTERN] from [FILE:LINE]?" # e.g., "caching pattern from CacheService.ts:78?"

**Result:** Implementation-ready PRD with exact file references, pattern templates, and integration approach - generated in under 3 minutes.

---

**This system transforms PRD generation from generic requirements gathering into architecture-aware, implementation-ready sprint planning.**