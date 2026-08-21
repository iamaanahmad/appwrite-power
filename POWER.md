---
name: "appwrite"
displayName: "Appwrite Backend Platform"
description: "Build and manage Appwrite Cloud backends with authentication, databases, storage, functions, messaging, sites, and current Appwrite documentation."
keywords: ["appwrite", "backend", "database", "auth", "authentication", "storage", "functions", "serverless", "baas", "api", "users", "sites", "messaging"]
author: "Appwrite"
---

# Appwrite Backend Platform

Appwrite provides a hosted MCP server for Appwrite Cloud. It combines project operations and documentation search in one remote HTTP server, so there is no local package, API key, or documentation server to install for Cloud projects.

## Onboarding

### 1. Prerequisite

Create or select an Appwrite Cloud project at [cloud.appwrite.io](https://cloud.appwrite.io). No local software or environment variables are required for the hosted server.

### 2. Configure the MCP server

This power's `mcp.json` configures the official hosted endpoint:

```json
{
  "mcpServers": {
    "appwrite": {
      "url": "https://mcp.appwrite.io/"
    }
  }
}
```

When your MCP client connects for the first time, it opens a browser. Sign in to Appwrite Cloud and approve the requested access. Authentication uses OAuth; do not create, copy, or place an API key in the configuration for this hosted connection.

### 3. Use Appwrite in natural language

After authorization, ask for the operation or documentation you need. For example:

- “List users in my Appwrite project.”
- “Create a database named `main`.”
- “Get the details of my portfolio site from Appwrite.”
- “Show me how to subscribe to user-creation events in real time.”

## Available MCP Servers

### appwrite

The single `appwrite` server at `https://mcp.appwrite.io/` uses HTTP transport and browser-based OAuth. It combines Appwrite Cloud project operations, workspace context, and current documentation search. Kiro loads this server from `mcp.json`; no local package, headers, environment variables, or API key are required.

The server gives Kiro access to:

- Appwrite Cloud project operations, including users, databases, storage, functions, messaging, sites, teams, and other supported services.
- Current Appwrite documentation and SDK/API guidance through semantic search.
- Workspace context covering the authenticated account, organization, and available projects.

The server initially exposes a compact set of tools and discovers its full operation catalog at runtime. Its core tools are:

- `appwrite_get_context` — summarize the connected account, organization, and projects.
- `appwrite_search_tools` — find an Appwrite operation and its parameter schema.
- `appwrite_call_tool` — execute the selected operation.
- `appwrite_search_docs` — search Appwrite documentation semantically.

Use a context or search tool before calling a detailed project operation when your client exposes these tools directly. Follow the returned schema exactly, and request the minimum necessary resource access.

## Available Steering Files

- `steering/steering.md` — Load on demand for detailed Appwrite guidance covering database schemas and indexes, permissions, user management, storage, functions, real-time subscriptions, error handling, performance, testing, monitoring, and production-readiness practices.

## Safety and implementation guidance

- Confirm project, organization, and resource identifiers before making changes.
- Use least-privilege Appwrite permissions; do not use public read/write access for sensitive data.
- Validate user input and handle Appwrite errors in application code.
- Create indexes for common query patterns and paginate large result sets.
- Keep application secrets in server-side environment variables. OAuth removes the need to configure an MCP API key, but it does not change normal application-secret handling.
- Test data, permission changes, deployments, and destructive operations in a non-production project first.

## Self-hosted Appwrite

The hosted endpoint authenticates against Appwrite Cloud. For a self-hosted Appwrite instance, use the local stdio server documented by Appwrite instead. That setup requires `uv`, `mcp-server-appwrite`, an API key, a project ID, and your instance endpoint. Database tools are enabled by default; enable only the additional service flags your workflow needs to limit tool-context use.

```json
{
  "mcpServers": {
    "appwrite": {
      "command": "uvx",
      "args": ["mcp-server-appwrite", "--users", "--storage"],
      "env": {
        "APPWRITE_PROJECT_ID": "your-project-id",
        "APPWRITE_API_KEY": "your-api-key",
        "APPWRITE_ENDPOINT": "https://your-appwrite-domain/v1"
      }
    }
  }
}
```

Do not use this local API-key configuration for Appwrite Cloud when the hosted server is available.

## Troubleshooting

### The browser authorization does not complete

Reconnect the `appwrite` server, finish the sign-in and consent flow in the browser, and verify that the signed-in account can access the intended Appwrite Cloud project.

### The server cannot find the intended project

Ask for the Appwrite workspace context, then specify the project or organization in your request. Confirm that the OAuth-authorized account has access to it.

### An operation is unavailable or fails

Search for the operation first, use the returned required parameters, and verify that your Appwrite role has permission. For self-hosted connections, ensure the needed service flag and API-key scope are configured.

## Resources

- [Appwrite MCP overview](https://appwrite.io/docs/tooling/ai/mcp-servers/)
- [Hosted Appwrite MCP server](https://appwrite.io/docs/tooling/ai/mcp-servers/api)
- [Self-hosted MCP server](https://appwrite.io/docs/advanced/self-hosting/mcp)
- [Appwrite documentation](https://appwrite.io/docs)
- [Appwrite Cloud console](https://cloud.appwrite.io)
