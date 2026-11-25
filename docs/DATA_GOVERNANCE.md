# Data Governance and Quality

**Status:** Initial principles. Retention, access and correction policies require detailed approval.

## 1. Purpose
Governance must be demonstrated through data structures, controls, ownership, validation and traceable operations—not documentation alone. All demonstration data must be synthetic.

## 2. Governance principles
- Ownership: governed data assets have an identifiable accountable owner or role.
- Accountability: significant actions are attributable to an actor or system identity.
- Classification: assets and fields receive controlled classifications where appropriate.
- Quality: validation requirements are explicit, versioned and measurable.
- Metadata: datasets and important fields have understandable definitions.
- Integrity: database constraints protect important relationships.
- Traceability: source and processing context remain discoverable.
- Controlled change: material changes to definitions, rules and data are reviewable.
- Transparency: processing and limitations are documented.
- Purpose limitation: information is used only for its defined demonstration purpose.

## 3. Proposed classification vocabulary
Public; Internal; Confidential; Restricted.

These are project-defined examples and do not claim to reproduce a particular institution's official classification scheme. Classification criteria and handling controls must be specified before sensitive categories are used.

## 4. Data quality dimensions

| Dimension | Meaning | Example control |
|---|---|---|
| Completeness | Required values are present | Required identifier is not null or blank |
| Validity | Values conform to rules | Timestamp parses and is within permitted bounds |
| Accuracy | Values agree with a suitable reference | Code matches an authoritative synthetic reference dataset |
| Consistency | Related values agree | Related records satisfy defined business constraints |
| Uniqueness | Duplicate identities are controlled | Source identity is unique within its defined scope |
| Timeliness | Data is current enough for its purpose | Source event age is within a defined threshold |

Passing a format check does not prove factual accuracy. Accuracy checks require a suitable reference or verification process.

## 5. Validation rule metadata
A rule should have a stable ID and name, description and rationale, target asset or field, version, severity, effective state, execution timestamp, pipeline run, result and failure details, and evaluated record references.

Rule changes must not make historical results impossible to interpret.

## 6. Quality issue lifecycle
Detailed design must define issue states, ownership, resolution evidence and reopening behaviour. Candidate states include Open, Assigned, Resolved, Accepted Exception and Closed. These are proposed labels, not approved transition rules.

An accepted exception must remain visible and must not be misrepresented as a passing validation result.

## 7. Ownership and metadata
For each governed asset, consider business name and technical identifier, description and intended use, owner role, classification, source and lineage references, quality expectations, retention category, and created/last-reviewed timestamps.

Business glossary definitions should be controlled and reused consistently.

## 8. Integrity, correction and retention
Distinguish correction from silent overwriting. The detailed policy must decide how to preserve prior values, record correction reasons, handle deletion requests and retain evidence.

Retention periods must not be invented. They will be explicit project assumptions for synthetic data and documented before implementation. Audit and evidence records need defined protection against unauthorised alteration.

## 9. Access and security
Use least privilege. Separate application, processing and administrative permissions where justified. Keep secrets out of source control. Logs should avoid unnecessary raw payloads and sensitive data.

## 10. Governance acceptance evidence
Demonstrate registered assets, definitions, ownership, classifications, versioned rules, recorded validation outcomes, visible exceptions, traceable corrections and attributable audit events. Do not claim compliance certification or production regulatory suitability.
