# Implementation Plan

**Historical baseline:** 25 November 2026. Foundation documentation established; detailed design and implementation increments remain subject to their respective approval gates.  
**Overall delivery scope:** Full phased scope approved, delivered incrementally.  
**Current phase:** Phase 1 — Database and Domain Design / Foundation.  
**Phase 1 design status:** APPROVED — SEN-DESIGN-001, 27 November 2026.  
**Current implementation increment:** SEN-DB-001 — SQL Server Ingestion Foundation.  
**Implementation status:** AUTHORISED; NOT STARTED pending Claude assignment review and file return.

## 1. Delivery principles

Follow **DISCOVER → DESIGN → BUILD → VERIFY → REVIEW → RECORD**, coordinated through FNEOS. ChatGPT owns architecture, requirements, technical specifications, documentation, task decomposition, handoffs and main-branch integration. Claude performs one independent review of the relevant Primary AI work and, if no blocking issue exists, implements within the same approved handoff. The Product Owner assembles and runs the returned code locally. Avoid repeated general review loops. Escalate only genuine blockers or material Product Owner decisions.

Work in manageable increments. Inspect before modifying. Preserve verified behaviour and repository history. Do not expand scope silently. Report actual test results. Code being written does not make a phase complete.

## 2. Phases

### Phase 0 — Project foundation

Deliverables: business purpose, scope and exclusions; controlled glossary; initial conceptual entity and relationship model; architecture and technology direction; governance, provenance and lineage principles; acceptance criteria and repository documentation.

**Historical status:** Foundation documentation established by the 25 November 2026 baseline.

### Phase 1 — Database and domain foundation

**Design status: APPROVED — SEN-DESIGN-001, 27 November 2026.**  
**Implementation:** Incremental; first increment SEN-DB-001 is authorised but not yet started.

#### Phase 1A — Detailed design and environment discovery
- Completed for the approved design baseline in `docs/PHASE-1-DATABASE-DOMAIN-DESIGN.md`.
- Domain identity, source delivery, raw payload, processing history, domain invariants, initial physical SQL design and SEN-DB-001 acceptance criteria are defined.
- Local SQL Server version/connectivity remains to be verified by the Product Owner during local assembly. No local verification is claimed.
- C#/.NET, Dapper/ADO.NET, ASP.NET Core and xUnit remain proposals and are not dependencies of the SQL-only first increment.

#### Phase 1B — Specialist review and Product Owner design approval
- Product Owner approved SEN-DESIGN-001 with no amendments on 27 November 2026.
- Under the active 27 November directive, Claude receives one combined review-and-implementation handoff. Claude reviews the approved design and assignment once; if no blocking issue exists, proceeds with the assigned implementation under that same handoff.
- Non-blocking findings are documented and implementation proceeds within the approved design.
- Blocking issues stop only affected work and are consolidated with impact, proposed resolution and exact Product Owner decision required.
- No repeated general review cycle.

#### Phase 1C — Bounded implementation: SEN-DB-001
**Objective:** Create the SQL Server source/ingestion/raw-payload foundation.

**Exact Claude-owned files:**
- `database/001-create-schemas.sql`
- `database/002-create-ingestion-foundation.sql`
- `database/tests/001-verify-ingestion-foundation.sql`

**Included:** schemas `ref`, `ingest`, `bronze`, `ops`; tables for DataSource, PipelineRun, IngestionBatch, SourceRecordIdentity, RecordReceipt and RawRecord; keys, constraints, justified indexes; repeat-safe/clear-precondition setup; rollback-safe synthetic verification scenarios.

**Excluded:** application/API code, .NET solution, CSV/JSON parser, automated ingestion service, quality engine, Silver/Gold tables, risk/investigation tables, cloud, containers, messaging, microservices, production security and reporting.

**Acceptance criteria:**
1. Setup creates all four schemas and six defined tables on SQL Server 2022.
2. Primary/foreign keys, unique constraints and check constraints enforce the approved model.
3. Source identity is unique within a source; every delivery is separately recordable.
4. Exact repeats and changed-content deliveries are retained without overwriting prior payload/receipt history.
5. SHA-256 is stored as 32 bytes and verification checks the hash against exact payload bytes.
6. Receipt-to-payload one-to-one relationship is enforced; transaction boundary is demonstrated or explicitly documented for the later application service.
7. UTC timestamps and valid start/completion ordering are enforced.
8. Deletes cannot cascade through preserved receipt/payload history.
9. Verification uses synthetic rollback-safe data and reports pass/fail clearly.
10. Setup, target version, permissions, database context and execution commands are documented in Claude's return.
11. Claude reports only commands actually run and real outcomes; unrun checks are identified.
12. Product Owner local execution evidence is supplied and reviewed before VERIFIED or ACCEPTED status.

**Execution sequence:** ChatGPT finalises and records the design/assignment; Claude reviews once and implements if no blocker; Product Owner assembles and executes in VS Code/SSMS; ChatGPT performs one return/alignment checkpoint and integration review; ChatGPT integrates approved code into main and records actual verification/acceptance state.

#### Phase 1 completion criteria
Phase 1 is not complete after SEN-DB-001 alone. Remaining increments will address domain tables, quality, lineage/governance and risk/investigation models as defined by approved scope. Design, implementation, verification and Product Owner acceptance remain distinct states.

### Phase 2 — Data ingestion
Deliverables: CSV and JSON ingestion; source and batch registration; raw payload preservation; record receipt tracking; idempotency, duplicate and conflict handling; pipeline run metadata.

### Phase 3 — Data quality and validation
Deliverables: versioned validation rules; validation execution and results; rejected-record handling; quality issue lifecycle; quality metrics and reports.

### Phase 4 — Governance, provenance and lineage
Deliverables: data asset metadata; ownership and classification; dataset-level lineage; record-level traceability where justified; transformation documentation.

### Phase 5 — Risk and compliance domain
Deliverables: risk indicators; synthetic risk rules; alerts and triggering context; investigation management; evidence references; documented outcomes.

### Phase 6 — Audit and monitoring
Deliverables: significant audit events; status-transition history; pipeline and exception monitoring; audit evidence queries.

### Phase 7 — Reporting and analytical outputs
Deliverables: governed reporting views; data-quality metrics; pipeline monitoring outputs; risk and investigation summaries; Power BI integration if justified.

### Phase 8 — Engineering hardening and demonstration
Deliverables: regression and integration testing; security and permission review; recovery and repeatability testing; workload-based performance measurements; setup, architecture and demonstration documentation.

## 3. Project-level acceptance criteria

| Capability | Required evidence |
|---|---|
| Ingestion | Processed synthetic input files |
| Validation | Passing and failing examples |
| Data quality | Measurable results and issue records |
| Duplicate handling | Exact duplicate and conflict scenarios |
| Provenance | Traceable source records |
| Lineage | Reconstructable processing paths |
| Governance | Assets, owners, definitions and classifications |
| Risk information | Distinct indicators and alerts |
| Investigations | Traceable examination lifecycle |
| Evidence | Identifiable supporting records |
| Outcomes | Documented evidence-supported conclusions |
| Audit | Attributable activity history |
| Reporting | Reproducible outputs |
| Testing | Actual automated test results |

## 4. Status vocabulary

- NOT STARTED: work has not begun.
- IN PROGRESS: work is actively underway.
- BLOCKED: a dependency or issue prevents progress.
- IMPLEMENTED: the change has been made.
- VERIFIED: defined checks have actually passed, with evidence.
- ACCEPTED: the Product Owner has accepted the deliverable.

Implementation, verification and acceptance are separate states.

## 5. Completion reporting

At each meaningful task completion, report accomplishments; files created or modified; important technical decisions; tests executed and actual results; outstanding issues; documentation updated; Git status and commit if applicable; recommended next action.
