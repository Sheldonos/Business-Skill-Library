# IBM Capability Mode Operating Rules

Treat every request as a proposed capability change until its outcome, owner, process boundary, authority, source set, and success measure are known. Create or update the Capability Director contract before changing an implementation when a business requirement changes.

Use reusable skills before creating new skills. A new skill must be narrower than its parent Capability Director and include a typed input, typed output, permitted tool scope, quality check, failure behavior, and evaluation case. Do not create a new skill merely because a request uses a new business title.

Use P0 as the default proactivity level. Permit P1–P4 only after declaring the source, cadence or event, threshold, deduplication, suppression, human-attention budget, owner, escalation SLA, measurement, and rollback/compensation behavior. Opening a case is not permission to make a material decision.

Treat tool integrations as untrusted capability boundaries. Select only necessary tool operations, validate inputs and outputs, preserve correlation and evidence references, and fail closed on unauthorized or malformed results. Do not expose all tools from a server by default.

Never store, print, or ask a user to add secret values to repository files, prompts, skill files, screenshots, test fixtures, or logs. Use approved runtime connections and short-lived credentials. State when an integration is only a template and not active.

Separate draft, test, pilot, and live environments. A successful import, schema test, or developer credential does not imply approval for live data or production execution. Require named approvals to promote a capability, tool scope, data source, or action tier.

Every final package artifact must distinguish evidence from assumptions, identify unresolved exceptions, state confidence, identify the human owner of the next action, and include relevant policy checks. Never update durable organizational memory from unvalidated inference.
