---
name: industry-blueprint-composer
description: Build an industry-specific IBM Mode blueprint from reusable horizontal Capability Directors and skills. Use when a capability needs sector ontology, regulation, integrations, expert review, and vertical evaluation.
---

# Industry Blueprint Composer

Create a vertical operating blueprint by overlaying concrete domain assets on reusable horizontal capabilities. Do not relabel a generic agent as industry-ready without domain process, data, controls, evaluation, and operating evidence.

## Procedure

1. Identify the target industry, jurisdiction, regulated decision boundaries, accountable industry sponsor, compliance owner, domain SME reviewers, and highest-risk workflows.
2. Reuse horizontal CDs and atomic skills where their outcome, authority, knowledge, and evaluation requirements remain valid. Record all adaptations and rejected reuse options.
3. Build the vertical process graph: events, states, decision points, systems of record, human roles, SLAs, exception taxonomy, and artifacts.
4. Define the ontology: entities, codes, relationships, reference data, calculation meanings, terminology, source authority, and privacy/retention rules.
5. Specify vertical connectors and tool scopes. Prefer sandbox/read-only first; define cross-border, residency, security, and vendor obligations.
6. Add policy overlays and non-negotiable human decision gates. Map obligations to test cases, evidence, retention, and incident procedures.
7. Build SME-reviewed evaluations containing representative, edge, negative, adverse, and regulated cases. Define quality, false-positive, false-negative, fairness/explainability, safety, and escalation thresholds.
8. Produce the operational blueprint: role graph, CD/skill graph, deployment prerequisites, SLOs, support model, training, change control, and managed-service boundaries.

## Blueprint manifest

```yaml
industry_blueprint:
  id: IB-<INDUSTRY>-<OUTCOME>
  jurisdiction: []
  sponsor: ""
  compliance_owner: ""
  horizontal_dependencies: []
  adapted_capability_directors: []
  domain_process_graph_ref: ""
  ontology_pack_ref: ""
  connector_profiles: []
  policy_overlays: []
  human_decision_gates: []
  domain_evaluation_pack_ref: ""
  sme_reviewer_model: []
  operations_profile_ref: ""
  deployment_boundary: ""
  evidence_retention: ""
```

## Release test

The blueprint is release-ready only when a domain SME can trace each material outcome to a process state, ontology/data source, permitted tool operation, policy control, human decision boundary, and evaluation case. A long list of vertical role names is not sufficient.
