# Appwrite Power for Kiro IDE

A comprehensive Kiro power for building backend services with Appwrite - databases, authentication, storage, functions, and messaging for web and mobile applications.

**Now with MCP Server 2.0!** Zero configuration, automatic service discovery, and minimal context usage.

[![License](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)
[![Kiro IDE](https://img.shields.io/badge/Kiro-IDE-purple.svg)](https://kiro.dev)
[![Appwrite](https://img.shields.io/badge/Appwrite-Backend-f02e65.svg)](https://appwrite.io)
[![MCP Server](https://img.shields.io/badge/MCP-2.0-green.svg)](https://github.com/appwrite/mcp-for-api)

## 🚀 Quick Start

### Installation

1. **Open Kiro IDE**
2. **Go to Powers Panel** → Add Power from GitHub
3. **Enter Repository URL**: `https://github.com/iamaanahmad/appwrite-power`
4. **Install the Power**

Or install from local path:
1. Clone this repository
2. Open Kiro IDE → Powers Panel → Add Power from Local Path
3. Select the cloned directory

### Prerequisites

**For API Server:**
- [uv](https://docs.astral.sh/uv/getting-started/installation/) - Python package manager (version 0.4.1+)
- Appwrite project with API key

**For Docs Server:**
- No prerequisites required (HTTP-based)

### Configuration

1. **Create an Appwrite Project** at [cloud.appwrite.io](https://cloud.appwrite.io)

2. **Get Your Credentials**:
   - Project ID (from Settings page)
   - API Key (from Settings → API Keys)
   - Endpoint URL (e.g., `https://nyc.cloud.appwrite.io/v1`)

3. **Set Environment Variables**:

   **Windows (PowerShell):**
   ```powershell
   $env:APPWRITE_PROJECT_ID="your-project-id"
   $env:APPWRITE_API_KEY="your-api-key"
   $env:APPWRITE_ENDPOINT="https://nyc.cloud.appwrite.io/v1"
   ```

   **macOS/Linux:**
   ```bash
   export APPWRITE_PROJECT_ID="your-project-id"
   export APPWRITE_API_KEY="your-api-key"
   export APPWRITE_ENDPOINT="https://nyc.cloud.appwrite.io/v1"
   ```

   Or add them to your MCP configuration file.

## 📚 What's Included

### MCP Server 2.0 Architecture

**Revolutionary Two-Tool Design:**
- Only 2 tools exposed to the model: `appwrite_search_tools` and `appwrite_call_tool`
- Full Appwrite catalog stays internal and is searched at runtime
- Minimal context usage - more room for your code
- Zero configuration - no service flags needed
- Automatic service discovery - all APIs available by default

### Dual MCP Servers

#### 1. Appwrite API Server (v0.4.1+)
Direct interaction with Appwrite services through Python-based MCP server.

**What's New in 2.0:**
- ✅ **No more service flags** - Remove `--users`, `--storage`, `--functions`, etc.
- ✅ **All services enabled** - Databases, users, storage, functions, messaging, sites, teams
- ✅ **Compact architecture** - Only 2 MCP tools instead of dozens
- ✅ **Smart search** - AI finds the right tool based on natural language
- ✅ **Validation on startup** - Credentials checked when server starts

**Migration from v1.x:**
```json
// OLD (v1.x) - Don't use this anymore
{
  "args": ["mcp-server-appwrite", "--users", "--storage", "--functions"]
}

// NEW (v2.0) - Use this instead
{
  "args": ["mcp-server-appwrite"]
}
```

#### 2. Appwrite Docs Server
Query Appwrite documentation for guidance, API references, and code examples.

### Service Coverage

- **Databases**: Collections, documents, queries, indexes, transactions
- **Authentication**: User management, sessions, OAuth, MFA
- **Storage**: Buckets, file operations, image transformations
- **Functions**: Serverless deployment, multiple runtimes
- **Messaging**: Email, SMS, push notifications
- **Sites**: Static sites, SSR applications
- **Teams**: Team management, memberships, roles

## 🎯 Features

### MCP Server 2.0 Benefits
- **Zero Configuration**: No service flags needed - everything works automatically
- **Minimal Context**: Two-tool architecture uses less context than v1.x
- **Natural Language**: Search for tools using conversational queries
- **All Services**: Databases, users, storage, functions, messaging, sites, teams - all available
- **Smart Discovery**: AI automatically finds the right tool for your task
- **Startup Validation**: Credentials validated when server starts, not on first call

### Automatic Activation
The power activates when you mention these keywords:
- appwrite, backend, database
- auth, authentication, storage
- functions, serverless, baas
- api, users, teams, messaging

### Comprehensive Documentation
- Step-by-step onboarding
- MCP 2.0 migration guide
- Natural language usage examples
- Complete workflows
- Best practices guide
- Troubleshooting tips

## 📖 Usage Examples

### Natural Language Queries (MCP 2.0)

```javascript
// Just ask in natural language - AI handles the rest!

"Create a database called 'production'"
// AI searches for and calls: databases_create

"Add a user with email john@example.com"
// AI searches for and calls: users_create

"Upload avatar.jpg to the avatars bucket"
// AI searches for and calls: storage_create_file

"List all users in my project"
// AI searches for and calls: users_list

"Deploy my function code"
// AI searches for and calls: functions_create_deployment
```

### Traditional API Calls (Still Supported)

```javascript
// Search for the right tool
appwrite_search_tools({
  "query": "create a new database"
})

// Call the tool
appwrite_call_tool({
  "tool_name": "databases_create",
  "arguments": {
    "database_id": "main",
    "name": "Main Database",
    "enabled": true
  }
})
```

## 📁 Repository Structure

```
appwrite-power/
├── POWER.md              # Main power documentation
├── mcp.json              # MCP server configuration
├── steering/
│   └── steering.md       # Best practices guide
├── README.md             # This file
└── LICENSE               # BSD-3-Clause license
```

## 🔧 Configuration

### Minimal Configuration (MCP Server 2.0)

```json
{
  "mcpServers": {
    "appwrite-api": {
      "command": "uvx",
      "args": ["mcp-server-appwrite"],
      "env": {
        "APPWRITE_PROJECT_ID": "${APPWRITE_PROJECT_ID}",
        "APPWRITE_API_KEY": "${APPWRITE_API_KEY}",
        "APPWRITE_ENDPOINT": "${APPWRITE_ENDPOINT}"
      }
    }
  }
}
```

### Full Configuration (API + Docs)

```json
{
  "mcpServers": {
    "appwrite-api": {
      "command": "uvx",
      "args": ["mcp-server-appwrite"],
      "env": {
        "APPWRITE_PROJECT_ID": "${APPWRITE_PROJECT_ID}",
        "APPWRITE_API_KEY": "${APPWRITE_API_KEY}",
        "APPWRITE_ENDPOINT": "${APPWRITE_ENDPOINT}"
      }
    },
    "appwrite-docs": {
      "url": "https://mcp-for-docs.appwrite.io",
      "type": "http"
    }
  }
}
```

**Important:** If upgrading from v1.x, **remove all service flags** (`--users`, `--storage`, `--functions`, etc.). They are no longer needed or supported.

## 📚 Documentation

- **POWER.md**: Complete power documentation with examples and workflows
- **steering/steering.md**: Best practices for production applications
- [Appwrite Documentation](https://appwrite.io/docs)
- [Kiro Powers Guide](https://kiro.dev/docs/powers)

## 🛠️ Troubleshooting

### "Invalid API key"
- Verify API key in Appwrite console
- Check environment variables are set
- Ensure API key has required scopes

### "Database not found"
- Verify database ID is correct
- Check database is enabled
- Create database if it doesn't exist

### "Permission denied"
- Check document/collection permissions
- Verify user is authenticated
- Update permissions to grant access

For more troubleshooting tips, see [POWER.md](POWER.md#troubleshooting).

## 🤝 Contributing

Contributions are welcome! Please feel free to submit issues or pull requests.

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## 📝 Best Practices

- **Use natural language** - MCP 2.0 understands conversational queries
- **All services available** - No need to configure specific services
- **Use document-level permissions** for fine-grained access control
- **Create indexes** for frequently queried attributes
- **Enable document security** on collections with sensitive data
- **Use transactions** for atomic multi-document operations
- **Store sensitive data** in environment variables
- **Test with sandbox** before production deployment
- **Upgrade from v1.x** - Remove all service flags from configuration

See [steering/steering.md](steering/steering.md) for comprehensive best practices.

## 🔗 Links

- [Appwrite Website](https://appwrite.io)
- [Appwrite Documentation](https://appwrite.io/docs)
- [MCP Server 2.0 Announcement](https://appwrite.io/blog/post/announcing-appwrite-mcp-server-2)
- [MCP Server GitHub](https://github.com/appwrite/mcp-for-api)
- [MCP Server on PyPI](https://pypi.org/project/mcp-server-appwrite/)
- [Appwrite GitHub](https://github.com/appwrite/appwrite)
- [Appwrite Discord](https://appwrite.io/discord)
- [Kiro IDE](https://kiro.dev)
- [Kiro Powers](https://github.com/kirodotdev/powers)

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🙏 Acknowledgments

- [Appwrite Team](https://appwrite.io) for the amazing backend platform and MCP Server 2.0
- [Kiro IDE Team](https://kiro.dev) for the powerful development environment
- MCP (Model Context Protocol) for enabling seamless integrations

## 💬 Support

- **Issues**: [GitHub Issues](https://github.com/iamaanahmad/appwrite-power/issues)
- **Discussions**: [GitHub Discussions](https://github.com/iamaanahmad/appwrite-power/discussions)
- **Appwrite Discord**: [Join Community](https://appwrite.io/discord)

---

**Made with ❤️ for the Kiro and Appwrite communities**
