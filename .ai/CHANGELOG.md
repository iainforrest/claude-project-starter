# Changelog

All notable changes to this project are documented here. This file is automatically updated by the `/update` command during memory system updates.

Format based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/).

---

## [Unreleased]

### Added
- Changelog auto-generation during `/update` command
- Template separation system: `templates/.ai/` contains clean starter files
- `templates/tasks/` directory structure for task organization
- CHANGELOG.md to authority map and memory navigation

### Changed
- Model selection now uses gpt-5.2-codex with reasoning effort levels instead of model switching
  - Complexity 1-2: gpt-5.2-codex with medium reasoning effort
  - Complexity 3: Sonnet (unchanged)
  - Complexity 4-5: gpt-5.2-codex with xhigh reasoning effort
- `/pull-fc` command now syncs `templates/.ai/` and `templates/tasks/` from fat-controller
- Project version bumped to 3.1.0 to reflect template separation and model selection updates
- Update-memory-agent now includes CHANGELOG.md in authority-based routing

### Fixed

### Deprecated

### Removed

### Security

---

## Version History

_Previous releases will be documented below as versions are tagged._

---

<!--
CHANGELOG MAINTENANCE GUIDE (for update-memory-agent):

1. Add entries under [Unreleased] as changes are made
2. When releasing, move [Unreleased] content to a versioned section
3. Categories:
   - Added: New features
   - Changed: Changes to existing functionality
   - Fixed: Bug fixes
   - Deprecated: Features to be removed
   - Removed: Removed features
   - Security: Security fixes

4. Entry format: "- Brief description of change"
5. Group related changes together
6. Most recent changes at top of each category
-->
