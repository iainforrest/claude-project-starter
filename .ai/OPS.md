# Operations Guide

*Runbooks, debug commands, deploy procedures, and operational playbooks*

**Authority**: This is the single source of truth for operational procedures. If it's about running, debugging, deploying, or responding to incidents, it lives here.

---

## Quick Operations Index

| Operation | Section | When to Use |
|-----------|---------|-------------|
| Build/test commands | Build Commands | Starting development |
| Debug issues | Debug Commands | Investigating problems |
| Deploy changes | Deploy Procedures | Releasing to production |
| Monitor health | Monitoring | Checking system status |
| Handle incidents | Incident Response | Production issues |

---

## Build Commands

```bash
# Build
[BUILD_COMMAND]              # e.g., "npm run build", "./gradlew build", "cargo build"

# Test
[TEST_COMMAND]               # e.g., "npm test", "./gradlew test", "cargo test"

# Development/Watch mode
[DEV_COMMAND]                # e.g., "npm run dev", "./gradlew run", "cargo run"

# Lint/Format
[LINT_COMMAND]               # e.g., "npm run lint", "./gradlew lint"

# Install dependencies
[INSTALL_DEPS]               # e.g., "npm install", "./gradlew dependencies"

# Clean build
[CLEAN_BUILD]                # e.g., "npm run clean && npm run build"
```

---

## Debug Commands

```bash
# Debug mode
[DEBUG_COMMAND]              # e.g., "npm run debug", "cargo build --debug"

# Logs
[LOG_COMMAND]                # e.g., "tail -f logs/app.log"

# Test specific file
[TEST_FILE_COMMAND]          # e.g., "npm test -- path/to/test"
```

### Common Debug Scenarios

#### Issue: [Common Problem]
**Symptoms**: [Description]
**Debug Steps**:
1. [First check]
2. [Second check]
3. [Resolution]

**Commands**:
```bash
[Specific diagnostic commands]
```

---

## Deploy Procedures

### Production Deploy

**Prerequisites**:
- [ ] Tests passing
- [ ] Code reviewed
- [ ] Staging validated

**Steps**:
```bash
# 1. Final checks
[PRE_DEPLOY_CHECKS]

# 2. Deploy
[DEPLOY_COMMAND]

# 3. Verify deployment
[POST_DEPLOY_VERIFY]
```

### Rollback Procedure

**When to rollback**: [Criteria for rollback decision]

**Steps**:
```bash
# 1. Identify last good version
[VERSION_CHECK]

# 2. Rollback
[ROLLBACK_COMMAND]

# 3. Verify rollback
[VERIFY_ROLLBACK]
```

---

## Monitoring

### Health Checks

```bash
# System health
[HEALTH_CHECK_COMMAND]

# Performance metrics
[METRICS_COMMAND]

# Error rates
[ERROR_CHECK_COMMAND]
```

### Key Metrics

| Metric | Command | Alert Threshold |
|--------|---------|-----------------|
| [Metric 1] | `[command]` | [threshold] |
| [Metric 2] | `[command]` | [threshold] |

---

## Incident Response

### Incident Severity Levels

| Level | Description | Response Time | Example |
|-------|-------------|---------------|---------|
| **P0** | Complete outage | Immediate | Service down |
| **P1** | Critical degradation | < 15 minutes | 50% error rate |
| **P2** | Partial degradation | < 1 hour | Feature broken |
| **P3** | Minor issue | < 1 day | Cosmetic bug |

### Incident Response Playbook

#### 1. Detect and Triage
- [ ] Identify severity level
- [ ] Check monitoring dashboards
- [ ] Review recent deployments

#### 2. Investigate
```bash
# Check logs
[LOG_INVESTIGATION_COMMAND]

# Check system resources
[RESOURCE_CHECK]

# Check dependencies
[DEPENDENCY_CHECK]
```

#### 3. Mitigate
- [ ] If deployment related: consider rollback
- [ ] If infrastructure: check service status
- [ ] If data: verify database integrity

#### 4. Resolve
- [ ] Apply fix
- [ ] Verify resolution
- [ ] Monitor for recurrence

#### 5. Document
- [ ] Create incident report
- [ ] Add solution to `.ai/solutions/`
- [ ] Update this playbook if new pattern discovered

---

## Performance Monitoring

```bash
# Profile
[PROFILE_COMMAND]            # e.g., "npm run profile"

# Analyze bundle/build
[ANALYZE_COMMAND]            # e.g., "npm run analyze"
```

---

## Runbook Template

When you discover a new operational procedure, add it here using this format:

### [Procedure Name]

**Purpose**: [What this procedure accomplishes]

**When to Use**: [Triggering conditions]

**Prerequisites**:
- [ ] [Requirement 1]
- [ ] [Requirement 2]

**Steps**:
```bash
# 1. [Step description]
[command]

# 2. [Step description]
[command]
```

**Validation**: [How to verify success]

**Rollback**: [How to undo if needed]

---

## Notes

- Update this file when you discover new operational patterns
- Add runbooks for any procedure you've done twice
- Keep commands platform-agnostic where possible (document platform differences)
- Link to `.ai/solutions/` when referencing past incidents
