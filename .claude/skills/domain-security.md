---
name: Domain Security
domain: security
description: Security-sensitive code patterns for authentication, authorization, cryptography, and input handling
triggers:
  - "*/auth/*"
  - "*/security/*"
  - "*/crypto/*"
  - "*password*"
  - "*token*"
  - "*session*"
---

# Security Domain Skill

## Patterns to Apply

### Input Sanitization
- Validate all user input at the boundary (never trust client data)
- Use allowlists over denylists when possible
- Parameterize queries to prevent injection attacks
- Sanitize output based on context (HTML, URL, CSS, JavaScript)
- Validate type, length, format, and range for every input

### Authentication Best Practices
- Never store plaintext passwords—use bcrypt/argon2/scrypt
- Implement rate limiting on login endpoints (prevent brute force)
- Use secure password hashing with proper salt/iterations
- Enforce strong password policies for admin accounts
- Implement account lockout after failed attempts
- Log all authentication attempts (successes and failures)

### Authorization & Access Control
- Default to deny—require explicit permissions
- Implement least-privilege principle
- Verify permissions on every request, not just once
- Use role-based or attribute-based access control
- Audit all permission changes and privileged operations

### Token & Session Management
- Use cryptographically secure token generation
- Set appropriate expiration times (short for access, longer for refresh)
- Invalidate tokens on logout or privilege change
- Use HttpOnly + Secure flags for session cookies
- Store tokens in secure, non-accessible storage (not localStorage)
- Regenerate session IDs after privilege escalation

### Secret Management
- Never commit secrets to version control (.env files in .gitignore)
- Use environment variables or secure vaults for production secrets
- Rotate secrets regularly and have a process for compromised secrets
- Use different secrets per environment
- Log secret access attempts (not the secrets themselves)
- Minimize secret exposure in logs/errors

### Cryptography
- Use well-vetted, standard algorithms (AES-256, SHA-256, TLS 1.2+)
- Never implement custom crypto—use established libraries
- Use authenticated encryption (AES-GCM) when encrypting
- Validate all cryptographic signatures before use
- Ensure proper key derivation (use KDF for password-based keys)

### Secure Defaults
- Deny by default, require explicit opt-in for features
- Use HTTPS everywhere (no mixed content)
- Implement CSRF protection (token-based, SameSite cookies)
- Set security headers (CSP, X-Frame-Options, X-Content-Type-Options)
- Disable unnecessary features and endpoints

### Audit Logging
- Log authentication/authorization decisions with context
- Include user ID, timestamp, action, resource, and result
- Never log sensitive data (passwords, tokens, PII)
- Store logs securely with tamper detection
- Monitor logs for suspicious patterns (multiple failures, privilege escalation)

## Pitfalls to Avoid

- **Reusing passwords/secrets** across environments or accounts
- **Hardcoding credentials** in source code or config files
- **Assuming client-side validation** is sufficient
- **Storing sensitive data in plain text** (logs, databases, caches)
- **Using weak cryptographic algorithms** (MD5, SHA1, DES)
- **Implementing custom authentication** instead of using proven libraries
- **Forgetting to validate tokens** on every request
- **Exposing error details** that reveal system information (use generic errors)
- **Ignoring OWASP Top 10** (Injection, Broken Auth, Sensitive Data, XML/XXE, Broken Access Control, Security Misconfiguration, XSS, Insecure Deserialization, Using Components with Known Vulns, Insufficient Logging)
- **Not rotating or managing API keys** and tokens
- **Trusting user-supplied identifiers** without server-side validation
- **Mixing authentication/authorization logic** (separation of concerns)

## Quality Checks

Before merging security code:

1. **Input Validation**
   - Are all inputs validated at entry points?
   - Is validation done server-side, not just client-side?
   - Are parameterized queries used for database access?

2. **Authentication**
   - Are passwords hashed with modern algorithms (bcrypt/argon2)?
   - Is rate limiting implemented on auth endpoints?
   - Are failed attempts logged?

3. **Secrets & Credentials**
   - Are secrets excluded from git (.gitignore checked)?
   - Are production secrets in environment variables, not code?
   - Are different secrets used per environment?

4. **Cryptography**
   - Are standard, well-vetted algorithms used (no custom crypto)?
   - Is HTTPS/TLS used for all sensitive data in transit?
   - Are keys properly generated and stored?

5. **Audit Trail**
   - Are security-relevant actions logged?
   - Do logs include timestamp, user, action, resource, result?
   - Are sensitive values excluded from logs?

6. **Error Handling**
   - Do error messages avoid leaking system information?
   - Are security exceptions handled gracefully?

7. **Dependencies**
   - Are vulnerable dependencies identified and updated?
   - Are security advisories monitored?

8. **OWASP Compliance**
   - Does the code address at least the Top 3 from OWASP Top 10?
