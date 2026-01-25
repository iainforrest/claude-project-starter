# Quick Reference

*Agent entry point and router to authoritative memory files*

---

## Authority Map

**Single source of truth for each content type. Content lives in ONE file only.**

| File | Purpose | Source of Truth For |
|------|---------|---------------------|
| `QUICK.md` | Router + Authority Map | Agent entry point |
| `ARCHITECTURE.json` | System topology | System design, data flows |
| `FILES.json` | File map (globs, NO line numbers) | File locations |
| `PATTERNS.md` | Implementation patterns | Coding conventions |
| `BUSINESS.json` | Business rules + data models | Domain logic, schemas |
| `OPS.md` | Debug, deploy, runbooks | Operations |
| `decisions/` | ADR files | Architecture decisions |
| `solutions/` | Solution capture YAML | Resolved investigation patterns |
| `DEPRECATIONS.md` | Deprecated modules | Deprecation tracking |
| `CONSTRAINTS.md` | Platform limits, non-goals | What we CAN'T do |
| `TECH_DEBT.md` | Unfixed code review findings | Known issues backlog |
| `CHANGELOG.md` | Release notes (auto-updated) | Version history |

---

## Quick Start

**Commands**: See `.claude/commands/` for available slash commands (`/prd`, `/execute`, `/update`, etc.)

**Operations**: See OPS.md for build/test/debug commands and runbooks

**File Structure**: See FILES.json for complete file index and locations

**How to Use**: Start with the authority map above to route content to the correct file
