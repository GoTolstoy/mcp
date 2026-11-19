# Tolstoy MCP

Connect any MCP client — Claude, ChatGPT, Cursor, Gemini, and more — to **Tolstoy**, the agentic platform for AI-native ecommerce brands. Manage your Tolstoy workspace right from chat: your store's products, your media library, uploads, saved models, templates, projects, credit usage, and store analytics.

Tolstoy exposes its remote MCP servers over Streamable HTTP, secured with OAuth 2.1 + PKCE — no API keys to paste, your client runs the OAuth sign-in on first connect.

| Server | Endpoint | What it does |
| --- | --- | --- |
| **Tolstoy** | `https://apilb.gotolstoy.com/mcp/v1/mcp` | Your Tolstoy workspace — search your products and media library, upload media, and read your saved models, templates, projects, and usage. |
| **Tolstoy Closet** | `https://apilb.gotolstoy.com/mcp/v1/closet/mcp` | A shopper's private closet — save, find, and remove the clothes they own, and continue in the Shopbots app. |

## Platforms the brand connects in Tolstoy

A brand connects its other platforms once in the Tolstoy platform, under **Settings > Connectors**. The Tolstoy Agent can then work with them, and an MCP client reaches the Tolstoy Agent with the `run_agent` tool. There is no separate MCP tool per platform.

| Group | Platforms |
| --- | --- |
| Social and video | Instagram, Pinterest, YouTube, TikTok, X |
| Paid ads | Meta Ads, OpenAI Ads (ChatGPT Ads), TikTok Ads |
| Customer support | Gorgias |
| Reviews and UGC | Yotpo, Judge.me, Okendo, Bazaarvoice |
| Email and SMS | Klaviyo, Attentive, Postscript, Drip |
| Store and attribution analytics | Triple Whale, Shopify, TikTok Shop, Google Analytics |
| Search and merchandising | Rebuy, Nosto, Klevu |
| Loyalty, returns and shipping | Smile.io, Loop Returns, AfterShip |
| Catalog, feeds and PIM | Feedonomics, Channable, Akeneo |
| Brand assets and team tools | Brandfolder, Canva, Google Drive, Airtable, Asana, Slack, Gmail, Outlook |

Each `run_agent` turn spends the workspace's credits. What each connector covers is listed in the [`tolstoy-connectors` skill](cursor/skills/tolstoy-connectors/SKILL.md).

## Start with one product

The Claude and Cursor plugins include the [`tolstoy-product-media` skill](skills/tolstoy-product-media/SKILL.md): confirm the product in your store, shortlist the library media that fits it, and upload what is missing.

The plugins also include the [`ecommerce-analytics` skill](skills/ecommerce-analytics/SKILL.md) for adding analytics to a store with the Tolstoy SDK.

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
- `run_agent` — send a request to the Tolstoy Agent, including requests about the platforms connected under Settings > Connectors. A turn spends credits.
- `get_agent_chat` / `stop_agent` — read or stop a Tolstoy Agent chat, including chats you started in the Tolstoy platform.
- `get_generation` — read a generation's status and the library items it saved.
- `list_voices` — search the voice library and its voice previews.
- `get_usage` — read your workspace's credit balances and usage for this billing period.
- `list_workspaces` — list your Tolstoy workspaces with their app keys; `currentAppKey` is the workspace of this connection.
- `get_store_analytics` — read a store's analytics report: its Tolstoy widgets, and the event and shopper counts of each event it sends with the Tolstoy SDK.
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

This repository is also a Claude plugin: [`.claude-plugin/plugin.json`](./.claude-plugin/plugin.json) and [`.mcp.json`](./.mcp.json). The plugin adds the Tolstoy workspace server and the `tolstoy-product-media` and `ecommerce-analytics` skills. Load it locally with `claude --plugin-dir .` from a clone of this repository.

### Cursor Marketplace plugin

This repository is also a Cursor plugin: [`.cursor-plugin/plugin.json`](./.cursor-plugin/plugin.json) and [`mcp.json`](./mcp.json). The plugin adds:

- the Tolstoy workspace server (`https://apilb.gotolstoy.com/mcp/v1/mcp`, OAuth);
- the `tolstoy-product-media` and `ecommerce-analytics` skills from [`skills/`](./skills/);
- the `tolstoy` (images, videos, audio, creative skills, saved models, credits), `widgets` (AI widgets) and `tolstoy-connectors` (platforms connected in Tolstoy) skills from [`cursor/skills/`](./cursor/skills/);
- the always-on rule [`rules/use-tolstoy.mdc`](./rules/use-tolstoy.mdc), which sends requests for the brand's own data in a connected platform to Tolstoy, and leaves code that integrates with a platform alone;
- the agent [`cursor/agents/tolstoy-commerce-agent.md`](./cursor/agents/tolstoy-commerce-agent.md).

To try it locally, link a clone of this repository to `~/.cursor/plugins/local/tolstoy` and reload Cursor. The Cursor-only skills and agent live under `cursor/` so the Claude plugin keeps its own two skills.

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
- Security reports: [rnd@gotolstoy.com](mailto:rnd@gotolstoy.com) (see [SECURITY.md](./SECURITY.md))
- Security overview: [gotolstoy.com/security](https://www.gotolstoy.com/security)

## Registry

Published in the official [MCP Registry](https://registry.modelcontextprotocol.io):
- `io.github.GoTolstoy/tolstoy` — the main Tolstoy server

Its `server.json` is [`registry/tolstoy.server.json`](./registry/tolstoy.server.json). Tolstoy Closet's (`io.github.GoTolstoy/closet`, not yet published) is next to it. Tolstoy runs no other server. The older `io.github.GoTolstoy/studio`, `library` and `shopper` entries are retired (status `deleted`); `studio` is replaced by `tolstoy` at the same endpoint. The publish workflow's `set-status` action changes a server's status over GitHub OIDC.

## About

Tolstoy is the agentic platform for AI-native ecommerce brands, powering shoppable video for thousands of stores — https://www.gotolstoy.com
