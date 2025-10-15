# Development System Bootstrap

**Welcome!** This interactive process will set up a complete AI-assisted development system customized for your project.

## How This Works

### The Process

1. **Question Gathering** (6-8 rounds)
   - I'll ask 1-3 related questions at a time
   - You answer based on what you know (or say "not sure yet")
   - I'll validate your answers and provide tech recommendations
   - We'll handle clarifications without losing track

2. **Plan Generation**
   - I'll create `bootstrap_tasks.md` using task generation principles
   - You review the plan before I execute it

3. **Systematic Execution**
   - I follow task execution rules to customize all files
   - I'll mark progress as I go
   - All files will be tailored to your project

4. **Final Setup**
   - Optional git configuration
   - Recommendations for next steps

### What Gets Customized

- `.claude/` rule files (PRD/Task/Execution processes)
- `.ai/` memory system (architecture, patterns, commands)
- Everything specific to your tech stack and workflow

### Time Required

- Question rounds: 10-15 minutes
- Execution: 5-10 minutes
- Total: ~20-25 minutes

---

## For Claude: Bootstrap Instructions

### Critical Rules

**STAY ON TRACK**: Use the internal checklist below to prevent getting lost in conversations. After each user response:
1. Validate/provide feedback
2. Handle ONE round of clarifying questions if needed
3. Return to checklist and proceed to next uncompleted round
4. If user goes off-topic: acknowledge, note for later, redirect politely

**NEVER skip rounds**. Complete all 8 rounds before proceeding to plan generation.

---

## Internal Question Checklist (FOR CLAUDE)

Track progress through this checklist. Do NOT skip ahead.

- [ ] Round 1: Project Basics (type, goal, name)
- [ ] Round 2: Technology Stack (validate compatibility)
- [ ] Round 3: Build & Test Systems
- [ ] Round 4: Architecture Patterns
- [ ] Round 5: Scale & Complexity
- [ ] Round 6: Development Workflow
- [ ] Round 7: Special Requirements
- [ ] Round 8: Confirmation & Recommendations
- [ ] Generate bootstrap_tasks.md
- [ ] Execute bootstrap_tasks.md
- [ ] Final setup (git, recommendations)

**Current Round**: [Update this as you progress]

---

## Round 1: Project Basics

**Ask these 3 questions:**

1. **What type of project are you building?**
   - Examples: Web app, mobile app (iOS/Android), API/web service, CLI tool, library/SDK, desktop app, game, other
   - User can be specific (e.g., "React web app") or general (e.g., "website")

2. **In 1-2 sentences, what does this project do?**
   - What problem does it solve?
   - Who is it for?

3. **Do you have a project name yet?**
   - If yes: what is it?
   - If no: we can use a placeholder

**After user answers:**
- Validate the project type makes sense
- If ambiguous, ask ONE clarifying question
- Note the answers internally
- **Return to checklist and proceed to Round 2**

---

## Round 2: Technology Stack

**Ask these questions (adapt based on Round 1):**

1. **What programming language will you use?**
   - If they know: note it
   - If unsure: "I can recommend based on your project type"
   - Common: JavaScript/TypeScript, Python, Java/Kotlin, Swift, Rust, Go, C#, Ruby, PHP

2. **Are you planning to use any specific frameworks or libraries?**
   - If they know: note them
   - If unsure: "I can suggest popular options for [language]"
   - Examples: React/Vue/Angular, Django/Flask/FastAPI, Spring Boot, SwiftUI, etc.

3. **(If applicable) Are there any other key technologies?**
   - Database (PostgreSQL, MongoDB, etc.)
   - Cloud platform (AWS, GCP, Azure, Vercel, etc.)
   - Other tools or services

**After user answers:**
- **VALIDATE TECH COMPATIBILITY**:
  - If good combination: "That stack works well together!"
  - If potential issues: "Note: [Framework X] requires [Language Y version Z+], is that okay?"
  - If incompatible: "That combination might cause issues because [reason]. Consider [alternative]?"
- If user said "not sure": offer 2-3 recommendations with brief reasoning
- Note all answers
- **Return to checklist and proceed to Round 3**

---

## Round 3: Build & Test Systems

**Ask these questions:**

1. **What build system will you use?**
   - Based on their tech stack, suggest if unknown
   - Examples: Gradle, npm/yarn/pnpm, cargo, make, CMake, Maven, pip/poetry
   - If unsure: "For [your language], I recommend [build tool]"

2. **What testing framework do you prefer?**
   - Examples: Jest/Vitest, pytest, JUnit, XCTest, etc.
   - If unsure: "I'll use the standard for [language]"

3. **Any other development tools you want to use?**
   - Linters, formatters, CI/CD tools, etc.
   - Can be "none yet" or "standard ones"

**After user answers:**
- Validate build tool matches their tech stack
- Provide brief reasoning if suggesting tools
- Note all answers
- **Return to checklist and proceed to Round 4**

---

## Round 4: Architecture Patterns

**Ask these questions:**

1. **Do you have an architectural pattern in mind?**
   - Examples: MVVM, Clean Architecture, MVC, Hexagonal, Layered, Microservices, Modular Monolith
   - If unsure: "For [project type], [Pattern X] works well because [reason]"

2. **Will this be a single-component app or multi-component system?**
   - Single: one main application
   - Multi: frontend + backend, microservices, modular system, etc.

**After user answers:**
- Validate pattern fits their project type
- If they chose pattern that's unusual for their type: gentle feedback with alternative
- If multi-component: note how components will interact
- **Return to checklist and proceed to Round 5**

---

## Round 5: Scale & Complexity

**Ask these questions:**

1. **Expected project size/complexity?**
   - Small: Personal project, simple app, < 50 files
   - Medium: Professional project, moderate complexity, 50-500 files
   - Large: Enterprise project, complex system, 500+ files

2. **Expected team size?**
   - Solo developer
   - Small team (2-5 developers)
   - Large team (6+ developers)

**After user answers:**
- Validate scale expectations match project description
- If mismatch (e.g., "simple personal project" but "large team"): clarify
- Note answers
- **Return to checklist and proceed to Round 6**

---

## Round 6: Development Workflow

**Ask these questions:**

1. **Git workflow preference?**
   - Feature branches (GitHub Flow, GitFlow, etc.)
   - Trunk-based development
   - Standard/no preference yet

2. **Any CI/CD plans?**
   - GitHub Actions, GitLab CI, Jenkins, CircleCI, etc.
   - Not yet / will add later
   - None needed

**After user answers:**
- Note preferences
- If no preference: suggest based on team size
- **Return to checklist and proceed to Round 7**

---

## Round 7: Special Requirements

**Ask these questions:**

1. **Any critical performance requirements?**
   - Real-time performance, low latency, high throughput
   - Offline capability
   - Resource constraints
   - None specific

2. **Any security or compliance requirements?**
   - Authentication/authorization needs
   - Data privacy (GDPR, HIPAA, etc.)
   - Security standards
   - Standard security practices

3. **Any other special considerations?**
   - Accessibility requirements
   - Internationalization
   - Platform-specific constraints
   - Anything else important to your project

**After user answers:**
- Note all requirements
- Validate requirements are feasible with chosen tech stack
- If concerns: mention them briefly
- **Return to checklist and proceed to Round 8**

---

## Round 8: Confirmation & Recommendations

**Present a summary:**

```markdown
## Project Configuration Summary

**Project**: [Name]
**Type**: [Type]
**Description**: [User's description]

**Technology Stack:**
- Language: [Language]
- Framework: [Framework(s)]
- Build System: [Build tool]
- Testing: [Test framework]
- [Other tech if mentioned]

**Architecture:**
- Pattern: [Pattern]
- Structure: [Single/Multi-component]

**Scale:**
- Size: [Small/Medium/Large]
- Team: [Solo/Small/Large]

**Workflow:**
- Git: [Workflow]
- CI/CD: [Tools or None]

**Special Requirements:**
- Performance: [Requirements]
- Security: [Requirements]
- Other: [Requirements]
```

**Then:**

1. **If user said "not sure" to any tech questions**: Provide recommendations now
   - "Based on your project, I recommend [specific stack] because [reasons]"
   - List 2-3 key recommendations with brief explanations

2. **Ask for confirmation**:
   - "Does this look correct?"
   - "Any changes needed?"

3. **After user confirms**:
   - Note final configuration
   - **Return to checklist and proceed to Plan Generation**

---

## Phase 2: Generate bootstrap_tasks.md

**Instructions for Claude:**

Now create `bootstrap_tasks.md` following `.claude/TASK_GENERATION.md` principles.

### Task File Structure

```markdown
# Bootstrap Task List

**Generated from**: BOOTSTRAP.md
**Date**: [Current date]
**Project**: [Project name]
**Pattern**: Bootstrap setup pattern

## Overview

Customize the development system starter kit for [Project name].

**Tech Stack**: [Summary]
**Architecture**: [Pattern]
**Build System**: [Build tool]

## Tasks

### 1.0 Customize .claude/ Rule Files
**Goal**: Replace all placeholders with project-specific values
**Files**: PRD_GENERATION.md, TASK_GENERATION.md, TASK_EXECUTION.md
**Validation**: All [PLACEHOLDERS] replaced correctly

- [ ] 1.1 - complexity 2/5 - Customize PRD_GENERATION.md
  - **Placeholders**: [List all to replace]
  - **Values**: [Specific values]

- [ ] 1.2 - complexity 2/5 - Customize TASK_GENERATION.md
  - **Placeholders**: [List all to replace]
  - **Values**: [Specific values]

- [ ] 1.3 - complexity 2/5 - Customize TASK_EXECUTION.md
  - **Placeholders**: [List all to replace]
  - **Values**: [Specific values]

### 2.0 Initialize .ai/ Memory System
**Goal**: Create project-specific memory file templates
**Files**: All .ai/ files except README.md
**Validation**: Structure correct, initial content added

- [ ] 2.1 - complexity 2/5 - Initialize ARCHITECTURE.json
  - **Add**: Project type, architecture pattern, initial structure

- [ ] 2.2 - complexity 2/5 - Initialize BUSINESS.json
  - **Add**: Project description, tech stack, initial metadata

- [ ] 2.3 - complexity 2/5 - Initialize FILES.json
  - **Add**: Initial folder structure expectations

- [ ] 2.4 - complexity 1/5 - Initialize PATTERNS.md
  - **Add**: Architecture pattern template

- [ ] 2.5 - complexity 1/5 - Initialize QUICK.md
  - **Add**: Build commands, test commands, project structure

- [ ] 2.6 - complexity 1/5 - Initialize TODO.md
  - **Add**: First task: "Set up initial project structure"

### 3.0 Validation
**Goal**: Verify all customizations are correct
**Validation**: No placeholders remain, all values make sense

- [ ] 3.1 - complexity 1/5 - Validate .claude/ files
  - **Check**: No [PLACEHOLDERS] remain
  - **Check**: Tech-specific values are correct

- [ ] 3.2 - complexity 1/5 - Validate .ai/ files
  - **Check**: Initial structure is correct
  - **Check**: Metadata matches user's project
```

**After generating bootstrap_tasks.md:**
1. Show the task file to the user
2. Ask: "Does this plan look good?"
3. If user approves, proceed to execution
4. If user wants changes, update and re-confirm

---

## Phase 3: Execute bootstrap_tasks.md

**Instructions for Claude:**

Follow `.claude/TASK_EXECUTION.md` rules to execute `bootstrap_tasks.md`.

### Execution Rules

1. **Start with Task 1.0** (Customize .claude/ files)
2. **Mark each subtask [x] immediately after completing it**
3. **For each file**:
   - Read the current generic file
   - Replace all placeholders with project-specific values
   - Verify no placeholders remain
   - Save the customized file

4. **Proceed to Task 2.0** (Initialize .ai/ files)
5. **For each .ai/ file**:
   - Use the template structure
   - Add initial project-specific content
   - Add helpful comments where needed
   - Save the file

6. **Complete Task 3.0** (Validation)
7. **Verify**:
   - All placeholders replaced
   - All files customized correctly
   - System ready to use

8. **Mark parent tasks [x] after all subtasks complete**

### No Build Verification

Since there's no code yet, skip build verification steps. Focus on file generation and validation.

---

## Phase 4: Final Setup

**After bootstrap_tasks.md is complete:**

### Git Setup (Optional)

Ask the user:

1. **"Would you like to set up git for this project?"**
   - If NO: skip to recommendations
   - If YES: proceed to next question

2. **"Should the .ai/ memory system folder be added to .gitignore?"**
   - If YES: create/update .gitignore with `.ai/` entry
   - If NO: memory system will be tracked in git
   - Explain trade-offs if user unsure:
     - Track: Team shares memory, larger repo
     - Ignore: Private memory, everyone builds their own

3. **If setting up git:**
   ```bash
   git init
   git add .
   git commit -m "Initial commit: Development system bootstrap complete"
   ```

### Recommendations

Present these recommendations:

```markdown
## Bootstrap Complete! 🎉

Your development system is ready. Here's what to do next:

### Immediate Next Steps

1. **Run `claude init`** to create your CLAUDE.md file
   - This file will guide Claude in understanding your project
   - See README.md for what typically goes in CLAUDE.md

2. **Review the memory system**:
   - Read `.ai/README.md` to understand how memory works
   - Review initialized memory files in `.ai/`
   - Add project-specific details as you learn more

3. **Clean up (optional)**:
   - Delete `bootstrap_tasks.md` if you don't need it
   - Keep or delete `BOOTSTRAP.md` (up to you)

### Start Building

1. **Create your first feature**:
   - Use `.claude/PRD_GENERATION.md` to create a PRD
   - Use `.claude/TASK_GENERATION.md` to break it into tasks
   - Use `.claude/TASK_EXECUTION.md` to implement systematically

2. **Update memory regularly**:
   - After each sprint, update `.ai/` files
   - Follow `.ai/SPRINT_UPDATE.md` for guidance

3. **Let the system grow with your project**:
   - Add patterns as you discover them
   - Update architecture as it evolves
   - Keep memory files current

### Files Created/Customized

- `.claude/` - 3 rule files customized for your tech stack
- `.ai/` - 8 memory files initialized for your project
- `bootstrap_tasks.md` - Task list (can delete)
[- `.gitignore` - Configured for your preferences (if git setup)]

### Project Configuration

[Repeat the summary from Round 8]

Ready to build something amazing! 🚀
```

---

## Anti-Rabbit-Hole Protocol

**For Claude**: If at any point during questions the user:
- Asks clarifying questions: answer briefly, return to current round
- Goes off-topic: "Good point - let's note that for later. First, let's finish [current round]..."
- Wants to discuss implementation details: "We'll handle that during setup. For now, [return to current question]"
- Seems uncertain: offer guidance, but keep moving forward

**Always return to the Internal Question Checklist after each interaction.**

**Never proceed to plan generation until all 8 rounds are complete.**

---

## Error Recovery

If something goes wrong during execution:
1. Note the error
2. Fix the issue
3. Resume from the failed task
4. Don't skip tasks

If user wants to restart:
1. Clear all generated files except templates
2. Restart from Round 1

---

## Ready to Start?

**Claude**: Begin with Round 1 questions now. Remember to use the Internal Question Checklist to stay on track!
