---
name: evidence-provenance-and-knowledge
description: Establish source authority, retrieval controls, evidence envelopes, and governed organizational memory for IBM Mode capabilities. Use whenever a skill retrieves, cites, learns from, or writes enterprise knowledge.
---

# Evidence, Provenance, and Knowledge

Bind the Capability Director and its skills to authorized information. Treat generic model knowledge as background context, never as the customer’s source of truth for material operational claims.

## Procedure

1. Classify the requested artifact and each source by owner, authority, jurisdiction, confidentiality, retention, freshness, and permitted use.
2. Define source precedence. State how to handle conflicts, missing fields, stale content, duplicate records, and partial evidence.
3. Build a minimum evidence set for each decision or material claim. Capture stable source references, access time, source version/date, extraction context, and the specific supporting content.
4. Require skills to separate observed facts, derived calculations, assumptions, uncertainty, and recommendations. Do not let a downstream skill overwrite upstream evidence.
5. Apply retrieval access rules, redaction/minimization, tenant boundary, output classification, and citation requirements before returning a work product.
6. Create a controlled memory change proposal only when the information has a named source, validation status, owner, version, affected CDs/skills, and rollback path.
7. Route conflicts in authoritative sources or ambiguity in data ownership to the data/knowledge steward. Do not silently reconcile them.

## Evidence envelope

```yaml
evidence_envelope:
  case_id: ""
  facts:
    - statement: ""
      source_ref: ""
      source_owner: ""
      source_date: ""
      classification: ""
      freshness_status: current | stale | unknown
  calculations: []
  assumptions: []
  uncertainty: []
  data_quality_issues: []
  citations_required: true
  retention_profile: ""
  memory_change_proposal:
    status: none | proposed | validated | rejected
    affected_capabilities: []
```

## Hard stops

Stop or route when an authoritative source conflicts, data classification or access is unclear, retrieval produces data outside the allowed scope, material evidence is stale/missing, citation cannot be established, or a requested memory update lacks a named human/data-steward validation.
