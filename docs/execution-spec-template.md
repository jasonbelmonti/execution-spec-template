# Operational Execution Specification Template

Authoring guidance lives in `docs/execution-spec-authoring-guide.md`. Review procedure lives in `docs/execution-spec-review-process.md`.

## Purpose

This document is a controlled execution artifact. It shall answer six questions in order:

1. What approved outcome, ticket, or design is being executed?
2. What work is in scope, out of scope, and blocked by dependencies?
3. What change surfaces, work packages, and sequencing will produce the outcome?
4. What controls will prevent unsafe drift during execution?
5. What evidence will prove the work is complete and fit to ship?
6. How will the change be reviewed, deployed, monitored, rolled back, and handed off?

If the source decision or success criteria are weak, this document shall expose that gap instead of inventing authority.

## Execution Level Selection

Select one execution level before writing the plan. Use the highest level that applies.

| Level | Use when | What the document is allowed to contain | Approval outcome |
| --- | --- | --- | --- |
| `E0 Discovery Execution` | The execution objective is to retire uncertainty through a spike, prototype, audit, or measurement pass. | Implementation details may be provisional if every unknown is bounded and tied to evidence capture. | Approval means "approved to investigate," not "approved to ship." |
| `E1 Bounded Change` | The work is small, reversible, contained to one owner, and has bounded operational risk. | Sections may be concise. Omitted sections require `N/A` rationale. Unknowns are allowed only if they do not block safe execution. | Approval means "approved to execute." |
| `E2 Standard Execution` | The work is intended for production or durable internal use and does not qualify for `E1` or trigger `E3`. This is the default execution level. | Work packages, validation, rollout, rollback, and handoff shall be complete enough for another engineer to execute. | Approval means "approved to execute." |
| `E3 Critical Execution` | Failure could cause safety impact, security incident, regulatory breach, irreversible data loss, large financial loss, or broad operational outage. | All required sections shall be complete, independently reviewable, and backed by heightened controls. Waivers shall be explicit and approved. | Approval means "approved to execute under heightened controls." |

Use `E1` only when all of the following are true:

- The work has one clear owning engineer or team.
- The implementation and rollout are reversible.
- The change introduces no new trust boundary.
- The change introduces no irreversible data, schema, API, event, contract, or config migration.
- The work does not affect safety, security, compliance, privacy, financial exposure, or a high-volume shared path.
- The validation evidence can be produced before or during normal review.

Use `E3` if any of the following are true:

- The execution changes authentication, authorization, cryptography, secret handling, payment behavior, or safety controls.
- The execution can delete, corrupt, or irreversibly transform customer or mission data.
- The execution requires a live migration, one-way rollout, or constrained rollback.
- The execution affects a shared platform, high-volume path, regulated workflow, or broad operational dependency.
- The execution depends on coordinated releases across multiple owners where partial deployment is hazardous.

## Controlled Vocabulary

Use words with specific force:

- `shall`: binding execution requirement or acceptance condition
- `will`: declared execution decision or planned action
- `may`: allowed option or non-mandatory action
- `blocked`: execution cannot proceed until the named condition is resolved
- `unknown`: known gap; must include a `Q-*` identifier, owner, due date, and resolution plan
- `deviation`: approved departure from the execution plan; must include a `DEV-*` identifier, owner, approver, rationale, impact, and evidence
- `waiver`: approved exception to a review or approval rule; must include a `WVR-*` identifier, approver, waived rule or finding, rationale, boundary or expiry, compensating control, and evidence

Use planning strategy terms with specific meaning:

- `critical path hypothesis`: the smallest execution path believed to prove or invalidate the approved outcome
- `proving slice`: the first work package or sequence segment that produces evidence about the critical path
- `risk retirement`: sequencing work to resolve high-risk unknowns before routine implementation
- `progressive value`: sequencing work so each completed slice produces independently reviewable value or evidence
- `validation checkpoint`: a `VAL-*` item that proves a work package output or decision point
- `deferred completeness`: explicitly delayed polish, breadth, or exhaustive implementation that is safe only after the proving slice succeeds

Avoid ambiguous execution language such as `clean up`, `wire up`, `make robust`, `add coverage`, or `handle edge cases` unless the statement defines the exact target behavior, files, tests, or evidence.

## Identifier Scheme

Assign stable identifiers and reuse them throughout the document:

- `SRC-*` for source inputs, such as designs, tickets, incidents, audits, or user requests
- `OBJ-*` for execution objectives
- `NG-*` for non-objectives
- `CON-*` for constraints and invariants
- `ASM-*` for assumptions
- `DEP-*` for dependencies and sequencing blockers
- `SURF-*` for change surfaces, modules, systems, or repositories
- `WP-*` for work packages
- `CTRL-*` for execution controls and safeguards
- `VAL-*` for validation items and evidence
- `REV-*` for review checks
- `REL-*` for rollout, rollback, migration, or release activities
- `OBS-*` for observability and monitoring signals
- `RISK-*` for material execution risks
- `Q-*` for unresolved questions
- `DEV-*` for approved deviations from the plan
- `WVR-*` for approved review waivers
- `EVD-*` for produced evidence artifacts

## Section Quality Model

Every section shall be evaluated on five dimensions:

- `Presence`: required fields exist
- `Precision`: statements are specific, singular, and falsifiable
- `Authority`: execution claims cite a source decision, owner, or approved assumption
- `Traceability`: work maps to objectives, validation, review, and release evidence
- `Execution utility`: another qualified engineer could act on the section without hidden context

Use one status per section:

| Status | Meaning | Allowed by level |
| --- | --- | --- |
| `Complete` | All required content is present and exit criteria are met | `E0`, `E1`, `E2`, `E3` |
| `Deferred` | The gap is explicit, bounded, owned, linked to one or more `Q-*` items, and backed by a validation or resolution plan | `E0`; limited use in `E1` and `E2`; not acceptable in `E3` without approved waiver |
| `N/A` | The section does not apply to this execution and the reason is stated | `E0`, `E1`, `E2`, `E3` |
| `Incomplete` | Required content or exit criteria are missing | never acceptable for approval |

Do not leave blanks. If something is unknown, write `unknown` and manage it explicitly.

## Section Applicability by Execution Level

| Section | `E0` | `E1` | `E2` | `E3` |
| --- | --- | --- | --- | --- |
| 0. Execution Summary | Required | Required | Required | Required |
| 1. Source Authority and Scope | Required | Required | Required | Required |
| 2. Objectives and Non-Objectives | Required | Required | Required | Required |
| 3. Ownership, Roles, and Decision Points | Required | Required | Required | Required |
| 4. Constraints, Assumptions, and Dependencies | Required | Required | Required | Required |
| 5. Change Surface Inventory | Required if any system, repo, document, data, or config changes | Required | Required | Required |
| 6. Work Packages and Sequencing | Required | Required | Required | Required |
| 7. Execution Controls and Drift Management | Required | Required | Required | Required |
| 8. Data, Schema, Config, and Contract Handling | Required if affected | Required if affected; otherwise `N/A` with rationale | Required if affected | Required if affected |
| 9. Validation and Evidence Plan | Required | Required | Required | Required |
| 10. Review Plan | Required | Required | Required | Required |
| 11. Rollout, Migration, Rollback, and Recovery | Required if anything ships, deploys, migrates, or affects live operation | Required | Required | Required |
| 12. Observability and Operational Readiness | Required if anything runs or can fail after delivery | Required if production-facing; otherwise `N/A` with rationale | Required | Required |
| 13. Risks, Questions, Deviations, and Waivers | Required | Required | Required | Required |
| 14. Execution Traceability Matrix | Required | Required | Required | Required |
| 15. Final Execution Gate | Required | Required | Required | Required |

## Document Control

| Field | Value |
| --- | --- |
| Title |  |
| Status | Draft / In Review / Approved to Investigate / Approved to Execute / Approved with Heightened Controls / Completed / Rejected / Superseded |
| Execution level | `E0` / `E1` / `E2` / `E3` |
| Execution level justification |  |
| Author(s) |  |
| Executor(s) |  |
| Reviewers |  |
| Decision owner |  |
| Target branch, release, or milestone |  |
| Last updated |  |
| Related source docs |  |
| Related tickets |  |

## 0. Execution Summary

### Required Output

- One paragraph that states the approved outcome, execution approach, and decision being requested.
- One sentence that states what must be true before execution begins.
- A short list of the three highest execution risks or unknowns.

### Exit Criteria

- `Decision requested`, `Approved outcome`, `Execution approach`, `Entry condition`, `Top risks or unknowns`, and `Section status` fields are present and non-empty.
- `Decision requested` exactly equals `Approve to investigate` for `E0`, `Approve to execute` for `E1` or `E2`, or `Approve with heightened controls` for `E3`.
- `Approved outcome` cites at least one `SRC-*`, ticket, design, incident, or explicit user request.
- `Top risks or unknowns` contains between 1 and 3 discrete items.
- `Execution approach` names the dominant work packages and validation posture.

### Template

Decision requested:

Approved outcome:

Execution approach:

Entry condition:

Top risks or unknowns:

Section status:

## Layer 1: Execution Basis

## 1. Source Authority and Scope

### Required Output

- Source authority for the work.
- In-scope and out-of-scope boundaries.
- Definition of done at the execution artifact level.
- Explicit statement of what shall not be re-decided during execution.

### Exit Criteria

- At least one `SRC-*` row is present.
- Every source row has non-empty `Source`, `Authority`, and `Execution implication` cells.
- `In scope`, `Out of scope`, `Definition of done`, `Re-decision boundaries`, and `Section status` fields are present and non-empty.
- `Re-decision boundaries` identifies design, product, or operational decisions that require escalation instead of local execution changes.

### Template

| ID | Source | Authority | Execution implication |
| --- | --- | --- | --- |
| SRC-1 |  |  |  |

In scope:

Out of scope:

Definition of done:

Re-decision boundaries:

Section status:

## 2. Objectives and Non-Objectives

### Required Output

- `OBJ-*` statements that define execution outcomes.
- `NG-*` statements that define excluded work.
- Completion horizon for each objective.

### Exit Criteria

- At least one `OBJ-*` row and one `NG-*` row are present.
- Every `OBJ-*` row has non-empty `Statement`, `Completion horizon`, and `Evidence` cells.
- Every `NG-*` row uses explicit exclusion language such as `will not`, `does not include`, or `out of scope`.
- No objective is merely a task verb without an outcome.

### Template

| ID | Statement | Completion horizon | Evidence |
| --- | --- | --- | --- |
| OBJ-1 |  |  |  |
| NG-1 |  |  |  |

Section status:

## 3. Ownership, Roles, and Decision Points

### Required Output

- Execution owner, implementers, reviewers, approvers, operators, and consulted domains.
- Decision points that can stop, redirect, or approve execution.
- Escalation path for blocked or unsafe work.

### Exit Criteria

- The role table contains at least one owner and one reviewer.
- Every role row has non-empty `Role or person`, `Responsibility`, and `Required action` cells.
- Every `Required action` cell contains only `Execute`, `Review`, `Approve`, `Consult`, `Operate`, or `Inform`.
- At least one decision point is present unless the section is `N/A` with rationale for `E0` discovery.

### Template

| Role or person | Responsibility | Required action |
| --- | --- | --- |
|  |  |  |

Decision points:

Escalation path:

Section status:

## 4. Constraints, Assumptions, and Dependencies

### Required Output

- Constraints and invariants that execution shall preserve.
- Assumptions that are safe enough to proceed.
- Dependencies, sequencing blockers, and external readiness conditions.

### Exit Criteria

- At least one `CON-*`, `ASM-*`, or `DEP-*` row is present.
- Every row has non-empty `Type`, `Statement`, `Owner`, and `Validation or resolution plan` cells.
- Every `DEP-*` row identifies whether it is blocking or non-blocking.
- Any blocking dependency appears in section 6 sequencing or section 15 entry gate.

### Template

| ID | Type | Statement | Owner | Blocking? | Validation or resolution plan |
| --- | --- | --- | --- | --- | --- |
| CON-1 | Constraint |  |  | No |  |
| ASM-1 | Assumption |  |  | No |  |
| DEP-1 | Dependency |  |  | Yes / No |  |

Section status:

## Layer 2: Execution Plan

## 5. Change Surface Inventory

### Required Output

- Repositories, packages, modules, docs, infrastructure, data stores, config, contracts, environments, or operational procedures that may change.
- Owner and review expectation for each surface.
- Read/write boundary for each surface.

### Exit Criteria

- Every material change surface has a `SURF-*` row.
- Every row has non-empty `Surface`, `Change type`, `Owner`, `Read/write boundary`, and `Review expectation` cells.
- Shared, high-risk, or externally consumed surfaces are explicitly marked.

### Template

| ID | Surface | Change type | Owner | Read/write boundary | Review expectation |
| --- | --- | --- | --- | --- | --- |
| SURF-1 |  | Code / Test / Docs / Config / Data / Infra / Contract / Runbook |  |  |  |

Section status:

## 6. Work Packages and Sequencing

### Required Output

- Planning preamble that states the sequencing strategy, critical path hypothesis, first proving slice, validation cadence, and deferred completeness.
- Work packages with objective, owner, inputs, outputs, dependencies, validation checkpoint, and completion criteria.
- Execution order, parallelization constraints, and integration points.
- File or module ownership if multiple implementers are involved.

### Exit Criteria

- At least one `WP-*` row is present.
- Planning preamble fields are present and non-empty.
- The first work package proves or invalidates the critical path hypothesis.
- High-risk unknowns are retired before routine implementation.
- Every work package has non-empty `Objective`, `Owner`, `Inputs`, `Outputs`, `Dependencies`, `Validation checkpoint`, and `Completion criteria` cells.
- Each `WP-*` row links to at least one `VAL-*` checkpoint.
- The sequence describes what must happen before integration and what can proceed in parallel.
- Parallelization is allowed only after the first proof or after contracts are stable.
- Component-order plans such as `schema -> API -> UI -> tests` are insufficient unless each step proves incremental value.
- Work packages cover every `OBJ-*` and every writable `SURF-*`.

### Template

Planning strategy:

Critical path hypothesis:

First proving slice:

Validation cadence:

Deferred completeness:

| ID | Objective | Owner | Inputs | Outputs | Dependencies | Validation checkpoint | Completion criteria |
| --- | --- | --- | --- | --- | --- | --- | --- |
| WP-1 |  |  |  |  |  | VAL- |  |

Execution sequence:

Parallelization rules:

Integration points:

Section status:

## 7. Execution Controls and Drift Management

### Required Output

- Controls that keep implementation aligned with source authority and scope.
- Rules for handling discovered complexity, scope expansion, or design gaps.
- Conditions that require pause, escalation, or re-estimation.

### Exit Criteria

- At least one `CTRL-*` row is present.
- Every control row has non-empty `Trigger`, `Required action`, `Owner`, and `Evidence` cells.
- The section identifies conditions that require a `DEV-*` deviation.
- The section identifies conditions that require returning to design, ticket, or decision owner review.

### Template

| ID | Trigger | Required action | Owner | Evidence |
| --- | --- | --- | --- | --- |
| CTRL-1 |  |  |  |  |

Deviation rules:

Pause or escalation conditions:

Section status:

## 8. Data, Schema, Config, and Contract Handling

### Required Output

- All data, schema, config, event, API, permission, and compatibility impacts.
- Migration or backfill steps where applicable.
- Rollback and compatibility constraints.

### Exit Criteria

- If any data, config, schema, API, event, permission, or contract changes, at least one row is present.
- Every row has non-empty `Impact`, `Compatibility`, `Reversibility`, and `Validation` cells.
- Irreversible or cross-version behavior is explicitly called out.
- If the section is `N/A`, the rationale names the checked surfaces.

### Template

| Change | Impact | Compatibility | Reversibility | Validation |
| --- | --- | --- | --- | --- |
|  |  |  |  |  |

N/A rationale:

Section status:

## Layer 3: Validation, Release, and Handoff

## 9. Validation and Evidence Plan

### Required Output

- Tests, inspections, manual checks, generated artifacts, measurements, or runtime evidence required before completion.
- Evidence owner and storage location for each item.
- Clear distinction between pre-merge, pre-release, and post-release validation.

### Exit Criteria

- At least one `VAL-*` row is present.
- Every row has non-empty `Method`, `Claim verified`, `Timing`, `Owner`, and `Evidence artifact` cells.
- Every `OBJ-*`, `WP-*`, and high-risk `RISK-*` has validation coverage.
- Validation includes the highest-risk claim, not only easy success cases.

### Template

| ID | Method | Claim verified | Timing | Owner | Evidence artifact |
| --- | --- | --- | --- | --- | --- |
| VAL-1 | Test / Review / Manual / Measurement / Runtime signal |  | Pre-merge / Pre-release / Post-release |  | EVD-1 |

Section status:

## 10. Review Plan

### Required Output

- Required reviewers and review scope.
- Review checklist tied to change surfaces and risks.
- Approval conditions for merge or completion.

### Exit Criteria

- At least one `REV-*` row is present.
- Every row has non-empty `Reviewer`, `Review scope`, `Blocking?`, and `Completion evidence` cells.
- Review covers every writable `SURF-*` and every material risk area.
- Approval conditions are explicit.

### Template

| ID | Reviewer | Review scope | Blocking? | Completion evidence |
| --- | --- | --- | --- | --- |
| REV-1 |  |  | Yes / No |  |

Approval conditions:

Section status:

## 11. Rollout, Migration, Rollback, and Recovery

### Required Output

- Rollout or activation plan.
- Migration or backfill plan if applicable.
- Rollback, containment, and recovery plan.
- Abort triggers and responsible operator.

### Exit Criteria

- At least one `REL-*` row is present for anything that ships, deploys, migrates, activates, or changes live operation.
- Every row has non-empty `Action`, `Timing`, `Owner`, `Abort trigger`, and `Evidence` cells.
- Rollback is executable by a named role and has a stated limit.
- If rollback is constrained, the execution level is `E3` and the constraint is represented in risks, controls, release actions, and the final gate.

### Template

| ID | Action | Timing | Owner | Abort trigger | Evidence |
| --- | --- | --- | --- | --- | --- |
| REL-1 |  |  |  |  |  |

Rollback or containment plan:

Recovery limit:

Section status:

## 12. Observability and Operational Readiness

### Required Output

- Signals, dashboards, logs, alerts, audit entries, or manual observation points.
- Operator actions and runbook updates.
- Post-release monitoring window.

### Exit Criteria

- If the change can affect live operation, at least one `OBS-*` row is present.
- Every row has non-empty `Signal`, `Purpose`, `Consumer`, and `Response` cells.
- Operator actions are explicit or the section states that no operator action is required.
- Monitoring duration is stated for production-facing work.

### Template

| ID | Signal | Purpose | Consumer | Response |
| --- | --- | --- | --- | --- |
| OBS-1 |  |  |  |  |

Operator actions:

Monitoring window:

N/A rationale:

Section status:

## 13. Risks, Questions, Deviations, and Waivers

### Required Output

- Material execution risks and mitigations.
- Open questions with owner and due date.
- Approved deviations from this plan.
- Approved review waivers from this process.

### Exit Criteria

- At least one risk row is present, or the section explicitly states `No material risks identified` with rationale.
- Every `RISK-*` row has non-empty `Impact`, `Likelihood`, `Mitigation`, and `Validation` cells.
- Open questions either contain at least one `Q-*` row with owner, due date, and resolution path, or state `None` with rationale.
- Approved deviations either contain at least one `DEV-*` row with owner, approver, rationale, impact, and evidence, or state `None` with rationale.
- Approved waivers either contain at least one `WVR-*` row with approver, waived rule or finding, rationale, boundary or expiry, compensating control, and evidence, or state `None` with rationale.

### Template

Risks:

| ID | Risk | Impact | Likelihood | Owner | Mitigation | Validation |
| --- | --- | --- | --- | --- | --- | --- |
| RISK-1 |  |  |  |  |  |  |

Open questions:

| ID | Question | Owner | Due date | Blocking? | Resolution path |
| --- | --- | --- | --- | --- | --- |
| Q-1 |  |  |  | Yes / No |  |

Approved deviations:

| ID | Deviation | Owner | Approver | Rationale | Impact | Evidence |
| --- | --- | --- | --- | --- | --- | --- |
| DEV-1 |  |  |  |  |  |  |

Approved waivers:

| ID | Waived rule or finding | Approver | Rationale | Boundary or expiry | Compensating control | Evidence |
| --- | --- | --- | --- | --- | --- | --- |
| WVR-1 |  |  |  |  |  |  |

Section status:

## 14. Execution Traceability Matrix

### Required Output

- Mapping from source authority to objectives, change surfaces, work packages, validation, review, release, and evidence.
- Explicit coverage for every objective and high-risk item.

### Exit Criteria

- Every `SRC-*` and `OBJ-*` appears in the matrix.
- Every writable `SURF-*` maps to at least one `WP-*`, `VAL-*`, and `REV-*`.
- Every `WP-*` maps to at least one `OBJ-*` and one `VAL-*`.
- Every high-risk `RISK-*` maps to at least one `CTRL-*`, `VAL-*`, or `REL-*`.
- Every release action maps to evidence or an `N/A` rationale.

### Template

| Source or objective | Change surfaces | Work packages | Controls | Validation | Review | Release or ops | Evidence |
| --- | --- | --- | --- | --- | --- | --- | --- |
| SRC-1 / OBJ-1 | SURF-1 | WP-1 | CTRL-1 | VAL-1 | REV-1 | REL-1 / OBS-1 | EVD-1 |

Section status:

## 15. Final Execution Gate

### Required Output

- Entry gate before execution starts.
- Merge or completion gate before declaring work done.
- Release gate before activation or deployment.
- Handoff record after execution.

### Exit Criteria

- `Entry gate`, `Completion gate`, `Release gate`, `Handoff record`, and `Section status` fields are present and non-empty.
- No gate contains vague approval language without named evidence.
- All blocking dependencies, blocking reviews, required validations, and unresolved `Q-*` items are represented.
- Final readiness state is one of `Ready to investigate`, `Ready to execute`, `Ready to execute with heightened controls`, `Not ready`, or `Completed`, and it satisfies the readiness semantics below.

Readiness semantics:

| State | Allowed when |
| --- | --- |
| `Ready to investigate` | Execution level is `E0`, investigation entry gates are satisfied, no required section is `Incomplete`, and any unresolved `Q-*` items are the investigation targets rather than blockers. |
| `Ready to execute` | Execution level is `E1` or `E2`, the entry gate is satisfied, completion/release/handoff gates are evidence-based, no required section is `Incomplete`, all blocking dependencies and reviews are satisfied, and every `Blocker` or `Major` finding is `Resolved` or validly `Waived by WVR-*`. |
| `Ready to execute with heightened controls` | Execution level is `E3`, the entry gate is satisfied, completion/release/handoff gates are evidence-based, no required section is `Incomplete`, all blocking dependencies and reviews are satisfied, every `Blocker` or `Major` finding is `Resolved` or validly `Waived by WVR-*`, and heightened controls, independent review, rollback or containment, and waiver approvals are recorded. |
| `Not ready` | Any required gate is unsatisfied, the execution level is incorrect, a required section is `Incomplete`, a blocking dependency or `Q-*` item is unresolved, approval is missing, or any `Blocker` or `Major` finding is still `Open`. |
| `Completed` | Approved execution is complete, validation evidence is recorded, release or containment actions are complete or explicitly `N/A`, and the handoff record is available. |

### Template

Entry gate:

Completion gate:

Release gate:

Handoff record:

Final readiness state:

Section status:
