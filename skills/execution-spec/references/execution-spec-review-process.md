# Execution Specification Review Process

Author-facing drafting guidance lives in `references/execution-spec-authoring-guide.md`. This document is the reviewer and decision-owner procedure.

## Purpose

This process shall determine seven things in order:

1. Is the selected execution level correct?
2. Is the execution source authority sufficient?
3. Does the plan organize execution around observable value and risk retirement?
4. Is the plan structurally complete for that level?
5. Is the execution sequence operationally viable?
6. Are milestone gates hard, evidence-based, and manually verifiable?
7. What approval decision, if any, is justified?

Review the artifact from authority to evidence. Do not spend most of the review on task mechanics if scope, ownership, validation, or rollback are weak.

## Review Outputs

Every review shall produce:

- An execution-level decision
- A source authority decision
- An evidence-led execution model decision
- A section-by-section status ledger
- A finding log with severity, status, owner, and required action
- A milestone gate result
- A traceability result
- A final verdict

## Review Roles

| Role | Responsibility |
| --- | --- |
| Author | Writes the execution spec, resolves findings, maintains traceability |
| Executor | Performs or coordinates the work packages |
| Moderator | Runs review order and prevents skipping source authority or validation |
| Domain reviewer | Challenges correctness, risk controls, and missing validation in a specific area |
| Decision owner | Approves, rejects, or requests rework |

For `E3` reviews, include at least one reviewer independent of the primary executor for the critical domain involved.

## Section Status Vocabulary

Use the same statuses as the template:

| Status | Review meaning |
| --- | --- |
| `Complete` | Required content exists and exit criteria are met |
| `Deferred` | Gap is explicit, bounded, owned, linked to one or more `Q-*` items, backed by a validation or resolution plan, and acceptable for the chosen execution level |
| `N/A` | Section truly does not apply; rationale is credible |
| `Incomplete` | Content or exit criteria are missing; approval cannot proceed |

## Severity Vocabulary

| Severity | Meaning |
| --- | --- |
| `Blocker` | If status is `Open`, approval shall not proceed |
| `Major` | Important weakness; review may continue, but approval shall not proceed while status is `Open` |
| `Minor` | Useful improvement; does not materially undermine execution |
| `Observation` | Reviewer note with no immediate action required |

## Finding Status Vocabulary

| Status | Meaning |
| --- | --- |
| `Open` | Finding remains unresolved and shall affect the verdict according to severity |
| `Resolved` | Required action completed and reviewer verified the result |
| `Waived by WVR-*` | Finding is covered by an approved review waiver that this process permits |
| `Closed` | No further action required because the item is informational or intentionally non-blocking; use only for `Minor` or `Observation` findings |

## Waiver Rules

Waivers are review-control exceptions, not execution-plan deviations. Record execution-plan departures as `DEV-*`; record review or approval exceptions as `WVR-*`.

A `WVR-*` waiver shall include the waived rule or finding, approver, rationale, boundary or expiry, compensating control, and evidence. The decision owner shall approve every waiver. For `E3`, the critical-domain reviewer shall also approve the waiver.

These findings are not waivable:

- Incorrect execution level.
- Missing or insufficient source authority.
- Any plan that asks executors to resolve product, design, security, or operational authority gaps locally.
- Missing validation for the highest-risk claim.
- Missing observable outcome, critical path hypothesis, or first proving slice.
- Missing rollback or containment for work that affects live systems.
- Broken traceability for a critical objective, work package, or high-risk surface.
- Missing or insufficient milestone gate specification.
- Missing milestone due point, manual verification guide, named human verifier, required milestone approval evidence definition, or milestone failure path.
- Unapproved milestone gate, or missing named verifier approval evidence, for an `MS-*` whose due point has arrived.
- Broken milestone traceability between covered work, validation, review, approval requirements, or evidence.

Section 9 milestone specification requirements and due milestone approval requirements are hard gates. They shall not be satisfied by `Deferred` status or by a `WVR-*` waiver.

All other `Blocker` or `Major` findings may be waived only when the process or template permits `Deferred` treatment, the gap is bounded, the compensating control is explicit, and the final verdict records the `WVR-*` identifier.

## Stage 0: Execution Level Calibration

Before reviewing the plan itself, verify that the selected execution level matches the operational risk.

### Calibration Questions

- Is the document asking for investigation approval or execution approval?
- If labeled `E1`, are all bounded-change eligibility conditions true?
- Could execution failure cause safety, security, compliance, financial, or irreversible data impact?
- Does the change touch a shared platform, high-volume path, or high-blast-radius dependency?
- Is rollback constrained, manual, expensive, or impossible?
- Does the plan depend on coordinated releases across multiple owners?

### Calibration Rules

- If the work is exploratory and intended to answer uncertainty, `E0` may be correct.
- If the work is small, reversible, owned by one party, and has bounded operational risk, `E1` may be correct.
- If the work is intended for production or durable internal use and does not qualify for `E1` or trigger `E3`, default to `E2`.
- If any `E3` trigger from the template applies, review as `E3`.

### Calibration Blocking Conditions

Stop the review and return the document if any of the following are true:

- The document is labeled `E0` but asks for shipping or production approval.
- The document is labeled below the true operational risk.
- The document is labeled `E1` while any bounded-change eligibility condition is false or unclear.
- The document asks executors to resolve product, design, security, or operational authority gaps locally.

### Calibration Output

| Field | Value |
| --- | --- |
| Proposed execution level |  |
| Reviewed execution level |  |
| Calibration result | Accept / Raise / Lower |
| Rationale |  |

## Stage 1: Source Authority and Structural Review

Structural review asks whether the plan is executable and reviewable.

Evaluate every section against five quality dimensions:

- `Presence`
- `Precision`
- `Authority`
- `Traceability`
- `Execution utility`

### Source Authority Output

| Field | Value |
| --- | --- |
| Source authority result | Accept / Insufficient |
| Rationale |  |

### Section Review Ledger

| Section | Reviewer question | Status | Findings |
| --- | --- | --- | --- |
| 0. Execution Summary | Can I state the requested execution decision and entry condition? |  |  |
| 1. Source Authority and Scope | Is the authority for the work explicit and sufficient? |  |  |
| 2. Objectives and Non-Objectives | Do outcomes and exclusions bound the work? |  |  |
| 3. Ownership, Roles, and Decision Points | Are owners, reviewers, and escalation paths explicit? |  |  |
| 4. Constraints, Assumptions, and Dependencies | Are blockers and assumptions visible and managed? |  |  |
| 5. Evidence-Led Execution Model | Are observable value, critical path, first proving slice, risk retirement, and validation cadence explicit? |  |  |
| 6. Change Surface Inventory | Are all touched systems and review surfaces identified? |  |  |
| 7. Agent-Focused Package Decomposition | Are package boundaries, ladder levels, dependency rules, agent edit boundaries, and value/risk traces explicit? |  |  |
| 8. Work Packages and Sequencing | Can the work be executed in the stated order and does it prove value or retire risk early? |  |  |
| 9. Milestone Gates and Manual Verification | Are human approval gates evidence-based and operator-verifiable? |  |  |
| 10. Execution Controls and Drift Management | Will the team detect unsafe scope or design drift? |  |  |
| 11. Data, Schema, Config, and Contract Handling | Are compatibility and reversibility impacts explicit? |  |  |
| 12. Validation and Evidence Plan | Does validation prove completion, observable outcome, and risky claims? |  |  |
| 13. Review Plan | Are required reviewers and approval conditions explicit? |  |  |
| 14. Rollout, Migration, Rollback, and Recovery | Can the change be deployed and recovered safely? |  |  |
| 15. Observability and Operational Readiness | Can operators detect and respond to failure? |  |  |
| 16. Risks, Questions, Deviations, and Waivers | Are risks, unknowns, deviations, and waivers honestly represented? |  |  |
| 17. Execution Traceability Matrix | Is the chain from source to milestone approval requirements and evidence intact? |  |  |
| 18. Final Execution Gate | Are entry, milestone, completion, release, and handoff gates evidence-based? |  |  |

### Structural Blocking Conditions

Stop the review if any of the following are true:

- Any required section is `Incomplete`.
- Source authority is absent or insufficient.
- Work packages do not cover the stated objectives.
- Milestone gates are absent, lack due points or manual verification steps, or do not define required human approval evidence.
- Section 5 does not define an observable outcome, critical path hypothesis, first proving slice, and risk-retirement logic.
- Writable change surfaces lack owners or review expectations.
- Applicable package boundaries lack ladder levels, public interfaces, forbidden dependencies, editable paths, value/risk trace, or validation commands.
- Reusable package candidates depend on app, UI, route, database, deployment, or product-specific runtime code without a waiver.
- Validation does not cover the observable outcome or highest-risk claim.
- Rollout or rollback is absent for work that can affect live systems.
- A blocking dependency is missing from the final gate.
- The traceability chain from source to milestone approval requirements and evidence for due milestones is visibly broken.

### Structural Output

| Finding ID | Severity | Status | Section | Finding | Required action | Owner |
| --- | --- | --- | --- | --- | --- | --- |
| ST-1 | Blocker / Major / Minor / Observation | Open / Resolved / Waived by WVR-* / Closed |  |  |  |  |

If any blocker has status `Open`, do not proceed to execution viability review. Go directly to Stage 4 and issue a verdict based on the completed stages.

## Stage 2: Execution Viability Review

Execution viability asks whether the plan would complete safely if followed exactly as written.

### Viability Dimensions

Score each applicable dimension from `0` to `3`. Use `N/A` only when the corresponding template section is explicitly marked `N/A` with rationale.

- `0`: absent or invalid
- `1`: weak; major doubt remains
- `2`: adequate; review can proceed with follow-up
- `3`: strong; well-supported and internally consistent
- `N/A`: not applicable because the corresponding template section is explicitly `N/A` with rationale; exclude from minimum numeric score thresholds

| Dimension | Review question |
| --- | --- |
| Authority fitness | Is the source decision sufficient for execution? |
| Scope control | Are inclusions, exclusions, and escalation rules clear? |
| Value/risk model adequacy | Does section 5 define observable outcome, critical path, first proving slice, primary risks or unknowns, and validation cadence clearly enough to govern execution? |
| Sequence adequacy | Are work packages ordered to prove the critical path early, retire the highest-risk unknowns, and produce validation evidence at each step? |
| Surface coverage | Are all changed systems, files, data, configs, and contracts represented? |
| Milestone adequacy | Do milestone gates state due points, require human verification, cover their full functionality, and link to evidence, review, and failure paths? |
| Package boundary adequacy | Are package levels, public interfaces, forbidden dependencies, editable paths, value/risk traces, and validation commands specific enough for isolated agent execution? |
| Validation adequacy | Does evidence prove the observable outcome and risky claims? |
| Review adequacy | Are the right reviewers assigned to the right surfaces? |
| Operational safety | Are rollout, rollback, recovery, and observability credible? |

### Viability Blocking Conditions

Return the document for rework if any of the following are true:

- Executors would need to make unapproved design, product, or operational decisions.
- Section 5 fails to identify a first proving slice, or the proving slice cannot produce decision-grade evidence.
- The sequence creates avoidable integration or deployment hazards.
- Package boundaries allow hidden coupling, shared editable paths, or undeclared cross-package changes.
- A required milestone lacks a named human verifier, manual verification guide, required evidence, approval decision, or failure path.
- The sequence is primarily component-layer order and does not identify incremental value, risk retirement, or validation checkpoints.
- Critical surfaces are omitted from review or validation.
- The validation plan could pass while the approved outcome remains unmet.
- The rollback or recovery plan is unsafe for the execution level.

### Minimum Acceptable Scores by Execution Level

| Execution level | Minimum acceptable posture |
| --- | --- |
| `E0` | No applicable dimension may score `0`; `Authority fitness`, `Scope control`, `Value/risk model adequacy`, `Milestone adequacy`, and `Validation adequacy` shall score at least `2` |
| `E1` | No applicable dimension may score `0`; `Authority fitness`, `Value/risk model adequacy`, `Sequence adequacy`, `Milestone adequacy`, `Validation adequacy`, and `Review adequacy` shall score at least `2`; `Package boundary adequacy` shall score at least `2` when section 7 applies |
| `E2` | No applicable dimension may score `0`; all applicable dimensions shall score at least `2`; `Package boundary adequacy` shall score at least `2` when section 7 applies; `Milestone adequacy` shall score at least `2` |
| `E3` | No applicable dimension may score below `2`; `Value/risk model adequacy`, `Validation adequacy`, `Review adequacy`, and `Operational safety` should normally score `3`; `Package boundary adequacy` shall score at least `2` when section 7 applies |

### Viability Output

| Finding ID | Severity | Status | Dimension | Finding | Evidence | Required action | Owner |
| --- | --- | --- | --- | --- | --- | --- | --- |
| EX-1 | Blocker / Major / Minor / Observation | Open / Resolved / Waived by WVR-* / Closed |  |  |  |  |  |

| Dimension | Score | Notes |
| --- | --- | --- |
| Authority fitness |  |  |
| Scope control |  |  |
| Value/risk model adequacy |  |  |
| Sequence adequacy |  |  |
| Surface coverage |  |  |
| Milestone adequacy |  |  |
| Package boundary adequacy |  |  |
| Validation adequacy |  |  |
| Review adequacy |  |  |
| Operational safety |  |  |

## Stage 3: Traceability Audit

Traceability review confirms that the plan forms an unbroken execution chain.

### Audit Questions

- Does every `SRC-*` map to at least one `OBJ-*` or `WP-*`?
- Does every `OBJ-*` map to one or more `WP-*` rows?
- Does the section 5 observable outcome map to one or more `OBJ-*`, `WP-*`, and `VAL-*` rows?
- Does the first proving slice map to the first `WP-*` or an explicitly bounded `E0` discovery package?
- Does every section 5 primary risk or unknown map to a `RISK-*` or `Q-*` row and one or more `VAL-*`, `CTRL-*`, `REL-*`, or `OBS-*` items?
- Does every applicable `PKG-*` map to one or more `SURF-*`, `WP-*`, `REV-*`, and `VAL-*` rows?
- Does every writable `SURF-*` map to one or more `WP-*`, `MS-*`, `REV-*`, and `VAL-*` rows?
- Does every `WP-*` have validation evidence?
- Does every `WP-*` map to a milestone gate?
- Does every `MS-*` map to covered work, manual verification steps, validation evidence path, review path, and an approval path, with an approval record when its due point has arrived?
- Does every high-risk `RISK-*` map to a control, validation item, release action, or observability signal?
- Does every blocking dependency and milestone appear in the final execution gate?

### Traceability Blocking Conditions

Return the document for rework if:

- Any objective has no work package.
- The observable outcome, critical path hypothesis, or first proving slice cannot be traced to work and validation.
- Any applicable package boundary has no work package, review, or validation path.
- Any work package has no validation path.
- Any work package has no milestone gate.
- Any milestone has no manual verification path, evidence path, review path, or approval path.
- Any high-risk surface lacks review coverage.
- Any release action lacks rollback, containment, or `N/A` rationale.
- The chain from source authority to milestone approval requirements and completion evidence cannot be followed by an independent reviewer.

### Traceability Output

| Finding ID | Severity | Status | Gap | Required action | Owner |
| --- | --- | --- | --- | --- | --- |
| TR-1 | Blocker / Major / Minor / Observation | Open / Resolved / Waived by WVR-* / Closed |  |  |  |

## Stage 4: Decision and Conditions

Make one base verdict after the last completed review stage.

If calibration, structural, viability, or traceability review stops the process early, skip the remaining stages and issue `Rework required` or `Reject` based on the evidence gathered so far.

Approval verdicts require every `Blocker` or `Major` finding to be `Resolved` or explicitly `Waived by WVR-*` where this standard permits a waiver. Conditions do not convert a `Major` finding into an approval.

Valid verdicts:

- `Approve to investigate`
- `Approve to execute`
- `Approve with heightened controls`
- `Rework required`
- `Reject`

### Conditions Format

| Condition ID | Applies to | Required action | Owner | Due |
| --- | --- | --- | --- | --- |
| COND-1 |  |  |  |  |

### Heightened Controls Format

| Control ID | Control | Owner | Evidence required |
| --- | --- | --- | --- |
| HC-1 |  |  |  |

## Review Record Template

| Field | Value |
| --- | --- |
| Reviewed artifact |  |
| Review date |  |
| Proposed execution level |  |
| Reviewed execution level |  |
| Calibration result |  |
| Source authority result |  |
| Evidence-led execution model result |  |
| Structural result |  |
| Viability result |  |
| Milestone gate result |  |
| Traceability result |  |
| Final verdict |  |

## Operating Rule

Do not approve execution because the task sounds small. Approve only when source authority, scope control, sequencing, milestone verification, validation, review, and recovery are strong enough for the selected execution level.
