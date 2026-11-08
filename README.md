# Accredible Certificates MCP server

Inspect an issued credential and create an unapproved credential for an existing credential group.

A direct-provider MCP server with useful local execution. No PipMCP account is required for local use. Provider API access and any provider charges are your responsibility.

## Quick start

Requires Node.js22+. Clone this repository, then run:

```sh
npm ci --ignore-scripts
npm test
npm start
```

The default command inspects the tools offline. Configure your own credentials in your environment:

- `ACCREDIBLE_API_KEY`



Credential help: https://docs.api.accredible.com/

## Execute a real read

Replace example record IDs with records you are authorized to access.

```sh
npm start -- --call accredible_get_credential '{"id":"REPLACE_WITH_AUTHORIZED_ID"}'
```

## Use with an MCP client

Launch `node /absolute/path/accredible-mcp/server.mjs` using stdio transport; pass credentials through the client environment. Stdout is reserved for JSON-RPC.

## Tools

| Tool | Effect | Purpose |
| --- | --- | --- |
| accredible_get_credential | Read | accredible get credential |
| accredible_create_credential | Explicit approval required | Create an unapproved credential in an existing group. Supply name/description when not configured on the group. |

## Concrete workflow

Inspect an issued credential and create an unapproved credential for an existing credential group.

1. accredible_get_credential
2. accredible_create_credential

## Optional writes

Writes are disabled by default. Set CONNECTOR_ALLOW_WRITES=true and supply `_approval: {approved:true,idempotencyKey:"unique-request-id"}` on the specific call. Do not reuse a key for a different request. Uncertain outcomes are never automatically replayed; inspect the provider before another attempt.

## Capability evidence

Local: **Tested — HTTP fixtures and real stdio tools/call**. Managed: **Documented**. Provider authentication and live operations have not been established by these fixture tests. Evidence applies per operation and execution mode; setup discovery does not imply provider execution.

## Managed production

[Activate with PipMCP](https://pipmcp.com/github/start?app=accredible&integration=accredible-mcp&utm_source=github&utm_campaign=github-accredible-mcp&utm_content=readme) when you want the hosted service.  Local credentials are not uploaded by this code. Review provider permissions in the managed onboarding. [Directory and related projects](https://jannikco.github.io/pipmcp-connectors/integrations/accredible/).

## Provenance and maintenance

- https://docs.api.accredible.com/openapi.json

Maintainer:jannikco. MIT license for this code. See connector.json for selected operations and integration.json for evidence. Runtime dependencies retain their own licenses. Report sensitive issues through https://pipmcp.com/contact; do not post credentials or customer data in public issues.
