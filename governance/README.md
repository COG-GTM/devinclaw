# DevinClaw Enterprise Security Compliance Framework

> Centralized CIS Benchmark, SOC 2 / ISO 27001, and Zero Trust compliance for the enterprise modernization with Devin, adapted for the DevinClaw platform.

## Platform Authorization Status

| Platform | Security Certification | IL Level | Use Case |
|----------|----------------|----------|----------|
| **Devin** | Not cloud security compliance Certified | N/A | Generate compliant code patterns, autonomous modernization agents |

## Quick Start

### For Devin Users
1. Copy `devin/knowledge.md` to Devin Knowledge
2. Copy `devin/playbook.md` to Devin Playbooks
3. Copy `devin/zero-trust-knowledge.md` to Devin Knowledge (Zero Trust)
4. Copy `devin/zero-trust-playbook.md` to Devin Playbooks (Zero Trust)
5. Done -- Devin will generate Zero Trust compliant code for enterprise modernization tasks.

3. Done -- Cascade will enforce Zero Trust compliance automatically.

## What's Included

| File | Purpose |
|------|---------|
| `devin/knowledge.md` | Security knowledge base for Devin agents |
| `devin/playbook.md` | Secure development workflow for Devin |
| `devin/zero-trust-knowledge.md` | Zero Trust principles for Devin |
| `devin/zero-trust-playbook.md` | Zero Trust workflow for Devin |
| `templates/` | Reusable secure Python modules |
| `tests/` | Automated compliance verification tests |
| `docs/` | Architecture and compliance documentation |

## Compliance Coverage

- **Zero Trust Architecture** -- Zero Trust Architecture implementation
- **CIS Benchmark** -- All 18 security categories
- **SOC 2 / ISO 27001** -- AC, AU, IA, SC, SI control families
- **cloud security compliance** -- Moderate and High baseline
- **Enterprise Enterprise Modernization** -- Aligned with Executive Order 14028 and enterprise systems modernization requirements

## Zero Trust Architecture

This framework implements **Zero Trust Architecture Zero Trust Architecture** principles for DevinClaw's autonomous modernization agents:

| Principle | Implementation | Why It Matters |
|-----------|----------------|----------------|
| **Never Trust, Always Verify** | Continuous session verification | Tokens can be stolen mid-session |
| **IP-Bound Sessions** | Sessions tied to originating IP | Stolen tokens useless from different IP |
| **Session Regeneration** | New session ID after auth | Prevents session fixation attacks |
| **15-Minute Timeout** | Sessions expire per CIS Benchmark SESS-001 | Limits attack window |
| **Least Privilege** | Default deny, explicit grants | Limits blast radius of compromise |
| **Full Audit Trail** | Every action logged | Forensics and compliance |

### Zero Trust Flow

```
Request --> Verify Session --> Check IP Binding --> Check Timeout --> Authorize --> Process --> Log
 | | | |
 Missing? Mismatch? Expired? Denied?
 | | | |
 REJECT DESTROY + REJECT REJECT
 LOG ALERT
```

## Key Security Controls

| Control | Implementation | Enterprise Mapping |
|---------|----------------|-----------------|
| Input Validation | Whitelist validation, sanitization | CIS Benchmark INPUT-001, security input validation |
| Authentication | 14+ char passwords, MFA | CIS Benchmark AUTH-001, security multi-factor authentication |
| Session Security | 15 min timeout, IP binding | CIS Benchmark SESS-001, security AC-12 |
| Encryption | AES-256 at rest, TLS 1.2+ in transit | CIS Benchmark CRYPTO-001/34, security encryption in transit/28 |
| Audit Logging | JSON format, all security events | CIS Benchmark AUDIT-001, security audit logging/3 |
| Security Headers | HSTS, CSP, X-Frame-Options | CIS Benchmark HEADERS-001, security SI-11 |

## Templates

### Python Security Modules
- `security_utils.py` -- Input validation, sanitization, rate limiting
- `auth_manager.py` -- Authentication, sessions, password policies
- `audit_logger.py` -- Structured audit logging
- `zero_trust_middleware.py` -- IP binding, continuous verification, session management
- `cac_piv_handler.py` -- hardware tokens certificate authentication for enterprise/enterprise systems

## Testing

Run the compliance test suite:

```bash
# Run all Zero Trust tests
pytest governance/tests/test_zero_trust.py -v

# Run with coverage
pytest governance/tests/ -v --cov=governance/templates

# Run specific test class
pytest governance/tests/test_zero_trust.py::TestIPBoundSessions -v
```

### What Tests Verify

| Test | Zero Trust Principle |
|------|---------------------|
| `TestIPBoundSessions` | Sessions reject requests from different IPs |
| `TestSessionTimeout` | Sessions expire after 15 minutes |
| `TestSessionRegeneration` | New session ID generated after login |
| `TestContinuousVerification` | Every request must have valid session |
| `TestAuditLogging` | Security events are properly logged |
| `TestAccountLockout` | Account lockout after 5 failed attempts |
| `TestSessionSecurity` | Session IDs are cryptographically random |

---

**Sensitivity: INTERNAL**
**Adapted for DevinClaw enterprise Enterprise Modernization**
