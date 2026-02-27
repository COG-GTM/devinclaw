# Playbook: Security Vulnerability Remediation

> **Required Knowledge:** `security-auditor`

## Overview
Scan codebases for security vulnerabilities against industry standards (CIS Benchmark, SOC 2 / ISO 27001, cloud security compliance) and auto-remediate findings. Integrates with Devin Review bug catcher for continuous security enforcement.

## When to Use
- Pre-deployment security hardening
- Remediating findings from security audits or penetration tests
- Continuous compliance monitoring during modernization
- Preparing for compliance certification review

## Instructions

1. **Run static analysis**: Scan the codebase with SonarQube MCP (if available) or built-in analysis for OWASP Top 10 vulnerabilities.

2. **Map findings to enterprise controls**: Each finding maps to CIS Benchmark V-number and . Classify by finding severity: Critical severity (fix now), High severity (30 days), Medium severity (90 days).

3. **Generate SDD remediation spec**: For each Critical severity/II finding, create a spec describing the vulnerability, impact, and remediation approach.

4. **Remediate**: Apply fixes following the spec. Common patterns:
 - SQL injection → parameterized queries
 - XSS → input sanitization + CSP headers
 - Hardcoded credentials → environment variables + secrets manager
 - Missing auth → middleware enforcement
 - Weak crypto → upgrade to industry encryption standards approved algorithms
 - Missing audit logs → structured logging with security events

5. **Write regression tests**: For each remediated vulnerability, write a test that reproduces the original attack vector and validates it's blocked.

6. **Devin Review**: Auto-review the remediation PR. Bug catcher validates no new vulnerabilities introduced.

7. **Generate compliance report**: Output: finding ID, severity, status (remediated/mitigated/accepted risk), test case ID, control mapping.

## Specifications
- Critical severity findings must be remediated before any production deployment
- All crypto must be industry encryption standards validated (cryptographic protection)
- TLS minimum: 1.2, prefer 1.3 (encryption in transit)
- Session timeout: ≤ 15 minutes (CIS Benchmark SESS-001)
- Password minimum: 14 characters (CIS Benchmark AUTH-001)

## Advice
- The most common enterprise finding is missing audit logging — it's also the easiest to fix and the hardest to retrofit later
- Hardcoded credentials in migrated code is extremely common — grep for them in every PR
- Don't just fix the symptom; fix the pattern. If one endpoint has SQL injection, check ALL endpoints


## Self-Verification (Devin 2.2)

Before declaring this playbook complete:

1. **Run all verification gates**: Execute the full self-verify loop — build, test, lint, typecheck, security scan. If the playbook produced code changes, run the test suite and confirm all tests pass.
2. **Auto-fix failures**: If any gate fails, attempt automated repair. Re-run the failing gate. If it fails again after 2 attempts, escalate to human reviewer.
3. **Computer-use E2E** (if applicable): For changes that affect UI or user-facing functionality, use Devin 2.2 computer use to run the application and verify functional correctness.

## Evidence Pack Generation

On completion, produce `evidence-pack.json` in the output directory:

```json
{
 "playbook": "<this playbook name>",
 "session_id": "<Devin session ID>",
 "timestamp": "<ISO 8601>",
 "artifacts": [
 { "filename": "<file>", "sha256": "<hash>", "stage": "<stage>" }
 ],
 "verification": {
 "tests_passed": true,
 "lint_clean": true,
 "security_scan_clean": true,
 "gates_failed_and_auto_fixed": []
 },
 "knowledge_updates": [],
 "escalations": []
}
```

This evidence pack is required for SDLC validation and audit trail compliance (FAR 4.703).
