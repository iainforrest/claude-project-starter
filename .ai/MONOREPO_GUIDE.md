# Mono-Repo Memory Guide

*How to scale the memory system for multi-app projects*

## When to Upgrade

Upgrade to mono-repo memory structure when:

1. **Memory exceeds ~3,000 lines** - Single-app structure is getting bloated
2. **Multiple apps in workspace** - You have web, mobile, api packages
3. **Teams work independently** - Different teams need isolated context
4. **Context loading is slow** - Loading full memory takes too long

## Mono-Repo Structure

### Before (Single-App)

```
.ai/
├── README.md
├── QUICK.md
├── ARCHITECTURE.json
├── BUSINESS.json
├── FILES.json
├── PATTERNS.md
├── patterns/
├── TODO.md
└── SPRINT_UPDATE.md
```

### After (Mono-Repo)

```
.ai/
├── README.md           # Updated for mono-repo navigation
├── QUICK.md            # Mono-repo commands, app navigation
├── MONOREPO.json       # Workspace architecture (NEW)
│
├── app1/               # First app's complete memory
│   ├── QUICK.md
│   ├── ARCHITECTURE.json
│   ├── BUSINESS.json
│   ├── FILES.json
│   ├── PATTERNS.md
│   └── TODO.md
│
├── app2/               # Second app's complete memory
│   ├── QUICK.md
│   ├── ARCHITECTURE.json
│   ├── BUSINESS.json
│   ├── FILES.json
│   ├── PATTERNS.md
│   └── TODO.md
│
└── shared/             # Shared library memory (if applicable)
    ├── QUICK.md
    └── ...
```

---

## Migration Steps

### Step 1: Create MONOREPO.json

Create `.ai/MONOREPO.json` with workspace architecture:

```json
{
  "meta": {
    "projectName": "Your Project Name",
    "version": "1.0.0",
    "lastUpdated": "YYYY-MM-DD",
    "description": "Mono-repo description"
  },
  "workspaceStructure": {
    "type": "npm-workspaces | yarn-workspaces | turborepo | custom",
    "packageManager": "npm | yarn | pnpm",
    "packages": [
      "packages/app1",
      "packages/app2",
      "packages/shared"
    ],
    "root": "/path/to/project"
  },
  "apps": {
    "app1": {
      "name": "App 1 Name",
      "status": "production | development | planned",
      "version": "0.1.0",
      "path": "packages/app1",
      "memoryPath": ".ai/app1/",
      "description": "What this app does"
    },
    "app2": {
      "name": "App 2 Name",
      "status": "development",
      "version": "0.1.0",
      "path": "packages/app2",
      "memoryPath": ".ai/app2/",
      "description": "What this app does"
    }
  },
  "sharedResources": {
    "database": {
      "type": "PostgreSQL | Firebase | etc.",
      "sharedCollections": ["users", "config"],
      "appSpecificCollections": {
        "app1": ["app1_data"],
        "app2": ["app2_data"]
      }
    },
    "authentication": {
      "method": "JWT | OAuth | etc.",
      "sharedAcross": ["app1", "app2"]
    }
  },
  "crossAppIntegration": {
    "description": "How apps communicate",
    "pattern": "API calls | Shared database | Event bus",
    "keyFiles": ["packages/shared/api.ts"]
  }
}
```

### Step 2: Create App Folders

For each app, create a memory folder:

```bash
mkdir -p .ai/app1
mkdir -p .ai/app2
```

### Step 3: Split Existing Memory

Move app-specific content from root files to app folders:

1. **ARCHITECTURE.json** → Split by app
2. **BUSINESS.json** → Split by app
3. **FILES.json** → Split by app
4. **PATTERNS.md** → Keep shared patterns at root, app-specific in app folders
5. **TODO.md** → Split by app

### Step 4: Update Root QUICK.md

Convert root QUICK.md to navigation hub:

```markdown
# Quick Reference - Mono-Repo

## Apps

| App | Status | Memory | Path |
|-----|--------|--------|------|
| App 1 | Production | .ai/app1/ | packages/app1/ |
| App 2 | Development | .ai/app2/ | packages/app2/ |

## Mono-Repo Commands

\`\`\`bash
npm run dev:app1     # Start app1 dev server
npm run dev:app2     # Start app2 dev server
npm run build        # Build all packages
npm run test         # Test all packages
\`\`\`

## Working on App 1?
→ Load: MONOREPO.json + .ai/app1/*

## Working on App 2?
→ Load: MONOREPO.json + .ai/app2/*

## Cross-App Integration?
→ Load: MONOREPO.json + relevant app ARCHITECTURE files
```

---

## Context Loading Strategy

### For App-Specific Work

```
Load: MONOREPO.json (workspace context)
     + .ai/[app]/QUICK.md
     + .ai/[app]/ARCHITECTURE.json
     + .ai/[app]/FILES.json (if needed)

Total: ~1,000-2,000 lines
```

### For Cross-App Work

```
Load: MONOREPO.json
     + .ai/app1/ARCHITECTURE.json
     + .ai/app2/ARCHITECTURE.json

Total: ~1,500-2,500 lines
```

### For Workspace-Level Work

```
Load: MONOREPO.json
     + Root QUICK.md

Total: ~800-1,200 lines
```

---

## Token Budget (Mono-Repo)

```
Component                 Lines       Tokens
───────────────────────────────────────────
Root QUICK.md             ~300        ~3,000
MONOREPO.json             ~300        ~3,000
───────────────────────────────────────────
Per-App Memory:
  QUICK.md                ~200        ~2,000
  ARCHITECTURE.json       ~200        ~2,000
  BUSINESS.json           ~300        ~3,000
  FILES.json              ~200        ~2,000
  PATTERNS.md             ~200        ~1,000
  TODO.md                 ~100        ~1,000
  ─────────────────────────────────────────
  App Subtotal            ~1,200      ~11,000
───────────────────────────────────────────
Typical Work Session:
  Root + 1 App            ~1,800      ~17,000
───────────────────────────────────────────
```

---

## Best Practices

### 1. Keep Root Level Lean
- Only navigation and shared config
- No app-specific details at root
- MONOREPO.json is the source of truth for workspace structure

### 2. Each App is Self-Contained
- App memory should work independently
- ~1,200 lines per app maximum
- No cross-references between app folders

### 3. Shared Resources in MONOREPO.json
- Database schemas shared across apps
- Authentication config
- Cross-app integration points

### 4. Update Strategy
- Update app memory when working on that app
- Update MONOREPO.json when workspace structure changes
- Run `/update` targeting specific app folder

---

## Command Integration

Commands auto-detect mono-repo structure:

1. **If `.ai/MONOREPO.json` exists** → Prompt for app selection
2. **If working in app directory** → Auto-select that app's memory
3. **Load root + app-specific memory** for context

Example flow:
```
/prd "Add user profile feature"

> Detected mono-repo structure.
> Which app is this feature for?
> 1. app1 (Web Frontend)
> 2. app2 (API Backend)
> 3. Both (cross-app feature)

[User selects 1]

> Loading: MONOREPO.json + .ai/app1/*
> Ready to gather requirements...
```

---

## Example: E-commerce Mono-Repo

```
.ai/
├── QUICK.md              # Workspace commands
├── MONOREPO.json         # Workspace architecture
│
├── web/                  # React frontend
│   ├── QUICK.md          # Web-specific commands
│   ├── ARCHITECTURE.json # Component patterns, state management
│   ├── BUSINESS.json     # User flows, UI requirements
│   ├── FILES.json        # Frontend file index
│   └── PATTERNS.md       # React patterns
│
├── api/                  # Node.js backend
│   ├── QUICK.md          # API-specific commands
│   ├── ARCHITECTURE.json # Service patterns, middleware
│   ├── BUSINESS.json     # API requirements, endpoints
│   ├── FILES.json        # Backend file index
│   └── PATTERNS.md       # Express/NestJS patterns
│
└── mobile/               # React Native app
    ├── QUICK.md
    └── ...
```

---

*Scale your memory as your project grows. Keep each app under ~1,200 lines.*
