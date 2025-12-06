---
description: Push improvements from this project back to claude-project-starter as a PR
---

# Push Improvements to Claude Project Starter

You are pushing improvements made in this project back to the claude-project-starter repository as a pull request.

**CRITICAL**: This is a public open-source repo. You MUST generalize all content and remove ANY project-specific information before pushing.

## Configuration

- **Target repo**: `iainforrest/claude-project-starter` (GitHub)
- **Method**: Pull request via GitHub CLI (`gh`)

## User Input Required

Ask the user: "What improvements do you want to push back to the starter? (e.g., 'the updated /prd command', 'the new review workflow', 'changes to execute.md')"

## Steps

### 1. Identify what to push

Based on user input, identify the specific files in `.claude/` or `.ai/` that contain the improvements.

Read each file and understand what has changed or been added.

### 2. Generalize the content

**This step is critical for security and privacy.**

For each file being pushed, remove or replace:

- **Project names** → use generic terms like "the project" or "your application"
- **Company/business names** → remove entirely or use "[Company]"
- **URLs and API endpoints** → remove or use `https://example.com`
- **User names, team names** → remove
- **Business-specific terminology** → generalize to common terms
- **Project-specific file paths** → use generic examples like `src/components/`
- **Proprietary business logic** → remove or abstract
- **Configuration values** → use placeholders

**Preserve**:
- Generic best practices and patterns
- Command structure and workflow logic
- Technical approaches that work across any project
- Helpful comments and documentation

### 3. Show generalized version for approval

Present the generalized version of each file to the user:
- Show the full content that will be pushed
- Highlight what was changed during generalization
- Ask: "Does this look properly generalized? Any sensitive info remaining?"

**Do not proceed until user explicitly confirms the content is safe to push publicly.**

### 4. Clone and create branch

```bash
TEMP_DIR=$(mktemp -d)
git clone https://github.com/iainforrest/claude-project-starter.git "$TEMP_DIR"
cd "$TEMP_DIR"

# Create a descriptive branch name based on the changes
BRANCH_NAME="update/descriptive-name-here"
git checkout -b "$BRANCH_NAME"
```

### 5. Apply changes

Copy the generalized files to the appropriate locations in the cloned repo.

### 6. Commit and push

```bash
cd "$TEMP_DIR"
git add .
git commit -m "feat: Description of the improvement

🤖 Generated with [Claude Code](https://claude.com/claude-code)

Co-Authored-By: Claude <noreply@anthropic.com>"

git push -u origin "$BRANCH_NAME"
```

### 7. Create PR

```bash
cd "$TEMP_DIR"
gh pr create \
  --repo iainforrest/claude-project-starter \
  --title "feat: Title describing the improvement" \
  --body "## Summary

Brief description of what this PR adds or improves.

## Changes

- List of files changed

## Generalization checklist

- [x] Project-specific names removed
- [x] URLs and endpoints removed or replaced with placeholders
- [x] No sensitive or proprietary information
- [x] Tested in source project

---
🤖 Generated with [Claude Code](https://claude.com/claude-code)"
```

### 8. Cleanup and report

```bash
rm -rf "$TEMP_DIR"
```

Provide the PR URL so the user can review it on GitHub.

---

**Execute this workflow now.** Start by asking what improvements the user wants to push.
