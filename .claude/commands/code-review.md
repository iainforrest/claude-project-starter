---
description: Run thorough code review on recent changes using Claude and Codex in parallel
---

# Code Review Command (Dual-Model)

**Objective:** Run comprehensive code review using both Claude (Opus) and OpenAI Codex in parallel, merging findings for maximum coverage with deduplication.

## Review Modes

- **Single Model (Codex)**: Use `--codex-only` for fast Codex-only review
- **Dual Model (Default)**: Claude + Codex in parallel, findings merged

## When to Use

- **End of sprint**: Before `/update` and `/commit`
- **Mid-sprint checkpoint**: After completing a significant feature
- **Before PR**: To catch issues before code review by humans
- **On-demand**: Anytime you want fresh eyes on recent work

## Execution Flow

### Mode Selection

If `--codex-only` flag is present:
- Skip parallel model spawning
- Run original Codex-only flow (Step 4)
- Output is not JSON-merged

Default: Dual-model parallel review

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

### Step 2: Parallel Model Review (Dual-Model Mode)

Skip this step when `--codex-only` is set.

Spawn both models in parallel. Each reviews independently.

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

**Claude (Opus) Review:** Task tool with code-review-agent

```
Task(
  subagent_type: "general-purpose",
  model: "opus",
  prompt: """
  Read .claude/agents/code-review-agent.md for your full protocol.

  Output your findings in JSON format as specified in the agent file.

  THE CHANGES TO REVIEW:
  {diff content from /tmp/git-diff.txt}
  """
)
```

Write Claude output to `/tmp/code-review-claude.json`.

**Codex Review:** Bash with codex exec

```bash
codex exec --full-auto "$(cat .claude/agents/code-review-agent.md)

Output your findings in JSON format as specified in the JSON Output Schema section.

THE CHANGES TO REVIEW:
$(cat /tmp/git-diff.txt)
" 2>&1 | tee /tmp/code-review-codex.json
```

**Codex Failure Handling:**
If Codex fails (non-zero exit, empty output, rate limit):
1. Log: "Codex failed. Proceeding with Claude-only review."
2. Continue with Claude findings only
3. Mark all findings as source: "claude"

### Step 3: Merge Findings (Dual-Model Mode)

Skip this step when `--codex-only` is set.

After both models complete, merge their findings.

**Inputs:** `/tmp/code-review-claude.json` and `/tmp/code-review-codex.json`

**Deduplication Algorithm:**

For each finding, compute a hash using:
```
hash = hash(normalize(severity + category + location + first_50_chars_of_issue))
```

Notes:
- `location` is the file path + line range (for example: `src/file.ts:12-24`)
- `normalize()` lowercases and removes whitespace for consistent matching
- `first_50_chars_of_issue` comes from the start of the `issue` text

**Merge Rules:**
1. If the same hash appears in both model outputs:
   - Keep one finding
   - Set `source: "both"`
   - Set `confidence: "convergent"`
   - Prefer the more detailed issue description (longer text)

2. If the hash appears in only one model output:
   - Keep the finding
   - Set `source: "claude"` or `source: "codex"`
   - Set `confidence: "single-model"`

3. Similar but not identical findings (same file:line, different severity):
   - Keep both findings
   - Mark them as related (for example: `related: true`)
   - Note the severity mismatch in the summary

**Output:** Write merged findings to `/tmp/code-review-merged.json`

**Summary Display:**
```
## Dual-Model Code Review Complete

**Findings by Model:**
- Convergent (both models): X
- Claude only: Y
- Codex only: Z
- Total unique: X+Y+Z

**Findings by Severity:**
- CRITICAL: X
- HIGH: X
- MEDIUM: X
- LOW: X
```

### Step 4: Run Codex Review (Codex-only Mode)

Only run this step when `--codex-only` is set (legacy flow).

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

### Step 5: Present Findings

After review completes:
1. For dual-model: read merged results from `/tmp/code-review-merged.json`
2. For codex-only: read the output from `/tmp/codex-review-output.txt`
3. Extract the summary section with model and severity counts
4. Present findings to the user in a clear summary

For codex-only mode, omit model breakdown and convergent tags; all findings are single-model (Codex).

**Summary format:**
```
## Code Review Complete

**Findings by Model:**
- Convergent (both models): X
- Claude only: Y
- Codex only: Z

**Findings by Severity:**
- CRITICAL: X
- HIGH: X
- MEDIUM: X
- LOW: X

[Show findings grouped by severity]
```

**Convergent Finding Indicator:**

When presenting findings, mark convergent ones specially:

```
### [CR-001] Security: SQL Injection Risk [CONVERGENT]
**Severity**: CRITICAL
**Source**: Both models
**Confidence**: High
...
```

Single-model findings should show their source and lower confidence:
- **Source**: Claude or Codex
- **Confidence**: Single-model

### Step 6: Auto-Fix Option (CRITICAL/HIGH)

If CRITICAL or HIGH findings exist in merged results (dual-model) or review output (codex-only), offer to auto-fix:

```
Found X CRITICAL and Y HIGH issues. Would you like me to auto-fix these?
- Yes: Codex will attempt to fix all CRITICAL and HIGH issues
- No: Review findings and fix manually
```

**If user approves auto-fix:**

Extract CRITICAL and HIGH findings:
- **Dual-model mode**: Read from `/tmp/code-review-merged.json`
- **Codex-only mode**: Read from `/tmp/codex-review-output.txt`

Then run Codex in full-auto mode:

```bash
codex exec --full-auto "Fix the following code review issues. Be precise and only change what's needed.

ISSUES TO FIX:
[Paste CRITICAL and HIGH findings from merged results]

Read the relevant files, make the fixes, and verify they work.
Do NOT make any changes beyond what's needed to fix these specific issues."
```

**After auto-fix completes:**
1. Show what was changed: `git diff`
2. Offer to re-run the review to verify fixes
3. If issues remain, present them for manual review

### Step 7: Triage MEDIUM/LOW Findings

After CRITICAL/HIGH issues are fixed (or if none exist), triage remaining MEDIUM and LOW findings.

**Skip this step if:**
- User passed `--no-triage` flag
- No MEDIUM or LOW findings exist

**Batch Mode Detection:**

If more than 5 MEDIUM/LOW findings exist, offer batch options first:

```
Found 12 MEDIUM/LOW findings. Would you like to:
1. Triage each individually
2. Add all to tech debt (TECH_DEBT.md)
3. Skip all non-critical findings
```

**Individual Triage:**

For each MEDIUM or LOW finding, present to user:

```
[CR-005] Code Quality: Magic number in timeout calculation
Severity: MEDIUM | Source: Claude only | Confidence: Single-model
Location: src/services/retry.ts:45

Issue: Hardcoded timeout value 30000 should be a named constant

Why it matters: Reduces code readability and makes future changes harder

Recommended fix: Extract to TIMEOUT_MS constant at file top

Options:
1. Fix now - Address this before proceeding
2. Tech debt - Add to TECH_DEBT.md for later
3. Skip - Not worth tracking

Your choice (1/2/3)?
```

**Based on user response:**

- **1 (Fix now)**: Add to `/tmp/code-review-fixes.json` for batch fixing
- **2 (Tech debt)**: Add to `/tmp/tech-debt-additions.json`
- **3 (Skip)**: Do not track, continue to next finding

**After triage completes:**

If any findings were marked "Fix now":
1. Extract all deferred fixes from `/tmp/code-review-fixes.json`
2. Run Codex auto-fix with these findings:
   ```bash
   codex exec --full-auto "Fix the following code review issues...
   [Paste findings marked for immediate fix]
   ..."
   ```
3. Show what was changed: `git diff`
4. Offer to re-run review if significant changes

If any findings were marked "Tech debt":
- Proceed to Step 8 to update TECH_DEBT.md

### Step 8: Update TECH_DEBT.md

Only run this step if findings were added to `/tmp/tech-debt-additions.json` during triage.

**Process:**

1. Read current `.ai/TECH_DEBT.md`
2. Find highest `TD-XXX` number in the file
3. For each tech debt item from `/tmp/tech-debt-additions.json`:
   - Assign next sequential `TD-XXX` ID
   - Format using the TECH_DEBT.md template
   - Include source attribution: `Source: CR-YYYY-MM-DD (Claude only | Codex only | Both)`
   - Add `Added: YYYY-MM-DD` timestamp
4. Append entries to appropriate severity section (MEDIUM or LOW)
5. Update the summary table at the top of TECH_DEBT.md

**Example Entry:**

```markdown
#### [TD-015] retry.ts: Magic number in timeout

**Severity**: MEDIUM
**Location**: `src/services/retry.ts:45`
**Description**: Hardcoded timeout value 30000 should be a named constant
**Why Deferred**: Low impact, cosmetic improvement
**Impact**: Reduces code readability
**Suggested Fix**: Extract to TIMEOUT_MS constant at file top
**Added**: 2026-02-02
**Source**: CR-2026-02-02 (Claude only)
```

**After updating TECH_DEBT.md:**
- Confirm: "Added X items to tech debt"
- Show the new TD-XXX IDs assigned

### Step 9: Wrap Up

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
