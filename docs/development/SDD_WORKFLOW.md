# SMART IT ACADEMY — Hybrid Spec-Driven Development Workflow

**Status:** Working process proposal  
**Audience:** Project owner, developers, Codex, and other approved AI coding agents  
**Applies to:** The SMART IT ACADEMY application repository  
**Last reviewed:** November 14, 2026

> This document describes the intended development process. It does not approve a feature, change the application repository, or replace the project's current instructions. The project owner must approve project-specific governance and feature decisions.

## 1. Purpose

This guide establishes a repeatable Hybrid Spec-Driven Development (SDD) lifecycle for SMART IT ACADEMY.

The approach combines:

- Existing project documentation as the source of business and technical context.
- A Project Constitution for durable principles and constraints.
- AGENTS.md for repository-specific instructions to coding agents.
- GitHub Spec Kit for structured specification, planning, task generation, and convergence.
- Codex as the primary AI coding agent.
- Human approval for business decisions, scope changes, risky operations, and release acceptance.
- Automated and manual verification as evidence that requirements have been met.

The objective is not to create more documents for their own sake. It is to make each important requirement traceable to a design decision, implementation task, and verification result.

## 2. Core principles of the workflow

1. **Understand before changing.** Inspect the repository, current branch, uncommitted changes, applicable instructions, and relevant feature context before planning or editing.
2. **Specify behavior before technology.** A feature specification describes the problem, users, behavior, rules, and acceptance criteria. Technology choices belong in the technical plan.
3. **Preserve existing work.** Do not overwrite existing instructions, migrations, user changes, or approved contracts without inspection and explicit authorization.
4. **Human owner controls business decisions.** Agents may identify options and recommend a choice, but must not silently invent policy or treat an unapproved recommendation as an approved decision.
5. **Implement in small, reviewable tasks.** Each task should have a clear outcome, dependencies, scope, and validation method.
6. **Test observable behavior.** A successful compile does not prove that a feature satisfies its requirements.
7. **Keep evidence.** Record tests actually executed, their outcomes, known gaps, and the environment used.
8. **Replan when facts change.** Update specifications and plans when approved requirements change; do not let code and documentation drift apart.
9. **Protect users and data.** Apply privacy, security, access-control, and data-retention requirements throughout design, implementation, and validation.
10. **Never claim completion without evidence.** Distinguish implemented, tested, reviewed, accepted, and released states.

## 3. Project-level governance

Project-level governance is established once and maintained as the project evolves.

| Artifact | Purpose | Source-of-truth responsibility |
|---|---|---|
| Project Constitution | Durable principles, quality bars, and non-negotiable constraints | Project governance |
| AGENTS.md | Instructions for coding agents, repository commands, and working conventions | Agent operating instructions |
| PROJECT_ROADMAP.md | Product phases, scope, dependencies, priorities, and milestones | Product direction |
| ARCHITECTURE.md | System structure, module boundaries, and technical rationale | Architecture |
| DATABASE_DESIGN.md | Database model, integrity rules, migration strategy, and data lifecycle | Data design |
| API documentation / OpenAPI | Externally observable API contracts | API behavior |
| Progress report | Current state, completed work, open risks, and next actions | Delivery status |
| ADRs / decision records | Durable decisions and their rationale | Decision history |

Do not maintain duplicate competing definitions. If one fact must appear in several documents, identify its authoritative source and keep secondary references concise.

## 4. Feature-level SDD lifecycle

Use the full workflow for production features and features involving security, personal information, payments, authorization, or database changes.

### Step 0 — Select and inspect the feature

Before creating artifacts:

- Identify the feature and its intended product outcome.
- Read the relevant roadmap and progress records.
- Read the Constitution, AGENTS.md, and any applicable nested instructions.
- Inspect existing implementation and tests related to the feature.
- Inspect the Git branch and working tree.
- Identify related API contracts, database migrations, and upstream/downstream dependencies.
- Record what is already implemented so the feature is not accidentally redesigned or duplicated.

**Output:** A short feature intake and repository-state summary.

**Gate:** Do not begin implementation while relevant existing changes or requirements are unknown.

### Step 1 — Specify the feature

Use the feature specification to define:

- Problem statement and business value.
- Target users and actors.
- Scope and explicit out-of-scope items.
- User stories and observable behavior.
- Functional requirements with stable IDs, such as FR-001.
- Non-functional requirements with stable IDs, such as NFR-001.
- Business rules and constraints.
- Main flows, alternative flows, errors, and edge cases.
- Privacy and security expectations.
- Acceptance criteria with stable IDs, such as AC-001.
- Dependencies and assumptions.
- Open questions that require owner decisions.

Focus on **what** the system must do and **why**. Avoid prescribing code structure or database implementation before the requirements are clear.

**Output:** spec.md and a list of unresolved questions.

### Step 2 — Clarify and approve requirements

Review ambiguities with the project owner. Prioritize questions that affect:

- Business policy or eligibility.
- User roles and permissions.
- Data collection, consent, retention, or deletion.
- API request/response behavior.
- Financial calculations or payment handling.
- Failure behavior and retry semantics.
- Compatibility and migration requirements.

Record each important decision with:

- Decision ID.
- Question and context.
- Options considered.
- Selected decision.
- Rationale.
- Owner and decision date.
- Affected requirements and artifacts.

A proposal is not an approved decision. Mark status explicitly as Proposed, Approved, Rejected, or Superseded.

**Output:** Updated spec.md and decisions.md (or the project's established decision record).

**Gate:** Do not design or implement around a business-critical unresolved decision.

### Step 3 — Create the technical plan

Only after the requirements are clear, prepare the plan. It should address relevant topics such as:

- Existing architecture and module boundaries.
- Backend services, components, and responsibilities.
- Frontend pages, state, accessibility, and localization.
- API contracts and error behavior.
- Database entities, relationships, constraints, and indexes.
- Flyway migration impact and rollback/recovery considerations.
- Authentication, authorization, privacy, and security controls.
- Logging, audit events, and personal-data handling.
- Performance and reliability considerations.
- Test strategy and test data.
- Deployment/configuration impact.
- Compatibility with existing features.

Reuse existing project architecture and approved contracts. Document proposed changes and trade-offs rather than assuming they have already been accepted.

**Output:** plan.md and supporting design artifacts, such as data-model.md, research.md, contracts/, or quickstart.md when appropriate.

**Gate:** Owner reviews material business, architecture, schema, security, and compatibility decisions.

### Step 4 — Quality-check the specification and plan

Before task breakdown and implementation:

- Check that requirements are clear, testable, and not contradictory.
- Check that the plan addresses every in-scope requirement.
- Check that API, frontend, backend, and database contracts agree.
- Check that privacy/security requirements have corresponding controls.
- Check that migrations preserve existing data and migration history.
- Check that out-of-scope work has not slipped into the feature.
- Resolve critical findings and repeat the analysis.

**Output:** Requirements checklist and consistency-analysis result.

**Gate:** No unresolved critical contradiction or high-impact ambiguity.

### Step 5 — Break the plan into tasks

Create small, ordered tasks with:

- Task ID.
- Description and expected outcome.
- Requirement/acceptance-criteria references.
- Files or components likely to be affected.
- Dependencies.
- Implementation notes and constraints.
- Verification command or test expectation.
- Completion checkbox.

Separate backend, frontend, database, documentation, and verification work where helpful. Keep migration tasks explicit. Avoid overly broad tasks such as "finish registration feature."

**Output:** tasks.md.

### Step 6 — Owner approval before implementation

Before editing application code, confirm:

- The specification is approved.
- Material decisions are approved.
- The technical plan is approved.
- Tasks are sufficiently small and ordered.
- Risks and rollback/recovery considerations are understood.
- The implementation scope and permitted environment are clear.

The owner may approve all work, approve one task group, request changes, or reject the plan.

**Gate:** No implementation on the basis of a draft or ambiguous plan.

### Step 7 — Implement with Codex / AI coding agents

For each approved task group:

1. Re-read the relevant specification, plan, tasks, Constitution, and agent instructions.
2. Confirm Git branch and working-tree state.
3. Make a focused change.
4. Run the narrowest relevant test.
5. Review the diff for correctness, security, scope, and maintainability.
6. Update task status only when the task's completion evidence exists.
7. Summarize files changed, decisions made, tests run, and remaining risks.

Use one primary agent to coordinate changes. Parallel agents are optional and should only be used when file ownership and task boundaries are independent and explicit.

**Output:** Code changes, tests, and task updates.

### Step 8 — Feature validation

Validation checks the actual application against the approved acceptance criteria.

Depending on the feature, perform:

- Backend unit and integration tests.
- Frontend component and form tests.
- Database migration and repository tests using a disposable test database.
- API contract and authorization tests.
- End-to-end tests for critical user journeys.
- Security and privacy checks.
- Build, lint, and static analysis.
- Desktop and mobile browser checks.
- Accessibility and localization checks.
- Regression tests for affected existing behavior.

For every acceptance criterion, record Pass, Fail, Blocked, or Not Applicable, with evidence and notes.

Never claim a test passed unless it was actually run and its result was observed. Clearly identify tests that were not run.

**Output:** verification.md or an equivalent test/verification report.

### Step 9 — Converge implementation with the specification

Compare the current codebase and test evidence against:

- Approved spec.md.
- Approved plan.md.
- tasks.md.
- Acceptance criteria and validation results.

Identify missing behavior, incomplete tasks, unapproved deviations, and documentation drift. Add corrective tasks and repeat implementation and verification until the feature is complete or the owner explicitly accepts a documented deferral.

Convergence does not replace tests, security review, or owner acceptance.

**Output:** Convergence result and remaining-gap list.

### Step 10 — Close the feature and replan

A feature may be closed only when its Definition of Done is met or when the owner explicitly records an accepted deferral.

Update:

- Feature task status.
- Verification evidence.
- API and database documentation, when changed.
- Architecture or decision records, when changed.
- Project progress report.
- Project roadmap, if scope, priority, or dependencies changed.
- Release notes or PR description, if applicable.

Then select the next feature based on product priority, dependencies, risks, and MVP needs.

**Output:** Feature closure report and next-feature recommendation.

## 5. Suggested feature artifact structure

Use Spec Kit's generated structure as the starting point and adapt only when necessary. A typical feature directory may contain:

~~~text
specs/
  003-registration-submission/
    spec.md
    plan.md
    tasks.md
    research.md
    data-model.md
    quickstart.md
    contracts/
    checklists/
~~~

The exact numbering, generated files, and templates should follow the installed Spec Kit version. Do not create duplicate copies if Spec Kit already generated an equivalent artifact.

Recommended artifact responsibilities:

| Artifact | What it answers |
|---|---|
| spec.md | What problem and behavior are required? |
| decisions.md / decision records | What did the owner decide, and why? |
| plan.md | How will the approved feature fit the existing system? |
| research.md | What technical questions were investigated? |
| data-model.md | What data structures or relationships change? |
| contracts/ | What API or integration contract is required? |
| tasks.md | What work must be completed and in what order? |
| checklists/ | Are requirements and plans sufficiently complete? |
| verification.md | What was tested, what passed, and what remains? |

If Spec Kit's templates generate a different standard artifact set, preserve the generated conventions and document the mapping rather than forcing this example structure.

## 6. Requirement traceability

Use stable IDs and maintain a simple mapping.

| Requirement | Acceptance criterion | Task | Verification |
|---|---|---|---|
| FR-001 | AC-001 | T-001 | Test/API evidence |
| FR-002 | AC-002 | T-002 | Integration test |
| NFR-001 | AC-003 | T-003 | Security/performance evidence |

Every in-scope requirement must have one or more acceptance criteria. Every acceptance criterion must have a verification method. Every implementation task should map to a requirement, an acceptance criterion, or an explicitly approved engineering need.

## 7. Definition of Ready

A feature is ready for implementation when:

- The repository and existing behavior have been inspected.
- The problem, users, value, scope, and out-of-scope items are clear.
- Requirements are uniquely identified and testable.
- Important edge cases and error behavior are defined.
- Owner decisions that affect implementation are recorded and approved.
- Technical design is consistent with current architecture.
- API and database impacts are understood.
- Privacy and security requirements are addressed.
- Tasks are dependency-ordered and verifiable.
- The owner has approved the implementation scope.

## 8. Definition of Done

A feature is done when:

- All in-scope acceptance criteria pass, or exceptions are explicitly accepted by the owner.
- Relevant automated tests pass.
- Relevant manual checks are recorded.
- Build and static checks pass, where applicable.
- Security/privacy requirements are verified.
- Database migrations are tested safely, where applicable.
- No unrelated changes are included.
- Documentation and decisions are updated.
- The diff has been reviewed.
- Known issues and deferred work are recorded.
- The owner accepts the feature for closure or release.

A feature can be implemented but not done. A feature can be tested but not released. Keep these statuses separate.

## 9. Project replanning and MVP

Project replanning occurs after feature validation and whenever an important product, technical, or operational assumption changes.

Review:

- Current phase and feature completion evidence.
- Unresolved risks and dependencies.
- New owner decisions.
- Security and maintenance findings.
- User feedback.
- MVP scope and launch constraints.
- Priority and effort of the next feature.

MVP is a product milestone, not a substitute for the feature lifecycle. Every feature included in the MVP still follows specification, approval, implementation, and validation.

Do not declare MVP ready solely because roadmap phases are marked complete. Verify the agreed end-to-end user journeys, production operations, security, privacy, backups, and support readiness.

## 10. Using Spec Kit with Codex

Spec Kit has two distinct kinds of operations:

1. The Specify CLI is used in a terminal to install, initialize, inspect, and manage Spec Kit.
2. The SDD workflow skills are invoked inside the coding agent's chat.

Install and initialize Spec Kit only after repository inspection and approval. For a new project, follow the official setup guide. For an existing project, use the documented existing-project integration process and inspect any files that would be added or changed.

Official installation and workflow references:

- https://github.com/github/spec-kit
- https://github.com/github/spec-kit/blob/main/docs/quickstart.md
- https://github.com/github/spec-kit/blob/main/docs/reference/agentic-sdd.md
- https://github.com/github/spec-kit/blob/main/docs/integrations/codex.md

For Codex, the documented skills use the dollar-prefixed names, for example:

~~~text
$speckit-constitution
$speckit-specify
$speckit-clarify
$speckit-plan
$speckit-checklist
$speckit-tasks
$speckit-analyze
$speckit-implement
$speckit-converge
~~~

Use only skills that have actually been installed and are recognized by the current Codex environment. Do not assume that slash-command notation shown in generic Spec Kit documentation is the exact invocation for Codex.

## 11. Recommended pilot for SMART IT ACADEMY

Use the public registration work as the first full SDD pilot, but do not restart it from scratch.

The saved project context indicates:

- Phase 3.2.4 still has verification and documentation reconciliation work.
- Phase 3.2.5 has a planning review and an existing backend submission endpoint.
- The public frontend submission and consent flow were not yet ready in the last recorded review.
- Owner decisions already recorded include retaining both guardian name fields, using an Idempotency-Key, applying rate limiting at application and reverse-proxy levels, and adopting a Guardian Error Contract.
- Privacy-notice content/versioning and some contract details still require final resolution.

Before implementation, inspect the current application repository and reconcile these records with its actual current state. Do not assume the saved review is still current.

Recommended pilot sequence:

1. Inspect the current application repository and reconcile Phase 3.2.4 status.
2. Confirm outstanding owner decisions for Phase 3.2.5.
3. Reuse the existing Phase 3.2.5 planning review and design work.
4. Create or normalize the feature specification and stable requirement IDs.
5. Review the technical plan and tasks against current code and migrations.
6. Obtain explicit owner approval.
7. Implement in small task groups.
8. Validate all acceptance criteria and security/privacy constraints.
9. Converge and close the feature with evidence.
10. Update the roadmap and select the next feature.

## 12. Change management

When an approved requirement changes:

1. Record the change and reason.
2. Identify affected requirements, decisions, plans, tasks, APIs, data models, tests, and documentation.
3. Assess compatibility, migration, security, and release impact.
4. Obtain owner approval for material scope or policy changes.
5. Update affected artifacts.
6. Re-run consistency checks and impacted tests.

Do not silently edit an approved specification to match existing code. The specification is the agreed target; implementation gaps must be visible.

---

**Operating rule:** Inspect → Specify → Clarify → Plan → Quality-check → Tasks → Owner approval → Implement → Validate → Converge → Replan.

This is the proposed standard workflow for SMART IT ACADEMY. The project owner remains responsible for approving the Constitution, business requirements, material technical decisions, and releases.
