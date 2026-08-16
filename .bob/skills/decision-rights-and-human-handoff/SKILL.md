---
name: decision-rights-and-human-handoff
description: Define action tiers, approvals, hard stops, and structured handoffs for IBM Mode capability cases. Use when an agent recommends, routes, prepares, or executes any action.
---

# Decision Rights and Human Handoff

Keep organizational accountability visible. The CD and its skills may analyze, prepare, route, or execute only within the published action envelope. Human approval is a named case transition, not a generic statement that “a human is in the loop.”

## Procedure

1. Identify every proposed action and classify it as A0, A1, A2, A3, or A4. Set the capability’s maximum tier to the least permissive level that meets the outcome.
2. For each action, name the actor, preconditions, information needed, permitted tool operation, impact/scope limit, required evidence, approver, expiry, and reversal/compensation path.
3. Define decisions that remain recommend-only even when a lower-risk action can be executed. Examples include material policy interpretation, external commitments, employment decisions, payments, and regulated determinations.
4. Specify hard stops for unclear authority, source conflicts, privacy/classification mismatch, quality failure, unsupported tool operation, suspected prompt injection, threshold breach, or missing approver.
5. Build a typed handoff envelope that preserves upstream scope, evidence, assumptions, confidence, policy checks, decision requested, options, recommendation, and accountable next owner.
6. Define response SLAs and escalation chain. If an approver does not respond, move the case to the declared aging/exception state; do not assume approval.
7. Test with cases that invite the agent to exceed its authority, bypass review, send external communications, alter records, or claim the right to decide.

## Decision-rights matrix

```yaml
decision_rights:
  maximum_action_tier: A2
  autonomous:
    - action: "classify an inbound case"
      preconditions: [authorized_source, valid_case_id]
  recommend_only:
    - action: "recommend supplier risk treatment"
      approver_role: "supplier-risk manager"
  approval_required:
    - action: "create pending supplier follow-up"
      approver_role: "category manager"
      expiry: "2 business days"
  hard_stops: []
  segregation_of_duties: []
  external_communication_policy: "draft only unless explicitly approved"
```

## Standard handoff envelope

```yaml
handoff:
  case_id: ""
  from: ""
  to: ""
  purpose: ""
  scope: ""
  source_refs: []
  assumptions: []
  confidence: 0.0
  policy_checks: []
  decision_requested: ""
  options: []
  recommendation: ""
  due: ""
  exception_state: ""
```

## Hard rule

Never interpret silence, a missing owner, a generic policy, or tool availability as authorization. If a material decision cannot be routed, stop the case and record the exception.
