# IBM Integration Registry

This registry is a design and packaging reference. It does not mean any endpoint, credential, connector, or service is active. Before implementation, obtain the target environment, named technical owner, approved use case, data classification, action scope, authentication model, and test path.

## Current package status

The current session has **no configured IBM-, watsonx Orchestrate ADK-, Instana-, or Vault-specific connector**. Build capability contracts and templates now; activate an integration only after a customer-authorized connection has been configured and verified.

## Integration catalog

| Integration | Use in IBM Mode | Preferred implementation | Minimum connection model | Default authority | Runtime guardrails |
|---|---|---|---|---|---|
| watsonx Orchestrate ADK | Create, import, inspect, test, and deploy agent packages. | Local ADK MCP server for IDE-assisted lifecycle work; ADK CLI in CI/CD. | Target environment URL and approved API credential. | Read/draft in development; promotion requires release approval. | Separate draft/live environments, package manifest, CI evaluation, no API key in source. |
| watsonx Orchestrate Documentation | Retrieve current product instructions and schema guidance. | Remote documentation MCP endpoint. | Public remote endpoint. | Read-only. | Cite the page/section, do not treat docs as authorization to change production. |
| Remote enterprise MCP toolkit | Connect an external service hosted outside Orchestrate. | ADK remote MCP toolkit using `streamable_http` or `sse`. | Customer-approved URL, protocol, tool allowlist, and connection. | Read-only/draft first. | Import specific tools, not `*`, when feasible; validate tool responses; trace tenant and agent context; use live user/OBO credentials when appropriate. |
| Local MCP toolkit | Run a tightly bounded tool next to Orchestrate. | ADK local MCP import. | Container/runtime ownership and local connection policy. | Read-only/draft first. | Image provenance, least privilege, resource limits, version pinning, process isolation. |
| Python toolkit | Execute deterministic low-latency enterprise logic. | ADK Python toolkit. | Package provenance and runtime dependencies. | Read-only/draft first. | Unit/integration tests, dependency scan, typed outputs, no credential embedding. |
| OpenAPI tool | Call a stable REST service with clear schemas. | ADK OpenAPI tool definition. | Approved server URL and typed connection. | Read-only/draft first. | Schema validation, field allowlist, pagination/rate limits, idempotency for write operations. |
| IBM Instana MCP | Retrieve observability evidence and support incident investigation. | Instana MCP server imported as a local or remote toolkit. | Instana base URL and scoped API token via approved connection. | Read-only by default; alert configuration changes require explicit approval. | Restrict to allowed metrics/apps/traces; open a case rather than taking production action; log query parameters and evidence references. |
| watsonx.data MCP | Retrieve/query governed lakehouse or document data. | watsonx.data MCP server, local or remote as supported by target deployment. | Customer data connection, role/row policy, and approved query scope. | Read-only by default. | Query allowlist, data minimization, cost/scan limit, output classification, no unrestricted SQL mutation. |
| IBM Verify / OBO | Execute a tool in the context of the authenticated user. | watsonx Orchestrate member/OBO connection. | Identity provider configuration and user consent/session. | User-scoped. | Do not substitute team credentials for a user-specific decision; show effective principal and scope in the case evidence. |
| HashiCorp Vault dynamic credentials | Supply short-lived credentials to a tool/runtime. | Approved Vault integration or credential broker; do not implement a secret-reading skill. | Vault policy, role, lease TTL, audit owner, rotation path. | None directly; broker supplies runtime credentials. | Never expose secret values to the model; log lease metadata only; renew/revoke via controlled runtime; fail closed when broker unavailable. |

## Tool-choice decision table

| Question | Yes | No |
|---|---|---|
| Is there an approved MCP server with the needed narrow tool set? | Use MCP after schema review and connection approval. | Continue. |
| Is the service a simple stable REST API with a strong OpenAPI definition? | Use OpenAPI tool. | Continue. |
| Is the function local, deterministic, performance-sensitive, and safe to package? | Use Python toolkit or local MCP. | Continue. |
| Does the work need external infrastructure, centralized tool updates, or an existing remote service? | Use remote MCP. | Obtain/implement a governed adapter before enabling the capability. |

## Remote MCP import policy

Before importing a remote MCP toolkit, obtain:

1. Exact server URL and selected transport (`streamable_http` or `sse`).
2. Named service owner, business owner, and data owner.
3. Selected tools and tool schemas; do not automatically expose an entire tool catalog.
4. Authentication type and draft/live connection plan.
5. Test data or sandbox environment.
6. Tool timeout, rate limit, data-classification, logging, and incident requirements.
7. A fallback behavior if the service or authorization is unavailable.

The ADK validates an imported MCP server’s schema during import; it does not prove that every tool executes safely. Run explicit tool-execution tests after import and before release.

## Draft/live connection policy

| Environment | Purpose | Credential posture |
|---|---|---|
| Draft | Schema import, mock/test execution, initial development. | Non-production least-privilege key-value or test credentials where approved. |
| Test/Pilot | Controlled business validation. | Pilot tenant or sandbox service account; sanitized data unless explicitly approved. |
| Live | Production execution. | User/OBO credentials for user-authorized work, or tightly scoped team credentials for automated service work. |

Do not copy a draft secret into live. Do not use a successful `tools/list` or schema import as evidence that live execution is authorized.

## Vault broker contract

```yaml
credential_broker:
  purpose: "Provide short-lived runtime credentials without exposing secret values to model context."
  provider: "HashiCorp Vault or customer-approved equivalent"
  agent_visibility: "lease metadata only; never secret material"
  requested_scope: "named tool operation and target environment"
  policy_owner: "identity or secrets-management owner"
  lease_ttl: "customer-configured"
  renewal: "runtime-controlled and audited"
  revocation: "on task completion, incident, or policy change"
  failure_mode: "fail closed; create an exception record"
  evidence: [credential_policy_id, lease_id_hash, issuance_time, expiry_time, requesting_agent_id]
```

## References

[1]: https://developer.watson-orchestrate.ibm.com/ "IBM watsonx Orchestrate Agent Development Kit"

[2]: https://developer.watson-orchestrate.ibm.com/tools/toolkits/remote_mcp_toolkits "IBM watsonx Orchestrate ADK — Importing remote MCP toolkits"

[3]: https://developer.ibm.com/tutorials/securing-ai-agents/ "IBM Developer — Secure AI agents with watsonx Orchestrate, IBM Verify, and HashiCorp Vault"

[4]: https://aws.amazon.com/blogs/ibm-redhat/integrating-kiro-with-ibm-mcp-servers-watsonx-orchestrate-instana-and-beyond/ "AWS — Integrating Kiro with IBM MCP servers: watsonx Orchestrate, Instana, and beyond"
