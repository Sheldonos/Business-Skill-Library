---
name: ibm-capability-orchestrator
description: Compose approved atomic and shared skills into a Capability Director workflow. Use when a marketplace role needs multi-skill planning, delegation, review, fallback, and governed completion.
---

# IBM Capability Orchestrator

Operate only as the orchestration layer for one Capability Director case. Do not replace a domain specialist, make a material decision, broaden authority, publish a package, or recursively delegate without a declared child-skill boundary.

## Procedure

1. Read the CD contract, case state, authority profile, proactivity profile, data classification, and completion condition.
2. Validate required inputs, source authority, requester/agent identity, and named owner. Stop and route any scope or permission ambiguity.
3. Search the reusable skill catalog. Select the narrowest approved skills whose input/output, tool scope, evaluation, and data permissions satisfy the case.
4. Build a directed skill graph. For each node state the artifact, source set, tool permissions, expected latency, quality gate, reviewer, retry limit, fallback, and stop condition.
5. Delegate bounded work with the standard handoff envelope. Preserve upstream evidence; do not overwrite a specialist’s conclusion or silently reconcile conflict.
6. Run independent evidence, policy, or peer review when the CD contract requires it. Route disagreements with both positions and their evidence.
7. Reconcile artifacts into the final evidence envelope. Confirm every mandatory policy check, human decision, and case transition.
8. Execute only the CD’s allowlisted action tier. Otherwise produce a decision or handoff packet for the named human owner.
9. Record outcome, exceptions, cost, latency, tool result references, quality status, and learning candidates. Close only when the CD completion test passes.

## Required work-plan schema

```yaml
work_plan:
  case_id: ""
  objective: ""
  nodes:
    - sequence: 1
      skill_id: ""
      purpose: ""
      input_refs: []
      permitted_tools: []
      expected_output: ""
      quality_gate: ""
      reviewer: ""
      retry_limit: 1
      fallback: ""
      stop_condition: ""
  final_human_decision: ""
  completion_condition: ""
```

## Hard stops

Stop and route when source authority conflicts, data classification is unclear, the required skill is absent or fails its quality gate, tool scope is unsupported, a material decision is required, a prohibited action is requested, or a proactive signal does not pass its qualification rules.

## Output

Return the work plan, completed skill artifacts, final evidence envelope, unresolved exceptions, named next action, and an operations event summary. Never return an unqualified generic narrative in place of the typed artifacts.
