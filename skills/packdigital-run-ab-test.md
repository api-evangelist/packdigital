---
name: Run and manage an A/B test via the Pack MCP server
description: Use the hosted Pack MCP server to list, update, and drive the lifecycle of a storefront A/B test.
api: https://pack-agent.packdigital.workers.dev/mcp
operations: [list_ab_tests, update_ab_test, start_ab_test, pause_ab_test, end_ab_test]
source: https://docs.packdigital.com/developer-resources/pack-mcp
---

# Run and manage an A/B test via the Pack MCP server

Connect an AI assistant to the hosted Pack MCP server (HTTP transport):
`https://pack-agent.packdigital.workers.dev/mcp`.

## Auth
Set these request headers:
- `Authorization: Bearer <PACK_ACCESS_TOKEN>`
- `x-pack-store-id: <PACK_STORE_ID>`
- `x-pack-content-environment-id: production` (optional; targets a content environment)

## Steps
1. **List tests** — call the A/B testing tool to list existing tests and their variants.
2. **Update** — update the test and its variants (targeting, allocation, content).
3. **Lifecycle** — start, pause, end, or delete the test as needed.
4. **Metrics** — retrieve the saved goal metrics for the test to evaluate results.

## Rules / limits
- Tool families are documented in `mcp/packdigital-mcp.yml`; exact tool names are exposed
  by the server at connect time — enumerate them rather than hard-coding.
- A/B **goal creation or deletion** and media-manager uploads are not yet available via MCP
  (admin-only). Create goals in the Pack admin, then manage the test through MCP.
- The MCP server is backed by the same GraphQL Content Management API, so the same
  draft/published and content-release semantics apply.
