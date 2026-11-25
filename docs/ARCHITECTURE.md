# Architecture

**Status:** Modular-monolith direction approved. Detailed technical design remains subject to review.

## 1. Architecture decision
Sentinel will use a modular monolith: one application and deployment boundary with explicit internal modules and responsibilities. This supports separation of concerns, testability and maintainability without distributed infrastructure.

Do not decompose the application into microservices merely to appear enterprise-grade.

## 2. Logical modules

| Module | Responsibility |
|---|---|
| Ingestion | Source registration, batch intake and record receipt |
| Data Quality | Validation rules, executions, results and issues |
| Governance | Data assets, definitions, ownership and classification |
| Provenance and Lineage | Source references and transformation relationships |
| Risk Information | Risk indicators, rules and alerts |
| Investigation Management | Investigations, evidence references and outcomes |
| Audit | Significant activities, status transitions and attribution |
| Reporting | Curated queries, snapshots and monitoring outputs |

Modules may share a relational database. Their business responsibilities and allowed dependencies must be explicit.

## 3. Technology direction

| Concern | Direction | Status |
|---|---|---|
| Language | C# | Proposed |
| Runtime/framework | .NET 10 LTS | Proposed; verify SDK and compatibility |
| Database | SQL Server 2022 Developer Edition | Product Owner approved |
| Data access | Dapper / ADO.NET and explicit SQL | Proposed |
| API | ASP.NET Core | Proposed |
| Tests | xUnit | Proposed |
| Development | VS Code and SSMS | Proposed |
| Version control | Git and GitHub | Established |
| Reporting | SQL views initially; Power BI if justified | Later phase |
| Containers | Optional local reproducibility aid | Not yet approved as dependency |

SQL Server 2022 Developer Edition is for development and testing, not production. Verify installed SDK, target framework and package compatibility before solution creation.

## 4. Data organisation
Use Bronze / Silver / Gold as logical processing layers:
- Bronze: source-oriented payloads and ingestion context preserved.
- Silver: validated and standardised records, with quality issues represented.
- Gold: governed datasets and reporting-ready outputs.

Do not create separate databases, storage accounts or distributed services for these layers without demonstrated need.

## 5. Processing flow
1. Receive a file or synthetic source submission.
2. Register source and ingestion context.
3. Preserve received payload and source identity.
4. Validate structure and business rules.
5. Classify records as accepted, rejected or requiring controlled exception handling.
6. Standardise eligible records.
7. Record pipeline execution and lineage.
8. Publish governed outputs for risk and reporting use.
9. Record relevant audit events and processing metrics.

Transaction boundaries, retry behaviour and partial-batch semantics require detailed design.

## 6. Data access and transactions
Use explicit SQL for important persistence and processing where it improves clarity and control. Dapper or ADO.NET are candidate approaches; final selection should consider consistency, maintainability, testability and dependency cost.

Transactions must protect operations requiring atomicity. Define idempotency and concurrency rules before implementing ingestion.

## 7. Security direction
Use synthetic data only. Define least-privilege database access and protect secrets through local configuration excluded from version control. Do not commit credentials or secret-bearing connection strings.

Introduce authentication and role-based authorisation when access boundaries and use cases are defined, not as speculative infrastructure.

## 8. Observability and failure handling
Expose identifiable run IDs, timestamps, outcomes, counts and failure details. Errors must be diagnosable without leaking sensitive payloads into logs. Failed operations must not be reported as successful.

## 9. Explicit exclusions
No initial requirement justifies Kafka, RabbitMQ, Kubernetes, multiple independently deployed services, machine-learning infrastructure or mandatory cloud deployment. Reconsider only through a documented requirement and Product Owner approval.

## 10. Verification
Before implementation, verify the local .NET SDK, SQL Server edition/version, connectivity and package compatibility. Diagrams are logical descriptions and do not represent implemented components.
