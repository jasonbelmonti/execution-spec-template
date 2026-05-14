---
name: execution-spec
description: Use when authoring, revising, or reviewing execution specifications for implementation work, especially when the spec needs source authority, execution level calibration, evidence-led execution, agent-focused package decomposition, work packages, milestone gates, validation gates, rollout, rollback, or review readiness.
metadata:
  short-description: Author and review execution specs
---

# Execution Spec

## Operating Modes

Use this skill in one mode per task:

- Author: create a new execution spec from a proposal, ticket, design, or implementation brief.
- Revise: update an existing execution spec while preserving identifiers, section numbering, and review traceability.
- Review: evaluate an execution spec against the required template and review process.

## Reference Loading

Load only the references needed for the current mode:

- Author or revise: read `references/execution-spec-template.md` and `references/execution-spec-authoring-guide.md`.
- Review: read `references/execution-spec-review-process.md` and the relevant template sections in `references/execution-spec-template.md`.
- Example calibration: read `references/examples/e1-bounded-docs-change-execution.md` when a concrete bounded-change example would reduce ambiguity.

## Required Discipline

- Establish source authority before drafting implementation details.
- Define the evidence-led execution model before package decomposition: observable outcome, critical path hypothesis, first proving slice, primary risks or unknowns, validation cadence, and deferred completeness.
- Treat observable value and risk retirement as the default sequencing doctrine, not an optional upstream planning concern.
- Choose and justify the execution level before expanding work packages.
- Apply Section 7, "Agent-Focused Package Decomposition", whenever code, contracts, schemas, packages, or multi-agent implementation are affected.
- Mark Section 7 `N/A` only when the template conditions allow it, and include the rationale.
- Apply Section 9, "Milestone Gates and Manual Verification", for hard human approval checkpoints with due points, named verifiers, required evidence, review gates, approval decisions, failure paths, and step-by-step manual verification.
- Give every `PKG-*` entry a boundary card with ownership, public interface, allowed dependencies, forbidden dependencies, agent editable paths, agent read-only paths, validation, and promotion blockers.
- Require every `PKG-*` and `WP-*` entry to trace to observable value, risk retired, milestone gates, and validation evidence.
- Keep milestone requirements non-waivable when missing, insufficient, due without approval evidence, or broken in traceability.
- Keep package levels precise: Level 2 is the default for app-specific agent-owned modules; Level 3 or 4 requires reusable cross-project value and stricter independence.
- Convert ambiguous ownership, overlapping editable paths, or bidirectional dependencies into explicit coordination triggers or package redesign.
- Reject specs organized only by component-layer order, such as `schema -> API -> service -> UI -> tests`, unless each step proves incremental value, retires a risk, and has decision-grade validation.
- Do not leave placeholder text, empty sections, or unresolved unknowns unless the template explicitly allows an `unknown` with owner, impact, and decision gate.

## Output Shape

- For authoring or revision, return the completed or changed execution spec sections and identify any unresolved decision gates.
- For review, lead with blocking findings, then non-blocking observations, then the verdict.
- For implementation handoff, include observable outcome, critical path hypothesis, first proving slice, package IDs, work package IDs, milestone IDs, editable paths, read-only paths, validation checkpoints, sequencing, value/risk traces, and coordination triggers.
