# IBM Mode Skill Catalog

Each skill is independently versioned, testable, and reusable. A Capability Director selects skills through a declared orchestration graph; it must not copy their procedures into a role prompt.

| Skill | Type | Required when | Primary artifact | Cannot do |
|---|---|---|---|---|
| `enterprise-capability-intake` | Shared foundation | Any new capability or major change. | Validated capability brief. | Invent a use case or approve the business outcome. |
| `role-capability-director` | Orchestration | A role must own an outcome and case lifecycle. | CD contract and state model. | Perform specialist work without calling an approved skill. |
| `ibm-capability-orchestrator` | Orchestration | Two or more skills must collaborate. | Executable skill graph and work plan. | Make material decisions, self-delegate recursively, or change authority. |
| `proactivity-signal-case-action` | Operating behavior | P1–P4 behavior is requested. | Proactivity profile and signal-to-case policy. | Send unbounded alerts or execute material actions. |
| `evidence-provenance-and-knowledge` | Assurance | The capability uses data, documents, policy, memory, or retrieval. | Source authority and evidence packet. | Convert an assumption or unvalidated result into durable memory. |
| `decision-rights-and-human-handoff` | Assurance | The capability recommends, routes, or changes a system state. | Decision-rights matrix and handoff envelope. | Grant authority beyond the published action tier. |
| `tool-and-integration-broker` | Integration | The capability needs ADK, MCP, API, Python, Instana, watsonx.data, or Vault pattern. | Tool adapter contract and connection plan. | Store secrets, create connectors without approval, or treat tools as policy sources. |
| `evaluation-and-release-governance` | Assurance | A package is piloted, promoted, updated, or retired. | Evidence pack and release decision. | Self-certify a package or waive failures. |
| `agent-operations-and-learning` | Operations | A capability will run after launch. | Operations profile, SLOs, incident and learning plan. | Apply learning directly to live behavior without review. |
| `industry-blueprint-composer` | Verticalization | A horizontal capability enters a regulated or specialist industry. | Vertical overlay manifest and validation plan. | Relabel a generic agent as a vertical solution without domain assets. |

## Skill graph conventions

Use the following graph notation in a CD contract:

```yaml
orchestration_graph:
  nodes:
    - skill: enterprise-capability-intake
      output: capability_brief
    - skill: evidence-provenance-and-knowledge
      depends_on: [enterprise-capability-intake]
      output: authorized_evidence_set
    - skill: <domain_atomic_skill>
      depends_on: [evidence-provenance-and-knowledge]
      output: domain_artifact
    - skill: decision-rights-and-human-handoff
      depends_on: [<domain_atomic_skill>]
      output: approval_or_handoff_packet
  completion_condition: "named reviewer accepts the packet or a declared stop condition is reached"
```

Every graph node must state: input schema, output schema, owner, expected latency, quality check, tool scope, evidence preserved, fallback, retry limit, and stop condition.

## Atomic role-skill contract

Use this structure for all domain-specific skills created under a capability.

```yaml
skill_id: SK-<DOMAIN>-<NAME>
version: 0.1.0
mission: "Perform one bounded procedure to produce one defined artifact."
when_to_use: "Specific triggering condition."
inputs:
  - name: case_context
    schema: case_context.v1
    required: true
outputs:
  - name: artifact
    schema: <artifact>.v1
    evidence_required: true
procedure:
  - validate scope, identity, classification, and authority
  - retrieve only declared knowledge and tool data
  - execute the domain procedure
  - run the skill quality check
  - return artifact, evidence, assumptions, confidence, and exception state
permitted_tools: []
prohibited_actions: []
quality_checks: []
failure_behavior:
  retry_limit: 1
  fail_closed_when: []
  route_to: "Capability Director"
handoff:
  required_fields: [case_id, scope, evidence_refs, assumptions, confidence, policy_checks, exceptions, next_action]
evaluation_cases: []
```

## Required shared skills by capability maturity

| Capability element | Mandatory skills |
|---|---|
| P0, read/draft-only | Intake, evidence, decision/handoff, evaluation, operations. |
| P1 schedule | P0 set plus proactivity. |
| P2 signal-to-case | P1 set plus integration broker and dedicated signal evaluation. |
| P3 intervention proposal | P2 set plus explicit human attention and approval workflow. |
| P4 delegated reversible action | P3 set plus idempotency, rate limiting, compensation, post-action verification, and independent control review. |
| Regulated/vertical deployment | Relevant maturity set plus industry blueprint composer. |

## Reuse rule

Reuse a skill when its procedure, inputs, outputs, data class, tool scope, authority, and evaluation requirements meet the new need. Fork only if reusing it would weaken quality, clarity, access segregation, policy compliance, or maintainability. Document every fork in the package manifest, with the rejected reuse candidate and reason.
