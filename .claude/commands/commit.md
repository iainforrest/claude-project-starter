---
description: Intelligently group and commit changes by related work, then push to GitHub
---

# Intelligent Git Commit Command

**Note:** This command can be invoked by agents (e.g., `update-memory-agent`) to commit their changes. When invoked by an agent, commit messages are generated from the agent's context and work.

## Context Detection

**When invoked by an agent (autonomous mode):**
- Skip approval step (agent is autonomous)
- Create commits immediately based on agent's work context
- Push automatically to GitHub
- Report completion back to agent

**When invoked by user (interactive mode):**
- Show proposed commit groupings
- Wait for user approval
- Create commits after approval
- Push to GitHub

## Objective
Analyze all uncommitted changes and create logical, grouped commits based on the work performed. If multiple unrelated features or fixes were worked on, create separate commits for better traceability.

## Process

1. **Check Current Status**
   - Run `git status` to see all changed files
   - Run `git diff --stat` to see the scope of changes
   - If there are no changes, notify the user and stop

2. **Analyze and Group Changes**
   - Examine all modified files and their changes
   - Consider the conversation history and work context
   - Group files by logical work units based on:
     - Related functionality (e.g., all files for a specific feature)
     - Related modules (e.g., frontend vs backend, UI vs business logic)
     - Documentation updates that go with code changes
     - Configuration files that support specific features

3. **Create Grouped Commits**
   For each logical group of work:
   - Stage only the files in that group
   - Generate a concise, descriptive commit message that:
     - Starts with a conventional commit prefix (feat:, fix:, docs:, refactor:, etc.)
     - Describes WHAT was done and WHY (not HOW)
     - Is 50-72 characters for the summary line
     - Includes the Claude Code footer
   - Create the commit
   - Show what was committed

4. **Push to GitHub**
   - After all commits are created, push to the current branch
   - Confirm successful push

## Example Grouping Logic

If working directory has:
- 8 files related to new feature (business logic + UI + tests)
- 4 files related to memory system documentation updates
- 2 files with unrelated bug fixes

Then create 3 commits:
1. "feat: Add [feature name] with [key capabilities]"
2. "docs: Update AI memory system with [feature] documentation"
3. "fix: [Description of bugs fixed]"

## Important Notes
- DO NOT create a single monolithic commit if changes span multiple features
- DO group related files together even if they're in different directories
- DO include documentation updates with the feature they document
- DO use conventional commit prefixes (feat, fix, docs, refactor, test, chore)
- DO add the Claude Code footer to all commits:
  ```
  🤖 Generated with [Claude Code](https://claude.com/claude-code)

  Co-Authored-By: Claude <noreply@anthropic.com>
  ```
- DO check if we're on the right branch before pushing
- DO NOT amend commits unless explicitly requested
- DO NOT force push
- DO NOT skip hooks (--no-verify, --no-gpg-sign, etc.) unless explicitly requested

## Execution Steps

Please execute the following:

1. Check git status and diff
2. Analyze the changes in context of recent work
3. Propose the commit groupings to me before executing
4. Wait for my approval (unless invoked by agent)
5. Create the commits with proper messages
6. Push to GitHub
7. Confirm success with commit SHAs

Begin analysis now.
