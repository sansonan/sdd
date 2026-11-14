# SMART IT ACADEMY — AI Agent Workflow

**Primary coding agent:** OpenAI Codex  
**Specification framework:** GitHub Spec Kit (Hybrid SDD)  
**Human authority:** SMART IT ACADEMY Project Owner  
**Status:** Proposed operating guide  
**Last reviewed:** November 14, 2026

> This guide defines how AI coding agents should participate in the development process. It does not grant repository, production, or database permissions by itself. Actual access is controlled by the user's tools, operating environment, repository settings, and explicit approvals.

## 1. Purpose

Use AI agents to improve analysis, implementation speed, and verification without giving up engineering judgment, data safety, or product-owner control.

The operating model is:

- The **Project Owner** sets product direction, approves requirements, decides business policy, and accepts releases.
- **Spec Kit** structures the specification and delivery workflow.
- **Codex** inspects the repository, plans approved work, implements tasks, runs checks, and reports evidence.
- **Other agents or reviewers** may perform independent research or review when their scope is clearly separated.
- **CI and test tools** provide repeatable build and test evidence.

One agent should coordinate the feature and maintain consistency across artifacts. Do not delegate authority for business decisions to an agent.

## 2. Responsibilities

### Project Owner

Responsible for:

- Product vision, roadmap, and MVP scope.
- Business rules and priorities.
- Approval of feature specifications and material technical plans.
- Security, privacy, data-retention, and operational policy decisions.
- Approval of destructive operations and production deployment.
- Review of diffs and acceptance of completed features.
- Deciding whether unresolved issues block closure or can be deferred.

### Codex — primary implementation agent

Responsible for:

- Reading Constitution, AGENTS.md, and applicable nested instructions.
- Inspecting current code, tests, APIs, migrations, and Git state.
- Working from approved specifications, plans, and tasks.
- Making focused and reviewable changes.
- Running relevant tests and reporting actual results.
- Updating task status and proposed documentation changes.
- Highlighting assumptions, risks, failed checks, and unimplemented requirements.

Codex must not silently change approved business policy or expand feature scope.

### Spec Kit — workflow assistant

Responsible for structured SDD artifacts and process steps such as:

- Constitution creation or maintenance.
- Feature specification.
- Clarification questions.
- Technical planning.
- Requirements-quality checklists.
- Task generation.
- Cross-artifact consistency analysis.
- Implementation guidance.
- Specification-to-code convergence.

Spec Kit commands are not shell commands. They are invoked in the coding agent's chat using the syntax for the installed integration.

### CI and verification tools

Responsible for repeatable automated evidence such as:

- Backend builds and tests.
- Frontend builds, lint, and tests.
- Database migration and integration tests.
- API and end-to-end tests.
- Static and security checks.

A green CI result only proves the checks that actually ran. It does not replace acceptance review.

## 3. Mandatory preflight before agent work

At the start of every feature or substantial task, the primary agent must:

1. Confirm the repository root.
2. Read the Project Constitution.
3. Read root AGENTS.md and every applicable nested AGENTS.md.
4. Read the current feature spec, plan, and tasks.
5. Read relevant roadmap and progress documents.
6. Inspect the current branch and Git-working-tree status.
7. Identify existing uncommitted changes and avoid disturbing them.
8. Inspect the relevant source code and test conventions.
9. Identify affected migrations, API contracts, security boundaries, and data flows.
10. Report the intended scope before making material changes.

If the Constitution or feature artifacts are missing, contradictory, or inaccessible, report the gap. Do not invent a replacement policy.

## 4. Three operating modes

### Mode A — Read-only assessment

Use this mode for repository audits, architecture reviews, planning reviews, and unfamiliar codebases.

Allowed:

- Read files and Git status.
- Search code and documentation.
- Inspect configuration and test commands.
- Explain architecture and identify risks.
- Draft recommendations in the conversation.

Not allowed unless separately approved:

- Modify files.
- Install packages.
- Run database migrations.
- Change Git branches or history.
- Deploy or access production systems.
- Change repository configuration.

A read-only report must say exactly what was inspected and what was not executed.

### Mode B — Planning

Use this mode to create or revise proposed SDD artifacts.

Typical outputs:

- Feature spec.
- Clarification questions.
- Decision log.
- Technical plan.
- Data model and API contracts.
- Requirements checklist.
- Implementation tasks.
- Validation plan.

Planning is not implementation approval. Clearly label artifacts Draft, Proposed, or Approved.

Do not modify application code or database migrations during a planning-only task.

### Mode C — Approved implementation

Use this mode only after the owner approves the relevant specification, plan, and task scope.

Before editing:

- Confirm branch and clean/known working-tree state.
- Confirm the files and modules in scope.
- Confirm permitted commands and environments.
- Confirm whether database, dependency, or infrastructure changes are allowed.

During implementation:

- Follow task dependencies.
- Work in small batches.
- Keep changes focused.
- Run relevant tests.
- Review diffs.
- Report blockers immediately.
- Do not silently alter the spec to make code appear compliant.

After implementation:

- Run validation.
- Record evidence.
- Update task status.
- Identify remaining gaps.
- Request review and owner acceptance.

## 5. Codex + Spec Kit operating sequence

For a substantial or production feature, use the full Spec Kit flow.

### Terminal setup (one-time / environment management)

Install the Specify CLI using the current official instructions. The current quickstart documents installation through uv:

~~~bash
uv tool install specify-cli
~~~

For a new project, the general form is:

~~~bash
specify init <project-directory> --integration codex
~~~

For an existing Spec Kit project, the Codex integration guide documents:

~~~bash
specify integration install codex
~~~

For an existing application repository that is not yet initialized, review the existing-project guide, inspect every managed-file conflict, and obtain owner approval before running initialization. Do not add --force as a shortcut.

### Agent chat workflow

The current Spec Kit Codex integration documents skills installed under:

~~~text
.agents/skills/speckit-<command>/SKILL.md
~~~

The Codex invocation examples use a dollar-prefixed skill name:

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

Check the installed skill files and Codex's recognized skills before relying on them. Do not assume that generic /speckit.* notation is the exact command syntax for Codex.

### Recommended production-feature sequence

1. Constitution: establish or update durable principles when necessary; usually this is a project-level activity, not a per-feature operation.
2. Specify: define user needs and behavior.
3. Clarify: resolve important ambiguities.
4. Plan: design within the established architecture.
5. Checklist: check specification quality.
6. Tasks: break work into ordered units.
7. Analyze: find inconsistencies across artifacts.
8. Owner approval: approve material decisions and implementation scope.
9. Implement: execute approved tasks.
10. Validate: run tests and inspect behavior.
11. Converge: compare implementation with the approved artifacts and add tasks for gaps.
12. Owner review and closure: accept the feature, record deferred work, and replan.

For low-risk changes, a shorter workflow may be appropriate, but requirements and verification must still be clear.

## 6. Task execution rules

Each implementation task should be:

- Small enough to review.
- Mapped to one or more requirement or acceptance-criterion IDs.
- Clear about expected behavior and boundaries.
- Explicit about likely files or components.
- Clear about dependencies.
- Testable through a command, automated test, or defined manual check.

Preferred implementation loop:

1. Read the task and relevant requirements.
2. Inspect the current implementation.
3. Explain the intended change briefly.
4. Make the smallest coherent change.
5. Run targeted tests.
6. Inspect the diff.
7. Check for unrelated changes and security issues.
8. Update task status with evidence.
9. Continue only when the task remains within approved scope.

Avoid asking an agent to implement an entire large phase in a single unbounded task.

## 7. Parallel agents and work isolation

Parallel agents are optional, not a default requirement.

Use them only when:

- Work can be split into independent areas.
- Each agent has a clearly defined task and file ownership.
- Shared contracts and dependencies are already understood.
- Changes can be isolated in separate branches or worktrees when appropriate.
- One primary agent is responsible for integration and final consistency.

Do not have multiple agents simultaneously edit:

- The same feature specification or task file.
- The same database migration sequence.
- The same API contract.
- Shared frontend/backend interfaces.
- The same high-conflict files.

Before merging parallel work, review every diff, resolve contract conflicts, run integrated tests, and confirm no task or requirement was lost.

## 8. Safety and approval boundaries

The agent must stop and request explicit owner approval before:

- Deleting or overwriting user data or existing work.
- Editing an applied Flyway migration or rewriting migration history.
- Running destructive or irreversible database operations.
- Accessing, changing, or deploying to production.
- Changing authentication, authorization, or sensitive privacy behavior beyond approved scope.
- Exposing personal information or adding new personal-data collection.
- Changing data-retention, consent, guardian, payment, or eligibility policy.
- Introducing a paid service, paid dependency, or external spend.
- Rotating or changing credentials and production secrets.
- Force-pushing, rewriting Git history, or deleting branches.
- Changing repository or GitHub App permissions.

A feature plan does not itself authorize every risky operation. Confirm scope and permissions at execution time.

## 9. Testing and evidence rules

The agent must distinguish:

- **Not run:** no test execution occurred.
- **Passed:** command completed successfully and result was observed.
- **Failed:** command ran and failed.
- **Blocked:** test could not run because of an identified dependency or environment issue.
- **Not applicable:** the test does not apply, with a short reason.

For each important check, record:

- Command or manual procedure.
- Environment and test data type.
- Result.
- Relevant failure summary.
- Evidence location when available.

Do not report "all tests passed" if only a subset ran. Never use production personal data for routine automated tests. Use isolated or disposable test resources for database and end-to-end tests.

## 10. Required implementation report

At the end of each approved implementation task group, Codex should report:

1. **Scope:** approved task IDs and requirements addressed.
2. **Files changed:** added, modified, or deleted paths.
3. **Behavior:** what changed from the user's perspective.
4. **Database/API impact:** migrations, schema, endpoints, and contracts affected.
5. **Tests:** exact commands and observed results.
6. **Security/privacy:** checks performed and remaining risks.
7. **Documentation:** artifacts updated or still needing updates.
8. **Known gaps:** failed, blocked, or deferred acceptance criteria.
9. **Git:** branch and diff summary; do not claim a commit or push unless it happened.
10. **Next action:** review, approval, corrective task, or next feature.

## 11. Standard prompt templates

### Read-only inspection

~~~text
Inspect this repository for the requested area.
Read all applicable AGENTS.md files and the Project Constitution.
Check Git status before proceeding.
Do not modify files, install dependencies, run migrations,
or execute destructive operations.
Report findings with file paths and evidence.
~~~

### Planning only

~~~text
Planning only. Do not implement application code.
Inspect current implementation and project documents first.
Create or revise the feature specification, clarify open
decisions, prepare a technical plan and ordered tasks.
Identify requirements, acceptance criteria, risks, dependencies,
API/database/security impact, and verification methods.
Mark unapproved decisions as Proposed and wait for owner approval.
~~~

### Approved implementation

~~~text
Implement only the owner-approved task IDs listed below.
Read the approved feature spec, technical plan, tasks,
Project Constitution, and applicable AGENTS.md files.
Inspect Git status and current implementation first.
Do not expand scope or change business policy.
Preserve unrelated work and existing migration history.
Implement in small steps, run relevant tests, review the diff,
and report exact files changed and test results.

Approved task IDs:
[LIST TASK IDS]

Out of scope:
[LIST EXCLUDED ITEMS]
~~~

### Validation only

~~~text
Validate the implemented feature against the approved
specification and acceptance criteria.
Do not change application files.
Run only the approved safe tests.
Map every acceptance criterion to Pass, Fail, Blocked,
or Not Applicable and provide evidence.
Identify security, privacy, regression, and documentation gaps.
Do not claim unexecuted checks passed.
~~~

## 12. Feature closure checklist

- [ ] Approved requirements and owner decisions are traceable.
- [ ] All in-scope implementation tasks are complete or explicitly deferred.
- [ ] Relevant automated tests have been run.
- [ ] Manual and end-to-end checks are documented where required.
- [ ] API and database contracts are consistent with implementation.
- [ ] Security and privacy controls have been verified.
- [ ] No unintended files or unrelated changes are included.
- [ ] Documentation and decision records are updated.
- [ ] Convergence gaps are resolved or explicitly accepted.
- [ ] The final diff has been reviewed.
- [ ] The project owner has accepted feature closure.

## 13. Official references

- Spec Kit repository: https://github.com/github/spec-kit
- Spec Kit quickstart: https://github.com/github/spec-kit/blob/main/docs/quickstart.md
- Agentic SDD reference: https://github.com/github/spec-kit/blob/main/docs/reference/agentic-sdd.md
- Codex integration: https://github.com/github/spec-kit/blob/main/docs/integrations/codex.md
- Codex CLI documentation: https://developers.openai.com/codex/cli/

---

**Operating rule:** The agent may propose, analyze, and implement approved work. The owner decides what the product should do, approves material constraints, and accepts the evidence before feature closure.
