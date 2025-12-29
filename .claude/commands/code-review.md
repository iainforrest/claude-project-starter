---
description: Run thorough code review on recent changes
---

# Code Review Command

**Objective:** Run a comprehensive code review on recent changes, outputting structured findings that can feed into task generation.

## When to Use

- **End of sprint**: Before `/update` and `/commit`
- **Mid-sprint checkpoint**: After completing a significant feature
- **Before PR**: To catch issues before code review by humans
- **On-demand**: Anytime you want fresh eyes on recent work

## Execution

Invoke the code-review-agent to analyze recent changes:

```
Use Task tool with subagent_type='code-review-agent'

Prompt: "Review all recent changes against project patterns and standards.
Analyze uncommitted changes and commits since [last sprint/specific commit].
Output structured findings with severity levels."
```

## What Gets Reviewed

The agent analyzes:
- All uncommitted changes (`git diff`, `git diff --cached`)
- Recent commits (configurable scope)

Against:
- `.ai/PATTERNS.md` - Established patterns
- `.ai/ARCHITECTURE.json` - Architectural constraints
- `.ai/BUSINESS.json` - Business logic rules
- Project coding standards

## Review Domains

1. **Pattern Adherence** - Following established patterns
2. **Architectural Alignment** - Respecting boundaries and data flows
3. **Code Quality** - Readability, maintainability, simplicity
4. **Security** - Input validation, secrets, auth
5. **Testing** - Coverage for new code paths
6. **Performance** - No obvious anti-patterns
7. **Error Handling** - Comprehensive and consistent
8. **Documentation** - Complex logic explained

## Output Format

Structured findings with severity levels:
- **CRITICAL** - Must fix immediately
- **HIGH** - Should fix before proceeding
- **MEDIUM** - Create task for next sprint
- **LOW** - Optional improvement

Each finding includes:
- Exact file:line location
- Clear description of issue
- Why it matters
- Recommended fix
- Task-ready description for task generation

## Handling Findings

### If CRITICAL or HIGH findings exist:
1. Extract tasks from review output
2. Add to current task list
3. Execute fixes
4. Re-run review if changes were significant

### If only MEDIUM/LOW findings:
1. Document for future action
2. Proceed with `/update` and `/commit`

## Integration with Pipeline

**Full pipeline:**
```
/execute → /code-review → (fix tasks if needed) → /update → /commit
```

**Standalone:**
```
/code-review → assess findings → take action as needed
```

## Example Usage

**End of sprint:**
```
"Run /code-review to check all changes before we update memory and commit"
```

**After feature completion:**
```
"Run /code-review on the authentication feature I just finished"
```

**Scoped review:**
```
"Run /code-review on commits since abc123"
```
