---
name: enterprise-capability-intake
description: Define and validate an enterprise outcome before building or changing an IBM Mode capability. Use for new agents, skills, workflows, industry overlays, or material capability changes.
---

# Enterprise Capability Intake

Convert an ambiguous request into an approved, testable capability brief. Do not design tools, prompts, or specialist roles until the outcome and accountability model are sufficiently clear.

## Intake procedure

1. Identify the requesting business unit, target user, accountable outcome owner, process owner, control owner, data/knowledge steward, and operational owner.
2. State the business outcome, current process, service level, pain point, expected value, guardrail, and measurable success criteria.
3. Define the case or work-item lifecycle, including initiation, system of record, state owners, human decisions, exceptions, handoffs, and terminal states.
4. Enumerate permitted inputs, data classifications, authoritative knowledge sources, systems, integrations, geographic/regulatory constraints, and retention rules.
5. Decompose the outcome into atomic tasks. For each task choose a reusable skill, new skill candidate, tool, knowledge pack, human role, or no-automation decision.
6. Define the highest permitted action tier and set P0 by default. If a higher proactivity level is requested, route to the proactivity skill.
7. Capture representative positive, negative, edge, and adversarial examples. State what excellent, unacceptable, and escalated outcomes look like.
8. Reject the intake as incomplete if it lacks an accountable owner, a measurable outcome, human decision boundaries, a source-of-truth plan, or a meaningful evaluation case.

## Capability brief

```yaml
capability_brief:
  id: CAP-<DOMAIN>-<NAME>
  outcome: ""
  primary_user: ""
  accountable_owner: ""
  process_owner: ""
  control_owner: ""
  operations_owner: ""
  current_process: ""
  measurable_value: []
  guardrails: []
  case_system_of_record: ""
  case_lifecycle: []
  inputs: []
  authoritative_sources: []
  tool_candidates: []
  highest_action_tier: A0
  requested_proactivity: P0
  human_decisions: []
  exclusions: []
  evaluation_examples: []
  open_questions: []
  status: proposed | validated | rejected
```

## Output

Return a status-labelled capability brief. Separate facts, assumptions, unknowns, and decisions required. Do not invent missing process knowledge; name the human owner needed to validate it.
