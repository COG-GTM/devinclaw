# DevinClaw

**AI-powered modernization for enterprise systems.**

One repo. One setup. Your engineer opens a chat and starts modernizing — 200+ applications, 3,000 databases, full audit trail, regulatory compliance baked in.

---

## What It Does

DevinClaw turns natural language into executed, tested, reviewed, and audited code. You say what needs to happen. The system handles the rest — from specification to deployment — and gets smarter with every task.

```
"Migrate the notification PL/SQL procedures to PostgreSQL"

→ Indexes the codebase (DeepWiki)
→ Generates a specification (SDD)
→ Writes tests first (TDD)
→ Spawns 12 parallel build sessions (Devin)
→ Reviews every PR automatically (Devin Review)
→ Validates the full lifecycle was followed (OpenClaw)
→ Updates the knowledge base (Advanced Devin)
→ Next task starts smarter than the last
```

---

## Quick Start

```bash
git clone https://github.com/COG-GTM/devinclaw.git
cd devinclaw
chmod +x setup.sh
./setup.sh # Installs OpenClaw, loads skills, configures APIs
openclaw # Start modernizing
```

**Prerequisites:** Node.js 20+, Git, Devin API key ([app.devin.ai](https://app.devin.ai))

---

## Architecture

```
 ┌──────────────────────┐
 │ ENGINEER │
 │ (Natural Language) │
 └──────────┬───────────┘
 │
 ┌──────────────▼──────────────┐
 │ OPENCLAW │
 │ (Orchestrator) │
 │ │
 │ • Skill routing │
 │ • Guardrail enforcement │
 │ • SDLC validation │
 │ • Audit trail │
 │ • MCP: Jira, Slack, Teams │
 └──────────────┬──────────────┘
 │
 ┌──────────────▼──────────────┐
 │ DEEPWIKI + ADVANCED DEVIN │
 │ (Brain + Knowledge) │
 │ │
 │ • Codebase intelligence │
 │ • Session analysis │
 │ • Playbook generation │
 │ • Self-improving knowledge │
 └──────────────┬──────────────┘
 │
 ┌────────┬───────────┼──────────┬─────────┐
 ▼ ▼ ▼ ▼ ▼
 ┌─────────┐┌────────┐┌────────┐┌─────────┐┌────────┐
 │ DEVIN ││ DEVIN ││ DEVIN ││ DEVIN ││ DEVIN │
 │ CLOUD ││ CLI ││ API ││ IDE ││ REVIEW │
 │ ││ ││ ││ ││ │
 │ 100+ ││ Local ││ CI/CD ││ cloud security compliance ││ Auto │
 │ parallel││ exec ││ webhooks│ High ││ PR │
 │ sessions││ air-gap││ batch ││ high-security tier-high-security tier ││ review │
 └─────────┘└────────┘└────────┘└─────────┘└────────┘
```

---

## Pre-Loaded Skills

15 skills covering enterprise modernization scenarios. Each skill is a complete workflow: specification → tests → build → review → audit.

| Skill | What It Does |
|-------|-------------|
| `legacy-analysis` | Index and assess a codebase with DeepWiki. Produce modernization roadmap. |
| `plsql-migration` | Migrate Oracle PL/SQL → PostgreSQL. Type mapping, exception handling, batch parallel. |
| `cobol-conversion` | Convert COBOL → Java/Python/TypeScript. Preserve exact business logic. |
| `db-rationalization` | Analyze, deduplicate, and consolidate database portfolios. |
| `security-scan` | CIS Benchmark/cloud security compliance compliance scanning and auto-remediation. |
| `test-generation` | Generate comprehensive test suites for untested legacy code. |
| `feature-dev` | Build new features from requirements using SDD + TDD pipeline. |
| `pr-review` | Automated PR review via Devin Review. Bug catch, auto-fix. |
| `incident-response` | Auto-investigate production alerts, open fix PRs. |
| `parallel-migration` | Spawn 100+ parallel sessions for large-scale batch work. |
| `api-modernization` | SOAP→REST, REST→GraphQL, monolith→microservices. |
| `containerization` | Dockerize legacy apps. Multi-stage builds, K8s manifests, Iron Bank compliance. |
| `sdlc-validator` | Validate every task followed the full SDLC lifecycle. |
| `guardrail-auditor` | Monitor Devin Enterprise Guardrails API for policy violations. |
| `skill-creator` | **Meta-skill**: creates new skills when no match exists. Self-evolving system. |

---

## Every Task Follows the Same Lifecycle

```
1. INTAKE → OpenClaw matches task to skill
2. CONTEXT → DeepWiki provides codebase intelligence
3. SPEC → Spec-Driven Design generates specification
4. TEST → Test-Driven Design writes tests first
5. BUILD → Devin executes (1 to 100+ parallel sessions)
6. REVIEW → Devin Review auto-reviews every PR
7. VALIDATE → OpenClaw checks all hard gates:
 ✅ Spec exists
 ✅ Tests pass
 ✅ Coverage met
 ✅ Review clean
 ✅ Security scan clean
 ✅ Guardrails: 0 violations
8. LEARN → Advanced Devin analyzes session → improves playbooks
```

If a task has no matching skill, the `skill-creator` meta-skill builds one, pushes it to the repo, and the whole team gains the capability.

---

## Verification System

DevinClaw uses a multi-layered verification architecture to ensure every output is defensible, traceable, and predictably escalated when confidence is insufficient.

### Self-Verification Loop
Every skill runs a self-verification loop after completing its primary procedure: verify → auto-fix → re-verify → escalate. This eliminates the "ship and hope" pattern that plagues autonomous AI systems.

### Arena Pattern (Divergence Detection)
For high-risk tasks (security scanning, database rationalization, incident response), DevinClaw runs **multiple independent Devin sessions** with different playbook variants, then compares their outputs using a divergence scoring algorithm. If sessions disagree beyond a configurable threshold (default: 0.35), the system escalates to human review rather than silently choosing one output.

| Risk Level | Default Mode | Example Skills |
|------------|-------------|----------------|
| Critical | Arena (N=3) | security-scan, db-rationalization, incident-response |
| High | Arena (N=2) | legacy-analysis, plsql-migration, cobol-conversion |
| Medium | Single-run | feature-dev, test-generation, containerization |
| Low | Single-run | pr-review, sdlc-validator, guardrail-auditor |

### Evidence Packs
Every completed task produces an `evidence-pack.json` containing artifact hashes, verification gate results, test summaries, scan results, and escalation records. These evidence packs are retained for the contract duration plus 3 years (FAR 4.703) and serve as the foundation for compliance certification evidence packages.

See [docs/VERIFICATION-SYSTEM.md](docs/VERIFICATION-SYSTEM.md) for the complete verification architecture.

---

## Enterprise Compliance

| Framework | Coverage |
|-----------|---------|
| SOC 2 / ISO 27001 Rev 5 | AC, AU, IA, SC, SI control families |
| Zero Trust Architecture | Zero Trust Architecture |
| industry security benchmarks | All 18 security categories |
| SOC 2 Type II | Devin Cloud platform |

Every session produces an immutable audit trail. See [SECURITY.md](SECURITY.md).

---

## MCP Integration

Both OpenClaw and Devin connect to external tools via Model Context Protocol:

**OpenClaw layer** (task intake + validation): Jira, Slack, Teams, GitHub, DeepWiki, PostgreSQL

**Devin layer** (execution): GitHub, Sentry, Datadog, SonarQube, databases

The orchestrator can independently verify what the executor did. See [docs/MCP-GUIDE.md](docs/MCP-GUIDE.md).

---

## Repository Structure

```
devinclaw/
├── README.md # This file
├── SOUL.md # Identity, mission, values
├── GUARDRAILS.md # Hard gates for all operations
├── TOOLS.md # MCP servers and tool registry
├── SECURITY.md # Regulatory compliance posture
├── SKILLS-MAP.md # Skill → enterprise cenario mapping
├── setup.sh # One-command bootstrap
│
├── skills/ # 15 pre-loaded OpenClaw skills
│ ├── legacy-analysis/
│ ├── plsql-migration/
│ ├── cobol-conversion/
│ ├── db-rationalization/
│ ├── security-scan/
│ ├── test-generation/
│ ├── feature-dev/
│ ├── pr-review/
│ ├── incident-response/
│ ├── parallel-migration/
│ ├── api-modernization/
│ ├── containerization/
│ ├── sdlc-validator/
│ ├── guardrail-auditor/
│ └── skill-creator/
│
├── sdd/ # Spec-Driven Design templates + playbooks
├── tdd/ # Test-Driven Design templates + playbooks
├── governance/ # CIS Benchmark, security controls, cloud security compliance, Zero Trust
├── knowledge/ # 6 Devin Knowledge entries (enterprise domain expertise)
├── playbooks/ # 8 Devin playbooks for common tasks
├── deepwiki/ # DeepWiki MCP config + enterprise nowledge base
├── mcp/ # MCP server configurations
├── audit/ # Guardrail config, SDLC checklist, arena config, artifact schemas
├── skills-parser/ # Convert OpenClaw skills → Devin playbooks
└── docs/ # Architecture, SDLC mapping, use cases, FAQ
```

---

## Documentation

| Document | What It Covers |
|----------|---------------|
| [docs/ARCHITECTURE.md](docs/ARCHITECTURE.md) | Full system architecture with data flow diagrams |
| [docs/SDLC-MAPPING.md](docs/SDLC-MAPPING.md) | Where each tool fits in the development lifecycle |
| [docs/USE-CASES.md](docs/USE-CASES.md) | enterprise cenarios mapped to skills and Devin capabilities |
| [docs/QUICK-START.md](docs/QUICK-START.md) | 5-minute setup guide |
| [docs/MCP-GUIDE.md](docs/MCP-GUIDE.md) | How MCP servers connect the layers |
| [docs/SELF-EVOLVING.md](docs/SELF-EVOLVING.md) | How the system gets smarter over time |
| [docs/FAQ.md](docs/FAQ.md) | Common questions and answers |
| [docs/VERIFICATION-SYSTEM.md](docs/VERIFICATION-SYSTEM.md) | Divergence detection, arena pattern, evidence gating |

---

## Objective Assessment

### Strengths
- **Parallelism at scale**: 100+ isolated Devin sessions with consistent tooling, governance, and audit. Each session operates independently with full knowledge base access.
- **Knowledge-as-a-service**: Repository intelligence via DeepWiki MCP and Devin MCP becomes reusable across tools and teams. The orchestrator does not need to understand code — the brain does.
- **Repeatability**: Playbooks and scheduled sessions encode institutional runbooks. Every workflow is reproducible, auditable, and improvable over time.
- **Independent verification**: Devin Review provides a separate analytical lens from session self-verification. The arena pattern runs competing analyses on high-risk tasks. Trust is earned through evidence, not assertion.
- **Governance primitives**: Service users with RBAC, session-scoped secrets, structured audit logs, and deterministic escalation policies. Built for accountability at scale.

### Known Limitations
- **Database migrations**: The highest-risk modernization activity across the industry. DevinClaw excels at schema comprehension, documentation, duplicate detection, and draft migration planning. Production migration execution (cutover, backfill, reconciliation) requires human SMEs and operational constraints that no AI system can fully model today.
- **False confidence risk**: AI systems can present uncertain conclusions with high confidence. DevinClaw mitigates this through divergence detection, evidence gating, and explicit uncertainty scoring — but the risk is not eliminated. The escalation system exists precisely because the AI cannot always know what it doesn't know.
- **Orchestrator hardening**: OpenClaw is single-operator, local-first with plaintext token storage. For enterprise production use, it must be treated as an untrusted orchestration layer or forked and hardened. See [SECURITY.md](SECURITY.md) for the objective assessment.
- **Environment heterogeneity**: enterprise systems span decades of technology choices — COBOL, Oracle, Java EE, mainframe batch, TIBCO messaging, proprietary frameworks. Expect integration work for each unique environment, internal artifact stores, scanners, and network configurations.

---

## The Compound Effect

```
Session 1: 4 hours (full ramp-up, no context)
Session 10: 2 hours (patterns known, playbooks established)
Session 50: 30 min (deep domain knowledge, near-autonomous)
Session 100: 15 min (human review only)
```

Every task makes the next one faster. After modernizing 200 enterprise applications, the framework encodes the collective knowledge of every migration, every edge case, every lesson learned.

---

*Built by [Cognition AI](https://cognition.ai) • [Devin](https://devin.ai) • [DeepWiki](https://deepwiki.com) • [OpenClaw](https://openclaw.ai)*
