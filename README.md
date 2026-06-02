# Tolstoy MCP

Connect any MCP client — Claude, ChatGPT, Cursor, Gemini, and more — to **Tolstoy**, the agentic platform for AI-native ecommerce brands. Generate marketing content and manage your media library directly from chat.

Tolstoy exposes **two remote MCP servers** over Streamable HTTP, secured with OAuth 2.1 + PKCE. There are no API keys to paste — your client runs the OAuth sign-in on first connect.

| Server | Endpoint | What it does |
| --- | --- | --- |
| **Tolstoy Studio** | `https://apilb.gotolstoy.com/mcp/v1/mcp` | Generate and iterate on marketing videos and images with Tolstoy Studio's AI creative director. |
| **Tolstoy Library** | `https://apilb.gotolstoy.com/mcp/v1/library/mcp` | Browse, search, rename, and favorite your Tolstoy media library — videos, images, social imports, and AI drafts. |

## Tools

**Studio**
- `generate_studio_content` — start a new Studio generation (image or video) from a prompt.
- `iterate_studio_content` — continue and refine an existing Studio generation in the same session.

**Library**
- `list_assets` — list your most recent library assets (videos, images, AI drafts).
- `search_assets` — search the library by query.
- `get_asset` — fetch details for a specific asset.
- `update_asset` — rename an asset or toggle its favorite status.

## Connect

1. In your MCP client, add a custom connector / remote MCP server.
2. Paste the Studio or Library endpoint above.
3. Sign in with your Tolstoy account when prompted (OAuth).

Per-client setup (Claude, ChatGPT, Cursor, Gemini CLI, Codex, Perplexity, Goose, Cherry Studio, and more) is available in the Tolstoy platform under **Settings → MCP**.

### Example client config

```json
{
  "mcpServers": {
    "tolstoy-studio": { "url": "https://apilb.gotolstoy.com/mcp/v1/mcp" },
    "tolstoy-library": { "url": "https://apilb.gotolstoy.com/mcp/v1/library/mcp" }
  }
}
```

## Authentication

OAuth 2.1 with PKCE, backed by Amazon Cognito. Discovery via RFC 9728 protected-resource metadata at each server's `/.well-known` endpoints. Each connection is bound to the Tolstoy workspace you authorize with.

## Registry

Published in the official [MCP Registry](https://registry.modelcontextprotocol.io):
- `io.github.GoTolstoy/studio`
- `io.github.GoTolstoy/library`

The `server.json` for each is in [`registry/`](./registry).

## About

Tolstoy is the agentic platform for AI-native ecommerce brands — https://www.gotolstoy.com
