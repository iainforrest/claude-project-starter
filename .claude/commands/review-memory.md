---
description: Review and optimize the memory system structure
---

# Memory Review Command

Analyze the AI memory system and suggest optimizations for efficient context loading.

## Purpose

This command reviews your `.ai/` memory files and provides:
- Size analysis with threshold warnings
- Pattern file splitting recommendations
- Mono-repo upgrade suggestions
- Token budget estimates
- Actionable optimization steps

## When to Run

- **After major sprints** - When memory has grown significantly
- **Before large features** - Ensure memory is optimized for efficient loading
- **Periodically** - Every 2-4 weeks as maintenance
- **When context loading feels slow** - Memory may need restructuring

---

## Analysis Process

### Step 1: Memory Structure Detection

Check which structure is in use:

```
Single-App:     .ai/ with core files only
Domain-Split:   .ai/ with patterns/ subfolder
Mono-Repo:      .ai/ with MONOREPO.json and app folders
```

### Step 2: Size Analysis

Get line counts for all memory files:

```bash
find .ai -type f \( -name "*.md" -o -name "*.json" \) -exec wc -l {} \;
```

**Thresholds:**

| File | Healthy | Warning | Action Needed |
|------|---------|---------|---------------|
| QUICK.md | <400 | 400-600 | >600 |
| ARCHITECTURE.json | <500 | 500-800 | >800 |
| BUSINESS.json | <800 | 800-1200 | >1200 |
| FILES.json | <600 | 600-900 | >900 |
| PATTERNS.md (index) | <250 | 250-400 | >400 |
| patterns/[DOMAIN].md | <500 | 500-700 | >700 |
| TODO.md | <200 | 200-350 | >350 |
| **Total (single-app)** | <3000 | 3000-4500 | >4500 |

### Step 3: Pattern Analysis

If PATTERNS.md exceeds 400 lines OR isn't using index format:

1. **Check for monolithic patterns file**
   - Is PATTERNS.md >400 lines with full code templates?
   - Recommendation: Split into `patterns/[DOMAIN].md` files

2. **Identify domain categories** in current patterns:
   - Count patterns by category (API, Web, Database, Testing, etc.)
   - Suggest domain files based on concentrations

3. **Check pattern index format**
   - Is PATTERNS.md a lightweight index pointing to domain files?
   - Or is it still a monolithic file with all patterns?

### Step 4: Mono-Repo Assessment

If total memory >4500 lines OR multiple distinct feature areas:

1. **Check for app boundaries**
   - Are there distinct applications in the codebase?
   - Could features be grouped into separate apps?

2. **Recommend MONOREPO.json**
   - Provide template from MONOREPO_GUIDE.md
   - Suggest app folder structure

### Step 5: Token Budget Estimate

Calculate approximate token usage:

```
Tokens ≈ Lines × 10 (rough estimate)

Example:
- QUICK.md: 150 lines → ~1,500 tokens
- ARCHITECTURE.json: 300 lines → ~3,000 tokens
- Total: ~X,XXX tokens
```

Compare to typical task load recommendations.

---

## Output Format

Generate a report like this:

```markdown
# Memory System Review

## Structure
Type: [Single-App | Domain-Split | Mono-Repo]
Total Lines: [X,XXX]
Estimated Tokens: [XX,XXX]

## File Analysis

| File | Lines | Status | Action |
|------|-------|--------|--------|
| QUICK.md | XXX | ✅ Healthy | None |
| PATTERNS.md | XXX | ⚠️ Warning | Split by domain |
| ARCHITECTURE.json | XXX | ❌ Bloated | Reduce examples |
| ... | ... | ... | ... |

## Recommendations

### Priority 1: [Title]
[Description of issue]
[Specific action to take]

### Priority 2: [Title]
[Description of issue]
[Specific action to take]

## Suggested Actions

1. [ ] [Specific action 1]
2. [ ] [Specific action 2]
3. [ ] [Specific action 3]

## Token Budget After Optimization

Current: ~XX,XXX tokens
After optimization: ~XX,XXX tokens
Savings: ~XX% reduction
```

---

## Common Recommendations

### Pattern File Splitting

**Symptom:** PATTERNS.md >400 lines with full code templates

**Solution:**
1. Create `patterns/` folder if not exists
2. Identify pattern domains (e.g., API, Web, Database)
3. Move patterns to domain files
4. Convert PATTERNS.md to index format:

```markdown
| Need | Pattern | Domain File |
|------|---------|-------------|
| API endpoint | Controller Pattern | patterns/API.md |
| Database query | Repository Pattern | patterns/DATABASE.md |
```

### Architecture Pruning

**Symptom:** ARCHITECTURE.json >800 lines

**Solution:**
- Remove verbose examples (keep references instead)
- Move implementation details to PATTERNS.md
- Focus on patterns, flows, and integration points only
- Use file:line references instead of code snippets

### Business Logic Splitting

**Symptom:** BUSINESS.json >1200 lines

**Solution:**
- Consider mono-repo structure if multiple feature domains
- Archive completed feature specs to a separate file
- Keep only active features and rules in BUSINESS.json

### Mono-Repo Upgrade

**Symptom:** Total memory >4500 lines with distinct apps

**Solution:**
1. Create MONOREPO.json (see MONOREPO_GUIDE.md)
2. Create app-specific folders under .ai/
3. Move app-specific content to respective folders
4. Update root QUICK.md to navigation hub

---

## Interactive Mode

After analysis, offer:

```
Memory review complete. Would you like me to:

1. Show detailed recommendations
2. Execute recommended optimizations
3. Generate optimization tasks for /execute
4. Skip for now
```

If user chooses #2, perform optimizations:
- Create missing folders
- Split patterns by domain
- Update index files
- Provide before/after comparison

---

## Anti-Patterns to Flag

- **Separate sprint files** (SPRINT_1.md, SPRINT_2.md, etc.)
- **Duplicate content** across files
- **Stale file references** (files that no longer exist)
- **Monolithic patterns** (all patterns in one large file)
- **Missing index format** (PATTERNS.md should be lightweight)
- **Orphaned pattern files** (patterns/ files not in index)

---

## Post-Review

After implementing recommendations:

1. Run `/review-memory` again to verify improvements
2. Update TODO.md with memory maintenance task
3. Consider scheduling periodic reviews (every 2-4 weeks)

---

*Keep your memory lean. Efficient memory = efficient AI assistance.*
