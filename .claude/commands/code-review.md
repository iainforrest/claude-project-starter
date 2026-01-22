---
description: Run thorough code review on recent changes using Codex
---

# Code Review Command (Codex-Powered)

**Objective:** Run a comprehensive code review using OpenAI Codex CLI, outputting structured findings with optional auto-fix for critical issues.

## When to Use

- **End of sprint**: Before `/update` and `/commit`
- **Mid-sprint checkpoint**: After completing a significant feature
- **Before PR**: To catch issues before code review by humans
- **On-demand**: Anytime you want fresh eyes on recent work

## Execution Flow

### Step 1: Determine Review Scope

Check what the user wants to review:
- **Default**: Uncommitted changes
- **Branch comparison**: Changes against a base branch (e.g., `--base main`)
- **Specific commit**: A single commit (e.g., `--commit abc123`)

If the user hasn't specified, check for uncommitted changes:
```bash
git status --porcelain
```

If there are uncommitted changes, review those. Otherwise, ask what to review.

### Step 2: Run Codex Review

**Option A: Quick Review (Codex Built-in)**

For a fast review using Codex's default review logic:
```bash
codex review --uncommitted 2>&1 | tee /tmp/codex-review-output.txt
```

For branch comparison:
```bash
codex review --base main 2>&1 | tee /tmp/codex-review-output.txt
```

**Option B: Full Review (Custom Instructions)**

For a comprehensive review with project-specific criteria, use `codex exec` with the full prompt from the agent file.

First, prepare the diff based on scope:

**For uncommitted changes (including untracked files):**
```bash
git add -N .  # Stage untracked for diff visibility
git diff > /tmp/git-diff.txt
git diff --cached >> /tmp/git-diff.txt
git reset HEAD -- . 2>/dev/null || true  # Reset intent-to-add
```

**For branch comparison:**
```bash
git diff main...HEAD > /tmp/git-diff.txt
```

**For specific commit:**
```bash
git show <commit> > /tmp/git-diff.txt
```

Then run Codex with the review prompt. Read `.claude/agents/code-review-agent.md` and pass its content as the prompt:

```bash
codex exec "$(cat .claude/agents/code-review-agent.md)

THE CHANGES TO REVIEW:
$(cat /tmp/git-diff.txt)
" 2>&1 | tee /tmp/codex-review-output.txt
```

**Notes:**
- The review runs non-interactively (no TTY required)
- Output is captured to `/tmp/codex-review-output.txt`
- Use Option A for quick checks, Option B for thorough pre-merge reviews

### Step 3: Present Findings

After Codex completes:
1. Read the output from `/tmp/codex-review-output.txt`
2. Extract the summary section with finding counts (CRITICAL, HIGH, MEDIUM, LOW)
3. Present findings to the user in a clear summary

**Summary format:**
```
## Code Review Complete

**Findings:**
- CRITICAL: X
- HIGH: X
- MEDIUM: X
- LOW: X

[Show findings grouped by severity]
```

### Step 4: Auto-Fix Option (CRITICAL/HIGH)

If CRITICAL or HIGH findings exist, offer to auto-fix:

```
Found X CRITICAL and Y HIGH issues. Would you like me to auto-fix these?
- Yes: Codex will attempt to fix all CRITICAL and HIGH issues
- No: Review findings and fix manually
```

**If user approves auto-fix:**

Extract the task list from the review output and run Codex in full-auto mode:

```bash
codex exec --full-auto "Fix the following code review issues. Be precise and only change what's needed.

ISSUES TO FIX:
[Paste CRITICAL and HIGH findings from review]

Read the relevant files, make the fixes, and verify they work.
Do NOT make any changes beyond what's needed to fix these specific issues."
```

**After auto-fix completes:**
1. Show what was changed: `git diff`
2. Offer to re-run the review to verify fixes
3. If issues remain, present them for manual review

### Step 5: Wrap Up

After review (and optional fixes):
- If all CRITICAL/HIGH resolved: "Ready for `/update` and `/commit`"
- If issues remain: List remaining tasks for manual attention

## Configuration Options

**Model selection:**
```bash
codex exec -m gpt-5.2-codex "..."
```

**Higher reasoning effort for complex codebases:**
```bash
codex exec -c 'model_reasoning_effort="high"' "..."
```

**Full auto mode (for fixes):**
```bash
codex exec --full-auto "..."
```

## Review Domains

The review checks against:
- `.ai/PATTERNS.md` - Established patterns
- `.ai/ARCHITECTURE.json` - Architectural constraints
- `.ai/BUSINESS.json` - Business logic rules
- Project coding standards

Domains covered:
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

## Example Usage

**Standard review of uncommitted changes:**
```
User: /code-review
Claude: [Checks git status, runs codex review]
Claude: [Presents findings]
Claude: Found 2 HIGH issues. Would you like me to auto-fix?
User: Yes
Claude: [Runs codex exec --full-auto to fix]
Claude: [Shows diff and results]
```

**Quick review:**
```
User: /code-review quick
Claude: [Runs codex review --uncommitted with default logic]
```

**Review against main branch:**
```
User: /code-review --base main
Claude: [Runs codex review --base main]
```

**Review without auto-fix:**
```
User: /code-review --no-fix
Claude: [Runs review, presents findings, doesn't offer auto-fix]
```

## Integration with Pipeline

**Full pipeline:**
```
/execute → /code-review → (auto-fix if needed) → /update → /commit
```

**Standalone:**
```
/code-review → assess findings → take action as needed
```

## Troubleshooting

**If Codex times out:**
- The review may take 1-2 minutes for large changesets
- Consider using Option A (quick review) for faster feedback

**If Codex can't read memory files:**
- Verify `.ai/` directory exists
- Codex will proceed with general best practices if files are missing

**If auto-fix introduces new issues:**
- Re-run `/code-review` to catch any regressions
- Consider manual review for complex fixes
