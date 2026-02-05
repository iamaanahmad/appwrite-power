# Appwrite Power for Kiro IDE

A comprehensive Kiro power for building backend services with Appwrite - databases, authentication, storage, functions, and messaging for web and mobile applications.

[![License](https://img.shields.io/badge/license-BSD--3--Clause-blue.svg)](LICENSE)
[![Kiro IDE](https://img.shields.io/badge/Kiro-IDE-purple.svg)](https://kiro.dev)
[![Appwrite](https://img.shields.io/badge/Appwrite-Backend-f02e65.svg)](https://appwrite.io)

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
- [uv](https://docs.astral.sh/uv/getting-started/installation/) - Python package manager
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

### Dual MCP Servers

#### 1. Appwrite API Server
Direct interaction with Appwrite services through Python-based MCP server.

**Default**: Databases API only (minimal context usage)

**Enable Additional APIs** with command-line flags:
- `--users` - User management and authentication
- `--storage` - File upload, download, and management
- `--functions` - Serverless function deployment
- `--messaging` - Email, SMS, and push notifications
- `--sites` - Static site and SSR deployment
- `--teams` - Team and membership management
- `--all` - Enable all APIs

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

### Automatic Activation
The power activates when you mention these keywords:
- appwrite, backend, database
- auth, authentication, storage
- functions, serverless, baas
- api, users, teams, messaging

### Comprehensive Documentation
- Step-by-step onboarding
- Tool usage examples
- Complete workflows
- Best practices guide
- Troubleshooting tips

### Modular Design
Enable only the APIs you need to minimize context usage and improve performance.

## 📖 Usage Examples

### Create a Database

```javascript
// Create database
await mcp_appwrite_api_databases_create({
  "database_id": "main",
  "name": "Main Database",
  "enabled": true
})

// Create collection
await mcp_appwrite_api_databases_create_collection({
  "database_id": "main",
  "collection_id": "posts",
  "name": "Blog Posts",
  "permissions": ["read(\"any\")"]
})

// Add attributes
await mcp_appwrite_api_databases_create_string_attribute({
  "database_id": "main",
  "collection_id": "posts",
  "key": "title",
  "size": 255,
  "required": true
})
```

### Manage Users

```javascript
// Create user
await mcp_appwrite_api_users_create({
  "user_id": "unique()",
  "email": "user@example.com",
  "password": "SecurePass123!",
  "name": "John Doe"
})

// List users
await mcp_appwrite_api_users_list({
  "queries": ["limit(25)"],
  "search": "john"
})
```

### Upload Files

```javascript
// Create storage bucket
await mcp_appwrite_api_storage_create_bucket({
  "bucket_id": "avatars",
  "name": "User Avatars",
  "permissions": ["read(\"any\")"],
  "maximum_file_size": 5000000
})

// Upload file
await mcp_appwrite_api_storage_create_file({
  "bucket_id": "avatars",
  "file_id": "unique()",
  "file": "/path/to/avatar.jpg"
})
```

### Deploy Functions

```javascript
// Create function
await mcp_appwrite_api_functions_create({
  "function_id": "unique()",
  "name": "Process Payment",
  "runtime": "node-18.0",
  "execute": ["any"]
})

// Create deployment
await mcp_appwrite_api_functions_create_deployment({
  "function_id": func.id,
  "code": "/path/to/function.tar.gz",
  "activate": true
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

### Minimal Configuration (Databases Only)

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

### Full Configuration (All Services)

```json
{
  "mcpServers": {
    "appwrite-api": {
      "command": "uvx",
      "args": [
        "mcp-server-appwrite",
        "--users",
        "--storage",
        "--functions",
        "--messaging",
        "--sites"
      ],
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

- **Use document-level permissions** for fine-grained access control
- **Create indexes** for frequently queried attributes
- **Enable document security** on collections with sensitive data
- **Use transactions** for atomic multi-document operations
- **Store sensitive data** in environment variables
- **Test with sandbox** before production deployment

See [steering/steering.md](steering/steering.md) for comprehensive best practices.

## 🔗 Links

- [Appwrite Website](https://appwrite.io)
- [Appwrite Documentation](https://appwrite.io/docs)
- [Appwrite GitHub](https://github.com/appwrite/appwrite)
- [Appwrite Discord](https://appwrite.io/discord)
- [Kiro IDE](https://kiro.dev)
- [Kiro Powers](https://github.com/kirodotdev/powers)

## 📄 License

This project is licensed under the BSD-3-Clause License - see the [LICENSE](LICENSE) file for details.

## 🙏 Acknowledgments

- [Appwrite Team](https://appwrite.io) for the amazing backend platform
- [Kiro IDE Team](https://kiro.dev) for the powerful development environment
- MCP (Model Context Protocol) for enabling seamless integrations

## 💬 Support

- **Issues**: [GitHub Issues](https://github.com/iamaanahmad/appwrite-power/issues)
- **Discussions**: [GitHub Discussions](https://github.com/iamaanahmad/appwrite-power/discussions)
- **Appwrite Discord**: [Join Community](https://appwrite.io/discord)

---

**Made with ❤️ for the Kiro and Appwrite communities**
