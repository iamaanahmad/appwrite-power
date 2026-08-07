# Appwrite MCP Quick Start for Kiro

## Appwrite Cloud

### 1. Have an Appwrite Cloud project

Create or choose a project in the [Appwrite Cloud console](https://cloud.appwrite.io).

### 2. Connect the hosted MCP server

This power configures:

```json
{
  "mcpServers": {
    "appwrite": {
      "url": "https://mcp.appwrite.io/"
    }
  }
}
```

On the first connection, your browser opens for Appwrite OAuth authorization. Sign in and grant access. No local installation, API key, project ID, or endpoint environment variable is needed.

### 3. Ask Kiro to work with Appwrite

```text
List users in my Appwrite project
Create a database named main
Get the details of my portfolio site from Appwrite
Show me how to set up real-time subscriptions that trigger when a user is created
```

The hosted server provides Appwrite project access and semantic documentation search. It discovers detailed Appwrite operations at runtime to keep the initial MCP tool surface compact.

## If you run Appwrite yourself

The hosted endpoint is for Appwrite Cloud. Self-hosted instances require Appwrite's local stdio server, an API key, your project ID, and the instance endpoint:

```json
{
  "mcpServers": {
    "appwrite": {
      "command": "uvx",
      "args": ["mcp-server-appwrite", "--users"],
      "env": {
        "APPWRITE_PROJECT_ID": "your-project-id",
        "APPWRITE_API_KEY": "your-api-key",
        "APPWRITE_ENDPOINT": "https://your-appwrite-domain/v1"
      }
    }
  }
}
```

The local server enables database tools by default. Add only the service flags you need, such as `--users`, `--storage`, or `--functions`.

## Troubleshooting

- **Authorization does not finish:** reconnect the MCP server and complete the browser sign-in and consent flow.
- **Wrong project is selected:** ask Kiro to retrieve Appwrite workspace context, then specify the project or organization.
- **An operation fails:** confirm the authenticated account has access and use the server-provided parameter schema. On self-hosted instances, verify API-key scopes and service flags.

## Learn more

- [Appwrite MCP overview](https://appwrite.io/docs/tooling/ai/mcp-servers/)
- [Hosted server details](https://appwrite.io/docs/tooling/ai/mcp-servers/api)
- [Self-hosted server setup](https://appwrite.io/docs/advanced/self-hosting/mcp)
