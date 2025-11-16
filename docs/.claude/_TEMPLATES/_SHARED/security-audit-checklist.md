# Security Audit Checklist

> **Comprehensive security audit checklist based on OWASP Top 10 and security best practices**

## Scope Definition

**Audit Target:** [Component/Feature/Application]
**Date:** [YYYY-MM-DD]
**Auditor:** [Name]
**Severity Scale:** Critical | High | Medium | Low

---

## OWASP Top 10 (2021)

### A01: Broken Access Control
- [ ] Authentication required for protected resources
- [ ] Authorization checks on all endpoints
- [ ] User can only access their own data
- [ ] Admin functions require admin privileges
- [ ] No IDOR (Insecure Direct Object References)
- [ ] CORS properly configured
- [ ] No path traversal vulnerabilities

### A02: Cryptographic Failures
- [ ] Sensitive data encrypted at rest
- [ ] Sensitive data encrypted in transit (HTTPS/TLS)
- [ ] Strong encryption algorithms used (AES-256, RSA-2048+)
- [ ] No hardcoded secrets/API keys
- [ ] Passwords hashed with strong algorithm (bcrypt, Argon2)
- [ ] Salt used for password hashing
- [ ] Secure random number generation

### A03: Injection
- [ ] No SQL injection (parameterized queries/ORM)
- [ ] No NoSQL injection
- [ ] No command injection
- [ ] No LDAP injection
- [ ] Input validation on all user input
- [ ] Output encoding/escaping
- [ ] Prepared statements used

### A04: Insecure Design
- [ ] Threat modeling performed
- [ ] Security requirements defined
- [ ] Least privilege principle applied
- [ ] Defense in depth implemented
- [ ] Fail securely (errors don't expose info)
- [ ] Rate limiting on sensitive endpoints
- [ ] Circuit breakers for external services

### A05: Security Misconfiguration
- [ ] Default passwords changed
- [ ] Unnecessary features disabled
- [ ] Error messages don't leak info
- [ ] Security headers configured
  - [ ] X-Frame-Options
  - [ ] X-Content-Type-Options
  - [ ] Content-Security-Policy
  - [ ] Strict-Transport-Security
  - [ ] X-XSS-Protection
- [ ] HTTPS enforced
- [ ] Debug mode off in production
- [ ] Proper file permissions

### A06: Vulnerable and Outdated Components
- [ ] Dependencies up to date
- [ ] No known vulnerabilities (npm audit / composer audit / pip-audit)
- [ ] Automated dependency scanning in CI/CD
- [ ] Deprecated dependencies replaced
- [ ] Unused dependencies removed

### A07: Identification and Authentication Failures
- [ ] Strong password policy enforced
- [ ] Multi-factor authentication available
- [ ] Session management secure
  - [ ] Secure session cookies (HttpOnly, Secure, SameSite)
  - [ ] Session timeout configured
  - [ ] Session fixation prevented
- [ ] Account lockout after failed attempts
- [ ] Credential stuffing protection
- [ ] No weak password recovery mechanisms

### A08: Software and Data Integrity Failures
- [ ] Code integrity verified (signed commits)
- [ ] Dependency integrity verified (lock files, checksums)
- [ ] Auto-update mechanisms secure
- [ ] CI/CD pipeline secured
- [ ] No unsigned/unverified third-party code
- [ ] Subresource Integrity (SRI) for CDN resources

### A09: Security Logging and Monitoring Failures
- [ ] Security events logged (login, logout, failures)
- [ ] Sensitive actions logged
- [ ] Logs protected from tampering
- [ ] No sensitive data in logs
- [ ] Log retention policy defined
- [ ] Alerting configured for suspicious activity
- [ ] Logs monitored regularly

### A10: Server-Side Request Forgery (SSRF)
- [ ] User input validated before making requests
- [ ] Allowlist for external URLs
- [ ] No requests to internal/private IPs
- [ ] Response validation
- [ ] Timeouts configured

---

## Authentication & Authorization

### Authentication
- [ ] Passwords hashed (not encrypted or plain)
- [ ] Password complexity requirements
- [ ] No credentials in URLs
- [ ] Logout functionality works
- [ ] Session invalidated on logout
- [ ] Concurrent session handling
- [ ] Remember me functionality secure

### Authorization
- [ ] Role-based access control (RBAC)
- [ ] Permissions checked on backend (not just frontend)
- [ ] Horizontal privilege escalation prevented
- [ ] Vertical privilege escalation prevented
- [ ] API endpoints properly secured

---

## Input Validation

- [ ] All user input validated
- [ ] Whitelist validation (not just blacklist)
- [ ] Length limits enforced
- [ ] Type checking performed
- [ ] Format validation (email, phone, etc.)
- [ ] File upload restrictions (type, size)
- [ ] File content validated (not just extension)

---

## Output Encoding

- [ ] HTML encoding for web output
- [ ] JavaScript encoding
- [ ] URL encoding
- [ ] SQL encoding (or use prepared statements)
- [ ] LDAP encoding
- [ ] XML encoding
- [ ] CSV injection prevention

---

## Session Management

- [ ] Session IDs random and unpredictable
- [ ] Session timeout configured
- [ ] Idle timeout configured
- [ ] Session regeneration on privilege change
- [ ] Logout destroys session
- [ ] No session ID in URLs
- [ ] Secure cookie attributes set

---

## API Security

### API Authentication
- [ ] API requires authentication (OAuth, JWT, API keys)
- [ ] Tokens expire
- [ ] Refresh tokens rotated
- [ ] API keys not in client-side code

### API Authorization
- [ ] Endpoint-level authorization
- [ ] Resource-level authorization
- [ ] Rate limiting per user/IP
- [ ] Input validation on all endpoints

### API Design
- [ ] Versioning implemented
- [ ] Proper HTTP methods used
- [ ] Appropriate status codes returned
- [ ] No sensitive data in URLs
- [ ] CORS properly configured

---

## Data Protection

### Data at Rest
- [ ] Database encryption enabled
- [ ] File storage encrypted
- [ ] Backups encrypted
- [ ] Encryption keys rotated
- [ ] Key management solution used

### Data in Transit
- [ ] HTTPS/TLS enforced
- [ ] TLS 1.2+ used (TLS 1.0/1.1 disabled)
- [ ] Strong cipher suites
- [ ] Certificate validation
- [ ] HSTS enabled

### Data Handling
- [ ] PII identified and protected
- [ ] Data minimization practiced
- [ ] Data retention policy enforced
- [ ] Secure data deletion
- [ ] No sensitive data in logs/errors

---

## Frontend Security

- [ ] No XSS vulnerabilities
- [ ] Content Security Policy configured
- [ ] No eval() or similar dangerous functions
- [ ] DOM-based XSS prevented
- [ ] Clickjacking protection
- [ ] Secure postMessage implementation
- [ ] Third-party scripts reviewed

---

## Backend Security

- [ ] SQL injection prevented
- [ ] Command injection prevented
- [ ] XML external entity (XXE) prevented
- [ ] Deserialization attacks prevented
- [ ] Template injection prevented
- [ ] Server-side includes (SSI) injection prevented

---

## Infrastructure Security

- [ ] Firewall configured
- [ ] Unnecessary ports closed
- [ ] Services run with minimal privileges
- [ ] OS and software patched
- [ ] Intrusion detection configured
- [ ] DDoS protection in place
- [ ] Backup and recovery tested

---

## Third-Party Integrations

- [ ] API keys stored securely
- [ ] OAuth flows implemented correctly
- [ ] Webhook signatures verified
- [ ] Third-party data validated
- [ ] Vendor security reviewed

---

## Compliance (if applicable)

- [ ] GDPR compliance (EU users)
- [ ] CCPA compliance (CA users)
- [ ] HIPAA compliance (health data)
- [ ] PCI DSS compliance (payment data)
- [ ] SOC 2 requirements met

---

## Testing

- [ ] Security testing in CI/CD
- [ ] Static analysis (SAST)
- [ ] Dynamic analysis (DAST)
- [ ] Dependency scanning
- [ ] Penetration testing performed
- [ ] Vulnerability scanning automated

---

## Findings Template

```markdown
## Finding: [Vulnerability Name]

**Severity:** [Critical/High/Medium/Low]
**CWE ID:** [CWE-XXX]
**CVSS Score:** [X.X]

### Description
[What is the vulnerability?]

### Location
- **File:** [path/to/file.ext:line]
- **Endpoint:** [/api/endpoint]
- **Component:** [Component name]

### Impact
[What could an attacker do?]

### Proof of Concept
```
[Code or steps to reproduce]
```

### Recommendation
[How to fix it]

### References
- [Link to OWASP]
- [Link to CWE]
```

---

## Quick Reference

### Severity Ratings

**Critical:**
- Remote code execution
- Authentication bypass
- SQL injection with data access
- Exposed admin functions

**High:**
- XSS in critical flows
- CSRF on state-changing operations
- Privilege escalation
- Sensitive data exposure

**Medium:**
- Information disclosure
- Missing security headers
- Weak cryptography
- Session fixation

**Low:**
- Security through obscurity
- Missing best practices
- Non-exploitable vulnerabilities
- Security recommendations

---

*Regular security audits should be performed quarterly or before major releases.*
