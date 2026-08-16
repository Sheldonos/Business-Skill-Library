---
name: role-capability-director
description: Create or revise a Capability Director contract for one enterprise role outcome. Use after capability intake and before composing atomic skills, tools, and proactive behavior.
---

# Role Capability Director

Create the thin accountable director for a role-level outcome. The director owns case state, orchestration, decision routing, and outcome telemetry. It does not absorb specialist procedures or assume human authority.

## Procedure

1. Read the validated capability brief and identify the one outcome this CD owns. Split unrelated outcomes into separate CDs.
2. Define scope, exclusions, parent/child interfaces, target users, named accountable human roles, and the system of record for the case.
3. Create a state machine with valid transitions, state owners, aging thresholds, exception states, and terminal completion criteria.
4. Select the reusable shared skills and domain atomic skills. Add a new atomic skill only with documented reuse failure and a discrete typed artifact.
5. Set input/output schemas, evidence envelope requirements, knowledge authority, and information classification boundaries.
6. Establish the maximum action tier, autonomous actions, recommend-only actions, mandatory approvals, hard stops, and human escalation route.
7. Set P0 by default. If P1–P4 is needed, require a completed proactivity profile before the CD is eligible for implementation.
8. Define outcome metrics, quality metrics, safety guardrails, SLOs, cost boundary, evaluation cases, and customer extension points.
9. Produce the contract and confirm it is reviewable by business, control, data, evaluation, and operations owners.

## Minimum contract

```yaml
capability_director:
  id: CD-<DOMAIN>-<OUTCOME>
  version: 0.1.0
  mission: ""
  job_to_be_done: ""
  outcome_metric: []
  guardrail_metric: []
  accountable_human_owner: ""
  case_system_of_record: ""
  states: [intake, qualified, planned, in_progress, awaiting_review, completed, exception, stopped]
  scope: []
  exclusions: []
  orchestration_graph_ref: ""
  knowledge_policy_ref: ""
  maximum_action_tier: A0
  decision_rights_ref: ""
  proactivity_profile_ref: "P0"
  evaluation_ref: ""
  operations_profile_ref: ""
  customer_extension_points: []
  protected_fields: [mission, authority, policy, evaluation_threshold, action_tier]
```

## Hard stops

Do not create a CD when there is no named outcome owner, no case system of record, unclear material-decision boundary, no controlled source plan, or no ability to evaluate the target outcome. Route the capability back to intake.
