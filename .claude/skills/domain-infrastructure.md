---
name: domain-infrastructure
domain: Infrastructure & DevOps
description: Docker, Kubernetes, CI/CD pipelines, infrastructure as code, cloud configs, secret management, and health checks. Triggered on container configs, workflow files, IaC templates, and k8s manifests.
---

## File Detection Patterns

Triggered on: `Dockerfile*`, `docker-compose*`, `*.yaml` (k8s), `.github/workflows/*`, `terraform/*`, `*.tf`

---

## Patterns to Apply

### Container Best Practices

- **Multi-stage builds**: Use separate build and runtime stages to minimize image size
- **Layer caching**: Order instructions from least to most frequently changed for cache efficiency
- **.dockerignore**: Exclude unnecessary files (node_modules, .git, tests, etc.)
- **Non-root user**: Run containers as unprivileged user for security
- **Health checks**: Include HEALTHCHECK instruction with appropriate timeout and interval
- **Minimal base images**: Use alpine, distroless, or scratch where possible

### CI/CD Pipeline Patterns

- **Branch protection**: Require reviews and CI checks before merge
- **Workflow matrix**: Use matrix strategy for testing multiple versions/platforms
- **Status checks**: Fail fast with early validation (lint → unit → integration)
- **Artifact management**: Cache dependencies, publish only final builds
- **Secrets rotation**: Use GitHub Secrets, never commit credentials
- **Deployment gates**: Approval steps before production deployments

### Infrastructure as Code (IaC) Principles

- **Declarative configuration**: Define desired state, not imperative steps
- **Version control all infra**: Every config change tracked and reviewable
- **Modular composition**: Use variables, modules, and composition over duplication
- **Environment parity**: Dev/staging/prod configs follow same patterns
- **Immutable infrastructure**: Redeploy instead of patch (cattle not pets)

### Environment Management

- **Environment-specific configs**: Separate files for dev/staging/prod (.env.local, .env.prod)
- **Override hierarchy**: CLI args > env files > defaults
- **Configuration validation**: Schema validation at startup, fail fast on misconfiguration
- **Feature flags**: Enable capability toggling without redeployment

### Secret Injection Patterns

- **Never in version control**: .gitignore secrets, use references only
- **Runtime injection**: Secrets via environment variables or mounted files
- **Principle of least privilege**: Each service gets only required secrets
- **Rotation support**: Support updating secrets without downtime
- **Audit logging**: Track secret access in production

### Health Check Implementations

- **Liveness probes**: Restart unhealthy containers (detects deadlocks/crashes)
- **Readiness probes**: Remove from load balancer until ready (prevents cascading failures)
- **Startup probes**: Support slow-starting apps without false restarts
- **Semantic checks**: Health checks verify actual functionality, not just process alive
- **Graceful degradation**: Return 503 when degraded but process running

---

## Pitfalls to Avoid

### Container Pitfalls

- Running as root (security risk, privilege escalation)
- Single-stage builds with full toolchain in production image (bloat + attack surface)
- Hardcoded configuration in image (forces rebuild for config changes)
- No image tagging/versioning (can't identify which code is running)
- Unvetted base images (security vulnerabilities, bloat)
- CMD as PID 1 without signal handling (zombie processes, hung shutdowns)

### CI/CD Pitfalls

- Secrets in workflow logs (visible in run history)
- Long build times blocking PRs (discourage frequent commits)
- No rollback mechanism (one bad deploy breaks everything)
- Skipping tests on "hotfix" branches (causes cascading failures)
- Deployments only from protected branches (prevents testing)
- No status checks on infrastructure changes (silently breaks deployments)

### IaC Pitfalls

- Manual changes outside version control (drift, reproducibility lost)
- Hardcoded values instead of variables (can't change without reapply)
- Missing documentation on non-obvious resources (causes confusion)
- No import/state tracking for existing resources (duplicate creation)
- State files in version control (secrets exposed, merge conflicts)
- No dry-run before apply (destructive surprises)

### Environment Pitfalls

- Hardcoded localhost/development URLs in production configs
- Different config parsing between environments (breaks in prod)
- Required values with no defaults (startup fails silently)
- Mixing config files and runtime flags (inconsistent sources)
- No validation of config schema (discovers errors at runtime)

### Secret Pitfalls

- Secrets in logs (grep finds them, breach spreads)
- Long-lived credentials without rotation (breach scope grows)
- Shared credentials across services (breach affects all)
- Secrets in environment variables without masking (visible in process listings)
- No audit trail for secret access (can't trace who accessed what)

---

## Quality Checks

### Container Image Checks

- [ ] **Size audit**: Run `docker images` - size reasonable for use case?
- [ ] **Layer history**: `docker history <image>` - unnecessary layers?
- [ ] **User check**: Verify non-root user with `docker inspect`
- [ ] **Health defined**: HEALTHCHECK present with reasonable thresholds?
- [ ] **Security scan**: Run `trivy image` or `grype` for vulnerabilities
- [ ] **Build reproducibility**: Same source → same image hash consistently?

### CI/CD Checks

- [ ] **No secrets in logs**: Grep workflow files for `password`, `key`, `token` patterns
- [ ] **Status requirement**: Failing build status blocks merges?
- [ ] **Artifact cleanup**: Old builds deleted automatically?
- [ ] **Deployment approval**: Production requires human sign-off?
- [ ] **Rollback documented**: Can you revert in <5 minutes if needed?
- [ ] **Test coverage**: Coverage reports generated and tracked?

### IaC Checks

- [ ] **Plan review**: Always `terraform plan` before `apply` - output reviewed?
- [ ] **State locked**: Remote state has locking enabled?
- [ ] **Variables documented**: All variables have descriptions and type hints?
- [ ] **Modules versioned**: Referencing specific versions, not branches?
- [ ] **Drift detection**: Plan output checked against actual state?
- [ ] **Destroy safeguard**: Prevent_destroy or similar protection on critical resources?

### Configuration Checks

- [ ] **Schema validation**: Config schema enforced at parse time?
- [ ] **Required fields**: Critical config fields have validation, not optional?
- [ ] **Environment separation**: Dev/staging/prod configs independently versioned?
- [ ] **Secrets externalized**: No hardcoded credentials anywhere?
- [ ] **Defaults reasonable**: All defaults safe for any environment?

### Observability Checks

- [ ] **Structured logging**: JSON logs, not unstructured text?
- [ ] **Health endpoint**: Service exposes `/health` or similar?
- [ ] **Metrics exported**: Prometheus/custom metrics available?
- [ ] **Probe thresholds**: Health checks timeout and failure threshold appropriate?
- [ ] **Alert coverage**: Missing service or deployment failures trigger alerts?
