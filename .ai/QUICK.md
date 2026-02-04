# Quick Reference

*Agent entry point and router to authoritative memory files*

---

## Authority Map

**Single source of truth for each content type. Content lives in ONE file only.**

| Authority | Purpose | Source of Truth For |
|-----------|---------|---------------------|
| Router | Authority map and navigation | Agent entry point |
| Architecture | System topology | System design, data flows |
| File Index | File map (globs, NO line numbers) | File locations |
| Patterns | Implementation patterns | Coding conventions |
| Business | Business rules + data models | Domain logic, schemas |
| Operations | Debug, deploy, runbooks | Operations |
| Decisions | ADR files | Architecture decisions |
| Solutions | Solution capture YAML | Resolved investigation patterns |
| Deprecations | Deprecated modules | Deprecation tracking |
| Constraints | Platform limits, non-goals | What we CAN'T do |
| Tech Debt | Unfixed code review findings | Known issues backlog |
| Changelog | Release notes (auto-updated) | Version history |

**File locations**: See File Index for actual file paths

---

## Quick Start

**Commands**: See commandWorkflow section in file index for available slash commands

**Operations**: See operations file for build/test/debug commands and runbooks

**File Structure**: See file index for complete file map and locations

**How to Use**: Start with the authority map above to route content to the correct file
