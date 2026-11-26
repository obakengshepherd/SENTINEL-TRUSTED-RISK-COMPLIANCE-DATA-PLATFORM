# AI Handoff — Sentinel

**Last updated:** 2026-11-26  
**Maintainer:** ChatGPT (Primary AI)  
**Repository:** [SENTINEL-TRUSTED-RISK-COMPLIANCE-DATA-PLATFORM](https://github.com/obakengshepherd/SENTINEL-TRUSTED-RISK-COMPLIANCE-DATA-PLATFORM)  
**Default branch:** `main`

## 1. Current project status

**Overall:** Foundation documentation accepted; Phase 1 design review pending.  
**Current phase:** Phase 1 — Database and Domain Foundation.  
**Phase status:** NOT STARTED for schema implementation; design/review work is the next activity.  
**Next milestone:** Complete independent specialist review, reconcile findings, present material design decisions to the Product Owner and obtain approval before schema implementation.

Sentinel is a synthetic enterprise portfolio demonstration. It is not a production banking, fraud, AML or regulatory system. All demonstration data must be synthetic.

## 2. Accepted baseline and decisions

The Product Owner accepted the foundation documentation as the implementation baseline. Preserve it.

| Area | Current position | Authority/status |
|---|---|---|
| Project purpose and phased scope | Full phased scope, delivered incrementally | Approved |
| Architecture | Modular monolith | Approved |
| Database direction | SQL Server 2022 Developer Edition for local development | Approved |
| Conceptual model | Initial proposal in `docs/DATA_MODEL.md` | Not approved as physical schema |
| Application language/runtime | C# / .NET 10 LTS | Proposed; verify environment and compatibility |
| Data access | Dapper / ADO.NET with explicit SQL | Proposed |
| API | ASP.NET Core | Proposed |
| Tests | xUnit | Proposed |
| Data organisation | Logical Bronze / Silver / Gold layers | Foundation direction; physical boundaries require design |
| Initial ingestion formats | CSV and JSON | Foundation baseline |
| Deployment | Local-first | Foundation baseline |
| Historical projects | Conceptual references only; no source code or Git history import | Accepted clean-start rule |

Do not silently promote proposed technology details into approved decisions. Material changes require Product Owner approval.

## 3. Critical domain invariants

These are non-negotiable:
- A **risk indicator** is not an **alert**.
- An **alert** is not proof of wrongdoing.
- An **investigation** is not proof of guilt.
- An **investigation outcome** must have a defensible, identifiable evidential basis.
- Evidence records and outcomes are distinct concepts.
- Invalid data must not silently enter trusted reporting datasets.
- Provenance and lineage must remain explainable.
- Source identity, processing context and material corrections must not be silently discarded.
- Exact duplicates and conflicting records must be distinguishable.

## 4. Latest known repository state

Latest known `main` commit at this handoff update:

`015458ec8d80a67dd903d09a2d82572599cc145b` — `docs(sentinel): establish AI collaboration agreement`

Immediately preceding repository head inspected:

`f26bad46961b78dc3491a2222fb269d3519db12a` — `docs(sentinel): clarify Phase 0 acceptance and Phase 1 design gate`

The repository was inspected before these collaboration documents were added. At that inspection:
- `main` was the only branch returned by branch search.
- No pull requests were found.
- The three latest foundation corrections were present on `main`: `README.md`, `docs/PROJECT_FOUNDATION.md`, `docs/IMPLEMENTATION_PLAN.md`.
- `docs/AI-COLLABORATION.md` and `docs/AI-HANDOFF.md` did not exist.
- The accepted foundation documents and conceptual model were present.
- No application code, schema, migrations, seed data, automated tests or deployment configuration were found in the reviewed project documentation/status.

The collaboration agreement was then created on `main` in commit `015458ec8d80a67dd903d09a2d82572599cc145b`. This handoff file is being added immediately afterwards. Fetch the live branch head before any future assignment; this SHA is the known base before this handoff-file commit.

## 5. Completed work

- Repository foundation established.
- Foundation documentation accepted by Product Owner.
- Modular-monolith and SQL Server 2022 directions retained.
- Phase 0 acceptance and Phase 1 design gate clarified in the latest README, foundation and implementation plan.
- AI collaboration agreement created at `docs/AI-COLLABORATION.md`.
- First Claude specialist review assignment prepared below.
- No schema or application implementation has started.

## 6. Outstanding work

1. Complete Claude's independent review of the conceptual model, database design concerns, governance, provenance/lineage and risk/investigation domain.
2. ChatGPT evaluates and reconciles each finding against the accepted foundation.
3. Present material design choices and unresolved trade-offs to the Product Owner.
4. Obtain explicit approval of the detailed design baseline.
5. Only then prepare and authorise a bounded Phase 1 implementation assignment.
6. Verify local SQL Server and .NET environment before choosing environment-dependent implementation details.

## 7. Pending decisions and approvals

Not yet approved:
- Detailed entity relationships, cardinalities and optionality.
- Physical schema, keys, constraints, indexes and transaction boundaries.
- Source-record identity and idempotency scope.
- Exact duplicate versus conflict semantics and correction/version handling.
- Data-quality issue lifecycle and exception semantics.
- Bronze/Silver/Gold physical representation and promotion rules.
- Record-level lineage granularity and retention.
- Evidence model, outcome versioning, reopening and supersession rules.
- Retention, deletion, audit immutability and access/security boundaries.
- Synthetic seed/reference dataset structure.
- Proposed .NET/data-access/API/test stack choices, subject to environment and compatibility verification.

## 8. Active assignment register

### SEN-REV-001 — Independent Phase 1 domain and data architecture review

| Field | Assignment record |
|---|---|
| Task ID | SEN-REV-001 |
| Assigned AI | Claude — Specialist AI |
| Assignment authority | REVIEW ONLY |
| Status | PREPARED — awaiting Product Owner to submit prompt to Claude |
| Branch | Not applicable; no file modifications authorised |
| Base commit | `015458ec8d80a67dd903d09a2d82572599cc145b` known before this handoff-file commit; Claude must inspect latest `main` when reviewing |
| Files assigned | Read-only: `README.md`; `docs/PROJECT_FOUNDATION.md`; `docs/DOMAIN_GLOSSARY.md`; `docs/DATA_MODEL.md`; `docs/ARCHITECTURE.md`; `docs/DATA_GOVERNANCE.md`; `docs/PROVENANCE_AND_LINEAGE.md`; `docs/IMPLEMENTATION_PLAN.md`; `docs/PROJECT_EVOLUTION.md`; `docs/AI-COLLABORATION.md`; `docs/AI-HANDOFF.md` |
| Files excluded | All files are excluded from modification. No edits, commits, branches or PRs for this review-only task. |
| File ownership | ChatGPT retains repository file-maintenance ownership. Claude receives read-only review access; no modification ownership is transferred. |
| Expected deliverable | Independent, evidence-based review report with findings, severity, affected documents/sections, rationale, recommendations, decision authority and unresolved questions |
| Verification | Check each finding against current repository text; distinguish confirmed defects, design gaps, options and preferences; no implementation tests are expected or authorised |
| Next action | Product Owner provides the assignment prompt below to Claude; then share Claude's complete report in this project conversation |

### Claude assignment prompt — SEN-REV-001

**Role:** You are the Sentinel Specialist AI. This is an independent technical review commissioned by ChatGPT, the Primary AI, for the Product Owner.

**Authority: REVIEW ONLY.** Do not modify any file. Do not create a branch, commit, pull request, schema, migration, seed data, application code or tests. Do not use write operations. Do not implement recommendations. You are being asked to assess the current accepted foundation and identify design risks before the Product Owner approves Phase 1.

**Repository:** https://github.com/obakengshepherd/SENTINEL-TRUSTED-RISK-COMPLIANCE-DATA-PLATFORM

**First steps:**
1. Inspect the latest `main` branch and note its exact commit SHA.
2. Read `docs/AI-COLLABORATION.md` and `docs/AI-HANDOFF.md`.
3. Read the README and all relevant foundation, domain, architecture, governance, provenance/lineage and implementation-plan documents listed in the assignment register.
4. Treat the repository as authoritative. Identify any inconsistency between documents and report it; do not resolve it by editing.
5. Confirm that your work remains review-only.

**Review scope — assess independently and in depth:**

1. Conceptual data model: entity completeness, responsibilities, relationships, cardinalities, optionality, associative entities, lifecycle boundaries and possible over/under-modelling.
2. SQL Server 2022 suitability: relational design fit, datatype considerations, constraints, transaction/concurrency implications, indexing considerations and SQL Server-specific risks. Do not assume the physical schema has been approved.
3. Keys and integrity: primary/foreign keys, candidate/natural keys, uniqueness scopes, referential integrity, check constraints, nullable relationships and historical references.
4. Source identity and ingestion: source registration, source record identity, batch-to-record relationships, re-delivery, idempotency, partial failures and replay.
5. Duplicate versus conflict semantics: repeated delivery of the same source record, same source identity with changed content, distinct source records representing the same business event, and merely similar records. Assess hash limitations and correction/version strategies.
6. Data quality: validation rule versioning, execution/result model, record/dataset-level issues, issue ownership and lifecycle, accepted exceptions, rejected records, reprocessing and prevention of invalid data silently entering trusted reporting.
7. Bronze / Silver / Gold: conceptual boundaries, promotion criteria, rejected/quarantined data treatment, traceability between layers and whether the design risks turning logical layers into unnecessary infrastructure.
8. Governance and metadata: asset ownership, business definitions, classification, access controls, retention categories, metadata lifecycle and accountability.
9. Provenance and lineage: source/file/batch/run context, dataset lineage, record-level traceability, transformation identity/version, hashes, timestamps/time zones and the ability to reconstruct processing.
10. Audit and corrections: attributable events, state-transition history, append-only versus mutable data, correction/deletion behaviour, historical reproducibility and audit tamper-resistance proportional to a local synthetic portfolio.
11. Risk indicators and alerts: distinct entities and lifecycles, rule-trigger context, indicator-to-alert cardinality, repeated alerts, alert dismissal/review and authorised non-rule alerts.
12. Alerts and investigations: zero-to-many and many-to-many relationships, authorised referrals that do not originate from alerts, investigation opening/closure/reopening and status history.
13. Investigations, evidence and outcomes: evidence provenance and integrity, evidence-to-investigation cardinality, evidence updates, outcome evidential basis, outcome versioning, supersession, reopening and historical decision preservation.
14. Retention and security: synthetic-data boundaries, least privilege, secrets, logging, payload minimisation, retention/deletion implications and access to evidence/audit records.
15. Synthetic reference and seed data: minimum coherent entities and relationships, useful edge cases, repeatability, deterministic identifiers and scenarios needed to prove constraints and lifecycle semantics.

**Critical domain rules — treat as mandatory:**
- A risk indicator is not an alert.
- An alert is not proof of wrongdoing.
- An investigation is not proof of guilt.
- An investigation outcome must have a defensible evidential basis.
- Evidence and outcome are different concepts.
- Invalid data must not silently enter trusted reporting datasets.
- Provenance and lineage must remain explainable.

Do not collapse these concepts into generic risk or case records unless you can demonstrate that the proposed model preserves their separate meanings, histories and integrity requirements.

**Review method:**
- Separate confirmed defects/contradictions from omissions, design risks, options and stylistic preferences.
- For each finding, cite the exact document and section (or quote a short identifying phrase).
- Explain why it matters and provide a practical recommendation.
- State whether the recommendation is routine engineering detail or requires Product Owner approval.
- Do not assume proposed technologies or conceptual entities are approved physical design decisions.
- Prefer a proportionate modular-monolith / SQL Server design; do not recommend microservices, brokers, cloud infrastructure or AI scoring without a demonstrated requirement.
- Do not invent legal/regulatory obligations or retention periods. Flag where legal or institutional policy would be needed in a real deployment.
- Do not claim tests or environment verification were performed unless you actually performed them.

**Required report structure:**
1. Executive assessment: overall readiness for Phase 1 physical design (not implementation).
2. Repository baseline reviewed: branch, commit SHA and documents reviewed.
3. Findings table: ID, severity (Critical / High / Medium / Low / Observation), topic, affected document/section, finding, consequence, recommendation, approval authority.
4. Domain relationship review: clear narrative or text-based relationship/cardinality model, explicitly preserving the four domain concepts.
5. Data integrity and ingestion review: identity, idempotency, duplicate/conflict/correction handling.
6. Governance, provenance, lineage, audit and security review.
7. SQL Server 2022-specific design considerations.
8. Synthetic reference/seed-data scenarios needed for credible verification.
9. Recommended design decisions: separate those you consider safe engineering defaults from those requiring Product Owner approval.
10. Open questions for the Product Owner.
11. Explicit conclusion: what must be resolved before physical schema design, what can be settled during detailed design, and confirmation that no files were modified.

**Stop condition:** Deliver the review report only. Wait for ChatGPT to reconcile the findings and for the Product Owner to approve material design decisions. Do not proceed to schema or application implementation.

## 9. Review findings and disposition

No Claude review findings received yet. This section will record each finding and whether it is accepted, modified, deferred or rejected, with rationale and Product Owner decision where required.

## 10. File ownership register

| File(s) | Current owner | Access / status |
|---|---|---|
| `docs/AI-HANDOFF.md` | ChatGPT | Maintainer; routine handoff updates |
| `docs/AI-COLLABORATION.md` | ChatGPT | Maintainer; permanent agreement |
| All other project files | No active modification assignment | Existing repository baseline |
| Review scope for SEN-REV-001 | Claude | Read-only; no file ownership for edits |

No simultaneous editing is authorised. Any subsequent Claude implementation/documentation task must receive its own task ID, fresh base commit, dedicated `claude/<work-item-slug>` branch, explicit file list and PR requirements.

## 11. Next authorised action

**Awaiting:** Product Owner submits the SEN-REV-001 review-only prompt to Claude and returns Claude's complete findings to this conversation.

**Not authorised:** Database schema creation, migrations, seed data, application code, tests or other substantial implementation.

After receiving the report, ChatGPT will reconcile findings against the current repository, prepare a decision-focused design proposal and seek Product Owner approval for material Phase 1 design choices.