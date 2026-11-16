# Contributing

Thank you for taking the time to help. Contributions are welcome.

## Setup

This is the consolidated **offensive-skills** project — one Claude Code project combining the
web-app pentest workflow with 10 OSINT / attack-surface / CTI skill packages. Clone the repo and
open the project directory:

```bash
git clone https://github.com/abdulgaphy/offensive-skills.git
cd offensive-skills
```

Optional tools (Burp MCP, PDF reports) are in the [README](README.md#getting-started). You do not need them to edit skills, payloads, commands, or docs.

## Read This First

This pack is for **authorized** security testing only — the web-app workflow and the OSINT/CTI
skills alike. Please do not contribute changes that make it easier to test systems, or profile
people or organizations, without authorization. The OSINT/CTI skills are passive/discovery by
default; do not weaken the gating on their active steps.

The project is still early. We may get things wrong, miss context, or ask follow-up questions. Smaller, focused PRs are easier for us to understand and review well.

The project is still early. We may get things wrong, miss context, or ask follow-up questions. Smaller, focused PRs are easier for us to understand and review well.

## What Helps Most

Small, focused bug fixes. Broken command paths, stale file names, missing `/scope` preconditions.

Small methodology fixes. Clearer WSTG mapping, tighter detection steps, better context notes.

Docs that make an existing command or skill easier to use.

## What Is Harder For Us To Review

Large PRs.

New vulnerability classes, new slash commands, or workflow changes opened without a conversation first.

Full exploit dumps in public `payloads/`. Those belong in gitignored `local-payloads/`.

Engagement data, credentials, cookies, tokens, or unredacted HTTP evidence.

Changes that weaken `/scope` as a mandatory gate.

If you are unsure whether something fits, open an issue first. We would rather talk it through than have you spend time on a PR that we cannot take.

## Opening A PR

Keep the change focused.

Explain what changed and why you think it belongs here.

Please do not mix unrelated fixes together.

If you add or rename a vuln class, update `commands/hunt.md`, the hunting skill, the payload file, and the coverage lists in `SKILL.md`, `CLAUDE.md`, and `README.md`. Keep the load order: command → agent → skill → payload → engagement state.

If you add or change an **OSINT / attack-surface / CTI skill package** under `skills/<name>/`,
keep it self-contained (its own `SKILL.md`), and update the skill tables in `CLAUDE.md`,
`SKILL.md`, and `README.md` so the three stay in sync. Do not move an OSINT skill's internal
files (e.g. `skills/cti-expert/intel_engine/`, `commands/`, `scripts/`) out of its package, and
preserve each package's upstream author/attribution notices.

Public `payloads/` stay methodology-first. Please do not commit `engagements/`, `local-payloads/`, `.mcp.json`, `.env`, or live secrets.

## Discuss Larger Changes First

If you are thinking about a non-trivial change, open an issue first. That helps us share context early and saves everyone time.

## Questions

If anything here is unclear, open an issue. We will do our best to help.
