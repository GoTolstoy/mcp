# Tolstoy MCP

Connect any MCP client — Claude, ChatGPT, Cursor, Gemini, and more — to **Tolstoy**, the agentic platform for AI-native ecommerce brands. Manage your Tolstoy workspace right from chat: your store's products, your media library, uploads, saved models, templates, projects, and credit usage.

Tolstoy exposes its remote MCP servers over Streamable HTTP, secured with OAuth 2.1 + PKCE — no API keys to paste, your client runs the OAuth sign-in on first connect.

| Server | Endpoint | What it does |
| --- | --- | --- |
| **Tolstoy** | `https://apilb.gotolstoy.com/mcp/v1/mcp` | Your Tolstoy workspace — search your products and media library, upload media, and read your saved models, templates, projects, and usage. |
| **Tolstoy Closet** | `https://apilb.gotolstoy.com/mcp/v1/closet/mcp` | A shopper's private closet — save, find, and remove the clothes they own, and continue in the Shopbots app. |

## Start with one product

The Claude and Cursor plugins include the [`tolstoy-product-media` skill](skills/tolstoy-product-media/SKILL.md): confirm the product in your store, shortlist the library media that fits it, and upload what is missing.

## Tools

**Tolstoy**

- `search_products` — find products in your store's catalog, with their variants and ids.
- `get_brand_context` — read your store's brand profile: logos, colors, fonts, audience, and size guide.
- `connect_products` — open the Tolstoy panel to connect your product catalog: a Shopify store, a product file, or a feed.
- `search_media` — search your library videos and images.
- `get_media` — read a media item's details: tagged products, creator, expiry, and source file.
- `analyze_media` — ask one question about a video or audio file. Spends credits and changes nothing in your library.
- `start_media_upload` / `finish_media_upload` — upload a local file to your library from a client that can run shell commands.
- `upload_media_from_panel` — open the Tolstoy panel and pick files to upload to your library.
- `search_fashion_models` — find your saved Tolstoy models: people with reference images.
- `save_fashion_model` — save existing images of one person as a new saved model.
- `search_templates` / `get_template` — find and read content templates.
- `search_projects` — list your projects and their folders.
- `list_skills` / `get_skill` — read Tolstoy's creative skills, the guidance the Tolstoy Agent follows.
- `get_agent_chat` / `stop_agent` — read or stop a Tolstoy Agent chat, including chats you started in the Tolstoy platform.
- `get_generation` — read a generation's status and the library items it saved.
- `list_voices` — search the voice library and its voice previews.
- `get_usage` — read your workspace's credit balances and usage for this billing period.
- `open_tolstoy` — open Tolstoy in the client to browse your library, models, templates, and conversations by hand.

**Tolstoy Closet**

- `search_closet` — list or search the shopper's saved clothes.
- `add_closet_items` — save clothes to the closet.
- `remove_closet_items` — remove saved items.
- `get_shopbots_link` — create a private link to continue in the Shopbots app.

App-aware clients (ChatGPT, Claude) also get an interactive Tolstoy view rendered inline in chat. It calls a few more tools that the model does not see.

## Connect

1. In your MCP client, add a custom connector / remote MCP server.
2. Paste the endpoint from the table above.
3. Complete the OAuth prompt: sign in to Tolstoy, or for Tolstoy Closet, approve the private closet connection.

Per-client setup (Claude, ChatGPT, Cursor, Gemini CLI, Codex, Perplexity, Goose, Cherry Studio, and more) is available in the Tolstoy platform under **Settings → MCP**.

### Claude plugin

This repository is also a Claude plugin: [`.claude-plugin/plugin.json`](./.claude-plugin/plugin.json) and [`.mcp.json`](./.mcp.json). The plugin adds the Tolstoy workspace server and the `tolstoy-product-media` skill. Load it locally with `claude --plugin-dir .` from a clone of this repository.

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
