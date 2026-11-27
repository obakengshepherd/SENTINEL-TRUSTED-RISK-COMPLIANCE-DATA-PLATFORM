# AI Handoff — Sentinel (FNEOS)

**Last updated:** 2026-11-27  
**Maintainer:** ChatGPT (Primary AI)  
**Product Owner:** User  
**Repository:** [SENTINEL-TRUSTED-RISK-COMPLIANCE-DATA-PLATFORM](https://github.com/obakengshepherd/SENTINEL-TRUSTED-RISK-COMPLIANCE-DATA-PLATFORM)  
**Branch:** `main`

## 1. Current project status

**Historical baseline:** 25 November 2026 — `82cb85867e3698b074714d076fb8e49fd4012cb4`.  
**Current verified main before this documentation update:** `205d01e81d5927db45e156fd51d7fb2a5d945f65`.  
**Current phase:** Phase 1 — Database and Domain Design / Foundation.  
**Design baseline:** SEN-DESIGN-001 APPROVED by Product Owner on 27 November 2026, no amendments.  
**First implementation increment:** SEN-DB-001 — SQL Server Ingestion Foundation.  
**SEN-DB-001 authorisation:** APPROVED 27 November 2026.  
**SEN-DB-001 implementation:** NOT STARTED; Claude has not yet received/returned the assignment in this workflow.  
**SEN-DB-001 verification/acceptance:** NOT VERIFIED / NOT ACCEPTED.  
**Application implementation:** None evidenced at the time of this handoff.

This is a governance/workflow correction and engineering activation, not a project restart. Preserve valid requirements, architecture, decisions and Git history. Sentinel remains a synthetic enterprise portfolio demonstration, not a production banking, fraud, AML or regulatory system. Synthetic data only.

## 2. Repository and authority

The repository is the shared authoritative project record. Product Owner has final authority. Active FNEOS responsibilities are in `docs/AI-COLLABORATION.md` and the 27 November Product Owner directive.

- ChatGPT owns architecture, requirements, specifications, all documentation, implementation planning, Claude handoffs, change control, main-branch governance, integration review and living handoff.
- Claude reviews the assigned Primary AI design once and implements only exact assigned code files. Claude returns complete files in chat and does not write to GitHub or edit documentation.
- Product Owner assembles files locally, runs commands/tests and supplies actual evidence. ChatGPT reviews and integrates approved work into `main`.

No branches unless Product Owner authorises a named exception. No force-push, history rewrite or deletion of historical commits. One active modification owner per file.

## 3. Approved project direction

| Area | Current position | Status |
|---|---|---|
| Architecture | Modular monolith | APPROVED |
| Database | SQL Server 2022 Developer Edition, local development | APPROVED |
| Scope | Full phased scope, incremental delivery | APPROVED |
| Input formats | CSV and JSON | Foundation requirement |
| Data organisation | Bronze / Silver / Gold logical layers | Foundation direction |
| Data | Synthetic only | MANDATORY |
| Domain | Risk indicator, alert, investigation and outcome are distinct | MANDATORY |
| SEN-DESIGN-001 | Detailed domain and initial SQL Server design | APPROVED |
| SEN-DB-001 | SQL Server Ingestion Foundation | AUTHORISED; NOT STARTED |
| C#/.NET, Dapper/ADO.NET, ASP.NET Core, xUnit | Proposed choices | NOT APPROVED / NOT REQUIRED for SEN-DB-001 |

See `docs/DECISIONS.md` and `docs/PHASE-1-DATABASE-DOMAIN-DESIGN.md`.

## 4. Approved domain and data integrity invariants

- Source record identity is scoped to a DataSource; content hash is not business identity.
- Every delivery is a distinct traceable receipt.
- Same source identity + same SHA-256 content hash is an exact repeat; same identity + different hash is changed content. Both deliveries remain preserved.
- Raw payload bytes are retained independently from later standardised data.
- Processing runs are identifiable and historical; retry does not erase a prior run.
- RiskIndicator, Alert, Investigation, EvidenceRecord and InvestigationOutcome are distinct.
- Alerts are not proof of wrongdoing; investigations are not proof of guilt.
- Every outcome requires at least one identifiable evidence association; a foreign key to Investigation alone is insufficient.
- UTC is the storage convention for system timestamps; source event time is distinct.
- Monetary values, if introduced, use explicit decimal precision and currency code.
- Invalid data must not silently enter trusted reporting outputs.
- No cascading deletes through preserved source receipt/payload history.

## 5. SEN-DB-001 — active assignment

**Task:** SEN-DB-001  
**Phase:** Phase 1 — Database and Domain Design / Foundation  
**Increment:** Initial SQL Server Ingestion Foundation  
**Assignment base main SHA:** `205d01e81d5927db45e156fd51d7fb2a5d945f65` (verified immediately before assignment documentation was prepared; re-check main if repository has advanced after this handoff commit).  
**Design authority:** SEN-DESIGN-001, Product Owner-approved 27 November 2026.  
**Review mode:** One independent review of the approved design and this assignment. If no blocking issue exists, Claude proceeds with implementation under this same handoff. No separate review-only loop.

### 5.1 Objective

Create the initial SQL Server source/ingestion/raw-payload foundation for Sentinel. This is a SQL-only database increment, not application implementation.

### 5.2 Exact Claude-owned code files

Claude may create only these three files:

1. `database/001-create-schemas.sql`
2. `database/002-create-ingestion-foundation.sql`
3. `database/tests/001-verify-ingestion-foundation.sql`

No other file ownership is transferred.

### 5.3 Approved objects

Create schemas: `ref`, `ingest`, `bronze`, `ops`.

Create tables:
- `ref.DataSource`
- `ops.PipelineRun`
- `ingest.IngestionBatch`
- `ingest.SourceRecordIdentity`
- `ingest.RecordReceipt`
- `bronze.RawRecord`

Use the detailed entity responsibilities, minimum columns, relationships, SQL Server types, constraints and indexing guidance in `docs/PHASE-1-DATABASE-DOMAIN-DESIGN.md`. SQL Server 2022-compatible T-SQL. Use `datetime2(7)` for UTC instants, SHA-256 as exactly 32 bytes, and `varbinary(max)` to preserve exact payload bytes. Source identity unique on (DataSourceId, SourceRecordKey). Repeated receipts must be allowed; do not create a unique constraint on source identity + hash. RawRecord must be one-to-one with RecordReceipt.

### 5.4 Required behaviour and acceptance criteria

1. Setup creates all four schemas and six tables with the approved relationships.
2. Primary/foreign keys, unique constraints and check constraints enforce the model.
3. A source identity is unique within its source, not globally.
4. Multiple deliveries for one source identity are retained independently.
5. Same identity/same hash and same identity/different hash both can be recorded as distinct receipts without overwriting history.
6. Hash is stored as 32 bytes; verification checks it against exact preserved payload bytes.
7. Every receipt is linked to one batch and one source identity; every raw payload is linked one-to-one to a receipt.
8. UTC timestamp and valid run start/completion ordering checks are present.
9. Deletes cannot cascade through preserved receipt/payload history.
10. Verification uses synthetic data and a rollback-safe transaction; pass/fail output is clear.
11. Setup has a clear database context, SQL Server version and permissions prerequisite; it must be repeatable or fail safely and must not drop existing user data.
12. Return includes actual commands run/results; unrun checks are explicitly identified.
13. Receipt/payload atomicity is demonstrated or clearly identified as a later application-service transaction boundary; do not claim database-level atomicity if it is not enforced.

### 5.5 Required test scenarios

- Valid source, batch, pipeline run, source identity, receipt and raw payload.
- Unknown-source batch rejected.
- Unknown batch or unknown source identity receipt rejected.
- Duplicate SourceCode rejected.
- Duplicate (DataSourceId, SourceRecordKey) rejected.
- Same source identity with same hash can be received more than once.
- Same source identity with changed hash can be recorded as a separate receipt.
- Exact payload bytes and their SHA-256 hash remain queryable and match.
- Invalid hash length and invalid status rejected.
- Invalid timestamp ordering rejected.
- Receipt/payload relationship and delete restrictions behave as specified.
- All fixture data rolled back; no persistent sample rows left behind.

### 5.6 Dependencies and environment assumptions

- Target is SQL Server 2022 Developer Edition.
- Local SQL Server installation, actual version, connectivity and permissions have NOT yet been verified by the Product Owner in this project conversation.
- SQL scripts must be SQL Server 2022-compatible and must clearly state how to select/create the target database and required permissions.
- No .NET SDK, API, Dapper, xUnit, container or cloud dependency is needed for this SQL-only increment.
- Use synthetic values only. No FNB, customer, real-person or confidential data.

### 5.7 Explicit exclusions

Do not create or modify:
- Any documentation, README, decision register, plan or handoff.
- Any files outside the three exact assigned SQL paths.
- Application/API code or .NET solution.
- CSV/JSON parsers or automated ingestion service.
- Validation/quality engine or issue lifecycle.
- Silver/Gold tables or transformation jobs.
- Risk, alert, investigation, evidence or outcome tables.
- Authentication/authorisation framework, cloud, containers, brokers, microservices, reporting or deployment configuration.
- Branches, commits or GitHub changes.

Do not change approved source identity, receipt, raw payload or domain semantics. Do not add dependencies or infrastructure.

### 5.8 One-review-then-implementation procedure

Before writing code, Claude performs one independent review of the design and assignment and classifies findings:
- **NON-BLOCKING:** explain briefly and proceed within the approved design.
- **BLOCKING:** stop only affected work; report precise issue, impact, recommended resolution and exact decision required.
- **PRODUCT OWNER DECISION:** request only where material approval is genuinely necessary.

If there is no blocking issue, proceed directly with implementation under this same assignment. Do not return for another general architecture review. Routine SQL implementation choices within the approved design do not require Product Owner approval.

If a material issue is discovered, provide one consolidated report and wait only for the specific Product Owner decision. Do not silently change architecture, requirements or file scope.

### 5.9 Complete-file return format

Return each file in full, with exact repository-relative path and a separate complete code block. Do not return diffs or partial snippets as substitutes.

Then include:
1. Review findings and classification.
2. Implementation summary and object inventory.
3. Design conformance and any justified non-material choices.
4. Dependencies and environment assumptions.
5. VS Code assembly instructions for the three exact paths.
6. Execution order and exact SSMS/sqlcmd commands.
7. Required permissions/database context.
8. Tests and commands actually executed, exact results, and checks not run.
9. Expected outcomes for Product Owner local verification.
10. Limitations, known issues and residual risks.
11. Confirmation that no excluded files/docs/branches/commits were modified.

### 5.10 Product Owner assembly and local verification

1. Create the exact folders if absent.
2. Place each complete returned file at its assigned path.
3. Review file contents before execution.
4. Verify SQL Server version, connectivity, target database and permissions.
5. Run setup scripts in order against a dedicated local development database, never an unintended database.
6. Run verification script and capture complete output.
7. Supply the three assembled files or diffs, Git status, SQL Server version, exact commands, complete output/errors and any deviations to ChatGPT.

ChatGPT then performs one return/alignment checkpoint: re-fetch latest main, inspect current files and supplied code, compare against exact assignment, review actual local evidence, identify defects and integrate approved code into main. No next increment is assigned before that checkpoint.

## 6. Current blockers and Product Owner decisions

**No additional Product Owner design decision is open for SEN-DB-001.** SEN-DESIGN-001 and SEN-DB-001 were approved on 27 November 2026 with no amendments.

**Environment verification pending:** Product Owner must verify local SQL Server 2022 version/connectivity and permissions during local assembly. This does not prevent Claude preparing the SQL files.

**Assignment state:** Prepared and authorised; not yet delivered to Claude by this ChatGPT interface. The Product Owner must paste the assignment below into Claude. No implementation has started and no files have been returned.

## 7. Assignment to send to Claude

The full assignment is the content of this handoff's section 5. Send sections 1–6 as repository context and section 5 as the binding assignment. Claude must follow the one-review-then-implementation procedure in section 5.8.

## 8. Status vocabulary

- NOT STARTED: work has not begun.
- IN PROGRESS: work is actively underway.
- BLOCKED: a dependency or issue prevents progress.
- IMPLEMENTED: the change has been made.
- VERIFIED: defined checks have actually passed with evidence.
- ACCEPTED: Product Owner has accepted the deliverable.

Implementation, verification and acceptance are separate states. Never claim tests, local environment status or repository changes without evidence.

## 9. Next authorised action

Product Owner sends SEN-DB-001 in section 5 to Claude. Claude reviews once and, if no blocking issue exists, returns the three complete SQL files and the required implementation/verification instructions. Product Owner assembles and executes locally, then returns the actual files and evidence for ChatGPT's single integration checkpoint.
