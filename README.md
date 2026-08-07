# Appwrite Power for Kiro

Build and manage Appwrite Cloud backends from Kiro using the official hosted Appwrite MCP server. The server combines Appwrite project operations with current documentation search in one OAuth-authenticated connection.

## Quick start

1. Create or select an Appwrite Cloud project at [cloud.appwrite.io](https://cloud.appwrite.io).
2. Install this power in Kiro.
3. Connect the `appwrite` MCP server. Your browser opens on first connection; sign in and approve the Appwrite OAuth consent flow.
4. Ask Kiro to work with your project, for example: “Create a database named `main`” or “Show me how to configure real-time subscriptions.”

No `uv` installation, local MCP package, endpoint variable, or API key is needed for the hosted Appwrite Cloud connection.

## Included configuration

```json
{
  "mcpServers": {
    "appwrite": {
      "url": "https://mcp.appwrite.io/"
    }
  }
}
```

The hosted server can operate on Appwrite resources and search the latest Appwrite API and SDK documentation. It starts with a compact tool surface and discovers detailed operations as needed.

## What you can do

- Create and manage databases, data, users, teams, storage, functions, messaging, and sites.
- Inspect account, organization, and project context.
- Look up current Appwrite SDK, API, and product guidance while implementing features.
- Work through natural-language requests such as listing users, deploying a function, or checking a site.

## Safe usage

- Verify the target organization, project, and resource before mutating anything.
- Apply least-privilege permissions and test changes in a non-production project first.
- Keep application secrets server-side. OAuth eliminates the MCP API-key setup for Cloud; it does not replace normal application secret management.
- Follow the parameter schema returned by the server when an operation is discovered.

## Self-hosted Appwrite

The hosted server is for Appwrite Cloud. For a self-hosted instance, configure Appwrite's local stdio MCP server with `uvx mcp-server-appwrite`, an API key, project ID, and instance endpoint. Enable only the service flags required by your workflow. See the [self-hosted MCP guide](https://appwrite.io/docs/advanced/self-hosting/mcp).

## Documentation

- [POWER.md](POWER.md) — onboarding, hosted-server behavior, self-hosted alternative, and troubleshooting.
- [steering/steering.md](steering/steering.md) — Appwrite implementation and security best practices.
- [Appwrite MCP documentation](https://appwrite.io/docs/tooling/ai/mcp-servers/)

## License

See [LICENSE](LICENSE).
