# Capability Director Contract v2

A Capability Director (CD) is the accountable orchestration layer for one business outcome. The CD is not a broad expert persona. It owns the case lifecycle, chooses approved skills, enforces authority, reconciles evidence, manages proactivity, and delivers the final decision or handoff packet.

## Required fields

| Facet | Required definition | Depth test |
|---|---|---|
| Identity | Stable ID, name, publisher, version, lifecycle, dependencies. | Can an operator identify exactly what is installed and changed? |
| Outcome | Target user, job to be done, business outcome, KPI, guardrail metric, service-level target. | Would a business owner recognize success without reading prompt text? |
| Scope | Included scenarios, exclusions, non-responsibilities, interfaces to sibling CDs. | Can a request be cleanly accepted, redirected, or stopped? |
| Case model | State machine, state owner, transitions, aging rules, close criteria, durable record location. | Does the CD know what work remains and who owns it? |
| Inputs/outputs | Typed schemas, classification, evidence, confidence, assumptions, artifact consumer. | Can skills and humans exchange results without free-text ambiguity? |
| Skill graph | Required/optional skills, sequence, dependencies, peer checks, fallback, retry and stop rules. | Can the work be repeated with the same controls? |
| Knowledge | Source-of-truth ranking, allowed sources, freshness SLA, citation, retention, memory policy. | Does it resist stale, unsupported, or conflicting information? |
| Tools | Tool adapters, exact operations, field scope, action tier, timeout, rate limit, idempotency. | Does access stop at the minimum needed for the outcome? |
| Authority | Autonomous/recommend-only/approval-required actions, limits, approvers, hard stops. | Is no material decision delegated by accident? |
| Proactivity | P0–P4 level, schedule/event source, thresholds, suppression, attention budget, owner. | Can it safely initiate work and avoid alert fatigue? |
| Evaluation | Benchmark, scenarios, expected quality, boundary tests, tool tests, regression, SME acceptance. | Can a release decision be evidenced independently? |
| Operations | SLOs, cost budget, telemetry, incident, rollback, knowledge refresh, retirement. | Can the package be operated safely after pilot? |
| Change control | Customer extension points, protected fields, versioning, impact analysis, approval and rollback. | Can a customer tailor the package without eroding safety? |

## Required evidence envelope

Every CD must produce a standard evidence envelope at final handoff.

```yaml
case_id: ""
outcome_status: completed | awaiting_approval | exception | stopped
scope: ""
artifact_refs: []
source_refs: []
assumptions: []
confidence:
  overall: 0.0
  rationale: ""
policy_checks: []
tool_calls:
  - adapter_id: ""
    operation: ""
    action_tier: A0 | A1 | A2 | A3 | A4
    result_ref: ""
    reversible: true
human_decisions_required: []
proactive_trigger:
  level: P0 | P1 | P2 | P3 | P4
  trigger_ref: ""
next_action:
  owner: ""
  due: ""
telemetry_refs: []
```

## Action tiers

| Tier | Behavior | CD requirement |
|---|---|---|
| A0 | Read and analyze. | Record provenance and classification. |
| A1 | Draft an artifact. | Label draft, name reviewer, prevent sending/submission. |
| A2 | Prepare and route a governed work item or pending transaction. | Create approval gate, preserve packet and owner. |
| A3 | Execute a reversible, allowlisted low-risk action. | Validate preconditions, idempotency, audit, rate limits, rollback. |
| A4 | Restricted material action. | Dual control, strict threshold, evidence retention, incident playbook, explicit authorization. |

No CD may decide employment, clinical, legal, lending, insurance coverage, trading, payment, public-benefit, safety-critical, or binding external commitment outcomes without the applicable accountable human approval and policy controls.

## Completion test

A CD case is complete only when all conditions are true:

1. The defined outcome artifact or system-state result exists.
2. Required evidence, source lineage, assumptions, and confidence are present.
3. All skill quality checks and policy controls pass or an exception is recorded.
4. Every required human decision has a named owner and recorded disposition.
5. Any permitted write action has confirmation, audit, and rollback/compensation evidence.
6. The case is moved to the correct terminal or waiting state.
7. Outcome, cost, latency, and learning candidates are emitted to the operations profile.
