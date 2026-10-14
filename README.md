# Tolstoy MCP

Connect any MCP client — Claude, ChatGPT, Cursor, Gemini, and more — to **Tolstoy**, the agentic platform for AI-native ecommerce brands. Manage your media library right from chat, and create product images and videos with Tolstoy Studio outside Claude, or in Claude once Tolstoy has enabled it for your account.

Tolstoy exposes its remote MCP servers over Streamable HTTP, secured with OAuth 2.1 + PKCE — no API keys to paste, your client runs the OAuth sign-in on first connect.

| Server | Endpoint | What it does |
| --- | --- | --- |
| **Tolstoy** | `https://apilb.gotolstoy.com/mcp/v1/mcp` | Your Tolstoy workspace — manage your media library, products, Tolstoy models, templates, and projects, and create and revise images and videos with Tolstoy Studio. Claude connections, including the Tolstoy connector in Claude's directory, have no Studio generation by default. To use it in Claude, ask [support@gotolstoy.com](mailto:support@gotolstoy.com) to enable your account, then add Tolstoy as a custom connector with this endpoint. |
| **Tolstoy Closet** | `https://apilb.gotolstoy.com/mcp/v1/closet/mcp` | A shopper's private closet — save, find, and remove the clothes they own, and continue in the Shopbots app. |

## Start with one product

Follow the [first-workflow guide](docs/first-workflow.md) to confirm your store, find existing media for a product, and create new content for it. The Cursor plugin also includes the [`tolstoy-product-media` skill](skills/tolstoy-product-media/SKILL.md) for this workflow.

## Tools

**Tolstoy**

- `run_agent` — send a request to Tolstoy Studio, which creates and revises images and videos. Pass the returned `chatId` to continue the same chat. Off by default on Claude connections; Tolstoy support can enable it for your account.
- `get_agent_chat` — read a Studio chat's status and the media it produced, including chats you made in the Tolstoy platform.
- `search_products` — find products in your store's catalog.
- `search_media` — search your library videos and images.
- `get_media` — read a media item's details: tagged products, creator, expiry, and source file.
- `update_media` — rename a media item, star it, and set its creator, expiration date, and product tags.
- `search_fashion_models` — find your saved Tolstoy models (people with reference images) to use in Studio.
- `search_templates` / `get_template` — find and read Studio templates.
- `search_projects` — find your Studio projects and folders, whose context files apply to chats started in them.
- `start_media_upload` / `finish_media_upload` — upload a local file to your library from a client that can run shell commands.
- `upload_media_from_panel` — open the Tolstoy panel and pick files to upload to your library.
- `open_tolstoy` — open Tolstoy in the client to browse and pick items by hand.

**Tolstoy Closet**

- `search_closet` — list or search the shopper's saved clothes.
- `add_closet_items` — save clothes to the closet.
- `remove_closet_items` — remove saved items.
- `get_shopbots_link` — create a private link to continue in the Shopbots app.

App-aware clients (ChatGPT, Claude) also get an interactive Tolstoy view rendered inline in chat. It calls a few more tools (`get_app_home`, `list_agent_chats`, `fail_media_upload`) that the model does not see.

## Connect

1. In your MCP client, add a custom connector / remote MCP server.
2. Paste the endpoint from the table above.
3. Complete the OAuth prompt: sign in to Tolstoy, or for Tolstoy Closet, approve the private closet connection.

Per-client setup (Claude, ChatGPT, Cursor, Gemini CLI, Codex, Perplexity, Goose, Cherry Studio, and more) is available in the Tolstoy platform under **Settings → MCP**.

### Cursor Marketplace plugin

This repository includes a Cursor plugin manifest in [`.cursor-plugin/plugin.json`](./.cursor-plugin/plugin.json). Install the repository as a local plugin while developing, or install Tolstoy from the Cursor Marketplace. The plugin adds the Tolstoy workspace server.

### Example client config

```json
{
  "mcpServers": {
    "tolstoy": { "url": "https://apilb.gotolstoy.com/mcp/v1/mcp" }
  }
}
```

### Codex CLI

`codex mcp add` targets STDIO servers, so add the remote server to `~/.codex/config.toml` and run the OAuth login:

```toml
[mcp_servers.tolstoy]
url = "https://apilb.gotolstoy.com/mcp/v1/mcp"
```

```bash
codex mcp login tolstoy
```

## Authentication

OAuth 2.1 with PKCE. Discovery via RFC 9728 protected-resource metadata at each server's `/.well-known` endpoints. A Tolstoy connection is bound to the Tolstoy workspace you authorize with. A Tolstoy Closet connection gets its own private guest closet after the shopper approves it. It needs no Tolstoy account; `get_shopbots_link` links it to a Shopbots account.

## Privacy, terms, and support

- [Privacy policy](https://www.gotolstoy.com/privacy-policy)
- [Terms of use](https://www.gotolstoy.com/terms-of-use)
- Support: [support@gotolstoy.com](mailto:support@gotolstoy.com)
- Security overview: [gotolstoy.com/security](https://www.gotolstoy.com/security)

## Registry

Published in the official [MCP Registry](https://registry.modelcontextprotocol.io):
- `io.github.GoTolstoy/studio` — the main Tolstoy server
- `io.github.GoTolstoy/closet` — Tolstoy Closet

The `server.json` for each is in [`registry/`](./registry).

## About

Tolstoy is the agentic platform for AI-native ecommerce brands, powering shoppable video for thousands of stores — https://www.gotolstoy.com
