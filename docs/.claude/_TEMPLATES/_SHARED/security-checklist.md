# Security Checklist

> **Universal security best practices**
>
> Stack-specific security configurations are in respective stack directories.

## OWASP Top 10 (2021)

### A01:2021 – Broken Access Control

**Risks:**
- Unauthorized access to resources
- Privilege escalation
- Insecure direct object references (IDOR)

**Prevention:**
- [ ] Implement proper authentication
- [ ] Enforce authorization on every request
- [ ] Use role-based access control (RBAC)
- [ ] Deny by default
- [ ] Validate user permissions server-side
- [ ] Use UUIDs instead of sequential IDs for public resources
- [ ] Log access control failures

**Example (Authorization Check):**
```python
# Python
def get_user_profile(user_id: str, current_user: User):
    """Get user profile with authorization check."""
    if current_user.id != user_id and not current_user.is_admin:
        raise PermissionDenied("Cannot access other user's profile")

    return User.objects.get(id=user_id)
```

```javascript
// JavaScript
function getUserProfile(userId, currentUser) {
  // Authorization check
  if (currentUser.id !== userId && !currentUser.isAdmin) {
    throw new ForbiddenError("Cannot access other user's profile")
  }

  return User.findById(userId)
}
```

### A02:2021 – Cryptographic Failures

**Risks:**
- Exposure of sensitive data
- Weak encryption
- Passwords stored in plain text

**Prevention:**
- [ ] Use HTTPS everywhere (TLS 1.2+)
- [ ] Never store passwords in plain text
- [ ] Use strong password hashing (bcrypt, Argon2, scrypt)
- [ ] Encrypt sensitive data at rest
- [ ] Use secure random number generators
- [ ] Implement proper key management
- [ ] Don't roll your own crypto

**Password Hashing:**
```python
# Python (using bcrypt)
import bcrypt

def hash_password(password: str) -> str:
    """Hash password using bcrypt."""
    salt = bcrypt.gensalt(rounds=12)
    return bcrypt.hashpw(password.encode('utf-8'), salt).decode('utf-8')

def verify_password(password: str, hashed: str) -> bool:
    """Verify password against hash."""
    return bcrypt.checkpw(password.encode('utf-8'), hashed.encode('utf-8'))
```

```javascript
// JavaScript (using bcrypt)
const bcrypt = require('bcrypt')

async function hashPassword(password) {
  const saltRounds = 12
  return await bcrypt.hash(password, saltRounds)
}

async function verifyPassword(password, hash) {
  return await bcrypt.compare(password, hash)
}
```

### A03:2021 – Injection

**Risks:**
- SQL injection
- Command injection
- LDAP injection
- Template injection

**Prevention:**
- [ ] Use parameterized queries / prepared statements
- [ ] Use ORMs properly
- [ ] Validate and sanitize all inputs
- [ ] Use allowlists over denylists
- [ ] Escape special characters
- [ ] Apply principle of least privilege

**SQL Injection Prevention:**
```python
# Python (Django ORM - SAFE)
User.objects.filter(email=user_input)  # ✅ Parameterized

# Raw SQL with parameters - SAFE
cursor.execute("SELECT * FROM users WHERE email = %s", [user_input])  # ✅

# NEVER DO THIS - VULNERABLE
cursor.execute(f"SELECT * FROM users WHERE email = '{user_input}'")  # ❌ DANGEROUS
```

```javascript
// JavaScript (with parameterized query - SAFE)
db.query('SELECT * FROM users WHERE email = $1', [userInput])  // ✅

// NEVER DO THIS - VULNERABLE
db.query(`SELECT * FROM users WHERE email = '${userInput}'`)  // ❌ DANGEROUS
```

### A04:2021 – Insecure Design

**Risks:**
- Missing security controls
- Flawed business logic
- No threat modeling

**Prevention:**
- [ ] Conduct threat modeling
- [ ] Implement security requirements
- [ ] Use secure design patterns
- [ ] Peer review security-critical code
- [ ] Implement defense in depth
- [ ] Plan for security from the start

### A05:2021 – Security Misconfiguration

**Risks:**
- Default credentials
- Unnecessary features enabled
- Verbose error messages in production
- Missing security headers

**Prevention:**
- [ ] Disable debug mode in production
- [ ] Remove default accounts/passwords
- [ ] Keep software updated
- [ ] Implement security headers
- [ ] Configure CORS properly
- [ ] Minimize installed packages
- [ ] Use environment-specific configs

**Security Headers:**
```
Content-Security-Policy: default-src 'self'
X-Frame-Options: DENY
X-Content-Type-Options: nosniff
Strict-Transport-Security: max-age=31536000; includeSubDomains
Referrer-Policy: no-referrer
Permissions-Policy: geolocation=(), microphone=(), camera=()
```

### A06:2021 – Vulnerable and Outdated Components

**Risks:**
- Known vulnerabilities
- Unpatched software
- Deprecated dependencies

**Prevention:**
- [ ] Keep dependencies updated
- [ ] Monitor security advisories
- [ ] Use dependency scanning tools
- [ ] Remove unused dependencies
- [ ] Pin dependency versions
- [ ] Audit third-party code

**Tools:**
- `npm audit` / `yarn audit` / `pnpm audit`
- `pip-audit` / `safety`
- `composer audit`
- Snyk, Dependabot, GitHub Security Alerts

### A07:2021 – Identification and Authentication Failures

**Risks:**
- Weak passwords
- No rate limiting
- Session hijacking
- Credential stuffing

**Prevention:**
- [ ] Implement multi-factor authentication (MFA)
- [ ] Enforce strong password policies
- [ ] Implement rate limiting on login
- [ ] Use secure session management
- [ ] Implement account lockout
- [ ] Rotate session IDs after login
- [ ] Secure password recovery

**Rate Limiting Example:**
```python
# Python (using decorator)
from functools import wraps
from flask_limiter import Limiter

limiter = Limiter(
    key_func=lambda: request.remote_addr,
    default_limits=["200 per day", "50 per hour"]
)

@app.route("/api/login", methods=["POST"])
@limiter.limit("5 per minute")  # Max 5 login attempts per minute
def login():
    # Login logic
    pass
```

```javascript
// JavaScript (using express-rate-limit)
const rateLimit = require('express-rate-limit')

const loginLimiter = rateLimit({
  windowMs: 60 * 1000, // 1 minute
  max: 5, // 5 requests per window
  message: 'Too many login attempts, please try again later'
})

app.post('/api/login', loginLimiter, (req, res) => {
  // Login logic
})
```

### A08:2021 – Software and Data Integrity Failures

**Risks:**
- Insecure CI/CD pipeline
- Auto-update without verification
- Untrusted deserialization

**Prevention:**
- [ ] Verify digital signatures
- [ ] Use trusted repositories
- [ ] Implement code signing
- [ ] Review CI/CD security
- [ ] Don't deserialize untrusted data
- [ ] Use integrity checks (checksums, SRI)

**Subresource Integrity (SRI):**
```html
<script
  src="https://cdn.example.com/library.js"
  integrity="sha384-oqVuAfXRKap7fdgcCY5uykM6+R9GqQ8K/ux..."
  crossorigin="anonymous">
</script>
```

### A09:2021 – Security Logging and Monitoring Failures

**Risks:**
- Undetected breaches
- Incomplete audit trails
- No alerting

**Prevention:**
- [ ] Log security events (login, logout, failed attempts, authorization failures)
- [ ] Monitor for suspicious activity
- [ ] Set up alerts for anomalies
- [ ] Protect logs from tampering
- [ ] Centralize log collection
- [ ] Don't log sensitive data (passwords, tokens, PII)

**What to Log:**
```javascript
// Log security events
logger.info('User login successful', {
  userId: user.id,
  ip: req.ip,
  userAgent: req.get('user-agent'),
  timestamp: new Date()
})

logger.warn('Failed login attempt', {
  email: req.body.email, // Email OK to log
  ip: req.ip,
  reason: 'Invalid password',
  timestamp: new Date()
})

// NEVER log sensitive data
logger.info('Login attempt', {
  password: req.body.password  // ❌ NEVER LOG PASSWORDS
})
```

### A10:2021 – Server-Side Request Forgery (SSRF)

**Risks:**
- Access to internal resources
- Port scanning
- Reading local files

**Prevention:**
- [ ] Validate and sanitize URLs
- [ ] Use allowlists for URLs/IPs
- [ ] Disable HTTP redirects
- [ ] Use network segmentation
- [ ] Don't expose error details

**URL Validation:**
```python
# Python
from urllib.parse import urlparse

ALLOWED_HOSTS = ['api.example.com', 'cdn.example.com']

def is_url_safe(url: str) -> bool:
    """Validate URL is from allowed hosts."""
    parsed = urlparse(url)

    # Block internal IPs
    if parsed.hostname in ['localhost', '127.0.0.1', '0.0.0.0']:
        return False

    # Check against allowlist
    if parsed.hostname not in ALLOWED_HOSTS:
        return False

    # Only allow HTTP/HTTPS
    if parsed.scheme not in ['http', 'https']:
        return False

    return True
```

## Input Validation

### Validation Principles

1. **Validate on server-side** (client validation is UX, not security)
2. **Use allowlists** over denylists when possible
3. **Validate type, length, format, and range**
4. **Reject invalid input** (don't just sanitize)
5. **Validate early** in the request pipeline

### Common Validation Patterns

```javascript
// JavaScript validation examples
const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/
const uuidRegex = /^[0-9a-f]{8}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{12}$/i

function validateEmail(email) {
  if (!email || typeof email !== 'string') {
    throw new ValidationError('Email is required')
  }

  if (email.length > 255) {
    throw new ValidationError('Email too long')
  }

  if (!emailRegex.test(email)) {
    throw new ValidationError('Invalid email format')
  }

  return email.toLowerCase().trim()
}

function validateUUID(id) {
  if (!uuidRegex.test(id)) {
    throw new ValidationError('Invalid ID format')
  }
  return id
}
```

## Output Encoding

### Cross-Site Scripting (XSS) Prevention

**Types of XSS:**
- **Reflected XSS** - Unsanitized user input in response
- **Stored XSS** - Malicious data stored in database
- **DOM-based XSS** - Client-side code vulnerability

**Prevention:**
- [ ] Encode output based on context (HTML, JS, URL, CSS)
- [ ] Use templating engines with auto-escaping
- [ ] Set Content-Security-Policy header
- [ ] Use HTTPOnly and Secure flags on cookies
- [ ] Validate input before storage

**Encoding Examples:**
```javascript
// JavaScript - Use framework's escaping
// React auto-escapes
<div>{userInput}</div>  // ✅ Safe

// Vue auto-escapes
<div>{{ userInput }}</div>  // ✅ Safe

// Manual escaping if needed
function escapeHtml(str) {
  return str
    .replace(/&/g, '&amp;')
    .replace(/</g, '&lt;')
    .replace(/>/g, '&gt;')
    .replace(/"/g, '&quot;')
    .replace(/'/g, '&#x27;')
}
```

## Authentication Best Practices

### Password Requirements

**Minimum Standards:**
- Minimum 8 characters (12+ recommended)
- Mix of uppercase, lowercase, numbers, special characters
- Check against common password lists
- Allow passphrases (don't limit max length)
- Don't expire passwords arbitrarily

### Session Management

**Best Practices:**
- [ ] Use framework's built-in session handling
- [ ] Set appropriate session timeout
- [ ] Regenerate session ID after login
- [ ] Invalidate session on logout
- [ ] Use secure, HTTPOnly cookies
- [ ] Implement CSRF protection

**Cookie Settings:**
```javascript
// JavaScript (Express)
app.use(session({
  secret: process.env.SESSION_SECRET,
  resave: false,
  saveUninitialized: false,
  cookie: {
    secure: true,      // HTTPS only
    httpOnly: true,    // No JavaScript access
    sameSite: 'strict', // CSRF protection
    maxAge: 3600000    // 1 hour
  }
}))
```

## API Security

### Authentication Methods

**Bearer Tokens (JWT):**
```
Authorization: Bearer <token>
```

**Best practices:**
- [ ] Short expiration times (15-60 minutes)
- [ ] Implement refresh tokens
- [ ] Validate signature
- [ ] Check expiration
- [ ] Validate issuer and audience

**API Keys:**
- [ ] Use for server-to-server only
- [ ] Rotate regularly
- [ ] Use different keys per environment
- [ ] Never commit to version control
- [ ] Rate limit API key usage

### CORS Configuration

```javascript
// Restrictive CORS (recommended)
const cors = require('cors')

app.use(cors({
  origin: ['https://app.example.com'],  // Specific origins
  methods: ['GET', 'POST'],
  allowedHeaders: ['Content-Type', 'Authorization'],
  credentials: true,
  maxAge: 86400
}))

// NEVER do this in production
app.use(cors({ origin: '*' }))  // ❌ DANGEROUS
```

## File Upload Security

### Upload Validation

**Checklist:**
- [ ] Validate file type (check magic bytes, not just extension)
- [ ] Limit file size
- [ ] Scan for malware
- [ ] Store outside web root
- [ ] Generate random filenames
- [ ] Implement rate limiting
- [ ] Use Content-Disposition: attachment

**Example:**
```javascript
// JavaScript (using multer)
const multer = require('multer')
const path = require('path')
const crypto = require('crypto')

const storage = multer.diskStorage({
  destination: '/var/uploads',  // Outside web root
  filename: (req, file, cb) => {
    // Random filename
    const randomName = crypto.randomBytes(16).toString('hex')
    const ext = path.extname(file.originalname)
    cb(null, `${randomName}${ext}`)
  }
})

const fileFilter = (req, file, cb) => {
  // Validate file type
  const allowedTypes = ['image/jpeg', 'image/png', 'image/gif']

  if (!allowedTypes.includes(file.mimetype)) {
    return cb(new Error('Invalid file type'))
  }

  cb(null, true)
}

const upload = multer({
  storage,
  fileFilter,
  limits: {
    fileSize: 5 * 1024 * 1024  // 5MB max
  }
})
```

## Environment Variables

### Secret Management

**Never commit:**
- ❌ API keys
- ❌ Database passwords
- ❌ JWT secrets
- ❌ Private keys
- ❌ OAuth client secrets

**Best practices:**
- [ ] Use `.env` files (add to `.gitignore`)
- [ ] Provide `.env.example` with dummy values
- [ ] Use secret management tools (Vault, AWS Secrets Manager)
- [ ] Rotate secrets regularly
- [ ] Use different secrets per environment

**.env.example:**
```bash
# Database
DATABASE_URL=postgresql://user:password@localhost/dbname

# API Keys
STRIPE_SECRET_KEY=sk_test_xxxxxxxxxxxx
SENDGRID_API_KEY=SG.xxxxxxxxxxxx

# Security
JWT_SECRET=your-256-bit-secret
SESSION_SECRET=your-session-secret

# External Services
AWS_ACCESS_KEY_ID=AKIAIOSFODNN7EXAMPLE
AWS_SECRET_ACCESS_KEY=wJalrXUtnFEMI/K7MDENG/bPxRfiCYEXAMPLEKEY
```

## Security Testing

### Tools

**SAST (Static Application Security Testing):**
- SonarQube
- Snyk Code
- Semgrep
- Bandit (Python)
- ESLint security plugins (JavaScript)

**DAST (Dynamic Application Security Testing):**
- OWASP ZAP
- Burp Suite
- Nikto

**Dependency Scanning:**
- `npm audit`
- `pip-audit`
- `composer audit`
- Snyk
- Dependabot

### Penetration Testing

**Frequency:**
- Before major releases
- After significant security changes
- Annually (minimum)

**Scope:**
- Authentication and authorization
- Input validation
- Session management
- Business logic flaws
- API security

## Incident Response

### Preparation

**Have a plan:**
- [ ] Incident response team identified
- [ ] Communication plan
- [ ] Escalation procedures
- [ ] Backup and recovery procedures
- [ ] Legal/PR contacts

### Detection

**Monitor for:**
- Unusual traffic patterns
- Failed login attempts
- Privilege escalation attempts
- Data exfiltration
- System performance anomalies

### Response Steps

1. **Contain** - Isolate affected systems
2. **Investigate** - Determine scope and impact
3. **Eradicate** - Remove threat
4. **Recover** - Restore normal operations
5. **Learn** - Post-incident review

---

**Last Updated:** 2025-01-16
**Version:** 1.0
**Reference:** [OWASP Top 10 2021](https://owasp.org/www-project-top-ten/)
