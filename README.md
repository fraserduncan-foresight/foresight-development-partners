# Foresight Development Partners

Private source handoff prepared November 8, 2026 for review and migration into Frontrunner.

## Start here

- `skills/development-partners/SKILL.md`: discovery, screening, scoring and handoff workflow.
- `skills/development-partners/references/rubric.json` and `agents.json`: rubric and worker prompts.
- `skills/development-partners/references/shared-master.md`: canonical Supabase storage, lease, checkpoint and recovery protocol.
- `skills/development-partners-setup/SKILL.md`: colleague onboarding.
- `automation/development-partners-nightly/`: scheduled research controller and runbooks.
- `automation/development-partners-outreach/`: durable, idempotent post-research queue. It does not send emails by itself.
- `policies/FORESIGHT-TARGETING.txt`: standing specialty scope; applies over conflicting historical examples/configuration.
- `policies/FORESIGHT-OUTREACH-PLAYBOOK.md`: current saved outreach playbook.

## Shared services

The canonical team master remains Supabase project `svdtzmjpqvdvntlicpvt`, schema `development_partners`, workspace `foresight`. HubSpot portal: `342239911`. Clay workspace: `723119`. Source access does not grant account or database access. Each operator must connect their own approved accounts. Do not initialize another remote master or rerun the schema SQL against the existing master.

## Installation and portability

Copy the skill folders into the receiving machine's skills directory, read the setup skill, resolve that machine's Python/Node/dependency paths, and run `scripts/configure_shared.py` as documented. The example config is not a ready-to-run machine config. Read-only code review requires no credentials.

This is a snapshot of the installed source, not a tested cross-machine deployment. Historical source/runbooks include Fraser-specific absolute paths, expired occurrence windows and prior authorization text. Adjust paths and establish new operator authorization before running. Repository access does not transfer Fraser's confirmation waivers, paid-enrichment permission, outreach authorization or schedules. No workflow or schedule was activated by this handoff.

## Scope and intentional differences

Target ONLY neurology, cardiology, endocrinology, rheumatology, pulmonology, internal medicine and primary care. The live machine config still contained older out-of-scope specialties; the shareable example is normalized to the standing scope. Its post-scoring automation is disabled, Clay approval is required, and expired heartbeat authorization was removed. Original installed scripts and references are retained as source evidence, with SHA-256 hashes in `SOURCE-MANIFEST.json`.

Development-partner research generally targets five or more clinical providers and retains the 10-location/60-provider maximum, with documented uncertainty handling. City clinic discovery is a separate workflow with a three-provider minimum. Read the skill and latest policy before use.

## Data and credentials

This package contains code, prompts, schemas and policies. It excludes live candidate databases, spreadsheets, CRM receipts, run logs, account sessions, webhooks, API keys, lease tokens, node_modules and caches. Access live research through the authorized shared master. The separate city-clinic, recontact and practice-administrator workflows are outside this repository.

## Validation

Snapshot integrity, JSON parsing and syntax of 37 Python files were checked locally. Three physician-identity regression tests passed using Python 3.12 (the system Python 3.9 lacks tomllib; use Python 3.11 or newer). No research, paid enrichment, CRM writes, emails or database migration is required to inspect the source. External integration and full production execution have not been tested from this package.
