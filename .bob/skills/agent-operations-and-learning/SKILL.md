---
name: agent-operations-and-learning
description: Define runtime operations, observability, incidents, cost controls, knowledge refresh, and governed learning for IBM Mode capabilities. Use for pilot readiness, production operation, performance issues, or approved capability improvement.
---

# Agent Operations and Learning

Operate every released capability as a measurable service. Improvement is a versioned change process, not an automatic alteration of prompts, skills, memory, tools, or authority.

## Procedure

1. Define outcome, quality, safety, timeliness, reliability, tool, human-handoff, cost, and proactivity metrics. Name their owners and alert thresholds.
2. Emit standard events for intake, evidence access, skill execution, tool call, policy check, case transition, escalation, approval, action, error, rollback, and evaluation result.
3. Establish SLOs and error budgets for each service level. Add a human-attention budget for P1+ capabilities and rate limits for tool/action use.
4. Define incident severity, detection, containment, kill-switch authority, communications, evidence preservation, recovery, and post-incident review.
5. Monitor knowledge freshness, source access failures, tool/schema drift, model or workflow drift, policy violations, quality decline, cost anomalies, and recurring escalation patterns.
6. Capture learning candidates as proposals with source, evidence, scope, affected packages, risk, test impact, owner, and rollback plan. Do not apply them directly to live behavior.
7. Route accepted learning through change control, regression evaluation, approval, versioning, release, and retirement management.
8. Periodically review whether the CD, skills, tools, permissions, knowledge, and metrics are still needed. Retire capabilities by revoking access, archiving evidence, migrating users, and marking dependencies.

## Operations profile

```yaml
operations_profile:
  capability_director: ""
  owners:
    business: ""
    operations: ""
    control: ""
  slo_targets: []
  metric_definitions: []
  cost_budget: ""
  alert_thresholds: []
  human_attention_budget: ""
  event_catalog: []
  incident_runbook_ref: ""
  kill_switch_authority: ""
  rollback_ref: ""
  knowledge_refresh_policy: ""
  drift_detection: []
  learning_change_policy: "versioned and evaluated"
  retirement_plan: ""
```

## Non-negotiable rule

An agent’s request volume, tool availability, or successful historical behavior does not create permission to expand scope, increase action tier, change durable memory, or bypass evaluation. Every material improvement is a controlled new version.
