# Tolstoy MCP

Connect any MCP client — Claude, ChatGPT, Cursor, Gemini, and more — to **Tolstoy**, the agentic platform for AI-native ecommerce brands. Run your **shoppable video** workspace right from chat: generate marketing content, manage your media library, build and publish shoppable widgets, browse your catalog, tag products, and track ad performance.

Tolstoy exposes its remote MCP servers over Streamable HTTP. The main **Tolstoy** server is secured with OAuth 2.1 + PKCE — no API keys to paste, your client runs the OAuth sign-in on first connect. **Shopper** is a separate public, no-auth marketplace server.

| Server | Endpoint | What it does |
| --- | --- | --- |
| **Tolstoy** | `https://apilb.gotolstoy.com/mcp/v1/mcp` | Your full shoppable-video workspace — generate and iterate on marketing videos and images, manage your media library, build and publish shoppable widgets, browse your product catalog, tag products, and review Meta ad performance. |
| **Tolstoy Shopper** | `https://apilb.gotolstoy.com/mcp/v1/shopper/mcp` | Shop across every brand store on Tolstoy — marketplace-wide product search, full product details, and virtual try-on. Public, no sign-in. |

## Tools

The main **Tolstoy** server exposes the following tools.

**Studio — content generation**
- `generate_studio_content` — start a new Studio generation (image or video) from a prompt.
- `iterate_studio_content` — continue and refine an existing Studio generation in the same session.
- `get_studio_session` — check status and retrieve the finished media for a generation.
- `list_studio_folders` — list your Studio projects and folders.
- `list_studio_chats` — list the chats inside a Studio project or folder.

**Media library**
- `list_assets` — list your most recent library assets (videos, images, AI drafts).
- `search_assets` — search the library by name or creator handle.
- `get_asset` — fetch full details for an asset, including tagged products and playlists.
- `update_asset` — rename an asset or toggle its favorite status.

**Shoppable widgets**
- `list_widgets` — list your onsite shoppable video widgets (Stories, Carousel, Spotlight, For You Feed, Tile, Collection Grid, Bubble Feed), live or draft.
- `get_widget` — inspect a widget: type, live status, content selection, and the actual videos it shows (per-product for PDP-mode shoppable widgets).
- `create_widget` — create a new shoppable widget from a template, with the platform's defaults.
- `update_widget` — rename, publish/unpublish, set PDP mode, or change a widget's content selection.

**Products & catalog**
- `list_collections` — list the catalog collections for a connected store.
- `search_products` — find store products by title or query.
- `browse_products` — browse catalog products and collections for a connected store.
- `tag_video_product` — tag (or untag) products on a video so it becomes shoppable in product-tagged playlists and PDP widgets.

**Stores**
- `list_stores` — list the connected stores on your account; widget, catalog, and product tools can target any of them.

**Paid ads**
- `list_ad_campaigns` — list your Meta ad campaigns with real delivery status (`effectiveStatus` truth-telling).
- `get_ads_performance` — Meta ads performance: spend, ROAS, CTR, purchases — per campaign, ad set, or ad.
- `publish_to_meta_ads_library` — push a library video or image into Meta Ads Manager, ready for ad creation (no campaign, no spend).

**Shopper** (separate public marketplace server — no auth)
- `search_products` — search products across every brand store on Tolstoy, one marketplace-wide catalog.
- `get_product` — full product details: description, variants, price, media, the brand's videos, and buy/cart links.
- `try_on` — open an interactive virtual try-on of a product (participating brands); the shopper uploads a photo and sees themselves wearing the actual item.

App-aware clients (ChatGPT, Claude) also get interactive views — a shoppable-widget card grid and asset previews — rendered inline in chat.

## Connect

1. In your MCP client, add a custom connector / remote MCP server.
2. Paste the Tolstoy (or Shopper) endpoint above.
3. Sign in with your Tolstoy account when prompted (OAuth). Shopper needs no sign-in.

Per-client setup (Claude, ChatGPT, Cursor, Gemini CLI, Codex, Perplexity, Goose, Cherry Studio, and more) is available in the Tolstoy platform under **Settings → MCP**.

### Example client config

```json
{
  "mcpServers": {
    "tolstoy": { "url": "https://apilb.gotolstoy.com/mcp/v1/mcp" },
    "tolstoy-shopper": { "url": "https://apilb.gotolstoy.com/mcp/v1/shopper/mcp" }
  }
}
```

### Codex CLI

`codex mcp add` targets STDIO servers, so add the remote server to `~/.codex/config.toml` and run the OAuth login:

```toml
[mcp_servers.tolstoy]
url = "https://apilb.gotolstoy.com/mcp/v1/mcp"

[mcp_servers.tolstoy-shopper]
url = "https://apilb.gotolstoy.com/mcp/v1/shopper/mcp"
```

```bash
codex mcp login tolstoy
```

## Authentication

OAuth 2.1 with PKCE, backed by Amazon Cognito. Discovery via RFC 9728 protected-resource metadata at the server's `/.well-known` endpoints. Each connection is bound to the Tolstoy workspace you authorize with. **Shopper** is a public marketplace server and requires no authentication.

## Registry

Published in the official [MCP Registry](https://registry.modelcontextprotocol.io):
- `io.github.GoTolstoy/studio` — the main Tolstoy server
- `io.github.GoTolstoy/shopper`

The `server.json` for each is in [`registry/`](./registry).

## About

Tolstoy is the agentic platform for AI-native ecommerce brands, powering shoppable video for thousands of stores — https://www.gotolstoy.com
