# Domain Glossary

**Status:** Initial controlled vocabulary; definitions and lifecycle semantics require detailed domain-model review.

## Risk and compliance concepts

| Term | Definition | Important distinction |
|---|---|---|
| Risk | Potential exposure to an undesirable event or consequence | Not itself an alert or finding |
| Risk indicator | Observation, measure or signal associated with potential risk | Does not establish wrongdoing |
| Risk rule | Defined condition or assessment logic used to evaluate information | Not the alert it may generate |
| Alert | Recorded notification produced by a rule or authorised process | Not proof of wrongdoing |
| Investigation | Structured examination of an alert or other authorised referral | Does not imply guilt |
| Evidence record | Reference to information considered relevant to an investigation | Retain origin and context |
| Investigation outcome | Documented conclusion reached through an investigation | Requires identifiable evidential basis |
| Referral | Authorised request or event initiating review | Not necessarily a system-generated alert |
| Status transition | Recorded movement between permitted states | Preserve actor, time and reason where applicable |

## Data engineering concepts

| Term | Definition |
|---|---|
| Data source | Registered system, file producer or other origin of information |
| Source record | Record as identified by its originating source |
| Ingestion batch | Group of records received and processed as a unit |
| Ingestion record | Sentinel tracking representation of an individual received record |
| Pipeline run | Particular execution of an ingestion or processing workflow |
| Raw data | Source data preserved with its received context |
| Standardisation | Transformation into agreed formats and conventions |
| Validation rule | Explicit, identifiable test of a data requirement |
| Validation result | Recorded result of applying a rule to a record or dataset |
| Data-quality issue | Identified failure or concern against a quality requirement |
| Exact duplicate | Repeat submission whose defined identity and content match an existing submission |
| Conflicting record | Submission with matching business identity but materially different content |
| Data asset | Governed dataset, table, file or other managed information resource |
| Metadata | Information describing data, meaning, structure, ownership or use |
| Provenance | Information describing where data originated and how it was obtained |
| Lineage | Recorded relationships and transformations through which data moves |
| Audit event | Record of a significant system or business activity |
| Reporting snapshot | Identifiable point-in-time reporting output or dataset version |

## Critical distinctions

### Risk indicator versus alert
An indicator is an observation or signal. An alert is a notification generated because a defined condition or authorised process warrants attention. One indicator may contribute to multiple alerts; not every indicator must produce an alert.

### Alert versus investigation
An alert may be reviewed, dismissed, referred or investigated according to defined processes. An alert does not automatically create an investigation. An investigation may also originate from another authorised referral.

### Investigation versus outcome
An investigation is the examination process. An outcome is a recorded conclusion. Evidence records and investigation history remain distinguishable from the outcome.

### Evidence versus outcome
Evidence is information considered. An outcome is a conclusion based on an identifiable evidential basis. Evidence must not be rewritten as though it were the conclusion.

## Illustrative outcome vocabulary
Potential synthetic classifications for detailed review: Substantiated; Not substantiated; Inconclusive; Closed with no further action; Referred for further review.

These are proposed examples, not approved regulatory or institutional standards. Definitions, exclusivity, reopening rules and permitted transitions require domain design.

## Data quality dimensions
- Completeness: required information is present.
- Validity: values conform to defined formats, domains and rules.
- Accuracy: values agree with an appropriate authoritative reference or verification process.
- Consistency: related records and fields do not contradict defined rules.
- Uniqueness: duplicate identities are controlled.
- Timeliness: information is sufficiently current for its intended use.

A value passing format validation is not thereby proven factually accurate.

## Data organisation
- Bronze: preserved source-oriented data and ingestion context.
- Silver: validated, standardised data with quality issues represented.
- Gold: governed, curated data prepared for defined business and reporting uses.

These are logical layers; they do not require separate databases or physical infrastructure.

Use glossary terms consistently in database objects, code, API contracts, tests and documentation. Do not use Risk, Alert, Investigation and Outcome interchangeably.
