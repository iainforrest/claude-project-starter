# AI-Optimized PRD Generation Rules

**Version:** 3.0
**Last Updated:** 2025-10-17
**Architecture:** Three-Phase Prompt Chain

**Change Log:**
- v1.0 (2025-09-01): Original PRD generation approach
- v2.0 (2025-10-17): Merged comprehensive idea exploration with memory integration
- v3.0 (2025-10-17): Chain architecture + decision frameworks + red flags + assumptions

---

## Core Philosophy

Generate PRDs that capture **deeply understood requirements** through thorough idea exploration, while leveraging the **AI memory system** for efficient architectural integration. Use a **three-phase prompt chain** for optimal quality, flexibility, and cost efficiency.

---

## PROMPT CHAIN ARCHITECTURE

This system uses **three sequential prompts** that can be executed together or independently:

```
┌─────────────────────────────────────────────────────────────┐
│  PROMPT 1: Memory Review & Context Extraction              │
│  Input: User request + memory files                        │
│  Output: Context summary document                          │
│  Duration: 30-60 seconds                                   │
└─────────────────────────────────────────────────────────────┘
                            ↓
┌─────────────────────────────────────────────────────────────┐
│  PROMPT 2: Idea Exploration & Validation                   │
│  Input: User request + context summary                     │
│  Output: Requirements summary document                     │
│  Duration: 3-8 minutes (interactive questioning)           │
└─────────────────────────────────────────────────────────────┘
                            ↓
┌─────────────────────────────────────────────────────────────┐
│  PROMPT 3: PRD Generation                                  │
│  Input: Requirements summary + context summary             │
│  Output: Complete PRD saved to /tasks/                     │
│  Duration: 1-2 minutes                                     │
└─────────────────────────────────────────────────────────────┘
```

**Benefits of Chain Architecture:**
- Reduces token usage per step (cost efficiency)
- Allows iteration on questioning without re-generating PRD
- Better error recovery (can restart from any phase)
- Clearer separation of concerns
- Can skip Phase 1 if no memory system exists

**Usage Mode:**
- **Full Chain (Recommended):** Execute all three phases sequentially
- **Quick Mode:** Skip Phase 1 if new project with no memory
- **Iteration Mode:** Re-run Phase 2 for clarification, then Phase 3 for new PRD

---

# PROMPT 1: MEMORY REVIEW & CONTEXT EXTRACTION

## Purpose
Silently review the project's memory system and extract relevant context to inform questioning and PRD generation.

## Input Structure (Three-Layer Architecture)

### Layer 1: Raw User Request
```
User provides:
- Initial feature idea (text description)
- Any rough notes, emails, or unstructured thoughts
- Links to reference materials (optional)
```

### Layer 2: Structured Memory Data (AI Retrieves)
```
If memory system exists (.claude/memory/):
- ARCHITECTURE.json → Patterns, integration points, constraints
- BUSINESS.json → Existing features, performance targets, core models
- FILES.json → Relevant files, dependencies, key implementations
- PATTERNS.md → Implementation templates and conventions
```

### Layer 3: Implicit Constraints (AI Identifies)
```
From memory system and user request:
- Technical constraints (language, framework, platform)
- Resource constraints (team size, timeline if mentioned)
- Compliance requirements (security, privacy if relevant)
- Existing system limitations
```

## Execution Steps

### Step 1: Check for Memory System
```
IF .claude/memory/ directory exists:
  → Proceed to Step 2 (Memory Review)
ELSE:
  → Skip to Step 4 (No memory context)
```

### Step 2: Memory System Review
Read and extract:

**From ARCHITECTURE.json:**
- [ ] What architectural patterns exist? (e.g., layered, microservices, MVC)
- [ ] What are the key integration points?
- [ ] What constraints or limitations exist?
- [ ] What technologies/frameworks are in use?

**From BUSINESS.json:**
- [ ] What similar features already exist?
- [ ] What are the current performance benchmarks?
- [ ] What are the core data models?
- [ ] What are the key business rules?

**From FILES.json:**
- [ ] Which files are most relevant to this feature type?
- [ ] What are the key dependencies?
- [ ] Where are similar features implemented?
- [ ] What naming conventions are used?

**From PATTERNS.md:**
- [ ] What implementation patterns are established?
- [ ] What templates or conventions should be followed?
- [ ] Are there anti-patterns to avoid?

### Step 3: Context Gap Analysis
Identify what memory **answers** vs. what needs **user clarification**:

```
MEMORY ANSWERS:
- Architecture patterns: [List patterns found]
- Similar features: [List existing features]
- Integration points: [List available integrations]
- Performance targets: [List benchmarks]
- File locations: [List relevant files]

NEEDS CLARIFICATION:
- Specific user problem being solved
- Must-have vs nice-to-have scope
- User flows and interactions
- Edge cases and error handling
- Timeline and resource constraints
- [Other gaps specific to this feature]

CONFLICTS DETECTED:
- [Any conflicts between user request and existing system]
```

### Step 4: Generate Context Summary Document

**Output Format:**
```markdown
# Context Summary: [Feature Name]

**Generated:** [Timestamp]
**Memory System:** [Available / Not Available]

## Project Context

### Architectural Patterns
[List patterns from memory or "New project - no existing patterns"]

### Similar Existing Features
[List similar features or "No similar features found"]

### Integration Points Available
[List integration options or "Standalone project"]

### Performance & Constraints
[List benchmarks and constraints or "No existing benchmarks"]

### Relevant Files & Patterns
[List key files and patterns or "New codebase"]

## Questions to Ask User

### Must Ask (Gaps in Understanding):
1. [Question about core problem]
2. [Question about scope]
3. [Question about user flows]

### Should Ask if Relevant:
- [Conditional questions based on complexity]

### Can Skip (Already Answered by Memory):
- [List what doesn't need asking]

## Red Flags Detected
[Any concerns from initial analysis - see Red Flag Framework below]

---
**Handoff to Phase 2:** Ready for idea exploration with [X] questions prepared.
```

### Step 5: Handoff to Phase 2
Pass the Context Summary Document to Prompt 2 along with the original user request.

---

# PROMPT 2: IDEA EXPLORATION & VALIDATION

## Purpose
Conduct batched questioning to thoroughly understand requirements, validate scope, identify risks, and gather sufficient detail to generate a complete PRD.

## Input
- Original user feature request
- Context Summary Document from Phase 1

## Decision Frameworks & Formulas

### Framework 1: Stopping Criteria Scoring

**Stop questioning when ALL criteria met:**

| Criterion | Weight | Check |
|-----------|--------|-------|
| Clear problem statement articulated | 20% | Can state problem in one sentence |
| User goals and success criteria defined | 15% | User can describe "done" objectively |
| Scope boundaries explicit (must-have vs nice-to-have) | 15% | Can list 3-5 must-haves, 2-3 nice-to-haves |
| User flows documented (happy path + errors) | 15% | Can write step-by-step flows |
| Integration points identified | 10% | Know what this connects to |
| Edge cases and error scenarios understood | 10% | Know what can go wrong |
| Data models and API requirements clear | 10% | Know what data structures are needed |
| Can write 80%+ of Functional Requirements | 5% | <3 "TBD" placeholders would remain |

**Scoring:**
- Each criterion is binary: ✓ (met) or ✗ (not met)
- Need 100% (all ✓) to proceed to confirmation
- If rounds >= 5 and score >= 85%, ask user if sufficient detail exists

**Example Check:**
```
After Round 2:
✓ Clear problem statement (user said: "Users can't track their preferences")
✓ User goals (user said: "Save preferences, sync across devices")
✓ Scope boundaries (must-have: save/load, nice-to-have: import/export)
✗ User flows (need step-by-step, not just "user saves preferences")
✗ Integration points (need to clarify: local storage? database? API?)
✓ Edge cases (user mentioned: "offline mode, conflicts")
✗ Data models (need structure: what fields, types, validation)
✗ Can write 80% of FRs (too many TBDs still)

Score: 50% → Continue questioning (Round 3)
```

### Framework 2: Feature Complexity Assessment

**Complexity Score = (Integrations × 2) + (New Components × 3) + (Breaking Changes × 5)**

| Score Range | Complexity | Expected Rounds | Risk Level |
|-------------|------------|-----------------|------------|
| 0-5 | Low | 2-3 rounds | Low |
| 6-15 | Medium | 3-4 rounds | Medium |
| 16-30 | High | 4-6 rounds | High |
| 31+ | Very High | 5-7+ rounds | Very High |

**Use this to:**
- Set expectations for questioning duration
- Trigger red flags if complexity higher than user expects
- Determine if prompt chain should iterate multiple times

**Example:**
```
Feature: User preference system
- Integrations: UserService, API, Database (3 × 2 = 6)
- New Components: PreferenceService, PreferenceModel (2 × 3 = 6)
- Breaking Changes: New database table (1 × 5 = 5)

Complexity Score: 6 + 6 + 5 = 17 → HIGH complexity
Expected: 4-6 questioning rounds
Risk: HIGH - significant integration and new components
```

### Framework 3: Priority Scoring (For Feature Components)

**Priority Score = (User Value × Impact) / (Effort × Risk)**

Where:
- **User Value:** 1-5 scale (how much does user care?)
- **Impact:** 1-5 scale (how much does it improve the product?)
- **Effort:** 1-5 scale (how hard to implement?)
- **Risk:** 1-5 scale (how likely to cause problems?)

| Score Range | Priority | Recommendation |
|-------------|----------|----------------|
| > 5.0 | Critical | Must have - do first |
| 2.0 - 5.0 | High | Should have - do early |
| 0.5 - 2.0 | Medium | Nice to have - do later |
| < 0.5 | Low | Consider cutting |

**Example:**
```
Component: Basic preference saving
- User Value: 5 (critical need)
- Impact: 4 (enables all other features)
- Effort: 2 (simple CRUD)
- Risk: 1 (low complexity)

Priority Score: (5 × 4) / (2 × 1) = 20 / 2 = 10.0 → CRITICAL priority

Component: Preference import from competitors
- User Value: 2 (nice but not critical)
- Impact: 2 (minor convenience)
- Effort: 4 (complex parsing)
- Risk: 3 (many edge cases)

Priority Score: (2 × 2) / (4 × 3) = 4 / 12 = 0.33 → LOW priority (consider cutting)
```

## Red Flag Framework

**During questioning, proactively flag these patterns:**

### 🚩 Category 1: Scope & Complexity Risks

| Red Flag | Trigger Condition | Action |
|----------|------------------|--------|
| **Scope Creep** | User adds >3 new components after Round 2 | Alert user: "The scope is growing. Should we split this into multiple PRDs?" |
| **Integration Overload** | Feature requires >7 integration points | Alert user: "This has many integrations. Complexity score: HIGH. Timeline may be longer than expected." |
| **Breaking Changes Detected** | Any change that affects existing users/APIs | Alert user: "This includes breaking changes. Migration strategy will be needed." |
| **Undefined Success** | User can't articulate completion criteria after 3 attempts | Ask: "Let's focus: what's ONE thing that must work for this to be successful?" |

### 🚩 Category 2: Communication & Clarity Risks

| Red Flag | Trigger Condition | Action |
|----------|------------------|--------|
| **Vague Language** | User uses "flexible", "dynamic", "smart", "modern" >5 times without specifics | Ask: "Can you give 2-3 concrete examples of what 'flexible' means here?" |
| **No User Flow** | Reached Round 3 without step-by-step user actions | Ask: "Walk me through this: User opens the app, then what? Click-by-click." |
| **Assumption Mismatch** | User assumes capabilities not in memory system | Clarify: "I don't see [X] in the existing system. Is this a new capability we need to build?" |

### 🚩 Category 3: Technical & Timeline Risks

| Red Flag | Trigger Condition | Action |
|----------|------------------|--------|
| **Timeline Mismatch** | Breaking changes + user expects <4 weeks | Alert: "Breaking changes typically need 4-8 weeks for migration. Is timeline flexible?" |
| **Performance Unrealistic** | User requests performance better than existing benchmarks without justification | Ask: "Current system does [X] in 500ms. You want 50ms. What's driving that requirement?" |
| **Security Sensitive** | Feature involves auth, permissions, PII, or payments | Flag: "This is security-sensitive. Security review will be required before launch." |
| **No Error Handling** | Reached Round 4 without discussing error cases | Ask: "What happens when [X] fails? When user is offline? When data is invalid?" |

### 🚩 Category 4: Organizational Risks

| Red Flag | Trigger Condition | Action |
|----------|------------------|--------|
| **Cross-Team Dependencies** | Feature requires work from >2 other teams | Alert: "This needs [TeamA] and [TeamB]. Coordination overhead may extend timeline." |
| **Resource Constraints** | User mentions team size limitations or competing priorities | Ask: "Given [constraint], what's the minimum viable version of this?" |
| **Compliance Unknown** | Feature touches regulated data (health, finance) without compliance discussion | Ask: "This involves [regulated area]. Are there compliance requirements I should know about?" |

## Questioning Strategy

### Batched Question Flow

**Maximum 3 questions per batch. Wait for answers before next batch.**

```
Round 1: Core Understanding (Max 3 questions)
  ↓
User answers
  ↓
AI evaluates: Check stopping criteria score
  ↓
IF score = 100% → Go to Confirmation
ELSE IF score >= 85% AND rounds >= 5 → Ask "Sufficient detail to proceed?"
ELSE IF red flags detected → Prioritize red flag questions
ELSE → Continue to Round 2

Round 2: Scope & User Experience (Max 3 questions)
  ↓
[Repeat evaluation loop]

Round 3+: Deep Dive & Integration (Max 3 questions each)
  ↓
[Repeat evaluation loop]

Maximum rounds: 7
After Round 7: Summarize what you have and ask user to confirm or add critical missing info
```

### Question Templates by Round

**Round 1: Core Understanding (Choose top 3 from context summary)**

WITHOUT memory:
- "What problem does this feature solve for the user?"
- "Who is the primary user, and what is their main goal?"
- "What are the must-have functionalities vs nice-to-have?"

WITH memory (context-informed):
- "This seems related to [EXISTING_FEATURE]. Is this an enhancement to that, or a new parallel feature?"
- "What problem does this solve that [EXISTING_SYSTEM] doesn't currently address?"
- "Should this work like [SIMILAR_FEATURE], or take a different approach?"

**Round 2: Feature Scope + User Experience (Max 3)**

- "Can you walk me through a typical user flow? What specific steps does a user take?"
- "What should happen when things go wrong? (error cases, edge cases)"
- "Are there any specific things this feature should NOT do or boundaries it shouldn't cross?"

WITH memory:
- "Given the existing [UI_PATTERN], should this follow that same pattern or introduce something new?"
- "Should this integrate with [EXISTING_COMPONENT] or be standalone?"

**Round 3+: Deep Dive + Integration (Max 3 per round)**

Ask follow-up questions when:
- User mentions integration with systems not yet discussed
- Answer reveals complexity (multiple user types, complex workflows)
- Validation rules or business logic mentioned but not detailed
- Performance/security requirements implied but not specified
- Answer uses vague terms ("sometimes", "usually", "various")
- New components mentioned in passing
- Conflict detected with existing system patterns
- Red flags triggered

Example follow-ups:
- "You mentioned [VAGUE_TERM] - can you be more specific? Give me 2-3 concrete examples."
- "What specific data do we need from [MENTIONED_SYSTEM]?"
- "You said 'various validations' - can you list the specific rules?"
- "When you say 'fast', what's the acceptable response time?"
- "Should this follow the [PATTERN_FROM_MEMORY] pattern, or something different?"
- "How should this handle conflicts with [EXISTING_FEATURE]?"

### Conflict Resolution Questions

If user's request conflicts with memory system, clarify immediately:

- "The existing system uses [PATTERN_A], but your description suggests [PATTERN_B]. Should we follow the existing pattern or introduce a new one?"
- "This seems to overlap with [EXISTING_FEATURE]. Should we enhance that feature or create something separate?"
- "The current architecture uses [APPROACH], but this might require [DIFFERENT_APPROACH]. Are you open to architectural changes?"

## Confirmation Process

### After Stopping Criteria Met

Summarize understanding and confirm:

```markdown
Based on our discussion, I understand:

**Problem:** [One-sentence problem statement]

**Users:** [Primary users and their goals]

**Must-Have Functionality:**
- [Must-have 1]
- [Must-have 2]
- [Must-have 3]

**Nice-to-Have (Lower Priority):**
- [Nice-to-have 1]
- [Nice-to-have 2]

**Integration:** [How it fits with existing system - if applicable]

**Success Criteria:** [How we know it's done]

**Complexity Assessment:** [Low/Medium/High] based on [X integrations, Y components, Z breaking changes]

**Red Flags Identified:**
- [Any red flags raised during questioning]

**Key Assumptions:**
- [List assumptions being made - see Framework 4 below]

Is this correct? Anything I've missed or misunderstood before I create the PRD?
```

**Wait for user confirmation.**

If user confirms → Proceed to Step: Generate Requirements Summary
If user adds info → Assess if rounds < 7, then continue questioning OR summarize
If user requests changes → Clarify specific changes and confirm again

## Generate Requirements Summary Document

**Output Format:**
```markdown
# Requirements Summary: [Feature Name]

**Generated:** [Timestamp]
**Complexity Score:** [Score] ([Low/Medium/High/Very High])
**Priority:** [Based on priority framework if components identified]
**Questioning Rounds:** [Number of rounds conducted]

## Problem Statement
[One clear sentence]

## User Goals
- [Goal 1]
- [Goal 2]
- [Goal 3]

## Scope Definition

### Must-Have (Priority: High)
- [Component 1] - [Brief description]
- [Component 2] - [Brief description]
- [Component 3] - [Brief description]

### Nice-to-Have (Priority: Medium/Low)
- [Feature A] - [Brief description]
- [Feature B] - [Brief description]

### Explicitly Out of Scope
- [Exclusion 1]
- [Exclusion 2]

## User Flows

### Happy Path
1. [Step 1]
2. [Step 2]
3. [Step 3]
4. [Result]

### Error Scenarios
- **Scenario 1:** [What goes wrong] → [How to handle]
- **Scenario 2:** [What goes wrong] → [How to handle]

### Edge Cases
- [Edge case 1 and handling]
- [Edge case 2 and handling]

## Integration Points
[If existing project]
- Integrates with: [System A], [System B]
- Uses: [Component X], [Utility Y]
- Depends on: [Service Z]

## Data Models (High-Level)
[Rough structure of data needed]

## Performance Requirements
- [Requirement 1 with metric]
- [Requirement 2 with metric]

## Security Requirements
- [Requirement 1]
- [Requirement 2]

## Assumptions (See Framework Below)
- [Assumption 1] - Risk: [Impact if wrong] - Validation: [How to verify]
- [Assumption 2] - Risk: [Impact if wrong] - Validation: [How to verify]

## Red Flags & Risks
- [Red flag 1 and mitigation]
- [Red flag 2 and mitigation]

## Success Criteria
- [Criterion 1 - measurable]
- [Criterion 2 - measurable]
- [Criterion 3 - measurable]

## Timeline Constraints
[If discussed: deadlines, dependencies, blockers]

---
**Handoff to Phase 3:** Ready for PRD generation.
**Estimated PRD Complexity:** [X sections, Y functional requirements, Z components]
```

### Framework 4: Assumptions Validation

**For each assumption identified during questioning, document:**

| Assumption | Risk if Wrong | Validation Method | Confidence Level |
|------------|---------------|-------------------|------------------|
| [What we're assuming] | [Impact] | [How to verify] | High/Med/Low |

**Example:**
```
| Assumption | Risk if Wrong | Validation Method | Confidence |
|------------|---------------|-------------------|------------|
| Users want sync across devices | Wasted effort on sync infrastructure | User survey: "Would you use this on multiple devices?" | Medium |
| Existing UserService can handle preference storage | Need to build separate service | Code review of UserService capacity | High |
| <200ms response time is acceptable | User dissatisfaction | Benchmark competitor apps | Medium |
```

**Include these assumptions in Requirements Summary → Phase 3 will add them to PRD.**

## Handoff to Phase 3
Pass the Requirements Summary Document to Prompt 3 along with the Context Summary from Phase 1.

---

# PROMPT 3: PRD GENERATION

## Purpose
Generate a complete, implementation-ready PRD using the structured information from Phases 1 and 2.

## Input
- Context Summary Document (from Phase 1)
- Requirements Summary Document (from Phase 2)
- Original user feature request

## Execution

### Step 1: Map Requirements to PRD Template
Transform Requirements Summary into full PRD structure using the template below.

### Step 2: Expand Details
- Convert bullet points into full functional requirements (with Input/Output/Validation/Error States)
- Add acceptance criteria for each component
- Expand user flows with more detail
- Add technical considerations from context summary
- Include all assumptions with validation methods

### Step 3: Generate Complete PRD
Use the PRD Structure Template below, filling ALL sections.

### Step 4: Validate Completeness

**Pre-Save Validation Checklist:**

- [ ] **Idea Clarity:** Core problem and solution clearly articulated
- [ ] **Scope Definition:** Must-haves vs nice-to-haves defined with priority scores
- [ ] **User Flows:** Happy path and error flows documented (at least 2 error scenarios)
- [ ] **Data Specifications:** All data structures defined with examples
- [ ] **Acceptance Criteria:** Every component has testable criteria
- [ ] **Error Handling:** All error states identified and handled
- [ ] **Assumptions:** All assumptions documented with risk assessment and validation methods

[IF MEMORY SYSTEM EXISTS:]
- [ ] **Architecture Alignment:** Follows established patterns from memory system
- [ ] **File References:** Includes specific files and line numbers from FILES.json (where applicable)
- [ ] **Pattern Application:** Maps to templates in PATTERNS.md (where applicable)
- [ ] **Integration Points:** Addresses connections from ARCHITECTURE.json
- [ ] **Performance Targets:** Aligns with benchmarks in BUSINESS.json

[IF NEW PROJECT:]
- [ ] **Architecture Suggestions:** Recommended patterns and approaches provided
- [ ] **Foundation for Memory:** PRD provides foundation for future memory system

### Step 5: Save PRD
Save to `/tasks/prd-[feature-name].md` using kebab-case.

### Step 6: Confirm to User
```
PRD saved to /tasks/prd-[feature-name].md

**Summary:**
- Complexity: [Low/Medium/High]
- Components: [X]
- Functional Requirements: [Y]
- Assumptions: [Z]
- Red Flags: [List if any]

Would you like me to:
1. Review the PRD with you
2. Generate implementation tasks from this PRD
3. Make any changes to the PRD
4. Update the memory system with new patterns from this PRD
```

---

## PRD STRUCTURE TEMPLATE

### Header (Memory-Informed If Applicable)

```markdown
# PRD: [Feature Name]

**Generated:** [Date]
**Status:** Draft
**Version:** v1.0
**Complexity:** [Low/Medium/High/Very High] (Score: [X])

[IF MEMORY SYSTEM EXISTS, ADD:]
**Architecture Pattern:** [Pattern from PATTERNS.md or "New Pattern"]
**Integration Points:** [Components from ARCHITECTURE.json or "Standalone"]
**Key Implementation Files:** [Files from FILES.json or "New files to be created"]
```

### 1. Overview

```markdown
## Overview

[2-3 sentence description of the feature, the problem it solves, and its primary goal]

[IF EXISTING PROJECT WITH MEMORY:]
**Architecture Integration:** [How this leverages/extends existing patterns]
**Performance Target:** [Target based on BUSINESS.json benchmarks or user requirements]
**Implementation Strategy:** [High-level approach]
```

### 2. Goals

```markdown
## Goals

- [Specific, measurable objective 1]
- [Specific, measurable objective 2]
- [Specific, measurable objective 3]
- [Additional goals as needed]

**Success looks like:** [Concrete description of successful implementation]
```

### 3. User Stories

```markdown
## User Stories

- As a [type of user], I want to [perform action] so that [benefit]
- As a [type of user], I want to [perform action] so that [benefit]
- As a [type of user], I want to [perform action] so that [benefit]

[Include enough user stories to cover main use cases and key user types]
```

### 4. Feature Components

```markdown
## Feature Components

Break down the feature into 3-7 logical components that map to implementation tasks.

**Priority Framework Applied:**
- Priority Score = (User Value × Impact) / (Effort × Risk)
- Critical: >5.0 | High: 2.0-5.0 | Medium: 0.5-2.0 | Low: <0.5

### Component 1: [Name] [Priority: Critical/High/Medium/Low]
**Responsibility:** [Brief description of what this component does]
**Priority Score:** [X.X] (User Value: [1-5], Impact: [1-5], Effort: [1-5], Risk: [1-5])

[IF MEMORY EXISTS:]
**Pattern:** [PATTERN_NAME] (following [EXAMPLE_FILE.ext:lineNumber])
**Files:** [Specific files from FILES.json or new files needed]
**Dependencies:** [Known dependencies from ARCHITECTURE.json]

[IF NEW PROJECT:]
**Implementation Approach:** [Suggested pattern or architecture]

### Component 2: [Name] [Priority: Critical/High/Medium/Low]
**Responsibility:** [Brief description]
**Priority Score:** [X.X] (breakdown)

[Continue for all components...]
```

### 5. Functional Requirements

```markdown
## Functional Requirements

Structure requirements by component, making each atomic and testable.

### [Component 1 Name] Requirements

**FR1.1:** The system must [specific requirement]
- **Input:** [What goes in - be specific with data types/formats]
- **Output:** [What comes out - be specific with expected results]
- **Validation:** [Rules to check - list all validation constraints]
- **Error States:** [What can go wrong and how to handle it]

[IF MEMORY EXISTS:]
- **Implementation File:** [Specific file from FILES.json:line]
- **Pattern Reference:** [Template from PATTERNS.md]
- **Integration Point:** [Connection from ARCHITECTURE.json]

**FR1.2:** The system must [specific requirement]
- **Input:** [what goes in]
- **Output:** [what comes out]
- **Validation:** [rules to check]
- **Error States:** [what can go wrong]

[Continue for all requirements, numbering consistently (FR1.x, FR2.x, etc.)]

### [Component 2 Name] Requirements

**FR2.1:** The system must [specific requirement]
...

[Continue for all components]
```

### 6. Data Specifications

```markdown
## Data Specifications

### Data Models

[Provide data structures in appropriate format for the tech stack]

```
// Example: TypeScript interface (adapt to project language)
interface UserProfile {
  id: string
  name: string
  email: string
  preferences: UserPreferences
  createdAt: Date
  updatedAt: Date
}

interface UserPreferences {
  theme: 'light' | 'dark'
  notifications: boolean
  // ... other fields
}
```

[IF MEMORY EXISTS:]
**Related Models:** [Reference existing models from BUSINESS.json]
**Database Schema Changes:** [If applicable, what tables/collections change]

### API Endpoints (if applicable)

- `GET /api/[resource]` - [Description, request/response format]
- `POST /api/[resource]` - [Description, request/response format]
- `PUT /api/[resource]/:id` - [Description, request/response format]
- `DELETE /api/[resource]/:id` - [Description, request/response format]

[IF MEMORY EXISTS:]
**API Pattern:** [Follows pattern from existing API endpoints]

### Data Examples

Provide concrete examples of data structures:

```json
{
  "id": "user123",
  "name": "Jane Doe",
  "email": "jane@example.com",
  "preferences": {
    "theme": "dark",
    "notifications": true
  },
  "createdAt": "2025-10-17T10:00:00Z",
  "updatedAt": "2025-10-17T10:00:00Z"
}
```

### Data Validation Rules

- **[Field Name]**: [Validation rules, constraints, formats]
- **[Field Name]**: [Validation rules, constraints, formats]

[List all validation rules for data integrity]
```

### 7. User Flow Examples

```markdown
## User Flow Examples

### Happy Path Flow

1. User navigates to [location/screen]
2. User performs [specific action with details]
3. System validates [what specifically]
4. System updates [what data/state changes]
5. User sees [specific result/feedback]
6. [Continue flow to completion]

### Error Flow Example 1: [Error Scenario Name]

1. User attempts [action]
2. System detects [invalid condition - be specific]
3. System displays [exact error message]
4. User can [specific recovery action]
5. [Resolution path]

### Error Flow Example 2: [Another Error Scenario]

1. [Step-by-step error flow]
...

### Edge Case Flow: [Edge Case Name]

1. [Step-by-step edge case handling]
...

[Include at least 1 happy path, 2 error flows, and 1-2 edge cases]
```

### 8. Technical Considerations

```markdown
## Technical Considerations

### Architecture Alignment

[IF MEMORY EXISTS:]
- **Pattern Compliance:** Follows [ARCHITECTURE_PATTERN] from existing system
- **State Management:** [How state is managed - reference existing approach]
- **Data Layer:** [Database/API integration approach]

[IF NEW PROJECT:]
- **Suggested Architecture:** [Recommended pattern for this feature]
- **State Management:** [Suggested approach]
- **Data Layer:** [Suggested approach]

### Integration Points

[IF MEMORY EXISTS:]
- Integrates with [existing system/module from ARCHITECTURE.json]
- Uses [existing component/utility from FILES.json]
- Depends on [external service/API]

[IF NEW PROJECT:]
- [Identify key integration needs]
- [External dependencies]

### Patterns & Conventions

[IF MEMORY EXISTS:]
- Follow [PATTERN_NAME] pattern from [EXAMPLE_FILE:line]
- Use [existing library/framework] for [purpose]
- Maintain consistency with [existing feature]

[IF NEW PROJECT:]
- Suggested patterns: [List recommended patterns]
- Consider using: [Suggested libraries/frameworks]

### Performance Requirements

- [Specific performance requirement with measurable target]
- [e.g., "API response time < 200ms for 95th percentile"]
- [e.g., "Page load time < 2s on 3G connection"]

[IF MEMORY EXISTS:]
**Performance Targets:** Based on [BUSINESS.json benchmarks]

### Security Requirements

- [Specific security requirement]
- [e.g., "All user data encrypted at rest"]
- [e.g., "API requires authentication via JWT"]

[IF MEMORY EXISTS:]
**Security Pattern:** Follows [existing security approach]
```

### 9. Assumptions & Validation

```markdown
## Assumptions & Validation

**Critical Assumptions:**

Each assumption identified during requirements gathering:

### Assumption 1: [What we're assuming to be true]
- **Risk if Wrong:** [Impact if this assumption is incorrect]
- **Validation Method:** [How to verify this assumption before implementation]
- **Confidence Level:** [High/Medium/Low]
- **Validation Owner:** [Who should verify this]
- **Validation Timeline:** [When to verify - before Phase 1 / during Phase 2 / etc.]

### Assumption 2: [Next assumption]
- **Risk if Wrong:** [Impact]
- **Validation Method:** [How to verify]
- **Confidence Level:** [High/Medium/Low]
- **Validation Owner:** [Who verifies]
- **Validation Timeline:** [When]

[Repeat for all assumptions from Requirements Summary]

**No Critical Assumptions Identified:** [If truly no assumptions, state this explicitly]
```

### 10. Breaking Changes Analysis (REQUIRED)

```markdown
## Breaking Changes Analysis

### User Impact Assessment
- [ ] Does this change existing user workflows?
  - [If YES: Describe impact and migration path]
- [ ] Will existing users need to take action (re-auth, migrate data, etc.)?
  - [If YES: Describe required actions]
- [ ] Are there data migrations required?
  - [If YES: Describe migration strategy]
- [ ] What is the communication plan for users?
  - [Outline communication approach]

### API/Interface Changes
- [ ] Are we removing or changing existing APIs?
  - [If YES: List changes and deprecation plan]
- [ ] Will this break existing integrations?
  - [If YES: Identify what breaks and migration path]
- [ ] Is backward compatibility maintained or possible?
  - [Describe compatibility approach]

### Data Model Changes
- [ ] Are we changing database schema or data structures?
  - [If YES: List schema changes]
- [ ] Is data migration required?
  - [If YES: Outline migration strategy]
- [ ] Can old and new versions coexist during transition?
  - [Describe rollout strategy]

### Migration Strategy (If Breaking Changes Identified)

[IF ANY BREAKING CHANGES EXIST, PROVIDE DETAILED MIGRATION STRATEGY:]

**Phase 1: Preparation**
- [Steps to prepare for migration]

**Phase 2: Migration**
- [Steps to execute migration]

**Phase 3: Validation**
- [Steps to validate migration success]

**Rollback Plan:**
- [How to rollback if migration fails]

[IF NO BREAKING CHANGES:]
**No breaking changes identified.** This feature is fully backward compatible.
```

### 11. Security Considerations (REQUIRED)

```markdown
## Security Considerations

### Authentication & Authorization
- [ ] Does this change authentication flow?
  - [If YES: Describe changes and security implications]
- [ ] Are new permissions required?
  - [If YES: List new permissions and justification]
- [ ] Is user data access modified?
  - [If YES: Describe changes and access controls]
- [ ] Are database access rules or security policies affected?
  - [If YES: Describe rule changes]

### Data Privacy
- [ ] Does this collect new user data?
  - [If YES: List data collected and justification]
- [ ] Is PII (Personally Identifiable Information) involved?
  - [If YES: Describe handling and compliance requirements]
- [ ] Are privacy policies affected?
  - [If YES: Describe necessary policy updates]

### API Security
- [ ] Are new API keys or credentials needed?
  - [If YES: Describe management approach]
- [ ] Is rate limiting affected?
  - [If YES: Describe rate limit strategy]
- [ ] Are there new attack vectors?
  - [If YES: Describe threats and mitigations]

### Security Review Checklist (For Security-Sensitive Features)

**Required for features involving authentication, authorization, user data, API keys, or permissions:**

- [ ] No secrets committed to git
- [ ] API keys properly secured (environment variables, secret management)
- [ ] Database security rules updated appropriately
- [ ] User data access follows principle of least privilege
- [ ] Authentication flows tested with edge cases
- [ ] Permission requests justified and documented
- [ ] Security implications documented in PRD

[IF NOT SECURITY-SENSITIVE:]
**No significant security considerations beyond standard practices.**
```

### 12. Asset & Resource Requirements

```markdown
## Asset & Resource Requirements

### Visual Assets
- [ ] New visual assets required?
  - [If YES: List assets needed]
- [ ] Asset specifications?
  - [If YES: Sizes, formats, variations]
- [ ] Asset source?
  - [Designer, existing library, AI-generated, purchased, etc.]
- [ ] Delivery method?
  - [Internal creation, external sourcing, other]

### Asset Checklist (If Visual Assets Required)

| Asset Type | Specifications | Source | Delivery Method | Location |
|------------|---------------|--------|-----------------|----------|
| Icon | 24x24px, 48x48px SVG | Design team | Figma export | /assets/icons/ |
| Logo | 200x200px PNG, SVG | Existing library | Copy from brand assets | /assets/logos/ |
| [Asset] | [Specs] | [Source] | [Method] | [Path] |

### Configuration Assets
- [ ] New configuration files required?
  - [If YES: List config files and purpose]
- [ ] Environment-specific configuration needed?
  - [If YES: List environment variables and values]
- [ ] Secret management changes?
  - [If YES: Describe secret management approach]

### Configuration Checklist (If Config Changes Required)

| Config Type | Purpose | Environment | Location | Security Level |
|-------------|---------|-------------|----------|----------------|
| API Key | External service auth | Production | .env | Secret |
| Feature Flag | Toggle new feature | All | config/features.json | Public |
| [Config] | [Purpose] | [Env] | [Path] | [Security] |

[IF NO ASSETS REQUIRED:]
**No special assets or resources required beyond standard development resources.**
```

### 13. Acceptance Criteria

```markdown
## Acceptance Criteria

Make each criterion specific, measurable, and testable.

### For [Component 1]
- [ ] [Specific criterion with measurable outcome]
  - **Test:** [How to verify this criterion]
- [ ] [Specific criterion with measurable outcome]
  - **Test:** [How to verify this criterion]

### For [Component 2]
- [ ] [Specific criterion with measurable outcome]
  - **Test:** [How to verify this criterion]
- [ ] [Specific criterion with measurable outcome]
  - **Test:** [How to verify this criterion]

[Continue for all components...]

### General Criteria
- [ ] All error states handled gracefully with appropriate user feedback
  - **Test:** [How to test error handling]
- [ ] Unit tests pass with >80% coverage (or project-specific target)
  - **Test:** Run test suite and check coverage report
- [ ] No runtime errors or warnings in development console
  - **Test:** Manual testing across all flows
- [ ] Feature works on all supported platforms/browsers
  - **Test:** Cross-platform/browser testing checklist
- [ ] Performance meets specified targets
  - **Test:** Performance testing with specified tools
- [ ] Security requirements validated
  - **Test:** Security testing checklist
- [ ] All assumptions validated
  - **Test:** Check Assumptions & Validation section completion

[Add any feature-specific general criteria]
```

### 14. Implementation Roadmap

```markdown
## Implementation Roadmap

Break down implementation into logical phases based on component priority.

### Phase 1: Foundation (Critical Priority Components)
**Goal:** [What this phase achieves]
**Duration:** [Estimated weeks based on complexity]
**Components:** [List Critical priority components]

**Tasks:**
- [Implementation task 1]
- [Implementation task 2]
- [Implementation task 3]

[IF MEMORY EXISTS:]
**Files:** [List from FILES.json or new files]
**Pattern:** [Template from PATTERNS.md]
**Integration:** [Points from ARCHITECTURE.json]

**Validation:** [How to verify Phase 1 completion]

### Phase 2: Core Functionality (High Priority Components)
**Goal:** [What this phase achieves]
**Duration:** [Estimated weeks]
**Components:** [List High priority components]

**Tasks:**
- [Implementation task 1]
- [Implementation task 2]
- [Implementation task 3]

[IF MEMORY EXISTS:]
**Dependencies:** [Cross-references from memory system]
**Testing:** [Strategy based on existing test patterns]

**Validation:** [How to verify Phase 2 completion]

### Phase 3: Enhancement & Polish (Medium/Low Priority Components)
**Goal:** [What this phase achieves]
**Duration:** [Estimated weeks]
**Components:** [List Medium/Low priority components]

**Tasks:**
- [Implementation task 1]
- [Implementation task 2]
- [Implementation task 3]

[IF MEMORY EXISTS:]
**Performance:** [Targets from BUSINESS.json]
**Analytics:** [Monitoring approach]

**Validation:** [How to verify Phase 3 completion]

[Add more phases as needed for complex features]

### Rollout Strategy
- [ ] [How feature will be rolled out - feature flags, gradual rollout, etc.]
- [ ] [User communication plan]
- [ ] [Monitoring and validation approach post-launch]

### Critical Path
**Blockers:** [List any dependencies that must be resolved first]
**Critical Timeline:** [Phases that cannot be delayed]
**Risk Mitigation:** [Backup plans for critical path items]
```

### 15. Non-Goals (Out of Scope)

```markdown
## Non-Goals (Out of Scope)

Be explicit about what this PRD does NOT cover:

- This feature will NOT [specific exclusion with rationale]
- We are NOT implementing [specific exclusion with rationale]
- [Future consideration] is out of scope for this PRD [explain why - future work, different team, etc.]
- [Another exclusion] is explicitly not included [rationale]

[List all significant exclusions to prevent scope creep and set clear boundaries]
```

### 16. Open Questions

```markdown
## Open Questions

[Use this section for questions that remain after the clarification process]

- [ ] [Question that needs clarification before implementation]
  - **Impact:** [Why this matters]
  - **Options:** [Possible answers or approaches]
  - **Decision Owner:** [Who decides]
  - **Decision Deadline:** [When this must be decided]

- [ ] [Decision that needs to be made]
  - **Impact:** [Why this matters]
  - **Options:** [Possible decisions]
  - **Decision Owner:** [Who decides]
  - **Decision Deadline:** [When]

[IF NO OPEN QUESTIONS:]
**No open questions.** All requirements clarified during PRD generation process.
```

### 17. Red Flags & Risks

```markdown
## Red Flags & Risks

**Red flags identified during requirements gathering:**

### 🚩 [Red Flag Category]: [Red Flag Name]
**Description:** [What the red flag is]
**Impact:** [Why this matters]
**Mitigation:** [How to address this]
**Owner:** [Who is responsible for mitigation]
**Status:** [Open / In Progress / Mitigated]

[Repeat for all red flags from Requirements Summary]

**Risk Summary:**
- **High Risk Items:** [Count and list]
- **Medium Risk Items:** [Count and list]
- **Mitigation Plan:** [Overall approach to managing risks]

[IF NO RED FLAGS:]
**No significant red flags identified.** Standard development risks apply.
```

---

## WRITING GUIDELINES

### Be Explicit
- Write requirements as if explaining to someone unfamiliar with the codebase
- Avoid assumptions about "obvious" behavior
- Specify exactly what happens in each scenario

### Use Examples
- Include concrete examples for every major concept
- Provide real data examples, not placeholders
- Show before/after states for changes

### Number Everything
- Use consistent numbering (FR1.1, FR1.2) for easy reference
- Make it easy to refer to specific requirements in discussions
- Group related requirements under same component

### Specify Errors
- Every requirement should include what happens when things go wrong
- Define error messages and recovery paths
- Consider edge cases and boundary conditions

### Think Components
- Structure requirements around logical components that map to implementation tasks
- Each component should have clear boundaries and responsibilities
- Make it easy to assign components to different developers

### Include Validation
- Every input should have clear validation rules
- Specify data types, formats, ranges, and constraints
- Define what makes data "valid"

### Avoid Ambiguity
- Use "must", "should", "may" consistently per RFC 2119:
  - **MUST**: Absolute requirement
  - **SHOULD**: Strong recommendation (exceptions need justification)
  - **MAY**: Optional or discretionary
- Avoid vague terms like "fast", "soon", "better" without quantification

---

## FINAL INSTRUCTIONS FOR AI ASSISTANT

### Chain Execution Mode

**Full Chain (Default):**
1. Execute Phase 1: Memory Review & Context Extraction
2. Execute Phase 2: Idea Exploration & Validation
3. Execute Phase 3: PRD Generation
4. Confirm completion to user

**Quick Mode (New Project):**
1. Skip Phase 1 (no memory system)
2. Execute Phase 2: Idea Exploration (without memory context)
3. Execute Phase 3: PRD Generation
4. Confirm completion to user

**Iteration Mode (Refinement):**
1. Re-run Phase 2 with updated questions
2. Re-run Phase 3 with new Requirements Summary
3. Preserve version history in PRD header

### Key Principles

1. **Always review memory system first** (if exists) - Phase 1 silent background activity
2. **Apply decision frameworks** - Use scoring and formulas to guide questioning
3. **Monitor red flags** - Proactively surface risks during discovery
4. **Batch questions** (max 3 per round) - Don't overwhelm user
5. **Check stopping criteria** - Use objective scoring, not gut feel
6. **Document assumptions** - Every assumption gets risk assessment and validation method
7. **Confirm understanding** - Summarize and get user confirmation before generating
8. **Generate complete PRD** - All sections, specific and actionable, no placeholders
9. **Validate completeness** - Use pre-save checklist before saving
10. **Save immediately** - To `/tasks/prd-[feature-name].md`
11. **Do NOT implement** - Unless explicitly requested by user

### Anti-Patterns to Avoid

**DON'T:**
- Ask all questions in one overwhelming batch (max 3 at a time)
- Continue questioning past clear stopping criteria (check score)
- Skip memory system review if it exists
- Leave sections empty without explicit justification
- Use vague terms without quantification
- Create generic requirements that need more clarification
- Forget to confirm understanding before generating PRD
- Generate PRD without asking ANY questions (unless trivially simple)
- Skip red flag detection
- Forget to document assumptions with validation methods

**DO:**
- Batch questions (max 3 at a time)
- Use decision frameworks to guide questioning
- Proactively surface red flags
- Document all assumptions with risk assessment
- Stop when stopping criteria score = 100%
- Leverage memory system to inform questions
- Fill all sections with specific, actionable content
- Quantify all vague terms (fast = <200ms)
- Create atomic, testable requirements
- Confirm understanding before PRD generation
- Ask clarifying questions based on user's idea

---

## SUCCESS METRICS

### PRD Quality
- **Completeness:** All sections filled with specific, actionable content (no "TBD" placeholders)
- **Clarity:** Junior developer can implement without additional clarification
- **Testability:** All acceptance criteria are measurable and verifiable
- **Implementability:** Requirements are atomic and directly actionable
- **Assumptions Documented:** All assumptions have risk assessment and validation methods
- **Red Flags Identified:** Proactive risk identification during discovery

[IF MEMORY SYSTEM EXISTS:]
- **Architecture Alignment:** Components map to existing patterns
- **Integration Clarity:** All dependencies identified and referenced
- **Pattern Reuse:** Leverages existing patterns where appropriate

### Process Efficiency
- **Question Quality:** Questions informed by context, not generic
- **Stopping Criteria:** Objective scoring used (not gut feel)
- **Red Flag Detection:** Risks surfaced during questioning, not after
- **Time to PRD:** Reasonable time from initial prompt to saved document
- **Assumption Coverage:** All assumptions identified and validated
- **Confirmation:** User confirms understanding before PRD generation

### User Experience
- **Question Batching:** Max 3 questions at a time (not overwhelming)
- **Progressive Refinement:** Each round builds on previous answers
- **Conflict Resolution:** Identifies and resolves conflicts with existing system
- **Idea Clarity:** User's vision fully understood before architectural fitting
- **Risk Awareness:** User aware of red flags before committing to implementation

---

**Remember:** The goal is comprehensive idea exploration FIRST, then efficient architectural integration using memory system. Balance thoroughness with efficiency using decision frameworks and objective stopping criteria.
