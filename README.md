# Foresight Development Partners

We identify physicians at independent US practices who could help shape Foresight’s clinical AI products. This page describes the overnight workflow as of November 10, 2026. The repository also contains the November 8 source handoff for review and migration.

## Current overnight workflow

1. **Intake.** Start from a HubSpot company segment. Use the official practice website and NPI registry to verify the organization, ownership, specialty, roster, and physician identity. The overnight workflow targets five or more clinical providers. A complete roster below five is excluded. An uncertain count can proceed with the uncertainty recorded. City clinic discovery has a separate three-provider minimum.
2. **Select and score one physician per clinic.** Prefer the organizational NPI’s authorized official when that person is a physician with a verified match. Otherwise use the first physician on the official clinic website and verify current affiliation. A verified score of 70 or higher earns the Development Partner label and the forward-facing route. Other eligible physicians can go through a bounded check for a current operational signal, such as an administrative hire, and receive needs-based or generic outreach.
3. **Enrich and update HubSpot.** Reuse a verified work email where available and use Clay for missing addresses. Match the physician and practice before writing the HubSpot contact and association. Record the actual result and verify the write. The current overnight contact workflow processes physicians.
4. **Enroll in Instantly.** Render the appropriate versioned template from the approved Google Doc using saved research. Check current suppression, duplicates, sender health and capacity, and the clinic’s local send window. Verify the lead in Instantly and track enrollment, campaign activation, and actual sends as separate milestones.

The specialty scope is neurology, cardiology, endocrinology, rheumatology, pulmonology, internal medicine, and primary care.

## How the worker runs

A standalone supervisor on Fraser’s Mac runs the worker and restarts it on interruption. An authenticated connector gateway handles external calls. Supabase/Postgres holds company and contact records, research evidence, task state, and claims. The controller admits up to three clinics for research and overlaps research with downstream work while the queues are healthy. The worker records request IDs and provider receipts so it can resume after an interruption. If a paid lookup or external write has an unknown outcome, the worker holds that item for reconciliation before any replay. Independent clinics can keep moving.

## Where throughput drops

| Stage | What we observed |
| --- | --- |
| Practice and physician verification | The November 10 test covered 30 clinics. It recorded 24 completed intakes, 17 routed clinics, and 7 verified lead enrollments in draft campaigns. Some attrition is expected from eligibility. The run totals alone cannot separate that from incomplete evidence, worker errors, and queue delays. |
| Email coverage | A separate 180-clinic collection run yielded 53 accepted work emails and 32 completed no-email outcomes. The accepted count measures address coverage. Delivery was outside that run’s scope. |
| External calls and recovery | One rejected contact receipt stalled unrelated admission. The November 10 repair isolated the affected journal and demonstrated three independent research admissions while the case was still open. Lost responses still require reconciliation. |
| Copy refresh and campaign activation | Full Google Doc reads repeatedly timed out. The worker now requests body and tab fields. In one November 10 recovery, Instantly required browser activation. Enrollment and activation can both succeed before the first send. |

## Engineering review

Start by tracing one clinic from intake through a verified send. Measure queue wait, active processing, connector latency, and retries by stage. Give every terminal outcome a reason, including eligibility exclusion, unresolved evidence, missing email, duplicate, failed connector call, and campaign hold. This will show whether research capacity, enrichment coverage, or the integration handoffs are worth improving first. A representative cohort and per-stage timing are still needed to quantify the largest time bottleneck.

## Source handoff

[Download the November 8 source snapshot](./foresight-development-partners-source.zip) and see its [source manifest](./SOURCE-MANIFEST.json). The archive documents the earlier research runner and outreach queue. The current standalone worker, live Instantly enrollment path, and November 9–10 changes are described above and are outside this archive. Its sample configuration requires Clay approval and disables post-scoring automation. The earlier discovery skill also has upper size limits of 10 locations and 60 clinicians. The current HubSpot-segment overnight policy has no upper size cap.

Start inside the archive with the following files.

- `skills/development-partners/SKILL.md` and its rubric and worker prompts for discovery and scoring.
- `skills/development-partners/references/shared-master.md` for the earlier Supabase storage and recovery protocol.
- `automation/development-partners-nightly/` and `automation/development-partners-outreach/` for the earlier controller and durable handoff queue.
- `skills/development-partners-setup/SKILL.md` for onboarding and `policies/` for the policies as archived.

Source review needs no service credentials. Running the archive on another machine would require local configuration and approved service connections. Snapshot validation covered integrity, JSON parsing, Python syntax, and three physician-identity regression tests. Cross-machine deployment and external integrations were outside that validation. The archive excludes live candidate data, run receipts, and credentials. City discovery, recontact, and practice-administrator workflows are separate.
