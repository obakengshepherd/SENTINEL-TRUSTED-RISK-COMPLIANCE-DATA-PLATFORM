# Phase 1 — Database and Domain Design Baseline

**Design ID:** SEN-DESIGN-001  
**Status:** APPROVED by Product Owner on 27 November 2026  
**Authority:** Product Owner  
**Prepared by:** ChatGPT (Primary AI)  
**Applies to:** Phase 1 and subsequent bounded increments  
**First authorised implementation increment:** SEN-DB-001 — SQL Server Ingestion Foundation

## 1. Purpose and authority

This document converts the approved Sentinel foundation into the detailed domain and initial relational design baseline. It is subordinate to Product Owner authority and must be read with `docs/PROJECT_FOUNDATION.md`, `docs/ARCHITECTURE.md`, `docs/DATA_MODEL.md`, `docs/DOMAIN_GLOSSARY.md`, `docs/DATA_GOVERNANCE.md`, `docs/PROVENANCE_AND_LINEAGE.md`, and `docs/DECISIONS.md`.

Sentinel remains a synthetic enterprise portfolio demonstration, not a production banking, fraud, AML or regulatory platform. Synthetic data only. The approved architecture is a modular monolith and SQL Server 2022 Developer Edition is the approved local development database.

## 2. Approved design principles

1. Preserve the distinction between RiskIndicator, Alert, Investigation, EvidenceRecord and InvestigationOutcome.
2. A risk indicator is not proof; an alert is not proof of wrongdoing; an investigation is not proof of guilt.
3. An outcome must have at least one identifiable evidence association. Evidence and outcome are distinct records.
4. Source identity is scoped to a registered DataSource. A content hash is not a business identity.
5. Every delivery is traceable. A repeat delivery is not silently discarded.
6. Same source identity plus same content hash is an exact repeat. Same source identity plus different content hash is a changed-content submission requiring controlled conflict/correction handling; it must not overwrite prior receipt or payload history.
7. Preserve raw source payload and receipt context independently from standardised/curated representations.
8. Processing executions are identifiable and historical. A retry does not erase a prior run.
9. Invalid or exceptional data must not silently enter trusted reporting outputs.
10. Use explicit constraints and transaction boundaries for integrity; do not rely solely on documentation or application convention.
11. Store system timestamps as UTC using `datetime2(7)`; retain source-provided event time separately with its original offset/zone or documented interpretation where available.
12. Monetary values, when introduced, use explicit decimal precision and a currency code; never floating point.
13. Prefer a single SQL Server database with logical schemas. Do not introduce separate databases or services for Bronze/Silver/Gold.
14. Keep the first increment deliberately narrow. Do not create speculative modules or infrastructure.

## 3. Domain model and relationship rules

### 3.1 Source and ingestion

- **DataSource** identifies a registered producer/source. One source has many IngestionBatches and SourceRecord identities.
- **IngestionBatch** belongs to exactly one DataSource. A batch groups receipts from a delivery unit such as a file or submission.
- **SourceRecordIdentity** identifies a record using a source-scoped key. Enforce uniqueness on (DataSourceId, SourceRecordKey).
- **RecordReceipt** represents one observed delivery of a SourceRecordIdentity in one batch. One source identity may have many receipts over time. Each receipt is immutable in the sense that later delivery does not replace it.
- **RawRecord** preserves the payload bytes and content hash associated one-to-one with a RecordReceipt. Preserve original bytes; do not assume UTF-8 or text-only payload at the storage boundary.
- A receipt's hash is SHA-256 over the exact preserved payload bytes. Hash equality is a content comparison aid, not a replacement for source identity.
- A repeated delivery with matching source identity and hash is an exact repeat. A matching source identity with a different hash is a changed-content submission. Record both deliveries. Resolution/version semantics belong to a later controlled processing increment; SEN-DB-001 must not silently select a winner.
- A source record key is mandatory for the first increment. If a future source lacks a stable key, it requires an explicit deterministic identity strategy and decision before ingestion support is added.

### 3.2 Processing

- **PipelineRun** identifies one processing execution, with run type, start/end UTC timestamps and a controlled status.
- A batch may be associated with a pipeline run; a pipeline run may process multiple batches in later increments. The initial schema may use a nullable PipelineRunId on IngestionBatch until multi-batch run orchestration is implemented.
- Reprocessing creates a new run. It does not overwrite previous run metadata or receipt payloads.
- Run status and batch status are constrained to defined values; completion time cannot precede start time.

### 3.3 Quality and data layers

- ValidationRule, ValidationExecution, ValidationResult and DataQualityIssue remain separate concepts.
- A failed validation remains a failed result even if an issue is accepted as an exception or later resolved.
- Bronze is source-oriented preservation; Silver is validated/standardised data with quality state represented; Gold is governed, rebuildable reporting output.
- Promotion criteria and quality issue lifecycle are later increments. SEN-DB-001 creates only the Bronze and ingestion foundation, not Silver/Gold tables.

### 3.4 Risk, investigation, evidence and outcome

- One RiskIndicator may contribute to zero or many Alerts.
- An Alert may have zero or many Investigation associations.
- An Investigation may be initiated by an authorised referral other than an Alert and may examine multiple Alerts. Model the many-to-many association explicitly when that phase is implemented.
- An Investigation has one or more EvidenceRecords as needed. Evidence retains origin, identity and context.
- InvestigationOutcome is a distinct, versioned decision record. A superseding outcome does not erase its predecessor; reopening does not erase investigation history.
- Each outcome must be associated with at least one EvidenceRecord. A foreign key from outcome to investigation alone is insufficient. Enforce the evidence association through a controlled transaction/service and, where practical, a database enforcement mechanism in the investigation increment.
- Outcome classifications are project-defined synthetic vocabulary, not institutional or regulatory standards.

### 3.5 Governance, lineage and audit

- DataAsset, DataOwner, DataClassification, BusinessGlossaryTerm, LineageNode, LineageEdge and AuditEvent remain distinct governance concepts.
- Significant status changes and corrections must preserve actor/system identity, UTC time, reason and prior context where applicable.
- Retention periods are not inferred from law or a bank's policy. Synthetic-project retention assumptions must be explicitly documented before retention behaviour is implemented.
- Detailed access roles and authentication are introduced only when the actual access boundary is defined. Least privilege and secret exclusion apply from the first increment.

## 4. Initial SQL Server physical design

### 4.1 Database and schema boundary

Use one SQL Server database. SEN-DB-001 creates these logical schemas only:

| Schema | Responsibility in SEN-DB-001 |
|---|---|
| `ref` | Registered source reference data |
| `ingest` | Batch, source identity and delivery receipt tracking |
| `bronze` | Preserved raw payload bytes |
| `ops` | Pipeline execution metadata |

Later schemas such as `quality`, `governance`, `lineage`, `risk`, `investigation`, `audit` and `reporting` are intentionally deferred until their increments.

### 4.2 Initial entities and minimum columns

The implementation may refine names/types within these responsibilities, but must not change the relationships or semantics without escalation.

**ref.DataSource**
- DataSourceId: surrogate primary key.
- SourceCode: required, stable, unique source identifier.
- DisplayName: required.
- IsActive: required.
- CreatedAtUtc: required UTC timestamp.

**ops.PipelineRun**
- PipelineRunId: surrogate primary key.
- RunType: required.
- Status: required controlled value (e.g. Running, Succeeded, Failed).
- StartedAtUtc: required.
- CompletedAtUtc: nullable until completion; if present, not earlier than start.
- Optional correlation/reference identifier where useful; no speculative orchestration framework.

**ingest.IngestionBatch**
- IngestionBatchId: surrogate primary key.
- DataSourceId: required foreign key.
- SourceBatchKey: optional source-supplied identifier; not globally unique.
- ReceivedAtUtc: required.
- Status: required controlled value (e.g. Received, Processing, Completed, Failed).
- PipelineRunId: nullable foreign key to ops.PipelineRun.
- Optional original file/delivery name as descriptive metadata, not an identity substitute.

**ingest.SourceRecordIdentity**
- SourceRecordIdentityId: surrogate primary key.
- DataSourceId: required foreign key.
- SourceRecordKey: required source-scoped identity.
- FirstSeenAtUtc: required.
- Unique constraint on (DataSourceId, SourceRecordKey).

**ingest.RecordReceipt**
- RecordReceiptId: surrogate primary key.
- IngestionBatchId: required foreign key.
- SourceRecordIdentityId: required foreign key.
- ReceivedAtUtc: required.
- PayloadHashSha256: exactly 32 bytes.
- No uniqueness constraint on identity/hash: repeated deliveries must remain individually recordable.

**bronze.RawRecord**
- RecordReceiptId: primary key and foreign key to ingest.RecordReceipt (one-to-one).
- PayloadBytes: required varbinary(max), preserving received bytes.
- PayloadMediaType: optional descriptive media type.
- CharacterEncoding: optional where known; do not assume.
- Content hash is recorded on RecordReceipt and must be computed from the exact PayloadBytes by the ingestion boundary; the later ingestion service must verify this invariant.

Use bigint identity surrogate keys unless a clear SQL Server constraint or repository convention justifies otherwise. Use datetime2(7) for UTC instants. Use nvarchar for identifiers and descriptive text. Avoid SQL reserved words as object names.

### 4.3 Integrity, indexing and transactions

- Primary keys on every entity.
- Foreign keys enforce source → batch, source → source identity, batch/identity → receipt, receipt → raw record, and batch → optional run.
- Unique source code and unique (DataSourceId, SourceRecordKey).
- Check constraints for required enumerated status values, 32-byte SHA-256 values and valid time ordering.
- Index foreign-key access paths and likely lookup paths (source + source record key, batch receipts, receipt/payload lookup). Avoid speculative indexes.
- No cascading deletes for source, batch, receipt or raw payload history.
- Create source identity and receipt/raw payload within a transaction so no receipt is committed without its required payload.
- Batch/run status transitions and processing semantics are constrained at the database boundary where practical; more complex orchestration is deferred.
- SQL setup scripts must be repeatable or fail safely with a clear precondition. They must never drop or destroy existing user data as a convenience.

## 5. First increment: SEN-DB-001

**Objective:** Create the initial SQL Server source/ingestion/raw-payload foundation.

**Exact Claude-owned code files:**
- `database/001-create-schemas.sql`
- `database/002-create-ingestion-foundation.sql`
- `database/tests/001-verify-ingestion-foundation.sql`

**Required objects:** schemas `ref`, `ingest`, `bronze`, `ops`; tables `ref.DataSource`, `ops.PipelineRun`, `ingest.IngestionBatch`, `ingest.SourceRecordIdentity`, `ingest.RecordReceipt`, `bronze.RawRecord`.

**Test scenarios:** valid source/batch/identity/receipt/raw payload; unknown-source batch rejected; unknown-batch receipt rejected; unknown identity receipt rejected; duplicate source code rejected; duplicate source-scoped identity rejected; same identity with same hash can be received more than once; same identity with changed hash can be recorded as a separate receipt; payload bytes and hash remain queryable; invalid hash length and invalid status rejected; invalid timestamp ordering rejected; required receipt/payload atomicity demonstrated or clearly documented as an application transaction boundary if a SQL-only script cannot model the future service transaction faithfully. Test data must be synthetic and rolled back.

**Not in scope:** CSV/JSON parser, automated file ingestion, duplicate classification service, correction resolution, validation engine, Silver/Gold, risk/investigation tables, API/application code, .NET solution, authentication framework, cloud, containers, broker, microservices, reporting, production hardening.

## 6. Environment and technology status

SQL Server 2022 Developer Edition is approved for local development; the Product Owner's actual local installation, version and connectivity have not yet been verified in this design record. The SQL scripts must target SQL Server 2022-compatible T-SQL and state any required database context/permissions.

C#/.NET 10 LTS, Dapper/ADO.NET, ASP.NET Core and xUnit remain proposals, not approved dependencies for SEN-DB-001. No application framework dependency is needed for this SQL-only increment.

## 7. Acceptance criteria for SEN-DB-001

1. All four schemas and six tables are created with the defined relationships.
2. All primary/foreign keys, unique constraints and check constraints behave as intended.
3. Every receipt is linked to one source identity and one batch; every raw payload is linked one-to-one to a receipt.
4. Source identity is unique within a source, not globally.
5. Exact repeat and changed-content submissions can both be retained without overwriting prior receipt/payload history.
6. SHA-256 is stored as 32 bytes and test scenarios verify the hash against exact payload bytes.
7. UTC timestamps and valid start/completion ordering are enforced.
8. Deletes cannot cascade through preserved receipt/payload history.
9. The verification script uses synthetic data, cleans up through transaction rollback, and reports pass/fail results clearly.
10. Setup and verification instructions identify target SQL Server version, permissions, database context and commands.
11. Claude reports commands actually executed and their results; unrun checks are explicitly identified.
12. Local Product Owner execution evidence is reviewed separately before the increment can be marked VERIFIED or ACCEPTED.

## 8. Design decisions deliberately deferred

- Final application/runtime, API, data access and unit-test stack.
- CSV/JSON parsing and schema-version policy.
- Automated idempotency/conflict classification and correction workflow.
- Quality issue lifecycle, rejection/quarantine/reprocessing.
- Silver/Gold physical models and promotion orchestration.
- Detailed risk rule, alert, referral, investigation, evidence and outcome tables.
- Governance/lineage/audit physical models beyond current requirements.
- Retention periods, deletion policy, authentication and role matrix.
- Cloud, containers, orchestration, distributed messaging and production deployment.

Any change to the approved domain invariants, source identity semantics, payload preservation, database boundary or assigned file scope is a blocking issue requiring Product Owner direction. Routine SQL naming, formatting and justified index details may be resolved by Claude within this design.

## 9. Approval record

Product Owner decision: **APPROVED — 27 November 2026.**  
Amendments/conditions: **None.**  
Approval covers this design baseline and authorises SEN-DB-001 under the 27 November FNEOS workflow. It does not represent implementation, verification or acceptance of database objects.
