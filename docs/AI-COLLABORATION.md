# FNEOS Collaboration Agreement — Sentinel

**Status:** Active and Product Owner-approved  
**Effective:** 27 November 2026  
**Authority:** Product Owner  
**Repository:** `obakengshepherd/SENTINEL-TRUSTED-RISK-COMPLIANCE-DATA-PLATFORM`

## 1. Purpose, authority and source of truth

This agreement governs the collaboration between the Product Owner, ChatGPT (Primary AI) and Claude (Specialist AI) for Sentinel.

The GitHub repository is the authoritative shared project record. The Product Owner has final authority over business requirements, scope, architecture, technology, security boundaries, data integrity rules, major dependencies, infrastructure commitments and project acceptance. Neither AI may convert a recommendation into a Product Owner decision.

The historical reset baseline is commit `82cb85867e3698b074714d076fb8e49fd4012cb4` (25 November 2026). Workflow arrangements and documentation changes introduced on 26 November are superseded by this agreement. Valid pre-cutoff requirements, architecture and project decisions remain in force. Git history is preserved.

## 2. Mandatory three-stage workflow

### Stage 1 — ChatGPT: Architecture and documentation

ChatGPT is the Primary AI and principal architecture, documentation and integration owner. Responsibilities:
- System architecture, requirements and technical specifications.
- README and all project documentation, including the decision register and handoff.
- Architecture decisions, change control and implementation plans.
- Acceptance criteria and Claude assignment preparation.
- Documentation maintenance and main-branch governance.
- Return/alignment checkpoint, integration review and final documentation synchronisation.
- Evidence-based project status and completion reporting.

ChatGPT owns project documentation. Claude may read and review all documentation but may not modify it unless the Product Owner explicitly approves a documented ownership transfer for specific files and a defined period/scope.

### Stage 2 — Claude: Specialist engineering and code

Claude is the Specialist AI. By default, Claude independently reviews architecture, domain design, technical risks and omissions. Claude may implement code only against a bounded assignment prepared by ChatGPT and authorised by the Product Owner where required.

Every implementation assignment must specify:
- Task ID, objective and approved requirements/design reference.
- Exact repository-relative code file paths Claude owns.
- Files and areas explicitly excluded.
- Expected complete code-file deliverables.
- Relevant tests, build/check expectations and execution instructions.
- Configuration/environment assumptions and dependencies.
- Any decisions Claude may make within scope and matters requiring escalation.

Claude must:
- Return complete code files in its chat, with exact paths.
- Explain implementation choices and relevant trade-offs.
- Supply tests and precise execution instructions.
- Report commands actually run and their real results; identify checks not run.
- Identify assumptions, limitations, errors and unresolved questions.
- Stop and request direction when implementation would require an unapproved material change.

Claude must not:
- Push or commit directly to GitHub.
- Modify ChatGPT-owned documentation.
- Modify files outside its explicit code assignment.
- Create or use a branch unless the Product Owner explicitly authorises branch-based work.
- Treat a review request as permission to implement or edit.
- Claim verification based on tests it did not run.

### Stage 3 — Product Owner, VS Code and ChatGPT: Assembly and integration

The Product Owner:
- Places Claude's returned code files into the local VS Code workspace.
- Runs the application, builds and tests.
- Supplies actual results, errors, relevant diffs and local Git information to ChatGPT.

ChatGPT:
- Performs the mandatory return/alignment checkpoint before issuing another implementation assignment.
- Reviews supplied changes against the approved assignment and current repository.
- Identifies omissions, inconsistencies, blockers and integration risks.
- Resolves integration issues with the Product Owner.
- Integrates approved changes into `main` and updates project documentation/status.
- Reports the actual repository commit and verification evidence.

ChatGPT cannot inspect uncommitted local files or local test results unless the Product Owner supplies them. It must not imply otherwise.

## 3. Zero-overlap file ownership

There must be exactly one active AI modification owner for each file.

- ChatGPT owns all project documentation and repository governance records.
- Claude owns only the exact code files explicitly assigned for the active engineering task.
- Claude's read-only review of documentation does not transfer file ownership.
- Neither AI may simultaneously modify the same file.
- Ownership begins when an assignment is explicitly activated and ends when the work is returned, cancelled or closed and recorded.
- Any documentation ownership transfer requires explicit Product Owner approval naming the files, scope and duration.

The assignment and handoff record must list file paths, owners, access mode and exclusions.

## 4. Branch, commit and main-branch governance

Branch-based work is prohibited unless the Product Owner explicitly authorises it for a named task.

Claude must not push or commit directly to GitHub under any circumstances in the standard workflow. Claude returns code files in chat for user-led assembly.

ChatGPT maintains `main) and may make normal, approved documentation and integration commits directly to it. Before each repository change, ChatGPT inspects the latest `main) and affected files. It must preserve history: no force-push, history rewrite or deletion of historical commits.

If the Product Owner explicitly authorises a branch exception, the authorisation must define who may create/use the branch, its purpose and integration route. That exception does not transfer documentation ownership or permit Claude to push directly.

## 5. Mandatory return/alignment checkpoint

Whenever the Product Owner returns after working with Claude or assembling code locally, ChatGPT must first:

1. Establish and record the latest `main) commit.
2. Inspect the repository state and relevant changes.
3. Compare the supplied implementation against the approved task and exact assigned file list.
4. Review actual test/build results supplied by the Product Owner.
5. Identify inconsistencies, omissions, unapproved changes and blockers.
6. Confirm alignment or explicitly state what remains unresolved.

Do not issue the next implementation assignment until this checkpoint is complete. Do not claim visibility into uncommitted local changes that were not supplied.

## 6. Change control

Product Owner approval is required before material changes to:
- Business requirements or project scope.
- Architecture or system boundaries.
- Technology stack.
- Security boundaries and access policy.
- Data integrity, identity, duplicate/conflict or lifecycle rules.
- Major dependencies or infrastructure commitments.
- Material domain definitions or acceptance criteria.

Routine engineering decisions may be made by the assigned AI only within the approved design and assignment boundaries. Record material approved decisions in `docs/DECISIONS.md`. Preserve superseded decisions rather than erasing history.

## 7. Engineering lifecycle and quality

Follow **DISCOVER → DESIGN → BUILD → VERIFY → REVIEW → RECORD**. Apply the three collaboration stages to that lifecycle.

Priorities: correctness, simplicity, maintainability, security, reliability, testability, explainability and practical business value. Avoid complexity for appearance. Work in bounded increments, preserve verified functionality, use meaningful changes, explain setup and configuration, and never invent test results.

Use status vocabulary consistently:
- **NOT STARTED:** work has not begun.
- **IN PROGRESS:** work is actively underway.
- **BLOCKED:** a dependency or issue prevents progress.
- **IMPLEMENTED:** the change has been made.
- **VERIFIED:** defined checks have actually passed and evidence is available.
- **ACCEPTED:** the Product Owner has accepted the deliverable.

Implementation, verification and Product Owner acceptance are separate states.

## 8. Assignments and specialist reviews

Claude reviews architecture by default. A review assignment must explicitly state REVIEW ONLY, its scope, expected report and stop condition. It does not grant file modification ownership.

An implementation assignment must be bounded, refer to an approved design, list exact code files and state verification expectations. If the design is not approved or a material question is open, stop and return the question rather than silently choosing.

## 9. Repository documentation and handoff

- `docs/AI-COLLABORATION.md` is the permanent FNEOS collaboration agreement maintained by ChatGPT.
- `docs/AI-HANDOFF.md` is the living project state, assignment, ownership, checkpoint and next-action record maintained by ChatGPT.
- `docs/DECISIONS.md` is the decision register.
- Existing project documents remain authoritative for their subject matter.
- Avoid duplicate instructions, handoffs and registers.

At meaningful transitions, update the handoff with the actual main commit, phase/status, assignment state, file ownership, decisions, verification evidence, blockers and next authorised action.

## 10. Disagreement, safety and professional integrity

If repository documentation conflicts with conversation history, inspect the relevant historical and current commits. The Product Owner decides material business and architectural questions. Preserve evidence and explain competing technical reasoning.

Sentinel is a synthetic portfolio demonstration, not a production banking, fraud, AML or regulatory system. Use synthetic data only. Never claim production deployment, regulatory certification, real customer use, business impact, implementation or verification without evidence.
