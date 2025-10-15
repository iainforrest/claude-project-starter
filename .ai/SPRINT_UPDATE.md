# Sprint Update Template

*Easy maintenance system for keeping AI memory current*

## 🚨 CRITICAL RULE: NO SEPARATE SPRINT FILES

**NEVER create separate sprint completion files** (e.g., `SPRINT_X_COMPLETION.md`). The .ai folder is designed to be a **condensed, efficient memory system** with only 8 core files.

**ALL sprint information must be integrated into existing files:**
- New features → `BUSINESS.json`
- New patterns → `PATTERNS.md`
- New files → `FILES.json`
- Architecture changes → `ARCHITECTURE.json`
- New commands → `QUICK.md`

**Goal**: Keep .ai folder at ~3000 lines across 8 core files. Do not create documentation sprawl.

## End-of-Sprint Update Checklist

### 1. Architecture Updates
- [ ] **New Patterns**: Add any new architectural patterns to `PATTERNS.md`
- [ ] **Dependencies**: Update dependency graph in `ARCHITECTURE.json`
- [ ] **Constraints**: Document new technical constraints discovered
- [ ] **Data Flows**: Add new component interactions to data flows

### 2. File Index Maintenance
- [ ] **New Files**: Add significant new files to `FILES.json`
- [ ] **Moved Files**: Update paths for any relocated files
- [ ] **Deprecated Files**: Mark deprecated files with status
- [ ] **Line References**: Update critical line number references

### 3. Business Logic Updates
- [ ] **New Features**: Add feature status to `BUSINESS.json`
- [ ] **API Changes**: Update integration points for API modifications
- [ ] **Performance Targets**: Update targets based on measurements
- [ ] **User Flows**: Document new or modified user workflows

### 4. Quick Reference Updates
- [ ] **New Commands**: Add development commands to `QUICK.md`
- [ ] **Debug Patterns**: Add new debugging approaches discovered
- [ ] **Performance Tips**: Document new optimization techniques
- [ ] **Error Solutions**: Add solutions to common problems encountered

## Update Process

### Step 1: Automated File Scan
```bash
# Run this command to find new/modified files
find [source_directory] -name "*.[ext]" -newer .ai/FILES.json | head -20
```

### Step 2: Review Sprint Artifacts
- [ ] Check completed PRDs for new architecture decisions
- [ ] Review task lists for implementation patterns used
- [ ] Analyze commit messages for significant changes
- [ ] Check test additions for new testing patterns

### Step 3: Update Memory Files

**ARCHITECTURE.json Updates:**
```json
// Add new patterns discovered
"newPattern": {
  "description": "What this pattern solves",
  "keyFiles": ["Implementation.ext:lineNumber"],
  "constraints": ["Limitation 1", "Limitation 2"],
  "benefits": ["Benefit 1", "Benefit 2"]
}

// Update data flows with new components
"newDataFlow": {
  "steps": ["Step 1", "Step 2", "Step 3"],
  "keyFiles": ["File1.ext:line", "File2.ext:line"]
}
```

**FILES.json Updates:**
```json
// Add new purpose categories
"newPurpose": {
  "primary": ["MainFile.ext:lineNumber"],
  "support": ["SupportFile1.ext", "SupportFile2.ext"],
  "tests": ["TestFile.test.ext:lineNumber"]
}

// Update dependencies
"NewFile.ext": {
  "uses": ["Dependency1", "Dependency2"],
  "implements": ["Feature1", "Feature2"],
  "tests": "TestFile.test.ext"
}
```

**PATTERNS.md Updates:**
```markdown
## New Pattern Name

### When to Use
- Specific use case 1
- Specific use case 2

### Template: Pattern Implementation
```[language]
// Template code with comments
class YourNewPattern {
    // Implementation following discovered pattern
}
```

### Implementation Checklist
- [ ] Requirement 1
- [ ] Requirement 2

**Pattern Reference**: ActualFile.ext:lineNumber
```

**BUSINESS.json Updates:**
```json
// Update feature status
"newFeature": {
  "status": "complete|in-progress|planned",
  "version": "v1.0",
  "description": "What this feature does",
  "keyFeatures": ["Feature 1", "Feature 2"]
}

// Update performance targets
"performanceTargets": {
  "newMetric": "Target value and measurement method"
}
```

**QUICK.md Updates:**
```markdown
### New Quick Lookup Category
```bash
# New file locations
NewImportantFile.ext:lineNumber    # Description of what this does
```

### New Development Command
```bash
# Command description
[BUILD_COMMAND] [options]
```

### New Debugging Pattern
```bash
# Debug new feature
[DEBUG_COMMAND] | grep "NewPattern"
```
```

## Memory System Usage Guide

### For PRD Creation
1. **Read `BUSINESS.json`** → Understand current features and targets
2. **Check `ARCHITECTURE.json`** → Identify integration points and constraints
3. **Review `PATTERNS.md`** → Find relevant implementation patterns
4. **Use `QUICK.md`** → Locate files for architecture analysis

### For Task List Generation
1. **Use `FILES.json`** → Find all files that need modification
2. **Check `PATTERNS.md`** → Apply appropriate implementation templates
3. **Reference `ARCHITECTURE.json`** → Understand component relationships
4. **Consult `QUICK.md`** → Verify build and test commands

### For Implementation
1. **Start with `PATTERNS.md`** → Copy relevant template
2. **Use `FILES.json`** → Find dependency files and references
3. **Follow `ARCHITECTURE.json`** → Maintain architectural consistency
4. **Reference `QUICK.md`** → Use correct development commands

### For Debugging
1. **Check `QUICK.md` Emergency Debugging** → Common issue solutions
2. **Use file line references** → Jump directly to relevant code
3. **Apply debugging patterns** → Structured troubleshooting approach

## Example: Using Memory for New Feature

**Scenario**: "Add [new feature request]"

**Memory Usage Flow**:
1. **`BUSINESS.json`** → Check current features and business logic
2. **`ARCHITECTURE.json`** → Find relevant architectural patterns and data flows
3. **`FILES.json`** → Locate related components and files
4. **`PATTERNS.md`** → Use appropriate pattern template
5. **`QUICK.md`** → Find testing and debugging commands

**Result**: Complete understanding of where to implement, how to follow patterns, and what files to modify - all in under 2 minutes.

## Automation Opportunities

### Auto-Update Triggers
```bash
# Git hook to remind about memory updates
echo "Don't forget to update .ai/ memory files!" > .git/hooks/post-commit
chmod +x .git/hooks/post-commit

# Build system integration
# Add to build configuration to check memory file freshness
task checkMemoryFreshness {
    doLast {
        // Warn if memory files older than recent commits
    }
}
```

### Memory Validation
```bash
# Check for broken file references
grep -r "\.[ext]:[0-9]" .ai/ | while read ref; do
  # Validate that line number references still exist
done
```

---

**Next Update Due**: End of next sprint (update meta.lastUpdated dates)
