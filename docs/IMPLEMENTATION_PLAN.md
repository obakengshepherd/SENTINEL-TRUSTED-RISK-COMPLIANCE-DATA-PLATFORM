# Implementation Plan

**Historical baseline:** 25 November 2026. Foundation documentation established; detailed design and implementation increments remain subject to their respective approval gates.  
**Overall delivery scope:** Full phased scope approved, delivered incrementally.  
**Current phase:** Phase 1 — Database and Domain Design.  
**Phase 1 implementation status:** NOT STARTED and NOT AUTHORISED.

## 1. Delivery principles
Follow **DISCOVER → DESIGN → BUILD → VERIFY → REVIEW → RECORD**, coordinated through the FNEOS three-stage workflow. Work in manageable increments. Inspect before modifying. Preserve verified behaviour. Do not expand scope silently. Report actual test results. Code being written does not make a phase complete.

## 2. Phases

### Phase 0 — Project foundation
Deliverables: business purpose, scope and exclusions; controlled glossary; initial conceptual entity and relationship model; architecture and technology direction; governance, provenance and lineage principles; acceptance criteria and repository documentation.

**Historical status:** Foundation documentation established by the 25 November 2026 baseline. This is not a claim that detailed design or implementation was approved or completed.

### Phase 1 — Database and domain foundation

**Current phase. Design status: NOT STARTED. Implementation status: NOT STARTED.**

#### Phase 1A — Detailed design and environment discovery
- Review and finalise domain entities, responsibilities, relationships, cardinalities and lifecycle boundaries.
- Define source identity, re-delivery, idempotency, exact-duplicate and conflict semantics, correction/version handling.
- Define investigation referral, alert relationships, evidence association, outcome evidential basis, versioning, reopening and supersession.
- Define governance, provenance, lineage, audit and security boundaries needed by the first database increment.
- Design the initial SQL Server relational schema, keys, constraints, indexes and transaction boundaries.
- Define Bronze / Silver / Gold promotion and exception/quarantine semantics without introducing unnecessary infrastructure.
- Identify the minimum coherent synthetic reference and seed scenarios.
- Verify the local SQL Server 2022 Developer Edition environment and inspect installed .NET SDK/runtime before selecting environment-dependent implementation details.
- Classify technology choices as approved, proposed or deferred.

#### Phase 1B — Specialist review and Product Owner design approval
- ChatGPT prepares a bounded, read-only Claude architecture/domain review assignment.
- Claude independently reviews the current repository and returns findings; it does not modify files.
- ChatGPT reconciles findings, identifies trade-offs and prepares a decision-focused design proposal.
- Product Owner approves material design decisions and the detailed Phase 1 design baseline.
- ChatGPT records approved material decisions in `docs/DECISIONS.md`.

**Implementation gate:** No schema, migration, seed data, application code or automated tests may be started as Phase 1 implementation until the detailed design is reviewed, material decisions are approved, and the Product Owner explicitly authorises a bounded first implementation increment.

#### Phase 1C — Bounded implementation increment (future; not authorised)
The exact scope will be proposed after design approval. Candidate deliverables include the solution structure, initial database schema, core source/ingestion entities and constraints, reference data, a small deterministic synthetic dataset and automated tests. The assignment must state exact files, boundaries, expected outputs and verification steps.

#### Phase 1 acceptance criteria
**Design acceptance evidence:**
- Approved conceptual domain model with explicit relationships/cardinalities.
- Documented source identity, idempotency, duplicate, conflict and correction rules.
- Documented investigation, evidence and outcome lifecycle rules.
- Reviewed physical SQL Server design including schemas, keys, constraints and justified indexes.
- Defined transaction and failure boundaries for the first increment.
- Defined synthetic seed scenarios and expected outcomes.
- Environment discovery recorded; proposed stack decisions remain clearly classified.
- Bounded implementation increment and tests specified.
- Material decisions explicitly approved by the Product Owner.

**Implementation exit evidence (only after authorisation):**
- Schema/setup can be created reproducibly on the verified target environment.
- Constraints and representative relationships are exercised by tests.
- Synthetic seed data is deterministic and repeatable.
- Domain invariants and agreed edge cases pass automated checks.
- Actual commands, results and limitations are recorded.
- Product Owner acceptance is separately recorded; passing tests alone do not imply acceptance.

### Phase 2 — Data ingestion
Deliverables: CSV and JSON ingestion; source and batch registration; raw payload preservation; record receipt tracking; idempotency, duplicate and conflict handling; pipeline run metadata.

Exit evidence: valid, repeated and conflicting submissions produce defined, tested results.

### Phase 3 — Data quality and validation
Deliverables: versioned validation rules; validation execution and results; rejected-record handling; quality issue lifecycle; quality metrics and reports.

Exit evidence: valid and invalid records are distinguishable and failures traceable.

### Phase 4 — Governance, provenance and lineage
Deliverables: data asset metadata; ownership and classification; dataset-level lineage; record-level traceability where justified; transformation documentation.

Exit evidence: selected records and datasets can be traced to origins and processing context.

### Phase 5 — Risk and compliance domain
Deliverables: risk indicators; synthetic risk rules; alerts and triggering context; investigation management; evidence references; documented outcomes.

Exit evidence: risk indicators, alerts, investigations and investigation outcomes remain distinct and their relationships are tested.

### Phase 6 — Audit and monitoring
Deliverables: significant audit events; status-transition history; pipeline and exception monitoring; audit evidence queries.

Exit evidence: representative activities can be reconstructed with attributable history.

### Phase 7 — Reporting and analytical outputs
Deliverables: governed reporting views; data-quality metrics; pipeline monitoring outputs; risk and investigation summaries; Power BI integration if justified.

Exit evidence: reports reconcile to underlying governed records and defined reporting rules.

### Phase 8 — Engineering hardening and demonstration
Deliverables: regression and integration testing; security and permission review; recovery and repeatability testing; workload-based performance measurements; setup, architecture and demonstration documentation.

Exit evidence: reproducible demonstration, recorded test evidence and honest limitations.

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
