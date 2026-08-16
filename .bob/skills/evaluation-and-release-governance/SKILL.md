---
name: evaluation-and-release-governance
description: Test, certify, promote, update, or retire IBM Mode capability packages. Use before pilot or production release and after material changes to skills, knowledge, tools, models, policies, or authority.
---

# Evaluation and Release Governance

Treat release as an evidence decision. A fluent demonstration, successful import, or passing happy path is not production readiness.

## Procedure

1. Identify the package version, changed components, dependencies, action tier, proactivity level, data class, industry overlay, and affected customers/cases.
2. Build a versioned evaluation set with representative, negative, adversarial, stale/conflicting evidence, tool failure, permission denial, collaboration, escalation, and rollback cases.
3. Test capability quality, grounding, source precedence, structured outputs, boundary compliance, tool selection/parameterization, action-tier enforcement, handoff completeness, proactivity precision, cost, latency, and recovery behavior.
4. Run independent review. The builder cannot be the sole evaluation approver. Collect process-owner, control-owner, data-owner, security/tool-owner, evaluation-owner, and operations-owner evidence as applicable.
5. Classify failures by severity and disposition. Block promotion on unresolved safety, authority, privacy, security, material-quality, or rollback failures.
6. Compare results against the prior released version. Require regression acceptance and change-impact review before promotion.
7. Produce a release decision: reject, sandbox, draft, pilot, production, restricted/regulated production, rollback, or retire.
8. Preserve test inputs/outputs according to classification and retention policy. Record signed approvals, package hashes/versions, connector versions, and release timestamp.

## Release gate schema

```yaml
release_gate:
  package_id: ""
  version: ""
  target_environment: sandbox | draft | pilot | production | regulated_production
  change_summary: []
  risk_profile: ""
  tests:
    capability: []
    grounding_and_evidence: []
    boundary_and_policy: []
    tool_and_connection: []
    collaboration_and_handoff: []
    proactivity: []
    security_and_abuse: []
    reliability_cost_latency: []
    rollback: []
  thresholds: []
  failure_register: []
  approvals:
    business_owner: ""
    process_owner: ""
    control_owner: ""
    evaluation_owner: ""
    operations_owner: ""
  decision: reject | approve_sandbox | approve_pilot | approve_production | rollback | retire
```

## Promotion rule

Promote only when the named approvals exist, all mandatory thresholds pass, no critical failure remains unresolved, the live tool/identity model has been tested appropriately, operations and rollback are ready, and the package contract accurately reflects the released behavior.
