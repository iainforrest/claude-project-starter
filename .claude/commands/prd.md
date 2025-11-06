---
description: Generate implementation-ready PRD from feature idea
---

# AI-Optimized PRD Generation Command

**Objective:** Generate a comprehensive, implementation-ready Product Requirements Document (PRD) and save it to `/tasks/prd-[feature-name].md`.

## Core Philosophy

Generate PRDs that are **instantly implementable** by leveraging the comprehensive AI memory system. Focus on **architectural integration** and **pattern-based implementation** rather than generic requirements.

## Output Requirements

**CRITICAL:** The PRD MUST be saved to a file:
- **Location:** `/tasks/` directory
- **Filename:** `prd-[feature-name].md` (use kebab-case for feature name)
- **Format:** Markdown (.md)
- **Action:** Use the Write tool to save the PRD after generation

**Example filenames:**
- Feature: "User Authentication System" → `prd-user-authentication-system.md`
- Feature: "Real-Time Notifications" → `prd-real-time-notifications.md`

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
- Reference existing patterns: "Should this follow the [PATTERN_NAME] pattern like [EXISTING_COMPONENT]?"
- Leverage architecture knowledge: "Given the [ARCHITECTURE_PATTERN], will this need [INTEGRATION_TYPE]?"
- Use performance baselines: "The current [METRIC] target is [VALUE] - does this need similar performance?"

## Streamlined Question Process

### Round 1: Memory-Informed Questions (3-5 questions max)
Based on memory system analysis, ask only the **gap-filling questions**:

**Architecture Integration:**
- "Looking at the current [ARCHITECTURE_PATTERN], should this integrate with [COMPONENT_A] or be [STANDALONE]?"
- "Given the [STATE_MANAGEMENT] architecture, what new state types will this feature need?"

**Pattern Application:**
- "Should this follow the [SPECIFIC_PATTERN from PATTERNS.md] like [EXISTING_COMPONENT]?"
- "Does this need [DATABASE_TYPE] integration following the [REPOSITORY_PATTERN]?"

**Business Logic Integration:**
- "How does this relate to the existing [CORE_SYSTEM]?"
- "Should this integrate with the [CACHING/PERFORMANCE_SYSTEM]?"

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

### Component 1: [Business Logic Layer]
**Pattern:** [BUSINESS_LAYER_PATTERN] (following [ExistingComponent.ext:line])
**Files:** [Specific files from FILES.json]
**Dependencies:** [Known dependencies from ARCHITECTURE.json]

### Component 2: [UI/Presentation Layer]
**Pattern:** [UI_PATTERN based on context]
**Files:** [UI files from FILES.json]
**State Management:** [State integration approach]
```

#### 3. Implementation-Ready Requirements
```markdown
## Functional Requirements

### [Component] Requirements

**FR1.1:** The system must [requirement]
- **Implementation File:** [Specific file from FILES.json:line]
- **Pattern Reference:** [Template from PATTERNS.md]
- **Integration Point:** [Connection from ARCHITECTURE.json]
- **Error Handling:** Follow [ERROR_HANDLING_PATTERN]
- **Testing:** Unit tests following [existing test pattern]
```

#### 4. Memory-Referenced Technical Considerations
```markdown
## Technical Considerations

### Architecture Alignment
- **[PRIMARY_PATTERN]:** [If applicable - reference integration approach]
- **[SERVICE_LAYER] Integration:** [State updates and new interfaces]
- **Caching Strategy:** [If applicable - caching approach]

### Pattern Compliance
- **Follow:** [Specific pattern from PATTERNS.md]
- **Files to Modify:** [Exact files from FILES.json with line references]
- **Dependencies:** [Known constraints from ARCHITECTURE.json]

### Performance Integration
- **Target:** [Specific target from BUSINESS.json performance requirements]
- **Monitoring:** [Analytics/monitoring integration approach]
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
**Monitoring:** [Monitoring approach]
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
Ask: "Given the existing [CORE_SYSTEM], how should this feature integrate with [EXISTING_FEATURE]?"

Instead of: "How should this work?"
Ask: "Should this follow the [PATTERN_NAME] like [EXISTING_COMPONENT], or the [ALTERNATIVE_PATTERN]?"
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
- **PRD Generation:** Under 5 minutes using memory system
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

**User Prompt:** "Add user authentication feature"

**Memory Consultation Results:**
- `BUSINESS.json` → Existing auth patterns and security requirements
- `ARCHITECTURE.json` → Authentication pipeline and session management
- `FILES.json` → AuthService.ts:148, UserRepository.ts:67, AuthMiddleware.ts:45
- `PATTERNS.md` → Service pattern template with authentication

**Informed Questions (2-3 max):**
1. "Should authentication integrate with the existing SessionManager (following the pattern at SessionManager.ts:45), or create a new AuthManager?"
2. "Should this support OAuth providers in addition to email/password, or start with email/password only?"
3. "Should this use JWT tokens following the existing TokenService pattern (TokenService.ts:89)?"

**Result:** Implementation-ready PRD with exact file references, pattern templates, and integration approach - generated in under 5 minutes.

---

## Final Step: Save the PRD

**MANDATORY FINAL ACTION:**

After generating the complete PRD following all the rules above:

1. **Determine filename:** Convert feature name to kebab-case (e.g., "User Authentication" → "user-authentication")
2. **Save to file:** Use the Write tool to save the PRD to `/tasks/prd-[feature-name].md`
3. **Confirm to user:** Tell the user the PRD has been saved and provide the file path

**Example:**
```
User request: "Add user authentication feature"
Generated PRD saved to: /tasks/prd-user-authentication.md
```

**DO NOT** just output the PRD to the screen. It MUST be saved to a file in the `/tasks/` directory.

---

**This system transforms PRD generation from generic requirements gathering into architecture-aware, implementation-ready sprint planning.**
