---
name: tool-and-integration-broker
description: Select, specify, and govern IBM watsonx Orchestrate ADK, MCP, OpenAPI, Python, Instana, watsonx.data, IBM Verify, and Vault-backed integrations. Use before adding any external tool or runtime connection to an IBM Mode capability.
---

# Tool and Integration Broker

Choose the smallest safe integration that can perform the declared capability task. This skill creates a tool adapter contract and connection plan; it does not activate a connector, acquire credentials, or place secrets in source files.

## Procedure

1. Read the CD contract. Identify the exact business operation, system owner, read/write need, data classification, action tier, expected volume/latency, source of truth, and fallback.
2. Consult the integration registry. Select remote/local MCP for existing MCP ecosystems, OpenAPI for stable REST APIs, Python for bounded deterministic local logic, ADK lifecycle tooling for Orchestrate administration, Instana for observability evidence, watsonx.data for governed retrieval, and a credential broker for short-lived secrets.
3. Specify the narrow tool allowlist: operation, input/output schemas, fields allowed, user/tenant context, timeout, rate limit, idempotency key, error categories, evidence returned, and maximum action tier.
4. Define draft/test/live connection posture. Name the service, technical, data, and credential-policy owners. For user-specific work, prefer user/OBO authorization in live execution.
5. For remote MCP, record server URL, transport, selected tools, authentication model, tool discovery behavior, and runtime trace/correlation requirements. Do not import all tools by default.
6. For Vault, specify only the runtime credential-broker contract. Never request or expose the secret value to the agent or include it in a template, prompt, code sample, or log.
7. Produce a test plan that verifies schema validation, valid tool call, denied scope, unavailable tool, timeout, malformed response, rate limit, and post-action verification.
8. Route connector creation, enabling, or credentials setup to the customer-approved integration workflow. Mark the adapter `planned`, not `active`, until verification succeeds.

## Tool adapter contract

```yaml
tool_adapter:
  id: TA-<SYSTEM>-<OPERATION>
  lifecycle: planned | draft | pilot | active | retired
  system: ""
  business_operation: ""
  implementation: adk_mcp | remote_mcp | local_mcp | openapi | python
  connection_ref: "customer-configured only"
  allowed_operations: []
  input_schema: ""
  output_schema: ""
  permitted_fields: []
  maximum_action_tier: A0
  identity_model: team | user_obo | service | credential_broker
  timeout_seconds: 0
  rate_limit: ""
  idempotency_key: ""
  validation: []
  error_handling: []
  evidence_fields: []
  post_action_verification: ""
  rollback_or_compensation: ""
  owners:
    service: ""
    data: ""
    credential_policy: ""
```

## Hard stops

Stop when endpoint, service owner, permitted operation, credential model, data classification, action tier, or test environment is unknown. Do not manufacture an endpoint, credential, MCP server, or API behavior. Do not enable a connector without explicit customer approval.
