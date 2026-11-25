# Conceptual Data Model

**Status:** Initial conceptual proposal. Not an approved physical schema. No database objects have been created.

## 1. Modelling objectives
Support source traceability, controlled ingestion, validation, governance, risk information, investigations, evidence and audit history. Preserve the distinction between a risk indicator, an alert, an investigation and an investigation outcome. Prefer explicit relationships and integrity constraints over speculative generalisation.

## 2. Conceptual entity catalogue

| Area | Entity | Responsibility |
|---|---|---|
| Source | DataSource | Identifies a registered source |
| Source | SourceRecord | Preserves source record identity and reference |
| Ingestion | IngestionBatch | Groups records received together |
| Ingestion | IngestionRecord | Tracks an individual received record |
| Processing | PipelineRun | Records a processing execution |
| Quality | ValidationRule | Defines a versioned validation requirement |
| Quality | ValidationExecution | Records application of rules in a run |
| Quality | ValidationResult | Stores an individual rule result |
| Quality | DataQualityIssue | Tracks an identified issue and resolution |
| Governance | DataAsset | Registers a governed dataset or resource |
| Governance | DataOwner | Identifies accountable ownership |
| Governance | DataClassification | Defines a controlled classification |
| Governance | BusinessGlossaryTerm | Registers controlled business definitions |
| Lineage | LineageNode | Represents a source, dataset or processing asset |
| Lineage | LineageEdge | Records a directed lineage relationship |
| Risk | RiskIndicator | Stores an observation associated with potential risk |
| Risk | RiskRule | Defines synthetic monitoring conditions |
| Risk | Alert | Records a notification and triggering context |
| Investigation | Investigation | Represents an examination |
| Investigation | InvestigationAlert | Associates alerts with investigations |
| Investigation | EvidenceRecord | References supporting information |
| Investigation | InvestigationOutcome | Records a documented conclusion |
| Audit | AuditEvent | Records significant actions and changes |
| Reporting | ReportingSnapshot | Identifies a reproducible reporting output |

This catalogue is conceptual. Detailed design may combine, split or represent concepts differently where justified.

## 3. Proposed relationships
- A DataSource can have many IngestionBatches.
- An IngestionBatch belongs to one DataSource and contains many IngestionRecords.
- An IngestionRecord retains its source record identity and received context.
- A PipelineRun can process many records and produce identifiable outputs.
- A ValidationRule can be applied many times.
- A ValidationExecution records a rule's application within a processing context and has ValidationResults.
- A ValidationResult refers to its evaluated target and may create or update a DataQualityIssue.
- A DataAsset can have an owner and classification according to governance rules.
- LineageEdges connect identifiable LineageNodes.
- A RiskIndicator may be associated with one or more Alerts.
- An Alert may be associated with zero or more Investigations.
- An Investigation may be linked to multiple Alerts through InvestigationAlert.
- An Investigation can have multiple EvidenceRecords.
- An Investigation can have a history of outcome records; current outcome and supersession semantics must be specified.
- AuditEvents refer to identifiable subjects and actors where available.
- ReportingSnapshots identify reporting period, execution and source dataset versions.

These relationships require detailed cardinality and lifecycle review.

## 4. Critical integrity requirements
1. Every ingestion batch identifies its source.
2. Every ingestion record identifies its batch and source record context.
3. Validation results identify the rule version and evaluated target.
4. Processing outputs identify the relevant pipeline execution.
5. Every risk indicator has an identifiable origin.
6. Every alert records its triggering rule or authorised creation reason.
7. Every investigation records its initiation reason.
8. Every outcome identifies its investigation and supporting evidence references.
9. Important status changes retain attributable history.
10. Corrections must not silently erase history needed to explain prior processing or decisions.

## 5. Investigation and outcome design
EvidenceRecord and InvestigationOutcome are separate concepts. An investigation may reference multiple evidence records. An outcome should capture its identifier, investigation, classification, decision timestamp, responsible actor, rationale and supporting evidence references.

The detailed model must decide whether outcomes are append-only records, versioned decisions or both. Reopening an investigation and superseding an outcome must not erase historical decisions.

## 6. Duplicate and conflict identity
Duplicate handling requires explicit identity rules. A content hash alone does not define business identity. Distinguish:
- Repeated delivery of the same source record.
- Same source identity with changed content.
- Different source records representing the same business event.
- Similar records that are not duplicates.

Define idempotency scope, conflict resolution and whether corrected source submissions are new versions.

## 7. Physical design still required
Specify primary and foreign keys; cardinalities and optionality; unique constraints and natural-key scope; status reference data and transitions; timestamp semantics and time-zone handling; numeric precision and currency representation where relevant; raw payload format and limits; indexes based on query patterns; retention, correction and deletion behaviour; transaction boundaries and concurrency expectations.

## 8. Design boundary
This is a conceptual model only. It does not claim that tables, migrations, stored procedures or application entities exist. Physical schema design requires separate review and Product Owner approval before implementation.
