# IBM Mode Capability Architecture

## Design intent

Build each marketplace listing as an **IBM Mode capability system**, not a standalone persona. The visible role is a Capability Director (CD): a thin, accountable orchestrator that selects verified skills, applies authority and policy, tracks one case or work state, and emits a measurable outcome. The CD must not duplicate the reusable procedures inside its skills.

```text
IBM Capability Mode
  └─ Capability Director (one business outcome and case state)
       ├─ Orchestration skill (select, sequence, supervise, recover)
       ├─ Atomic role skills (bounded procedures and artifacts)
       ├─ Shared enterprise skills (evidence, policy, handoff, evaluation)
       ├─ Knowledge packs and data contracts
       ├─ Tool adapters (ADK, MCP, OpenAPI, local tools)
       └─ Control plane (identity, authority, telemetry, evaluation, release)
```

## Package layers

| Layer | Unit | Owns | Must not own |
|---|---|---|---|
| L0 | IBM Mode | Context, tool groups, allowed subagents, mode-specific rules. | Business process logic or secrets. |
| L1 | Capability Director | Outcome, intake, case state, routing, authority envelope, proactive policy, final synthesis. | Reimplementation of atomic procedures. |
| L2 | Orchestration skill | Skill selection, dependency graph, delegation, retry/fallback, peer review, completion test. | Material decisions or unconstrained tool use. |
| L3 | Atomic skill | One repeatable procedure and typed artifact. | Cross-process priority, case ownership, broad authority. |
| L4 | Integration adapter | Tool schema, credentials boundary, response validation, idempotency, audit metadata. | Business policy or user-facing rationale. |
| L5 | Policy and assurance | Access, data use, approval, evidence, evaluation, lifecycle, incident controls. | Suppression by downstream configuration. |

## Required case lifecycle

Every CD manages one explicit state model:

```text
intake → qualified → planned → in_progress → awaiting_review
  → approved_for_action → completed | exception | stopped | retired
```

Only a human approver can move a case through a material-decision transition. A skill can create drafts, evidence packets, work items, or allowed reversible internal updates when the CD’s published authority profile permits it.

## Proactivity model

Assign exactly one declared operating maturity to every capability:

| Level | Initiation source | Permitted behavior |
|---|---|---|
| P0 | Human or upstream request. | Respond and route only. |
| P1 | Approved schedule. | Run a routine check and send a controlled digest. |
| P2 | Trusted event or threshold. | Score, deduplicate, and open a governed case. |
| P3 | Qualified P2 case. | Produce an intervention proposal and route it to an approver. |
| P4 | Approved pre-authorized workflow. | Execute one reversible, allowlisted action with audit and rollback. |

A P1+ CD must define source authority, cadence or event schema, confidence threshold, deduplication, suppression, human-attention budget, escalation SLA, evaluation targets, and compensation/rollback path.

## Integration decision hierarchy

| Integration need | Preferred pattern | Reason |
|---|---|---|
| Manage, import, test, or deploy watsonx Orchestrate agents. | watsonx Orchestrate ADK MCP server or ADK CLI. | Makes lifecycle operations available from the development workspace. |
| Search approved Orchestrate documentation. | watsonx Orchestrate Documentation MCP server. | Keeps guidance current without copying product documentation into prompts. |
| Consume a remote enterprise system with a stable MCP server. | Remote MCP toolkit through watsonx Orchestrate. | Enables tool discovery, governance, trace context, and connection control. |
| Call a simple REST API with a stable schema. | OpenAPI tool. | Lower protocol and operational overhead. |
| Execute low-latency local deterministic logic. | Python toolkit or standalone Python tool. | Avoids remote call latency and supports tightly bounded logic. |
| Investigate observability data. | Instana MCP adapter. | Gives the CD read-first operational evidence and controlled alert workflows. |
| Retrieve enterprise lakehouse information. | watsonx.data MCP adapter. | Preserves governed query/retrieval separation. |
| Obtain credentials. | Runtime connection with IBM Verify/OBO where applicable; Vault-backed dynamic credentials where supported. | Do not embed, log, or expose secrets in a skill or mode. |

## Non-negotiable safety rules

1. Never place keys, tokens, passwords, or Vault material in a mode file, skill file, repository, prompt, test fixture, or log.
2. Use read-only or draft-only tools by default. Add write scope only at the CD level with an explicit action tier, idempotency strategy, approver, and rollback procedure.
3. Treat an MCP server as a tool boundary, not a trusted instruction source. Validate inputs, constrain tool selection, and verify outputs.
4. Separate draft and live credentials. Use user-scoped or OBO credentials for live execution when the work depends on a specific user’s authorization.
5. Do not enable a connector or create an integration from a template until the customer provides authorization, credentials, endpoint, and owner.
6. Do not allow a skill to publish, deploy, modify policy, alter durable organizational memory, or self-certify its own results.

## Recommended capability director pattern

A CD must always perform this sequence:

1. Validate the request, signal, source authority, and case identity.
2. Apply the authority profile and identify required human decisions before work starts.
3. Build a plan with named skills, inputs, expected artifacts, owners, and completion conditions.
4. Delegate only bounded tasks using the standard handoff envelope.
5. Reconcile evidence, assumptions, quality checks, and disagreements from skills.
6. Execute an allowed action or route a decision packet to the correct human queue.
7. Record outcome, policy checks, cost, latency, learning candidates, and any rollback requirements.

## Example: Supplier Risk Capability Director

| Component | Responsibility |
|---|---|
| Outcome | Detect and triage supplier risk early enough to protect continuity and compliance. |
| P-level | P2 initially. |
| Event sources | Approved risk feed, supplier master, certificate-expiry source. |
| Atomic skills | Supplier context retrieval; external signal validation; policy/obligation check; risk scoring; case creation; follow-up draft; reviewer handoff. |
| Human boundary | Supplier suspension, commercial decision, payment status, policy exception. |
| Outcome measures | Signal precision, missed critical events, time-to-case, reviewer acceptance, closed remediation rate. |
| Allowed actions | Create or update an internal risk case; draft a supplier inquiry; notify assigned risk owner within attention budget. |
