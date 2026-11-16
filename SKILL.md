---
name: offensive-skills
description: Authorized offensive security toolkit — a structured OWASP web-app penetration-testing workflow (scope-gated commands, curated payloads, 6-gate validation, report generation) bundled with 10 OSINT / attack-surface / threat-intel skill packages (external recon, org-footprint mapping, cloud/identity/email exposure, CTI, continuous monitoring, FAIR risk scoring).
---

# Offensive Skills

A single project with two halves for **authorized** offensive security:

1. **Web-app penetration-testing workflow** — structured methodology, curated payload references,
   and strict validation for authorized web application testing (this file's main focus).
2. **10 OSINT / attack-surface / CTI skill packages** — external reconnaissance, organization
   footprint mapping, cloud/identity/email exposure analysis, threat intelligence, continuous
   monitoring, and risk quantification (see *OSINT / Attack-Surface / CTI Skills* below).

The master contract is `CLAUDE.md`; full documentation is in `README.md`.

## When to use

**Web-app workflow** — use when performing authorized web application penetration testing. It provides:
- A structured engagement workflow: scope definition, reconnaissance, vulnerability hunting, finding validation, and report generation
- OWASP Web Security Testing Guide (WSTG) methodology with coverage tracking
- 18 vulnerability class references with PayloadAllTheThings links
- A 6-gate validation process that eliminates false positives
- Professional pentest report generation (markdown + PDF)

**OSINT / attack-surface / CTI** — use the matching skill package (below) when mapping an
organization's external footprint, enumerating assets, analyzing cloud/identity/email exposure,
running a CTI investigation, standing up continuous monitoring, or quantifying risk.

**Only use against systems you own or have explicit written authorization to test.**

## Instructions

### Standard Workflow

```
/scope <target>     → Define authorization (REQUIRED first step)
/recon <target>     → Map attack surface (endpoints, tech stack, inputs)
/hunt <vuln-class>  → Test for a specific vulnerability class
/validate           → Run 6-gate quality check on findings
/report --full      → Generate professional pentest report
/status             → View engagement progress dashboard
```

### Safety Rules (Non-Negotiable)

1. **Never** test without running `/scope` first
2. **Never** send requests to out-of-scope domains or paths
3. **Always** log every payload attempt before analyzing the response
4. **Stop and ask** the user if uncertain whether an action is in scope
5. **Warn and get confirmation** before testing destructive payloads (DELETE, data modification)
6. **Never** send attack payloads to third-party services (Auth0, AWS, etc.) — only test the client's own infrastructure

### Hunt Targets

Valid arguments for `/hunt`:

| Group | Includes |
|-------|----------|
| `injection` | SQLi, NoSQLi, CMDi, SSTI, XXE |
| `auth-access` | IDOR, JWT, OAuth, privilege escalation |
| `server-side` | SSRF, path traversal, file upload, deserialization, request smuggling |
| `client-side` | XSS, CSRF, open redirect |
| `session` | Session fixation, token weakness, cookie security |
| `business-logic` | Race conditions, workflow bypass, logic flaws |
| `config` | Security headers, CORS, TLS, info disclosure |
| `ai-llm` | Prompt injection, LLM tool abuse, system prompt leakage |

Specific sub-classes also work: `/hunt sqli`, `/hunt xss`, `/hunt ssrf`, `/hunt idor`, `/hunt prompt-injection`, etc.

### Agent Personas

Three specialized personas are activated by commands:

- **Recon Agent** (`/recon`) — Systematic mapper. Passive-first, methodical, records everything.
- **Hunter Agent** (`/hunt`) — Creative attacker. Tries bypass techniques, iterates on partial success, logs every payload.
- **Validator Agent** (`/validate`) — Skeptical critic. Assumes false positive until proven otherwise. Runs the 6-gate quality check.

When no command is active, behave as a general security consultant.

### 6-Gate Validation

Every finding must pass all 6 gates to be included in reports:

1. **Reproducible PoC** — Complete HTTP request that triggers the vulnerability
2. **HTTP Evidence** — Both request AND response captured
3. **Impact Verified** — Concrete and demonstrated, not theoretical
4. **In-Scope** — Endpoint is within authorized scope
5. **Real Vulnerability** — Not informational or best-practice observation
6. **Client Reproducible** — A third party can follow the documented steps

### Engagement State

All engagement data is stored in `engagements/<target>/`:

- `scope.md` — Authorization and scope boundaries
- `findings.md` — Finding table with detailed evidence
- `payload-log.md` — Append-only payload testing history
- `coverage.md` — OWASP WSTG test coverage tracker
- `tech-stack.md` — Discovered technologies
- `notes.md` — Observations and hypotheses

### Tool Integration

- **Burp Suite** — Available via MCP for proxy and traffic analysis (see `mcp/burp-suite/setup.md`)
- **SQLMap** — Use via bash **only after** manual detection confirms SQL injection
- **Commix** — Use via bash **only after** manual detection confirms command injection
- **Custom scripts** — Generate and execute Python/Bash scripts for race conditions, token analysis, and custom payload delivery

### File Loading

When a slash command is invoked, load files in this order:
1. `commands/<command>.md` — Command orchestration
2. `agents/<agent>.md` — Agent persona (if command activates one)
3. `skills/<skill>.md` — Web-app methodology (`recon.md`, `validate.md`, `report.md`, `hunting/<class>.md`)
4. `payloads/<payload>.md` — Payload reference (if hunting)
5. `engagements/<target>/<state-files>` — Current engagement state

For an **OSINT / attack-surface / CTI task**, load the matching package instead:
`skills/<skill-name>/SKILL.md` (see below).

Load on demand, not all at startup.

## OSINT / Attack-Surface / CTI Skills

Alongside the web-app workflow, `skills/` holds **10 self-contained OSINT / recon / threat-intel
skill packages**. Each is a folder with its own `SKILL.md` (plus `scripts/`, `workflows/`,
`README.md`). When a task matches one, **load `skills/<skill-name>/SKILL.md` and follow it** — on
demand, never all at startup. All are **passive / discovery-oriented** unless a stage inside them
is explicitly marked active; every active step stays bound by the Safety Rules above.

| Skill | Load | Use for |
|-------|------|---------|
| **osint-methodology** | `skills/osint-methodology/SKILL.md` | The 6-stage external recon pipeline + severity rubric + deliverable templates |
| **osint-autopilot** | `skills/osint-autopilot/SKILL.md` | Running the full methodology end-to-end for an authorized domain |
| **offensive-osint** | `skills/offensive-osint/SKILL.md` | The arsenal — wordlists, 80-pattern secret-regex catalog, dork corpus, probes, APK pipeline |
| **org-attack-surface** | `skills/org-attack-surface/SKILL.md` | Legal entity → owned domains → netblocks/ASN → live assets, with attribution discipline |
| **cloud-saas-exposure** | `skills/cloud-saas-exposure/SKILL.md` | Buckets, offline AWS account-ID recovery, dependency confusion, K8s/CI fingerprint |
| **identity-provider-recon** | `skills/identity-provider-recon/SKILL.md` | Tenant/federation fingerprint + user-enumeration oracles (enumeration only) |
| **email-domain-security** | `skills/email-domain-security/SKILL.md` | Email spoofability verdict + SPF supply-chain analysis from DNS alone |
| **cti-expert** | `skills/cti-expert/SKILL.md` | CTI/OSINT investigations (any indicator). **Runnable** — ships `intel_engine` + `/cti*` commands |
| **continuous-exposure-monitoring** | `skills/continuous-exposure-monitoring/SKILL.md` | Scheduled re-scan + diff + CTI-chatter alerting + finding lifecycle |
| **exposure-risk-quantification** | `skills/exposure-risk-quantification/SKILL.md` | FAIR 0–100 / A–F score + $-loss estimate + board one-pager |

**cti-expert** additionally exposes its own slash commands (in `skills/cti-expert/commands/`),
separate from the web-app commands: `/cti`, `/cti-recall`, `/cti-check`, `/cti-case`,
`/cti-cluster`, `/cti-pivot`, `/cti-report`, `/cti-status`, `/cti-proxy`. Its outbound actions
(`engage_account`, `anyrun_submit`, `harvest_authenticated`, any `--submit`) are hook-gated and
prompt before running. Load `skills/cti-expert/SKILL.md` first for routing.
