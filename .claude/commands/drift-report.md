---
description: Weekly drift analysis - aggregate patterns from code reviews into systemic insights and required decisions
---

# Weekly Drift Report Command

## Purpose

Turn individual code review findings into **systemic insights**. This command fights entropy by:
- Aggregating violation patterns over time
- Identifying hotspots (files/areas with repeated issues)
- Forcing decisions: fix, revise rules, or accept as tech debt
- Feeding improvements back into PATTERNS.md

**Core insight:** Individual code reviews catch issues. Drift reports catch *patterns of issues* that indicate systemic problems - bad rules, missing training, or architectural rot.

---

## When to Run

- **Weekly:** End of sprint or weekly checkpoint
- **Before retrospectives:** Feed insights into team discussions
- **After major features:** Check if new patterns emerged
- **When something feels off:** "We keep hitting the same issues"

---

## Data Sources

The report aggregates from multiple sources:

| Source | What It Provides |
|--------|------------------|
| `.ai/TECH_DEBT.md` | Accumulated deferred issues with severity and dates |
| `.ai/PATTERNS.md` | Current rules/patterns being enforced |
| `.ai/solutions/` | Recently captured solutions (patterns emerging?) |
| Git history | Recent commits, files changed frequently |
| Code review outputs | Recent findings (if saved to `/tmp/codex-review-*.txt`) |

---

## Execution Process

### Step 1: Gather Data

**Read all data sources in parallel:**

```
1. Read .ai/TECH_DEBT.md - parse entries by severity, location, date added
2. Read .ai/PATTERNS.md - understand current rule set
3. List .ai/solutions/*.yaml - check for recent solutions (last 2 weeks)
4. Run: git log --oneline --since="2 weeks ago" - recent commit activity
5. Run: git log --since="2 weeks ago" --name-only --pretty=format: | sort | uniq -c | sort -rn | head -20
   (most frequently changed files)
6. Check for code review outputs: ls -la /tmp/codex-review-*.txt 2>/dev/null
```

### Step 2: Analyze Patterns

**For each data source, extract:**

**From TECH_DEBT.md:**
- Count by severity (CRITICAL/HIGH/MEDIUM/LOW)
- Count by category (Security/Architecture/Pattern/Quality/Testing/Performance)
- Count by location (which files/directories appear most?)
- Age distribution (how old is the oldest debt?)

**From solutions/:**
- Tags frequency (which problem types keep recurring?)
- Component frequency (which areas need repeated solutions?)

**From git history:**
- Hotspot files (changed frequently = high churn = potential problem area)
- Correlation: Do hotspot files also appear in TECH_DEBT.md?

**From code review outputs (if available):**
- Finding categories and frequencies
- Which rules triggered most violations?

### Step 3: Diagnose Hotspots

For each hotspot identified, diagnose the root cause:

| Diagnosis | Indicators | Action |
|-----------|------------|--------|
| **Training problem** | Same violation by different people, rule exists but not followed | Improve onboarding, add examples to PATTERNS.md |
| **Rule problem** | High exception rate, rule conflicts with reality | Revise or deprecate the rule |
| **Architecture problem** | Violations concentrated in integration points, coupling issues | Consider refactoring, add to roadmap |
| **Process problem** | Issues slip through review, caught late | Improve review checklist, add automation |

### Step 4: Generate Report

**Output format:**

```markdown
# Weekly Drift Report
**Period:** [Date range]
**Generated:** [Today's date]

---

## Executive Summary

**Health Score:** [Good / Needs Attention / Critical]
**Key Finding:** [One sentence summary of most important insight]

---

## Violation Patterns

### By Severity
| Severity | Count | Trend vs Last Period |
|----------|-------|---------------------|
| CRITICAL | X | ↑/↓/→ |
| HIGH | X | ↑/↓/→ |
| MEDIUM | X | ↑/↓/→ |
| LOW | X | ↑/↓/→ |

### By Category
| Category | Count | Top Location |
|----------|-------|--------------|
| Security | X | [file/dir] |
| Architecture | X | [file/dir] |
| Pattern | X | [file/dir] |
| Quality | X | [file/dir] |
| Testing | X | [file/dir] |
| Performance | X | [file/dir] |

---

## Hotspots

Files/areas with concentrated issues:

### 1. [file or directory path]
- **Issue count:** X violations
- **Categories:** [list]
- **Diagnosis:** [Training / Rule / Architecture / Process] problem
- **Evidence:** [Why this diagnosis]
- **Recommended action:** [Specific action]

### 2. [file or directory path]
[Same structure]

### 3. [file or directory path]
[Same structure]

---

## Recurring Solutions

Patterns emerging from .ai/solutions/:

| Tag/Pattern | Occurrences | Consider Adding to PATTERNS.md? |
|-------------|-------------|--------------------------------|
| [tag] | X times | Yes / No - [reason] |

---

## Required Decisions

**These are not optional.** Each requires a decision this week:

### Decision 1: What Gets Fixed This Week?

**Candidates (CRITICAL + oldest HIGH):**
1. [TD-XXX] [Location]: [Issue] - Added [date]
2. [TD-XXX] [Location]: [Issue] - Added [date]
3. [TD-XXX] [Location]: [Issue] - Added [date]

**Recommendation:** Fix items 1-2, defer item 3 because [reason]

**Your decision:** [ ] Accept recommendation / [ ] Different selection: ___

---

### Decision 2: What Rules Get Revised?

**Rules with high violation/exception rates:**

| Rule | Violations | Exceptions | Recommendation |
|------|------------|------------|----------------|
| [Rule from PATTERNS.md] | X | Y | Tighten / Loosen / Deprecate / Split |

**Specific revision proposal:**
```
Current: [Current rule text]
Proposed: [Revised rule text]
Rationale: [Why this change]
```

**Your decision:** [ ] Accept revision / [ ] Keep current / [ ] Different revision: ___

---

### Decision 3: What Tech Debt Gets Accepted?

**Items older than 30 days with no action:**
1. [TD-XXX] [Location]: [Issue] - Added [date]
   - **Accept as permanent?** Consequences: [what happens if we never fix this]
2. [TD-XXX] [Location]: [Issue] - Added [date]
   - **Accept as permanent?** Consequences: [what happens if we never fix this]

**Your decision:** [ ] Accept items as permanent debt / [ ] Escalate to fix / [ ] Remove from tracking

---

## Pattern Evolution

### Patterns to Add
Based on recurring solutions and violations:

1. **[Pattern name]**
   - Source: [Which solutions/violations suggested this]
   - Proposed addition to PATTERNS.md:
   ```markdown
   ## [Pattern Name]
   [Pattern description]
   ```

### Patterns to Revise
Based on violation patterns:

1. **[Existing pattern]**
   - Problem: [Why current version isn't working]
   - Revision: [Proposed change]

### Patterns to Deprecate
Based on low value or conflict:

1. **[Pattern name]**
   - Reason: [Why deprecate]
   - Replacement: [What replaces it, if anything]

---

## Action Items

| Priority | Action | Owner | Due |
|----------|--------|-------|-----|
| 1 | [From Decision 1] | [Assign] | This week |
| 2 | [From Decision 2] | [Assign] | This week |
| 3 | [From Decision 3] | [Assign] | This week |
| 4 | [Pattern update] | [Assign] | This week |

---

## Metrics for Next Report

Track these for trend analysis:
- Total TECH_DEBT entries: [X]
- Oldest unresolved item: [TD-XXX, Y days old]
- Hotspot file churn: [X changes in period]
- New patterns added: [X]
- Patterns revised: [X]
```

---

## After Report Generation

### If user accepts decisions:

1. **Fix items:** Create tasks or fix inline based on complexity
2. **Revise rules:** Update PATTERNS.md with approved changes
3. **Accept debt:** Mark items in TECH_DEBT.md as `status: accepted` with rationale
4. **Add patterns:** Add approved patterns to PATTERNS.md

### Offer next steps:

```
Drift report complete. Based on your decisions:

1. [ ] Create fix tasks for selected tech debt items
2. [ ] Update PATTERNS.md with rule revisions
3. [ ] Mark accepted debt items in TECH_DEBT.md
4. [ ] Add new patterns to PATTERNS.md

Which would you like me to do?
```

---

## Integration with Pipeline

**Weekly rhythm:**
```
Monday:    /drift-report → decisions made
Tuesday:   Fix tasks created from decisions
Week:      Normal development with updated patterns
Friday:    /code-review on week's work
Weekend:   Findings feed into next Monday's drift report
```

**The feedback loop:**
1. Code review catches violations → TECH_DEBT.md
2. Drift report aggregates patterns → Required decisions
3. Decisions update PATTERNS.md → Better enforcement
4. Better enforcement reduces violations → Healthier codebase

---

## Edge Cases

**No TECH_DEBT.md exists:**
- Create one with template from code review agent output format
- Report based on git history and solutions only

**No recent code reviews:**
- Focus on git history analysis and existing tech debt
- Recommend running `/code-review` before next drift report

**First time running:**
- No trend data available, skip trend columns
- Focus on current state assessment
- Establish baseline for future reports

**Very clean codebase (no issues found):**
- Celebrate briefly
- Look for patterns that could be extracted to PATTERNS.md
- Check if rules are too loose (nothing being caught = maybe nothing being checked)

---

## Anti-Patterns

**DON'T:**
- Generate report without forcing decisions (that's just a dashboard)
- Skip the "Required Decisions" section
- Accept all debt without consequences analysis
- Revise rules without evidence of problems
- Run without reading TECH_DEBT.md and PATTERNS.md first

**DO:**
- Force uncomfortable decisions (that's the point)
- Connect violations to root causes
- Propose specific rule text changes
- Track trends over time
- Close the loop by updating memory system

---

## Example Invocation

**User:** `/drift-report`

**Process:**
1. Read .ai/TECH_DEBT.md, .ai/PATTERNS.md, .ai/solutions/
2. Run git log analysis
3. Check for code review outputs
4. Generate structured report
5. Present required decisions
6. Wait for user decisions
7. Execute approved actions

---

**Remember:** A drift report that doesn't force decisions is just noise. The value is in the decisions, not the data.
