# Execution Specification Authoring Guide

## Purpose

This guide is the author-facing operating procedure for writing an execution specification. The template defines the artifact. The review process defines approval control. This guide explains how to draft an execution plan without skipping source authority, sequencing, validation, or release control.

## Authoring Sequence

Write the document in this order:

1. Select `E0`, `E1`, `E2`, or `E3`.
2. Fill Document Control, section 0, and Layer 1 before drafting work packages.
3. Fill the change surface inventory before assigning work packages.
4. Fill controls before validation, so validation proves the risky claims instead of only confirming happy paths.
5. Fill rollout, rollback, observability, and handoff before requesting review.
6. Complete the traceability matrix and final execution gate last.

Do not use work packages to smuggle in new product, design, or operational decisions. If execution reveals a missing decision, record a `Q-*` question or `DEV-*` deviation and escalate it.

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
- `WP-*` identifies owned work packages.
- `CTRL-*` identifies execution safeguards.
- `VAL-*` identifies validation activities.
- `REV-*` identifies review checks.
- `REL-*` identifies rollout, rollback, migration, or release actions.
- `OBS-*` identifies operational signals.
- `EVD-*` identifies produced evidence.
- `RISK-*`, `Q-*`, `DEV-*`, and `WVR-*` identify risk, unresolved questions, approved execution deviations, and approved review waivers.

Use `VAL-*` for proof activities. Use `EVD-*` for the evidence artifacts those activities produce.

## E1 Bounded Change Drafting Rules

For `E1`, keep the artifact short but explicit:

- Preserve section numbers so reviewers can compare documents consistently.
- Mark omitted sections `N/A` and state the checked surfaces or reason.
- Use compact tables, but do not combine unrelated objectives, work packages, or validation claims.
- Raise to `E2` or `E3` if the work touches a new trust boundary, irreversible migration, high-blast-radius dependency, security-sensitive path, or ambiguous rollback.

## Author Self-Check

Before requesting review, the author shall be able to answer `yes` to each question:

- Does every work package trace to approved source authority?
- Does every writable surface have an owner and review expectation?
- Can another engineer execute the sequence without asking for hidden context?
- Does validation prove the highest-risk claims?
- Is rollback or containment executable by a named role?
- Are unresolved questions either non-blocking or represented in the final gate?
- Would the plan still be honest if the execution level were raised by one step?

## Review Handoff

Send reviewers the execution spec, source design or ticket, branch or diff if available, test evidence already produced, and any deviations from the plan. State the requested decision exactly as one of the allowed decision phrases in section 0.
