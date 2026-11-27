# Sentinel Decision Register

**Authority:** Product Owner  
**Maintainer:** ChatGPT (Primary AI)  
**Purpose:** Record approved project decisions, proposals, unresolved questions and superseded workflow arrangements. The repository is the authoritative project record.

## 1. Decision status conventions
- **APPROVED:** Explicit Product Owner decision.
- **PROPOSED:** Recommended direction awaiting approval.
- **OPEN:** Requires investigation, design or Product Owner decision.
- **DEFERRED:** Deliberately postponed; not required for the current increment.
- **SUPERSEDED:** Replaced by a later recorded decision. Historical record is retained.

A recommendation, draft design or tool default does not become an approved decision without the required Product Owner authority.

## 2. Approved project decisions and constraints

| ID | Area | Decision | Status | Notes |
|---|---|---|---|---|
| SEN-DEC-001 | Architecture | Use a modular monolith with one application/deployment boundary and clear internal modules. | APPROVED | No microservices absent a demonstrated requirement and further approval. |
| SEN-DEC-002 | Database | Use Microsoft SQL Server 2022 Developer Edition for local development. | APPROVED | Development/testing edition; verify local installation and connectivity before implementation. |
| SEN-DEC-003 | Scope | Preserve the full phased project scope and deliver it incrementally. | APPROVED | Phase-level designs and bounded implementation increments retain their own approval gates. |
| SEN-DEC-004 | Data formats | Support structured CSV and JSON ingestion as initial input formats. | FOUNDATION REQUIREMENT | Detailed parsing and error semantics remain design work. |
| SEN-DEC-005 | Data organisation | Use Bronze / Silver / Gold as logical processing layers. | FOUNDATION DIRECTION | No separate databases/services are implied; promotion rules remain to be designed. |
| SEN-DEC-006 | Data safety | Use synthetic data only. No real personal, financial, customer or confidential data. | MANDATORY CONSTRAINT | Applies to examples, fixtures, logs, evidence and demonstrations. |
| SEN-DEC-007 | Domain semantics | Keep risk indicator, alert, investigation and investigation outcome distinct. | MANDATORY DOMAIN INVARIANT | Alert is not proof; investigation is not guilt; outcome requires identifiable evidential basis; evidence and outcome are separate. |
| SEN-DEC-008 | Historical code | Historical project names are conceptual references only; do not import old source code, dependencies, repository structures or Git history. | ACCEPTED BASELINE RULE | See `docs/PROJECT_EVOLUTION.md`. |
| SEN-DEC-009 | Collaboration | Adopt the FNEOS three-stage workflow, ChatGPT documentation ownership, Claude assigned-code ownership, user-led VS Code assembly and ChatGPT return/alignment checkpoint. | APPROVED 2026-11-27 | See `docs/AI-COLLABORATION.md`. |
| SEN-DEC-010 | Branch governance | Branch-based work is prohibited unless the Product Owner explicitly authorises it. Claude must not push or commit directly to GitHub. | APPROVED 2026-11-27 | Routine approved documentation corrections are committed by ChatGPT directly to main. |
| SEN-DEC-011 | Phase 1 design | Approve the detailed domain and initial SQL Server relational design in `docs/PHASE-1-DATABASE-DOMAIN-DESIGN.md`. | APPROVED 2026-11-27 | Product Owner approved SEN-DESIGN-001 with no amendments. Includes source-scoped identity, immutable delivery receipts, raw payload preservation, historical processing and evidence-supported outcomes. |
| SEN-DEC-012 | Initial database increment | Authorise SEN-DB-001, SQL Server Ingestion Foundation, under the approved design and bounded file list. | APPROVED 2026-11-27 | SQL-only database foundation; no application/API/.NET/cloud implementation. Implementation is not complete until files are returned, assembled and verified. |

## 3. Proposed technical choices — not approved

| ID | Area | Proposal | Status | Required next step |
|---|---|---|---|---|
| SEN-PROP-001 | Language/runtime | C# / .NET 10 LTS | PROPOSED | Verify installed SDK/runtime, support lifecycle and dependency compatibility; then seek approval if material. |
| SEN-PROP-002 | Data access | Dapper / ADO.NET with explicit SQL | PROPOSED | Compare suitability against approved design and testability needs. |
| SEN-PROP-003 | API | ASP.NET Core | PROPOSED | Confirm whether an API is needed in the first increment and select compatible framework. |
| SEN-PROP-004 | Testing | xUnit | PROPOSED | Confirm with selected target framework and solution design. |
| SEN-PROP-005 | Development tools | VS Code and SSMS | PROPOSED | Verify actual local environment. |
| SEN-PROP-006 | Deployment | Local-first development | FOUNDATION DIRECTION | Confirm practical setup; no cloud commitment is approved. |

## 4. Open and deferred design decisions

The following remain outside SEN-DB-001 and must be resolved in their relevant increments:
- CSV/JSON parsing, schema versioning and malformed-input semantics.
- Automated idempotency/conflict classification, correction and version-resolution workflow.
- Data-quality issue lifecycle, rejected/quarantined records and reprocessing.
- Bronze/Silver/Gold promotion criteria and lineage granularity.
- Detailed risk rule, alert, referral, investigation, evidence and outcome physical models.
- Retention, deletion, audit history, security roles and access boundaries.
- Deterministic synthetic datasets beyond SEN-DB-001's rollback-safe verification scenarios.
- Final selection of proposed application/runtime, data-access, API and test technologies.

Do not invent legal retention requirements or regulatory obligations. A real deployment would require relevant institutional/legal policy review.

## 5. Superseded workflow records

| Record | Superseded position | Replacement |
|---|---|---|
| 26 November 2026 AI collaboration agreement and handoff workflow | Mandatory Claude branches and pull requests; broad AI documentation/implementation overlap; ChatGPT may independently implement delegated code. | FNEOS three-stage workflow approved 27 November 2026. Git history remains intact. |
| SEN-REV-001 assignment as recorded in the 26 November handoff | Prepared under the superseded workflow; not treated as an active assignment or evidence of a completed Claude review. | Superseded by the 27 November FNEOS single-review-then-implementation workflow. |

## 6. Decision change procedure
For each material decision, record a stable ID, date, topic, exact decision, status, rationale, alternatives where material, affected requirements/architecture/data/security/delivery, approval authority and any superseded decision. Update relevant project documents in the same documentation change set. Do not erase superseded decisions or rewrite historical Git commits.
