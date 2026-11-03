# Installing the Tolstoy MCP server

Tolstoy is a hosted remote MCP server. There's nothing to install, build or run locally, and you don't need an API key.

1. Add this remote server to the MCP settings file (Cline: `cline_mcp_settings.json`):

```json
{
  "mcpServers": {
    "tolstoy": {
      "type": "streamableHttp",
      "url": "https://apilb.gotolstoy.com/mcp/v1/mcp"
    }
  }
}
```

2. Save the file. The client starts the OAuth 2.1 sign-in (PKCE, Dynamic Client Registration) in the browser on first connect. Ask the user to sign in to their Tolstoy workspace and approve access.
3. After sign-in, the tools are listed automatically. To check the connection, call `get_usage` or `search_products`.

If the user doesn't have a Tolstoy workspace yet, they can create one at https://platform.gotolstoy.com.
