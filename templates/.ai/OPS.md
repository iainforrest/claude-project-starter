# Operations & Runbooks

*Authority: This is source of truth for build, test, deploy, and debug procedures*

## Build & Run

### Development
```bash
[YOUR_DEV_COMMAND]
```

### Production Build
```bash
[YOUR_BUILD_COMMAND]
```

### Run Tests
```bash
[YOUR_TEST_COMMAND]
```

---

## Environment Setup

### Prerequisites
- [Dependency 1] version X.X
- [Dependency 2] version X.X

### First-Time Setup
```bash
# Clone and install
git clone [YOUR_REPO]
cd [YOUR_PROJECT]
[YOUR_INSTALL_COMMAND]

# Configure environment
cp .env.example .env
# Edit .env with your values
```

### Environment Variables

| Variable | Purpose | Example |
|----------|---------|---------|
| `[VAR_NAME]` | [Description] | `value` |

---

## Debug Commands

### [Category 1]
```bash
# [Description of what this does]
[COMMAND]
```

### [Category 2]
```bash
# [Description]
[COMMAND]
```

---

## Common Issues & Fixes

### [Issue Name]
**Symptoms**: [What you see]
**Cause**: [Why it happens]
**Fix**:
```bash
[COMMAND_TO_FIX]
```

---

## Deployment

### Staging
```bash
[STAGING_DEPLOY_COMMAND]
```

### Production
```bash
[PRODUCTION_DEPLOY_COMMAND]
```

### Rollback
```bash
[ROLLBACK_COMMAND]
```

---

## Monitoring

### Health Checks
- [Endpoint or command to check health]

### Logs
```bash
# View logs
[LOG_COMMAND]
```

### Metrics
- [Where to find metrics/dashboards]

---

## Database

### Migrations
```bash
# Run migrations
[MIGRATION_COMMAND]

# Rollback
[ROLLBACK_MIGRATION_COMMAND]
```

### Backup/Restore
```bash
# Backup
[BACKUP_COMMAND]

# Restore
[RESTORE_COMMAND]
```

---

*Update this file when build/deploy procedures change.*
