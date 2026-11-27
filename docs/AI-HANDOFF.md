# AI Handoff — Sentinel (FNEOS)

**Last updated:** 2026-11-27  
**Maintainer:** ChatGPT (Primary AI)  
**Product Owner:** User  
**Repository:** [SENTINEL-TRUSTED-RISK-COMPLIANCE-DATA-PLATFORM](https://github.com/obakengshepherd/SENTINEL-TRUSTED-RISK-COMPLIANCE-DATA-PLATFORM)  
**Branch:** `main`

## 1. Current project status

**Historical baseline:** 25 November 2026 — `82cb85867e3698b074714d076fb8e49fd4012cb4`.  
**Historical project status:** Foundation documentation established. Detailed design and implementation increments remain subject to their respective approval gates. No application implementation.  
**Current phase:** Phase 1 — Database and Domain Design.  
**Phase 1 design:** NOT STARTED.  
**Phase 1 implementation:** NOT STARTED; NOT AUTHORISED.  
**Phase 1 progress:** 0% of Phase 1 design/implementation deliverables. No design deliverable has yet been completed or approved against the Phase 1 acceptance criteria.

This is a governance/workflow correction, not a project restart. Preserve all valid requirements, architecture and project decisions established by the historical cutoff. Do not treat 26 November workflow instructions or changes as active authority.

Sentinel is a synthetic enterprise portfolio demonstration, not a production banking, fraud, AML or regulatory system. Synthetic data only.

## 2. Historical and current repository state

### Historical baseline
- Baseline commit: `82cb85867e3698b074714d076fb8e49fd4012cb4`.
- Date: 25 November 2026.
- Foundation documentation exists; no application implementation.
- The initial baseline contains the project README and eight foundation documents under `docs/`.

### Current state inspected before this reset
- `main) HEAD inspected: `22a1c8b8cc1089fcbb72af344a115cf6942c0ad3` — `docs(sentinel): correct repository handoff state`.
- This was six commits after the historical baseline, all dated 26 November.
- The 26 November commits changed README/foundation/implementation status wording and introduced a branch/PR-oriented AI collaboration agreement and handoff.
- The branch search returned only `main); no pull requests were found.
- The 26 November handoff contained assignment SEN-REV-001 prepared under the superseded workflow. There is no evidence in the inspected repository that Claude completed that review.
- The inspected project documentation records no application code, database schema, migrations, seed data, automated tests or deployment configuration as implemented.

### Corrective commits created on 27 November
The following commits were made sequentially on `main), without creating branches or rewriting history:

| Commit | File | Purpose |
|---|---|---|
| `3459ee158da4aa69af53d2dcbfaa5d95dac696d7` | `README.md` | Restore historical status; classify approved versus proposed direction; link governance records |
| `9bab024cc80dd46a70a6b690627aac1e6014cc27` | `docs/PROJECT_FOUNDATION.md` | Restore historical baseline status and clarify approval boundaries |
| `3b66f37625e0dca74b8895232f7350bab50b33a9` | `docs/IMPLEMENTATION_PLAN.md` | Establish Phase 1 design/implementation gates and acceptance criteria |
| `81b8b026b232b9303fba3409569ac1172b088b22` | `docs/DECISIONS.md` | Create the authoritative decision register |
| `61b1d556dfd8307975090b2c0d1c8fbea816dc17` | `docs/AI-COLLABORATION.md` | Replace the 26 November workflow with the approved FNEOS agreement |

The GitHub contents operations produced one normal commit per file, so the original two-commit proposal was not realised. No history was rewritten and no branch was created. The handoff update itself will be the next normal commit. Verify the final `main) head after that update before relying on it for a later assignment.

## 3. Approved project direction and constraints

| Area | Current position | Status |
|---|---|---|
| Architecture | Modular monolith | APPROVED |
| Database | SQL Server 2022 Developer Edition for local development | APPROVED |
| Scope | Full phased scope, delivered incrementally | APPROVED |
| Initial ingestion formats | CSV and JSON | Foundation requirement |
| Data organisation | Bronze / Silver / Gold logical organisation | Foundation direction; physical implementation rules open |
| Data | Synthetic only | MANDATORY |
| Domain semantics | Risk indicator, alert, investigation and investigation outcome are distinct | MANDATORY |
| Historical projects | Conceptual references only; no code/dependencies/repository histories imported | Accepted baseline rule |
| C# / .NET 10 LTS | Proposed | NOT APPROVED; verify SDK and compatibility |
| Dapper / ADO.NET | Proposed | NOT APPROVED |
| ASP.NET Core | Proposed | NOT APPROVED |
| xUnit | Proposed | NOT APPROVED |
| VS Code / SSMS | Proposed local tooling direction | Verify actual environment |

The decision register in `docs/DECISIONS.md` is authoritative for decision classification and open design questions.

## 4. Mandatory domain invariants

- A risk indicator is not an alert.
- An alert is not proof of wrongdoing.
- An investigation is not proof of guilt.
- An investigation outcome must have a defensible, identifiable evidential basis.
- Evidence and outcome are separate concepts.
- Invalid data must not silently enter trusted reporting datasets.
- Provenance and lineage must remain explainable.
- Source identity, processing context and material corrections must not be silently discarded.
- Exact duplicates and conflicting records must be distinguishable.

## 5. FNEOS workflow and file ownership

The approved workflow is defined in `docs/AI-COLLABORATION.md`.

1. **ChatGPT — Architecture & Documentation:** owns architecture, requirements, technical specifications, all project documentation, decision records, implementation plans, assignments, main-branch governance and integration.
2. **Claude — Engineering & Code:** reviews architecture by default; implements only exact assigned code files; returns complete files in chat with paths, explanations, tests and execution instructions. Claude does not push or commit to GitHub and does not modify documentation without explicit Product Owner-approved ownership transfer.
3. **Product Owner + VS Code + ChatGPT — Assembly & Integration:** Product Owner assembles code and runs it; supplies actual diffs/results/errors; ChatGPT performs the return/alignment checkpoint, reviews against the approved assignment and integrates approved changes into `main).

**Zero-overlap:** one active modification owner per file. ChatGPT owns documentation. Claude is read-only on documentation by default and owns only explicitly assigned code files during an active assignment.

**Branch rule:** Branch-based work is prohibited unless the Product Owner explicitly authorises it for a named task. No Claude direct pushes or commits.

## 6. Return/alignment checkpoint

Whenever the Product Owner returns after Claude work or local VS Code assembly, ChatGPT must first:
1. Establish the latest `main) commit.
2. Inspect repository state and relevant changes.
3. Compare supplied implementation with the approved assignment and file list.
4. Review actual test/build results supplied by the Product Owner.
5. Identify inconsistencies, omissions, unapproved changes and blockers.
6. Confirm alignment or list unresolved items.

Do not issue the next implementation assignment until this checkpoint is complete. ChatGPT cannot claim access to uncommitted local changes or local test results that have not been supplied.

## 7. Phase 1 — Database and Domain Design

**Status: NOT STARTED. No implementation is authorised.**

Required design work:
- Domain entities, responsibilities, relationships, cardinalities and lifecycle boundaries.
- Source identity, re-delivery, idempotency, exact-duplicate/conflict semantics, correction and version history.
- Investigation referral sources, alert/investigation relationships, evidence association and outcome lifecycle.
- SQL Server physical design: schemas, tables, keys, constraints, indexes and transaction boundaries.
- Data-quality issue lifecycle, rejected/quarantined records and reprocessing.
- Bronze/Silver/Gold promotion criteria and provenance/lineage boundaries.
- Governance, audit, retention and security boundaries proportionate to this synthetic local portfolio.
- Deterministic synthetic reference/seed scenarios and acceptance tests.
- Verify local SQL Server installation/connectivity and inspect .NET SDK/runtime before finalising proposed stack choices.

### Phase 1 approval gates
1. ChatGPT prepares the bounded design/review scope and assignment.
2. Claude independently reviews the current repository and returns a review report only, unless a later task explicitly authorises code.
3. ChatGPT reconciles findings and prepares design decisions.
4. Product Owner approves material design choices and the detailed design baseline.
5. ChatGPT records approved decisions.
6. Product Owner explicitly authorises the first bounded implementation increment.

No schema, migrations, seed data, application code or implementation tests before the above gates are satisfied.

### Phase 1 design acceptance evidence
- Approved conceptual domain model and cardinalities.
- Defined source identity, idempotency, duplicate/conflict and correction rules.
- Defined investigation, evidence and outcome lifecycle.
- Reviewed physical SQL Server design.
- Defined transaction/failure boundaries for the first increment.
- Synthetic seed scenarios and expected outcomes.
- Environment discovery and accurate technology classification.
- Bounded implementation scope and test plan.
- Material decisions approved by the Product Owner.

Implementation exit evidence is separate and requires reproducible schema creation, tested constraints/relationships, repeatable synthetic seed data, passing agreed tests and recorded actual results. Product Owner acceptance is separate from technical verification.

## 8. Outstanding decisions and blockers

Open design decisions are listed in `docs/DECISIONS.md`, including:
- Entity relationships/cardinalities and physical schema.
- Source identity/idempotency and duplicate/conflict/correction semantics.
- Quality issue lifecycle and rejected/quarantine handling.
- Bronze/Silver/Gold promotion and lineage granularity.
- Alert, investigation, evidence and outcome lifecycle/versioning.
- Retention, audit history, deletion and security/access boundaries.
- Seed-data scenarios.
- Proposed .NET, data-access, API and test stack.

No legal retention periods or regulatory requirements are assumed. A real deployment would require institutional/legal policy review.

## 9. Assignment register and review history

The previous SEN-REV-001 assignment was prepared under the 26 November workflow. It is **SUPERSEDED** and is not an active assignment. No Claude review completion is evidenced in the repository.

No new Claude assignment is active at this handoff revision. A fresh review-only assignment may be prepared under FNEOS after the current repository head and scope are rechecked. Claude's review is read-only; no branch or file modification ownership is implied.

## 10. File ownership register

| Files | Owner | Access/status |
|---|---|---|
| All project documentation, including README and `docs/**.md` | ChatGPT | Documentation owner |
| `docs/AI-COLLABORATION.md` | ChatGPT | Permanent FNEOS agreement |
| `docs/AI-HANDOFF.md` | ChatGPT | Living handoff; this file |
| `docs/DECISIONS.md` | ChatGPT | Decision register |
| Code files | No active Claude owner | No implementation assignment authorised |
| Claude review scope | Claude | Read-only only when assigned |

No simultaneous editing is authorised. Ownership transfer requires explicit Product Owner approval.

## 11. Next authorised action

Prepare a new bounded **Claude REVIEW ONLY** assignment for Phase 1 domain/data architecture review under FNEOS. First re-check the latest `main) SHA and relevant documents. The assignment must prohibit edits, branches, commits, pushes, schema creation and implementation. ChatGPT will reconcile the returned findings and present design decisions to the Product Owner.

**Not authorised:** schema implementation, migrations, seed data, application code, implementation tests or deployment configuration.
