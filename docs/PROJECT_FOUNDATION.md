# Project Foundation

**Historical status (25 November 2026):** Foundation documentation established. Detailed design and implementation approvals remain outstanding.

## 1. Definition
Sentinel is a synthetic enterprise Data Engineering platform demonstrating how organisations collect, validate, govern, trace and responsibly use risk- and compliance-related information.

Central question: How can an organisation establish that information used to identify, monitor, investigate and report risk is trustworthy, traceable, governed and supported by evidence?

Sentinel focuses on trustworthy information and its processing, not autonomous risk adjudication.

## 2. Business scenario
The working scenario is a fictional financial institution, Sentinel Financial Services (SFS). It receives structured information from hypothetical operational sources. Records may be incomplete, invalid, duplicated, inconsistent, outdated or difficult to trace.

The platform demonstrates controls for preserving source context, validating data, managing exceptions, documenting transformations and producing explainable downstream information. All people, organisations, accounts, transactions and evidence must be synthetic.

## 3. Business objectives
1. Establish controlled, repeatable ingestion.
2. Preserve original source context and record identity.
3. Validate data against explicit, versioned rules.
4. Identify and manage quality issues, duplicates and conflicts.
5. Record pipeline executions and transformations.
6. Maintain data ownership, metadata and classification.
7. Preserve the distinctions between risk indicators, alerts, investigations and outcomes.
8. Make important changes and processing activities traceable.
9. Produce reproducible, quality-controlled reporting outputs.

## 4. Scope

### In scope
- Source registration and structured CSV/JSON ingestion.
- Batch and record-level ingestion tracking.
- Controlled raw-data preservation.
- Validation rules, results and quality issue management.
- Exact duplicate and conflicting-record handling.
- Metadata, business definitions, ownership and classification.
- Dataset lineage, with record-level traceability introduced incrementally.
- Risk indicators and synthetic rule-based alerts.
- Investigation records, evidence references and documented outcomes.
- Audit events, exception handling, monitoring and reporting.
- Automated tests, local setup instructions and engineering documentation.

### Out of scope initially
- Production banking or customer integrations.
- Real personal, financial or confidential information.
- Regulatory submissions or certification claims.
- Autonomous determinations of criminality or guilt.
- Machine-learning risk scoring or generative AI decision-making.
- Mandatory cloud hosting, Kubernetes, message brokers or microservices.
- Infrastructure or framework complexity without a demonstrated need.

Future scope changes require Product Owner approval.

## 5. Illustrative stakeholders
Data Engineer; Data Analyst; Data Governance Officer; Risk Analyst; Investigator; Compliance Officer; Auditor; Management. These are hypothetical demonstration roles, not claims about a real institution.

## 6. Functional requirements

| ID | Requirement | Priority |
|---|---|---|
| FR-001 | Register data sources | Must |
| FR-002 | Ingest structured CSV and JSON data | Must |
| FR-003 | Preserve source context and original payload | Must |
| FR-004 | Identify ingestion batches and records | Must |
| FR-005 | Execute defined validation rules | Must |
| FR-006 | Record validation failures and quality issues | Must |
| FR-007 | Distinguish exact duplicates from conflicting records | Must |
| FR-008 | Maintain source provenance | Must |
| FR-009 | Record pipeline executions | Must |
| FR-010 | Record dataset-level lineage | Must |
| FR-011 | Maintain data asset metadata | Must |
| FR-012 | Register ownership and classification | Should |
| FR-013 | Maintain risk indicators | Must |
| FR-014 | Record rule-triggered or authorised alerts | Must |
| FR-015 | Manage investigations | Must |
| FR-016 | Associate evidence with investigations | Must |
| FR-017 | Record evidence-supported outcomes | Must |
| FR-018 | Maintain significant audit events | Must |
| FR-019 | Produce data-quality reports | Must |
| FR-020 | Produce risk and investigation reports | Should |
| FR-021 | Monitor pipeline executions and exceptions | Should |

## 7. Non-functional requirements
- Integrity: constraints and transactions protect important relationships and state changes.
- Reliability: failures are visible and do not silently appear successful.
- Traceability: records retain identifiable source and processing references.
- Auditability: significant actions are attributable and historically inspectable.
- Security: access is controlled according to defined responsibilities.
- Maintainability: modules have clear responsibilities and limited coupling.
- Testability: domain rules, ingestion and persistence are testable.
- Explainability: outputs can be traced to underlying records and rules.
- Reproducibility: processing and reporting retain sufficient execution context.
- Portability: local development does not depend on cloud services.

Performance targets will be set after representative workloads are defined.

## 8. Domain invariants
- A risk indicator is not an alert.
- An alert is not proof of wrongdoing.
- An investigation is not proof of guilt.
- An outcome must reference its investigation and supporting evidential basis.
- Evidence and outcomes are distinct concepts.
- Source identity and ingestion context must not be silently discarded.
- Exact duplicates and conflicting submissions must be distinguishable.
- Important status transitions and corrections must be traceable.
- Invalid data must not silently enter trusted reporting datasets.

## 9. Success definition
A reviewer can select a synthetic record and determine where it originated, when it was received, which validation rules were applied, what transformations occurred, which datasets depend on it and whether it is associated with risk information or an investigation.

Demonstrate this through working structures, processing behaviour, tests and reproducible queries—not documentation claims alone.

## 10. Approval boundaries
The Product Owner-approved project direction includes the modular-monolith architecture, SQL Server 2022 Developer Edition direction and full phased project scope, delivered incrementally.

The 25 November foundation is the historical baseline, not blanket approval of detailed design. Entity relationships, physical schema, lifecycle rules, source identity and duplicate/conflict semantics, retention and correction policy, security boundaries, proposed application technologies, implementation design and substantial implementation increments remain subject to review and Product Owner approval where material.
