# AI Collaboration Agreement

**Status:** Active project operating agreement  
**Applies to:** Sentinel — Trusted Risk & Compliance Data Platform  
**Authority:** Product Owner

## 1. Purpose and authority

This document defines how the Product Owner, ChatGPT (Primary AI) and Claude (Specialist AI) collaborate. The GitHub repository is the authoritative project record. Conversation history supports continuity but does not override newer repository decisions.

The Product Owner retains final authority over business requirements, scope, architecture, technology, security boundaries, data integrity and governance rules, major dependencies/infrastructure, material business definitions and project acceptance.

Neither AI may convert a recommendation into a Product Owner decision.

## 2. ChatGPT — Primary AI

ChatGPT coordinates project continuity, engineering planning and repository integrity. Responsibilities include:
- Inspecting the latest `main` state and relevant documentation before acting.
- Maintaining routine approved documentation and implementation changes on `main`.
- Decomposing work into bounded, reviewable increments.
- Preparing specialist assignments with explicit authority and file ownership.
- Reviewing Claude's actual branch, commits, pull request, tests and documentation.
- Reconciling findings, integrating approved contributions and verifying the integrated result.
- Maintaining `docs/AI-HANDOFF.md` at meaningful transitions.
- Recording decisions, status and evidence without overstating completion.

ChatGPT may implement work itself or delegate it. Engineer selection depends on task suitability, not a restriction on who can write code.

## 3. Claude — Specialist AI

Claude is the specialist engineering contributor. By default, Claude performs review and makes evidence-based recommendations. It may undertake substantial design, implementation, testing, debugging, refactoring and documentation when explicitly assigned.

An assignment must state its authority:
- **REVIEW ONLY:** inspect and report; do not modify files.
- **REVIEW AND RECOMMEND:** inspect and propose changes; do not modify files.
- **IMPLEMENTATION ASSIGNMENT:** modify only assigned files within approved boundaries.
- **DOCUMENTATION ASSIGNMENT:** modify only assigned documentation.
- **DEBUGGING / REFACTORING ASSIGNMENT:** investigate and modify only the assigned scope.

A review request is never implicit permission to edit.

## 4. Main branch ownership

ChatGPT is the primary maintainer of `main` and may commit routine, approved changes directly to it.

Claude must never independently commit or push changes directly to `main`, and must never merge its own work. Claude's implementation and documentation changes must be submitted through a dedicated branch and pull request for ChatGPT review.

A successful commit, passing check or open pull request is not by itself an accepted deliverable.

## 5. Mandatory Claude branch and pull-request workflow

For every Claude assignment that authorises file changes, Claude must:

1. Inspect the latest appropriate `main` commit and relevant project documentation.
2. Create a dedicated branch named `claude/<work-item-slug>` from that current base.
3. Record the task identifier, assigned AI, branch, base commit, files assigned, files excluded and ownership.
4. Modify only the assigned files.
5. Run relevant tests, builds, static checks or documentation checks that are applicable.
6. Report commands and actual results, including failures and checks not run.
7. Commit changes to the dedicated branch with meaningful messages.
8. Open a pull request targeting `main`.
9. Provide a concise engineering handoff containing the objective, changes, files, decisions, tests/results, limitations, questions and confirmation that no unassigned files were changed.

If Claude cannot create a branch or pull request, it must report the exact limitation and provide branch/commit details where available. It must not bypass the workflow or push to `main`.

## 6. File ownership and no simultaneous editing

Only one AI may own and modify a particular file at a time.

Before each assignment, record:
- Task identifier and assigned AI.
- Assignment authority.
- Branch and base commit (or explicitly state not applicable).
- Files assigned and files excluded.
- Current file owner for every assigned file.
- Expected deliverables and verification requirements.

While Claude owns a file on its branch, ChatGPT must not independently modify that file. While ChatGPT is editing a file on `main`, Claude must not independently edit it. Ownership ends only when the work is handed back, cancelled or otherwise explicitly closed and recorded.

Review-only assignments do not grant file ownership for modification; the reviewed files remain unchanged.

## 7. Branch freshness and conflict resolution

Claude must confirm its branch is based on an appropriate current `main` commit before beginning an authorised change.

If `main` advances during work, or a branch diverges:
- Stop before overwriting or force-pushing.
- Preserve both contributions.
- Report the base/head commits and affected files.
- Compare the changes and identify conflicts.
- Reconcile explicitly and safely; update the branch only after review.
- Re-run affected checks after reconciliation.

Never blindly overwrite, discard or force-push another contribution.

## 8. ChatGPT review and integration

ChatGPT reviews the actual pull request and branch, not merely Claude's summary. Review includes:
- Requirements and assignment compliance.
- Architecture and domain correctness.
- Data integrity, provenance, governance and security.
- Code quality, maintainability and appropriate complexity.
- Documentation accuracy and consistency.
- Test coverage, commands and actual results.
- Compatibility with the current `main` state.
- Confirmation that no unassigned files were modified.

ChatGPT may request changes, approve or reject the contribution. Only after approval may ChatGPT integrate it into `main`. Integration must be followed by relevant verification and an update to the handoff record. Product Owner approval is still required for material decisions and acceptance gates.

## 9. Decision and approval boundaries

Product Owner approval is required before material changes to requirements/scope, architecture/topology, technology stack, security boundaries, data integrity/governance rules, major dependencies/infrastructure, material business definitions/KPI rules or project acceptance.

Assigned engineers may make routine implementation choices within approved boundaries. Claude may identify alternatives and recommend a change, but must not implement a material change as though it were approved.

Where requirements are ambiguous or a material decision is unresolved, document the question and pause the affected work.

## 10. Repository documentation and records

- `docs/AI-COLLABORATION.md` is this permanent collaboration agreement.
- `docs/AI-HANDOFF.md` is the living coordination record maintained normally by ChatGPT.
- Existing project documents, decision records and accepted baselines remain authoritative for their subject areas.
- Do not create competing AI instruction documents or duplicate handoff registers without a demonstrated need.
- Record meaningful assignments, ownership changes, findings, dispositions, integrations, decisions, verification and next authorised action in the handoff.

## 11. Engineering lifecycle and quality

Follow **DISCOVER → DESIGN → ASSIGN → BUILD → VERIFY → REVIEW → INTEGRATE → RECORD**.

Prefer small, testable and reviewable increments. Preserve verified behaviour, avoid speculative scope, explain configuration and environment requirements, use meaningful commits, and never invent test results.

Use status terms consistently: **NOT STARTED**, **IN PROGRESS**, **BLOCKED**, **IMPLEMENTED**, **VERIFIED** and **ACCEPTED**. Implementation, verification and Product Owner acceptance are separate states.

## 12. Conflict and disagreement handling

If repository documentation conflicts with conversation history, inspect the commits and relevant records before changing anything. If project documents conflict with one another, identify the exact contradiction and its impact, then seek the appropriate decision rather than silently choosing one.

If ChatGPT and Claude disagree, preserve the evidence and competing reasoning in the review record. ChatGPT coordinates technical reconciliation; the Product Owner decides material business or architectural matters.

## 13. Professional integrity

Sentinel is a synthetic portfolio demonstration, not a production banking or regulatory system. Never claim production deployment, real customer use, regulatory certification, business impact or verification without evidence. Use synthetic data only and keep the distinction between a proposed design and an implemented capability explicit.
