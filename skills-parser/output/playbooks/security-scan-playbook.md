# security-scan

## Overview
Scan codebases for CIS Benchmark, SOC 2 / ISO 27001, and cloud security compliance compliance violations. Use this skill when performing enterprise security audits on enterprise applications, when validating compliance posture before compliance certification submissions, or when scanning for vulnerabilities and security misconfigurations in modernized code.

## When to Use
This skill performs comprehensive security compliance scanning of codebases against industry security CIS Benchmark benchmarks, families, and cloud security compliance baselines. It connects to the SonarQube MCP server for static analysis, runs the security benchmark scanner MCP for security benchmark validation, checks through the security-controls-mcp, and validates Zero Trust architecture principles. When violations are found, the skill generates SDD remediation specifications, TDD test cases for security fixes, and spawns Devin sessions to auto-remediate findings at scale.

Enterprises operate critical national infrastructure with strict security requirements. All enterprise applications must maintain compliance certification through continuous compliance with regulatory compliance, cloud security compliance, and industry security CIS Benchmark requirements. Safety-critical systems in the mission-critical systems are additionally subject to DO-178C (Software Considerations in Airborne Systems and Equipment Certification) and DO-326A (Airworthiness Security Process Specification). A single unmitigated High finding on a CIS Benchmark scan can block a compliance certification renewal, grounding modernization efforts. This skill automates the scan-remediate-validate cycle to maintain continuous compliance posture.

## Instructions
1. **Connect to SonarQube MCP and establish scan baseline**
 - Connect to the SonarQube MCP server via SSE transport.
 - Verify the project exists in SonarQube or create a new project configuration.
 - Retrieve the current quality profile for the project's language(s).
 - Ensure the quality profile includes the enterprise Enterprise Security ruleset (CIS Benchmark-aligned rules, OWASP Top 10, CWE Top 25).
 - If a previous scan exists, retrieve the baseline metrics (findings count, coverage, quality gate status) for delta comparison.
 - Record the scan initiation event in the session audit log.

2. **Run security benchmark compliance scan (AUTH-001 through HEADERS-001)**
 - Invoke the benchmark-scanner-mcp to run security benchmarks against the codebase.
 - Scan for each applicable CIS Benchmark rule:
 - **AUTH-001 (Authentication)**: Verify password policy enforcement (minimum 14 characters, complexity requirements, bcrypt with 12+ rounds), multi-factor authentication implementation, and account lockout after 5 failed attempts with 15-minute lockout duration.
 - **SESS-001 (Session Management)**: Check session timeout configuration (15-minute inactivity), secure cookie flags (Secure, HttpOnly, SameSite=Strict), session ID regeneration after authentication, and session invalidation on logout.
 - **INPUT-001 (Input Validation)**: Verify whitelist-based input validation on all user-facing endpoints, length limit enforcement (max 255 characters default), format validation with regex patterns, and rejection of unexpected input patterns.
 - **SEC-XXX (Input Sanitization)**: Check for parameterized database queries (no string concatenation in SQL), output encoding to prevent XSS, removal of dangerous characters (< > " ' ; & | $ ( ) `), and CSRF token validation on state-changing operations.
 - **CRYPTO-001 (Encryption at Rest)**: Verify AES-256 encryption for data at rest, industry encryption standards validated cryptographic modules, encrypted database connections, and encrypted file storage for sensitive data.
 - **TLS-001 (Encryption in Transit)**: Check TLS 1.2+ enforcement (TLS 1.0 and 1.1 disabled), certificate validation, HSTS header configuration, and mutual TLS where required by system architecture.
 - **AUDIT-001 (Audit Logging)**: Verify structured JSON audit logging for authentication events (success and failure), authorization failures, data access and modification, administrative actions, and security-relevant system events.
 - **RBAC-001 (Access Control)**: Check role-based access control (RBAC) or attribute-based access control (ABAC) implementation, principle of least privilege enforcement, and separation of duties for administrative functions.
 - **SEC-XXX (Configuration Management)**: Verify no hardcoded credentials, API keys, or secrets in source code; environment-variable-based configuration; and secure default settings.
 - **SEC-XXX (Integrity Checking)**: Check for file integrity monitoring, code signing verification, and tamper detection mechanisms.
 - **SEC-XXX (Error Handling)**: Verify generic error messages returned to users (no stack traces, no internal details), detailed internal logging with stack traces, and graceful degradation under error conditions.
 - **SEC-XXX (Secure Communications)**: Check for secure inter-service communication, API authentication and authorization, and certificate pinning where applicable.
 - **HEADERS-001 (Security Headers)**: Verify HTTP security headers on all responses: Strict-Transport-Security, X-Frame-Options (DENY), X-Content-Type-Options (nosniff), Content-Security-Policy (default-src 'self'), and X-XSS-Protection.
 - Parse SCAP/compliance report results and classify each finding by severity: Critical, High, Medium, Low, Informational.
 - Map each CIS Benchmark finding to the specific source file, line number, and code construct that triggered it.

3. **Check (AC, AU, IA, SC, SI)**
 - Invoke the security-controls-mcp to validate control implementations for each applicable control family:
 - **AC (Access Control)**: account management (Account Management), access enforcement (Access Enforcement), least privilege (Least Privilege), unsuccessful login attempts (Unsuccessful Logon Attempts), AC-8 (System Use Notification), AC-11 (Session Lock), AC-12 (Session Termination), remote access (Remote Access), AC-20 (Use of External Systems).
 - **AU (Audit and Accountability)**: audit logging (Event Logging), audit logging (Content of Audit Records), AU-4 (Audit Storage Capacity), audit review (Audit Review, Analysis, and Reporting), audit timestamps (Time Stamps), AU-9 (Protection of Audit Information), AU-11 (Audit Record Retention), audit generation (Audit Generation).
 - **IA (Identification and Authentication)**: multi-factor authentication (Identification and Authentication for Organizational Users), identifier management, authenticator management (Authenticator Management), authenticator feedback, external user authentication, re-authentication.
 - **SC (System and Communications Protection)**: SC-7 (Boundary Protection), encryption in transit (Transmission Confidentiality and Integrity), cryptographic key management (Cryptographic Key Establishment and Management), cryptographic protection (Cryptographic Protection), SC-23 (Session Authenticity), encryption at rest (Protection of Information at Rest).
 - **SI (System and Information Integrity)**: flaw remediation (Flaw Remediation), malicious code protection (Malicious Code Protection), system monitoring (System Monitoring), SI-5 (Security Alerts and Advisories), input validation (Information Input Validation), SI-11 (Error Handling), SI-16 (Memory Protection).
 - For each control, determine the implementation status: Implemented, Partially Implemented, Planned, Not Implemented, or Not Applicable.
 - Generate control assessment evidence by mapping code artifacts (configuration files, security middleware, authentication modules, logging implementations) to specific control requirements.
 - Flag any controls marked as Not Implemented or Partially Implemented as findings requiring remediation.

4. **Check cloud security compliance baselines and continuous monitoring requirements**
 - Based on the system's cloud security compliance baseline (Low, Moderate, or High), validate that all required controls from the cloud security compliance Security Controls Baseline are addressed.
 - Verify continuous monitoring artifacts:
 - Vulnerability scan results are current (within 30 days for High, 90 days for Moderate).
 - Software inventory (SBOM) is current and complete.
 - Configuration baselines are documented and enforced.
 - Plan of Action and Milestones (remediation plan) is maintained for open findings.
 - Check for cloud security compliance-specific requirements beyond SOC 2 / ISO 27001:
 - cloud security compliance parameter values (e.g., unsuccessful login attempts lockout after 3 consecutive attempts for cloud security compliance vs. 5 for security baseline).
 - Additional cloud security compliance controls not in the security baseline.
 - Incident response plan alignment with cloud security compliance IR requirements.
 - Invoke the sbom-mcp to generate or validate the Software Bill of Materials in CycloneDX format.
 - Run dependency scanning through sonarqube-mcp to identify CVEs in third-party components.

5. **Validate Zero Trust architecture principles**
 - Assess the codebase against Zero Trust Architecture (Zero Trust Architecture) principles:
 - **Verify explicitly**: Check that every request is authenticated and authorized regardless of network location. Verify that API endpoints do not rely on network perimeter security alone.
 - **Use least privilege access**: Validate that service accounts, API keys, and user roles are scoped to minimum required permissions. Check for overly permissive IAM policies or broad database grants.
 - **Assume breach**: Verify that the application implements defense-in-depth: encrypted communications between microservices, segmented access to data stores, and monitoring for anomalous behavior.
 - Check for Zero Trust implementation patterns:
 - Service mesh authentication (mTLS between services).
 - Token-based authentication with short-lived tokens (JWT expiration <= 15 minutes).
 - API gateway enforcement with rate limiting and request validation.
 - Microsegmentation in network policies (if Kubernetes manifests or infrastructure-as-code are present).
 - Flag any reliance on perimeter-only security (e.g., "trusted" internal networks, IP-based allowlists without authentication) as architectural findings.

6. **Generate SDD specification for remediation**
 - For all findings sensitive as Critical or High, generate a Software Design Document (SDD) that specifies:
 - Finding identifier (CIS Benchmark V-ID, security control ID, CVE number, or CWE ID).
 - Current vulnerable code location (file, line number, function).
 - Description of the vulnerability and its potential impact on enterprise perations.
 - Proposed remediation approach with specific code changes.
 - Mapping to the SDD constitution's security requirements.
 - Risk assessment if the finding is deferred (for remediation plan documentation).
 - Group related findings into remediation packages (e.g., all authentication findings in one package, all encryption findings in another).
 - Produce a remediation SDD per package following the template in `sdd/templates/spec.md`.
 - Include architectural guidance for systemic issues (e.g., if the application lacks a centralized authentication module, specify the design for one).

7. **Generate TDD test cases for security fixes**
 - For each remediation SDD, generate test cases that:
 - Verify the vulnerability is no longer exploitable after the fix.
 - Test boundary conditions and edge cases (e.g., password exactly 13 characters must be rejected, exactly 14 must be accepted).
 - Validate that the fix does not break existing functionality (regression tests).
 - Test for related vulnerabilities (e.g., if fixing SQL injection in one endpoint, test all endpoints for the same class of vulnerability).
 - Create test stubs organized by security domain:
 - `tests/security/test_authentication.py` (or .java, .ts): Password policy, MFA, lockout, session management.
 - `tests/security/test_input_validation.py`: Input validation, sanitization, injection prevention.
 - `tests/security/test_encryption.py`: Encryption at rest, in transit, key management.
 - `tests/security/test_audit_logging.py`: Audit event generation, log format, log protection.
 - `tests/security/test_access_control.py`: RBAC enforcement, least privilege, separation of duties.
 - `tests/security/test_security_headers.py`: HTTP security headers on all response types.
 - Tests must be runnable in CI/CD and produce machine-readable results (JUnit XML, pytest XML, or Jest JSON).
 - For safety-critical systems (DO-178C), generate additional structural coverage tests per the applicable DAL requirements.

8. **Spawn Devin sessions to auto-remediate findings**
 - If remediation mode is auto-remediate, create Devin sessions via the Devin API to implement fixes:
 - Group findings by file or module to minimize context switching.
 - Create one Devin session per remediation package (e.g., one for authentication fixes, one for encryption fixes).
 - Each session receives: the remediation SDD, TDD test stubs, the source files requiring modification, and the governance/devin/knowledge.md and governance/devin/playbook.md as Devin Knowledge and Playbook.
 - Configure each session with the security-scan skill context and the project's constitution.
 - Limit to 10 concurrent Devin sessions per scan run to avoid resource contention.
 - For each Devin session:
 - Instruct Devin to implement the fix per the SDD specification.
 - Instruct Devin to make the TDD tests pass.
 - Instruct Devin to run the local linter and formatter.
 - Instruct Devin to create a feature branch named `security/{finding-id}-{short-description}` or `security/{security-control}-{short-description}`.
 - Instruct Devin to commit with conventional commit format: `fix(security): remediate {finding-id} - {short-description}`.
 - Monitor all sessions for completion, collecting artifacts and test results.

9. **Invoke Devin Review on remediation PRs**
 - For each remediation PR created by Devin sessions:
 - Submit the PR to Devin Review via the devin-review-mcp.
 - Configure Devin Review with the enterprise Enterprise Security review ruleset:
 - security benchmark compliance rules mapped to the specific V-IDs being remediated.
 - validation rules for the applicable control families.
 - OWASP Top 10 detection rules.
 - CWE Top 25 detection rules.
 - Secret detection (TruffleHog/GitLeaks patterns).
 - Review must confirm that:
 - The fix addresses the original finding.
 - The fix does not introduce new security issues.
 - The fix follows the project's coding standards.
 - All tests pass and coverage thresholds are met.
 - Address any Devin Review findings before proceeding.
 - If Devin Review identifies new findings, loop back to step 6 for those findings.

10. **Execute guardrails audit and produce compliance report**
 - Run the full DevinClaw guardrails checklist against all remediation changes:
 - HG-001 (Tests Pass): All unit, integration, and security tests execute and pass.
 - HG-002 (CIS Benchmark Scan Clean): Re-run the security benchmark scanner to confirm zero High findings on remediated code.
 - HG-003 (Lint/Format Pass): Linter and formatter report zero errors.
 - HG-004 (Coverage Threshold): Code coverage >= 80% for new/modified code.
 - HG-005 (No Secrets): Secret scanner reports zero findings.
 - HG-006 (Dependency Scan): No Critical/High CVEs in dependencies.
 - HG-007 (Signed Commits): All commits are GPG-signed.
 - HG-008 (Audit Trail Complete): Session audit log contains all required events.
 - HG-010 (Security Controls Met): All applicable validated.
 - Generate the compliance report containing:
 - Executive summary with overall compliance posture (pass/fail/partial).
 - Scan results summary: total findings by severity, findings remediated, findings remaining.
 - security benchmark compliance matrix: each V-ID with pass/fail status and evidence.
 - assessment: each control with implementation status and evidence.
 - cloud security compliance readiness assessment: baseline coverage percentage and gaps.
 - Zero Trust maturity assessment: current posture and recommendations.
 - remediation plan entries for any findings not remediated in this scan cycle.
 - Delta comparison with previous scan (if baseline existed).
 - Store the report in the repository under `docs/governance/` with the naming convention `{app-name}-security-scan-{YYYY-MM-DD}.md`.
 - Attach compliance report scan results, test results (JUnit XML), and coverage reports as artifacts.
 - Update DeepWiki with scan findings and remediation learnings for future sessions.

## Specifications
- **CIS Benchmark benchmark version**: Use the latest available industry security CIS Benchmark benchmark for each technology in the stack. If the exact technology CIS Benchmark is not available, apply the Application Security and Development CIS Benchmark (SEC-XXX series) as the general baseline.
- **SOC 2 / ISO 27001 revision**: Use SOC 2 / ISO 27001 Rev. 5 (September 2020) control catalog. Map all controls to the applicable baseline per industry encryption standards 199 categorization.
- **cloud security compliance baselines**: Use the current cloud security compliance Security Controls Baseline documents (Rev. 5). Apply cloud security compliance-specific parameter values where they differ from baseline defaults.
- **Scan output format**: CIS Benchmark scan results must be produced in standard compliance format security control assessments must be produced in machine-readable JSON format where possible.
- **Severity classification**: Use industry security severity categories: Critical severity (Critical/High -- exploitable vulnerability that directly leads to unauthorized access), High severity (Medium -- vulnerability that could lead to unauthorized access with additional information), Medium severity (Low -- vulnerability that degrades security posture).
- **Remediation SLA**: Critical severity findings must be remediated within 30 days. High severity findings within 90 days. Medium severity findings within 180 days. These align with industry security CIS Benchmark timelines and enterprise security officer expectations.
- **Coverage for security tests**: Security test coverage must be 100% for code paths implementing security controls (authentication, authorization, encryption, input validation). Overall coverage threshold remains 80%.
- **DO-178C applicability**: For safety-critical systems (DAL A through DAL C), structural coverage analysis (MC/DC for DAL A, decision coverage for DAL B, statement coverage for DAL C) must be performed on security-relevant code.
- **Sensitivity**: All scan reports must be marked CONFIDENTIAL — INTERNAL USE ONLY unless otherwise directed. Scan results may contain Sensitive Security Information and must be handled per organizational security policy.
- **Retention**: Scan results and compliance artifacts must be retained for the duration of the compliance certification plus 3 years per organizational data retention policy and SOC 2 / ISO 27001 AU-11.
- **Concurrency**: Maximum 10 concurrent Devin remediation sessions per scan run. Maximum 5 concurrent SonarQube scans to avoid overloading the analysis server.

## Advice
- Always run the scan against the full codebase on the first pass, even if the user requests a targeted scan. The initial full scan establishes the baseline. Subsequent scans can be targeted.
- security findings often cluster. If you find one SQL injection vulnerability, assume there are more throughout the codebase and scan all database access patterns, not just the one file where the finding occurred.
- enterprise systems frequently use hardware tokens (Common Access Card / Personal Identity Verification) for authentication. When scanning IA controls, check for CAC middleware integration (e.g., mod_ssl with client certificate authentication, PKCS#11 configurations).
- Many legacy enterprise applications were built before current CIS Benchmark baselines existed. Expect a high volume of findings on initial scan. Prioritize Critical severity findings and create a realistic remediation plan for High severity and Medium severity.
- SonarQube quality profiles should be configured before scanning. The default profiles miss many enterprise-specific rules. Ensure the enterprise Enterprise Security ruleset is active.
- When scanning Java applications, pay special attention to deserialization vulnerabilities (CWE-502). Many enterprise applications use older versions of Apache Commons, Jackson, or XStream that are vulnerable.
- When scanning COBOL-to-Java converted code, check that packed decimal handling does not introduce arithmetic overflow vulnerabilities. COBOL's fixed-point arithmetic has different overflow behavior than Java's BigDecimal.
- Zero Trust validation is particularly important for enterprise applications that span multiple security enclaves (e.g., enterprise operational systems connecting to administrative systems). Network segmentation alone is insufficient.
- For safety-critical systems under DO-178C, coordinate with the Designated Engineering Representative (DER) before auto-remediating findings. Safety-critical code changes require additional verification beyond standard security benchmark compliance.
- The cloud security compliance PMO periodically updates baseline requirements. Check for baseline revisions before submitting compliance certification packages. A scan against an outdated baseline will be rejected.

## Forbidden Actions
- Do not skip the CIS Benchmark scan step. Every codebase scan must include CIS Benchmark benchmark validation regardless of the user's requested scope. security benchmark compliance is a hard gate in the DevinClaw guardrails (HG-002).
- Do not auto-remediate findings in safety-critical systems (DO-178C DAL A through DAL C) without explicit user approval. Safety-critical code changes require human-in-the-loop verification and DER sign-off.
- Do not suppress or downgrade the severity of security findings. Severity classifications are set by industry security and cannot be altered. If a finding is believed to be a false positive, document it as such with evidence but do not change its severity.
- Do not store scan results containing vulnerability details in publicly accessible locations. Scan results must be stored in access-controlled directories and marked with appropriate handling caveats.
- Do not scan production systems directly. Scans must be performed against code repositories or staging environments. If runtime scanning is required, coordinate with the enterprise ISSO and obtain explicit authorization.
- Do not generate remediation code that disables security controls, even temporarily. Fixes must maintain or strengthen the security posture at every intermediate step.
- Do not commit scan results or compliance reports that contain Sensitive Security Information to unprotected Git branches. Use encrypted storage or access-controlled artifact repositories.
- Do not ignore Zero Trust validation findings. Even if all CIS Benchmark and security controls pass, perimeter-only security architectures represent a systemic risk that must be documented and addressed.
- Do not run more than 10 concurrent Devin remediation sessions or 5 concurrent SonarQube scans. Resource contention degrades scan accuracy and session reliability.
- Do not produce a compliance report without completing all prior scan and validation steps. Partial reports create a false sense of compliance and endanger compliance certification renewals.

---
*Generated by DevinClaw Skills Parser at 2026-02-25T06:27:28Z*
*Source: skills/security-scan/SKILL.md*
