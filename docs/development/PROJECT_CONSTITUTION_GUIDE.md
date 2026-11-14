# SMART IT ACADEMY — Project Constitution Guide

**Status:** Guidance and draft principles for owner review  
**Audience:** Project owner, developers, and AI coding agents  
**Last reviewed:** November 14, 2026

> This is a guide for creating and maintaining the Project Constitution. It is not itself the approved Constitution. The project owner must review and approve the principles before they become binding.

## 1. What is a Project Constitution?

A Project Constitution is a concise set of durable principles and constraints that govern how the product is designed, implemented, tested, secured, and maintained.

It answers questions such as:

- Which architecture principles must every feature respect?
- What is the minimum acceptable quality?
- How should personal information be protected?
- What is the rule for database migrations?
- What evidence is required before a feature is considered complete?
- Which decisions require explicit human approval?

The Constitution should be stable across many features. It should not contain the detailed requirements of one feature or a list of every current task.

## 2. Constitution vs AGENTS.md

These documents have different jobs and should work together.

| Document | Primary question | Typical contents |
|---|---|---|
| Project Constitution | What principles and constraints govern this project? | Architecture principles, security, quality, data integrity, approval boundaries |
| AGENTS.md | How should an AI coding agent work in this repository? | Inspection steps, commands, file conventions, testing instructions, safe workflow |
| Feature specification | What must this feature do and why? | Users, scope, user stories, business rules, requirements, acceptance criteria |
| Technical plan | How should this feature fit into the system? | Architecture, API, database, security controls, test design |
| Tasks | What implementation work must be done? | Ordered, verifiable tasks and dependencies |

The existing SMART IT ACADEMY AGENTS.md already contains useful operating rules such as inspecting the repository, working in small phases, running tests, using migrations, protecting secrets, avoiding destructive changes, and updating documentation. Preserve those rules unless an audit identifies a real conflict or gap.

Do not copy the full Constitution into AGENTS.md. AGENTS.md can state that agents must read and comply with the Constitution.

## 3. Recommended location

When adopting GitHub Spec Kit, its standard Constitution location is:

~~~text
.specify/
  memory/
    constitution.md
~~~

The repository root can also retain:

~~~text
AGENTS.md
~~~

Use the generated location and template from the installed Spec Kit version. Do not create a competing Constitution in a second location unless the project has a clear reason and an explicit pointer to the authoritative version.

This guide lives in the separate learning/documentation repository. The binding Constitution should be maintained in the actual SMART IT ACADEMY application repository, alongside its source code and instructions.

## 4. Characteristics of a good principle

Each constitutional principle should be:

- **Durable:** It should apply to many features, not just one task.
- **Clear:** A developer or agent can understand what it requires.
- **Verifiable:** Reviewers can identify evidence of compliance.
- **Necessary:** It protects product quality, users, maintainability, or important constraints.
- **Non-duplicative:** It does not repeat an existing rule without a reason.
- **Technology-aware but not needlessly brittle:** Pin exact versions in the architecture or dependency configuration unless a version is a deliberate project-wide constraint.

Prefer statements such as:

> All schema changes must use reviewed, versioned database migrations. Existing applied migrations must not be edited to change deployed schema history.

Avoid vague statements such as:

> The database must be very good.

## 5. Proposed Constitution topics for SMART IT ACADEMY

The following are candidate principles for discussion. They are **not approved project rules until the owner accepts them**.

### Principle 1 — Product and user value

Candidate rule:

- Features should solve an identified academy, staff, teacher, student, or applicant need.
- Feature scope should be explicit, with out-of-scope behavior documented.
- MVP and release decisions should prioritize essential end-to-end user journeys over a large number of incomplete modules.

Possible evidence:

- Product requirement and user story.
- Approved scope and acceptance criteria.
- Demonstrable end-to-end workflow.

### Principle 2 — Architecture integrity

Candidate rule:

- New features must respect the architecture and module boundaries documented in the application repository.
- Reuse existing patterns where they remain suitable.
- Material architectural changes require documented rationale and owner approval.
- Do not introduce a second implementation of an existing capability without a justified decision.

Possible evidence:

- Architecture review.
- Component/module boundaries.
- Decision record for material changes.

Do not hard-code framework or runtime versions in this principle until verified against the repository's actual build files and deployment configuration.

### Principle 3 — API contract consistency

Candidate rule:

- Public and internal APIs must use the project's approved API conventions.
- Requests, responses, validation errors, status codes, authentication, authorization, pagination, and versioning must be documented where applicable.
- Contract changes must be reflected in implementation, tests, and API documentation.
- Breaking changes require compatibility analysis and explicit approval.

Possible evidence:

- OpenAPI contract.
- API tests.
- Error-response tests.
- Compatibility review.

### Principle 4 — Database integrity and migration safety

Candidate rule:

- Schema changes must use the project's migration tool and established migration conventions.
- Applied migrations must be treated as immutable.
- Destructive data changes require backup/recovery planning and explicit owner approval.
- Constraints and indexes should reflect documented business and query requirements.
- Production database operations must never be assumed safe based only on a local development test.

Possible evidence:

- Versioned migration.
- Migration test against a disposable database.
- Data-integrity tests.
- Backup and recovery notes for risky changes.

### Principle 5 — Security by design

Candidate rule:

- Authentication and authorization must be enforced on the server, not only in the UI.
- Validate and normalize untrusted inputs at appropriate boundaries.
- Protect credentials, tokens, personal data, logs, backups, and configuration.
- Apply least privilege and secure defaults.
- Security-sensitive behavior must be covered by tests and reviewed before release.

Possible evidence:

- Authorization tests.
- Input-validation tests.
- Secret scanning or configuration review.
- Security review findings and remediation evidence.

### Principle 6 — Privacy and personal-data protection

Candidate rule:

- Collect only personal information needed for a documented purpose.
- Explain consent and privacy expectations in the required supported languages.
- Keep personal information out of logs, metrics, and unnecessary audit details.
- Define retention, redaction, access, and hold behavior before relying on a data collection feature.
- Do not expose private application records through anonymous endpoints.

Possible evidence:

- Data inventory and purpose.
- Approved privacy notice and its version.
- Access-control tests.
- Retention and redaction design.

The precise retention period and legal obligations must be owner-approved and checked against applicable requirements; this principle does not invent those values.

### Principle 7 — Testing and verification

Candidate rule:

- Every feature must have testable acceptance criteria.
- Relevant automated tests must be executed for changed behavior.
- Tests must use controlled test data and safe test environments.
- Test failures and unexecuted checks must be reported honestly.
- A passing build alone is insufficient evidence that a feature is complete.

Possible evidence:

- Test report with commands and results.
- Acceptance-criteria matrix.
- Regression and end-to-end test results.

### Principle 8 — User experience and localization

Candidate rule:

- User-facing content must follow the product's approved language and localization requirements.
- Khmer and English interfaces must remain behaviorally consistent where bilingual support is required.
- Forms must provide understandable validation and error messages.
- Accessibility, responsive behavior, and usability must be considered for critical user journeys.

Possible evidence:

- Khmer and English UI checks.
- Form and error tests.
- Desktop/mobile checks.
- Accessibility review.

### Principle 9 — AI agent governance

Candidate rule:

- AI agents must inspect relevant instructions and existing code before making changes.
- Agents must work from approved specifications and plans.
- Agents must not invent business policy, credentials, dependencies, or test results.
- Agents must preserve unrelated user changes.
- Agents must report every material change, command, test, and unresolved risk.
- Human approval is required for business-policy decisions and designated high-impact operations.

Possible evidence:

- Reviewed specification and task list.
- Pull request/diff review.
- Verification report.
- Recorded owner decisions.

### Principle 10 — Documentation and traceability

Candidate rule:

- Requirements, decisions, plans, tasks, implementation, and verification must remain traceable.
- Authoritative documents must be clearly identified.
- Material changes must update affected documentation.
- Accepted exceptions and deferred work must be recorded with an owner and rationale.

Possible evidence:

- Requirement-to-test mapping.
- Decision records.
- Updated progress and roadmap documentation.

## 6. How to create the actual Constitution

Use this controlled sequence:

### Step 1 — Audit existing rules

Inspect:

- Root and nested AGENTS.md files.
- README and project instructions.
- Architecture documentation.
- Database and migration rules.
- API standards.
- Security and privacy documentation.
- Existing decisions and test policy.

Classify each rule as:

- Existing and valid.
- Existing but unclear.
- Duplicated.
- Contradictory.
- Missing.
- Needs owner decision.

### Step 2 — Draft principles

Use the candidate topics in Section 5. For every proposed principle, write:

- Principle title.
- Normative rule.
- Why it exists.
- Scope.
- How compliance is verified.
- Exceptions, if any.

### Step 3 — Resolve conflicts

Do not silently decide conflicts between existing documents. Present the conflict and options to the project owner.

Examples:

- An old instruction says to use one approach, while the current architecture uses another.
- An old roadmap names a framework version that differs from the actual build configuration.
- A privacy requirement has a proposed but unapproved retention period.

### Step 4 — Obtain owner approval

Review the complete draft. Record:

- Constitution version.
- Approval status.
- Owner.
- Approval date.
- Principles accepted or rejected.
- Deferred decisions.

### Step 5 — Install or update with Spec Kit

After repository inspection and approval, use the installed Codex Spec Kit skill to create or update the Constitution.

The documented Codex integration uses the skill name:

~~~text
$speckit-constitution
~~~

Ask the agent to preserve approved principles, identify conflicts, and update dependent templates only after reviewing the impact.

### Step 6 — Synchronize AGENTS.md

Update AGENTS.md only where the audit identifies missing or contradictory agent instructions.

Keep it operational and concise. Include:

- A requirement to read and comply with the Constitution.
- Repository inspection rules.
- Safe file-editing and Git rules.
- Commands to build and test.
- Approval boundaries.
- Documentation update requirements.

### Step 7 — Review the diff

Check the Constitution and any AGENTS.md changes. Ensure no existing user instructions or unrelated work were removed. Obtain owner acceptance before treating the new Constitution as binding.

## 7. Constitution maintenance

The Constitution should not change for every feature.

Update it when:

- A durable architecture principle changes.
- A project-wide security or privacy requirement changes.
- The required quality bar changes.
- A recurring project-wide exception reveals that a principle is no longer suitable.
- A new business or operational constraint applies across many features.

For each amendment, record:

| Field | Description |
|---|---|
| Version | Constitution version |
| Change | Added, changed, or retired principle |
| Reason | Why the amendment is needed |
| Impact | Affected specifications, templates, and work |
| Approval | Owner approval and date |

Re-check active feature plans if an amendment changes their constraints.

## 8. Suggested owner approval checklist

- [ ] Existing repository rules have been inspected.
- [ ] Proposed principles have been reviewed.
- [ ] Technology versions have been verified against the actual repository.
- [ ] Security and privacy obligations have been checked.
- [ ] Conflicts and exceptions have been resolved or recorded.
- [ ] Each principle has a practical verification method.
- [ ] The owner has approved the final Constitution.
- [ ] AGENTS.md has been reviewed for consistency.
- [ ] The final diff has been accepted.

---

**Important:** The Constitution is a project governance artifact. Do not treat this guide's candidate principles as approved until the SMART IT ACADEMY project owner explicitly accepts them.
