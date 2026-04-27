# Execution Specification Authoring Guide

## Purpose

This guide is the author-facing operating procedure for writing an execution specification. The template defines the artifact. The review process defines approval control. This guide explains how to draft an execution plan without skipping source authority, package boundaries, sequencing, milestone verification, validation, or release control.

## Authoring Sequence

Write the document in this order:

1. Select `E0`, `E1`, `E2`, or `E3`.
2. Fill Document Control, section 0, and Layer 1 before drafting work packages.
3. Fill the change surface inventory before defining package boundaries.
4. Fill agent-focused package decomposition before assigning work packages for code, contract, schema, package, or multi-agent implementation.
5. After inventorying change surfaces and package boundaries, identify the core value proposition, critical path hypothesis, top unknowns, first proving slice, and sequencing strategy before assigning work packages.
6. Define milestone gates and their manual verification guides after assigning work packages and before filling controls or validation.
7. Fill controls before validation, so validation proves the risky claims instead of only confirming happy paths.
8. Fill rollout, rollback, observability, and handoff before requesting review.
9. Complete the traceability matrix and final execution gate last.

Do not use work packages to smuggle in new product, design, or operational decisions. If execution reveals a missing decision, record a `Q-*` question or `DEV-*` deviation and escalate it.

## Sequencing Strategy

Default to `STRATEGIES.RISK_RETIREMENT` when unknowns, dependencies, migrations, interfaces, or operational behavior could invalidate the plan.

Default to `STRATEGIES.PROGRESSIVE_VALUE` when the path is understood and the safest execution shape is a series of independently reviewable slices.

Use `CONTRACT_FIRST` when multiple implementers, repositories, services, or clients need stable schemas, APIs, events, permissions, fixtures, or document structure before parallel execution.

Use `OPERABILITY_FIRST` when observability, rollback, support procedure, migration safety, or incident response capability must exist before feature completion.

Use `SPIKE_THEN_SLICE` when a bounded investigation must retire an unknown before the author can define executable work packages.

Avoid sequencing by component layer alone. A plan ordered as `schema -> API -> UI -> tests` is acceptable only when each step identifies the evidence it produces and the decision it unlocks.

## Execution Level Selection

Use `E0` when the work is an investigation, audit, measurement pass, or prototype whose purpose is to retire uncertainty.

Use `E1` when the work is small, reversible, has one owner, and has bounded operational risk.

Use `E2` when the work is production or durable internal execution and does not qualify for `E1` or trigger `E3`.

Use `E3` when failure could cause safety impact, security incident, regulatory breach, irreversible data loss, large financial loss, broad operational outage, or constrained rollback.

If another engineer could not execute the plan from the artifact and linked sources, raise the level or revise the artifact.

## Identifier Discipline

Assign stable IDs before review and do not renumber casually after review starts.

- `SRC-*` identifies the authority for the work.
- `OBJ-*` and `NG-*` define execution outcomes and exclusions.
- `SURF-*` identifies change surfaces.
- `PKG-*` identifies package, module, or reusable library boundaries that constrain agent execution.
- `WP-*` identifies owned work packages.
- `MS-*` identifies milestone gates that require human verification and approval.
- `CTRL-*` identifies execution safeguards.
- `VAL-*` identifies validation activities.
- `REV-*` identifies review checks.
- `REL-*` identifies rollout, rollback, migration, or release actions.
- `OBS-*` identifies operational signals.
- `EVD-*` identifies produced evidence.
- `RISK-*`, `Q-*`, `DEV-*`, and `WVR-*` identify risk, unresolved questions, approved execution deviations, and approved review waivers.

Use `VAL-*` for proof activities. Use `EVD-*` for the evidence artifacts those activities produce.

Use `MS-*` for hard approval gates. Each milestone shall name the covered work, human verifier, prerequisite evidence, step-by-step manual verification guide, approval decision, and failure path.

## Agent-Focused Package Decomposition

Use section 6 to convert architecture intent into agent execution boundaries.

Each `PKG-*` entry shall answer:

- What the unit owns.
- What the unit explicitly does not own.
- What public interface other code may use.
- What imports and calls are allowed.
- What imports and calls are forbidden.
- What state the unit may read or mutate.
- What paths an assigned agent may edit.
- What paths an assigned agent may read but not edit.
- What command proves the unit still works.
- What blocks promotion to a higher package-ladder level.

Do not classify a unit as a reusable candidate because it seems generally useful. Classify it as level 3 only when it has no product-specific routes, UI assumptions, deployment assumptions, direct database ownership, implicit environment reads, or app-layer imports.

Use the ladder conservatively:

- Use level 0 or 1 for local implementation details that do not need isolated agent ownership.
- Use level 2 when multiple features need the unit or when an app-specific feature/module needs isolated agent ownership.
- Use level 3 when the API is project-agnostic but not yet published.
- Use level 4 only when compatibility, release, and ownership processes exist.

Every `PKG-*` entry shall include a boundary card. If a proposed boundary cannot name forbidden dependencies and editable paths, it is not ready to support parallel agent execution. Revise the boundary before assigning independent work packages.

## Agent Work Package Rules

Each `WP-*` row shall name a `PKG-*` boundary when package decomposition applies. Editable paths are the write authorization for that agent. Read-only paths are context, not ownership.

Before assigning parallel work, check for these invalid conditions:

- Two work packages list the same editable path.
- A work package needs to change another package's public interface without a coordination trigger.
- A reusable candidate depends on app, UI, route, database, deployment, or product-specific runtime code.
- Package validation requires the full application when a package-level command should exist.
- Business rules are assigned to UI, request-handler, script, or integration-glue surfaces without an explicit rationale.

If any invalid condition is present, either revise the package decomposition, serialize the work packages, or add a named coordination trigger and control.

## Milestone Drafting Rules

Treat milestones as operator-verifiable checkpoints, not schedule labels.

- Write the milestone around the functionality or operational capability being approved.
- Link each milestone to the `WP-*`, `VAL-*`, `REV-*`, and `EVD-*` rows that prove it.
- Include manual verification steps that a human operator can execute without hidden context.
- Cover the full functionality encapsulated by the milestone; excluded behavior requires an explicit `N/A` rationale.
- Record what evidence the verifier must capture and what decision phrase marks approval, rejection, or conditional approval.
- Define the failure path before execution so a failed milestone cannot silently become drift.

## E1 Bounded Change Drafting Rules

For `E1`, keep the artifact short but explicit:

- Preserve section numbers so reviewers can compare documents consistently.
- Mark omitted sections `N/A` and state the checked surfaces or reason.
- Use compact tables, but do not combine unrelated objectives, work packages, or validation claims.
- Raise to `E2` or `E3` if the work touches a new trust boundary, irreversible migration, high-blast-radius dependency, security-sensitive path, or ambiguous rollback.

## Author Self-Check

Before requesting review, the author shall be able to answer `yes` to each question:

- Does every work package trace to approved source authority?
- Does every applicable work package map to a `PKG-*` boundary with explicit editable paths?
- Does every work package map to a milestone gate with human verification?
- Does every writable surface have an owner and review expectation?
- Are forbidden dependencies and coupling tripwires explicit enough to keep agents inside their assigned scope?
- Can another engineer execute the sequence without asking for hidden context?
- Can the named verifier execute each milestone guide step-by-step and capture evidence?
- Does validation prove the highest-risk claims?
- Is rollback or containment executable by a named role?
- Are unresolved questions either non-blocking or represented in the final gate?
- Would the plan still be honest if the execution level were raised by one step?

## Review Handoff

Send reviewers the execution spec, source design or ticket, branch or diff if available, milestone evidence already produced, test evidence already produced, and any deviations from the plan. State the requested decision exactly as one of the allowed decision phrases in section 0.
