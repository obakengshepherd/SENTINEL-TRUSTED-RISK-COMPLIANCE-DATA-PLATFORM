# Provenance and Data Lineage

**Status:** Initial approach. Physical implementation and detailed lineage granularity require design approval.

## 1. Purpose
Sentinel must explain where information originated, how it entered the platform, which processing operations affected it and which downstream datasets use it.

Provenance describes origin and acquisition context. Lineage describes relationships and transformations through the data lifecycle. They are related but not interchangeable.

## 2. Provenance metadata

| Attribute | Purpose |
|---|---|
| Data source ID | Identifies the registered source |
| Source record ID | Preserves source record identity |
| Ingestion batch ID | Identifies the received batch |
| Ingestion record ID | Identifies Sentinel's tracking record |
| Received timestamp | When Sentinel received the record |
| Source timestamp | When the source created or changed it, if supplied |
| Content hash | Supports integrity checks and exact-content comparison |
| Pipeline run ID | Identifies relevant processing execution |
| Processing status | Records current processing state |
| Source file/reference | Identifies submitted input where appropriate |

Timestamp meanings and time-zone handling must be explicit. A source timestamp must not be substituted for a received timestamp.

## 3. Raw-data preservation
Preserve the original received payload or a faithful, controlled representation alongside its metadata. Do not silently replace raw data with standardised output.

Physical storage format, size limits, access controls, retention and correction policy require detailed design. Raw payload preservation must not become an excuse to retain unnecessary or sensitive information.

## 4. Dataset-level lineage
Initial lineage identifies source assets, processing steps and output assets.

Illustrative flow:

Transaction Source → Raw Transactions → Validated Transactions → Standardised Transactions → Risk Monitoring Dataset → Risk Reporting

Represent lineage as directed relationships with identifiable inputs, outputs, processing operation and execution context. Do not claim field-level lineage until implemented.

## 5. Record-level traceability
Introduce progressively. For a selected record, the target capability is to identify:
- Original source and source record identity.
- Ingestion batch and received timestamp.
- Validation rules and results.
- Processing run and transformation references.
- Destination record or dataset.
- Related risk indicator, if any.
- Related alert or investigation, if any.

Distinguish direct relationships from inferred associations.

## 6. Pipeline execution context
A pipeline run should retain enough context to explain its identifier and pipeline/version, start and completion timestamps, trigger or initiating actor, input and output references, processing status, counts received/accepted/rejected/skipped, failure or exception references, and relevant rule or configuration versions.

Counts must reconcile according to explicitly defined processing semantics.

## 7. Integrity and hashes
A cryptographic content hash can help detect exact-content repetition or unexpected changes. It does not by itself prove source authenticity, business identity or factual accuracy. Specify algorithm, canonicalisation and comparison scope in technical design.

## 8. Lineage acceptance scenarios
A reviewer should be able to select a curated reporting record, identify its source dataset, find the relevant processing run, inspect validation outcomes, follow the transformation path and identify related risk information without conflating entity types.

## 9. Implementation boundary
Start with batch, record and dataset-level traceability. Add finer-grained lineage only where a demonstrated use case justifies its storage and maintenance cost.
