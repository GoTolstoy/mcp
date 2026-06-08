# Tolstoy MCP

Connect any MCP client — Claude, ChatGPT, Cursor, Gemini, and more — to **Tolstoy**, the agentic platform for AI-native ecommerce brands. Run your **shoppable video** workspace right from chat: generate marketing content, manage your media library, build and publish shoppable widgets, tag products, and track ad performance.

Tolstoy exposes **two remote MCP servers** over Streamable HTTP, secured with OAuth 2.1 + PKCE. There are no API keys to paste — your client runs the OAuth sign-in on first connect.

| Server | Endpoint | What it does |
| --- | --- | --- |
| **Tolstoy Studio** | `https://apilb.gotolstoy.com/mcp/v1/mcp` | Generate and iterate on marketing videos and images with Tolstoy Studio's AI creative director. |
| **Tolstoy Library** | `https://apilb.gotolstoy.com/mcp/v1/library/mcp` | Run your shoppable video workspace — media library, shoppable widgets (Stories, Carousel, Spotlight), product tagging, multi-store, and Meta ads. |

## Tools

**Studio**
- `generate_studio_content` — start a new Studio generation (image or video) from a prompt.
- `iterate_studio_content` — continue and refine an existing Studio generation in the same session.

**Library — media assets**
- `list_assets` — list your most recent library assets (videos, images, AI drafts).
- `search_assets` — search the library by query.
- `get_asset` — fetch full details for an asset, including tagged products and playlists.
- `update_asset` — rename an asset or toggle its favorite status.

**Library — shoppable widgets**
- `list_widgets` — list your onsite shoppable video widgets (Stories, Carousel, Spotlight, For You Feed, Tile, Collection Grid, Bubble Feed), live or draft.
- `get_widget` — inspect a widget: type, live status, content selection, and the actual videos it shows (per-product for PDP-mode shoppable widgets).
- `create_widget` — create a new shoppable widget from a template, with the platform's defaults.
- `update_widget` — rename, publish/unpublish, set PDP mode, or change a widget's content selection.

**Library — products & shoppability**
- `search_products` — find a store product by title to make videos shoppable.
- `tag_video_product` — tag (or untag) products on a video so it becomes shoppable in product-tagged playlists and PDP widgets.

**Library — stores**
- `list_stores` — list the connected stores on your account; widget and product tools can target any of them.

**Library — paid ads**
- `list_ad_campaigns` — list your Meta ad campaigns with real delivery status (`effectiveStatus` truth-telling).
- `get_ads_performance` — Meta ads performance: spend, ROAS, CTR, purchases — per campaign, ad set, or ad.
- `publish_to_meta_ads_library` — push a library video or image into Meta Ads Manager, ready for ad creation (no campaign, no spend).

App-aware clients (ChatGPT, Claude) also get interactive views — a shoppable-widget card grid and asset previews — rendered inline in chat.

## Connect

1. In your MCP client, add a custom connector / remote MCP server.
2. Paste the Studio or Library endpoint above.
3. Sign in with your Tolstoy account when prompted (OAuth).

Per-client setup (Claude, ChatGPT, Cursor, Gemini CLI, Codex, Perplexity, Goose, Cherry Studio, and more) is available in the Tolstoy platform under **Settings → MCP**. The Tolstoy Library is also a published **ChatGPT app** — search "Tolstoy Library" in ChatGPT and click Connect.

### Example client config

```json
{
  "mcpServers": {
    "tolstoy-studio": { "url": "https://apilb.gotolstoy.com/mcp/v1/mcp" },
    "tolstoy-library": { "url": "https://apilb.gotolstoy.com/mcp/v1/library/mcp" }
  }
}
```

### Codex CLI

`codex mcp add` targets STDIO servers, so add the remote server to `~/.codex/config.toml` and run the OAuth login:

```toml
[mcp_servers.tolstoy-library]
url = "https://apilb.gotolstoy.com/mcp/v1/library/mcp"

[mcp_servers.tolstoy-studio]
url = "https://apilb.gotolstoy.com/mcp/v1/mcp"
```

```bash
codex mcp login tolstoy-library
```

## Authentication

OAuth 2.1 with PKCE, backed by Amazon Cognito. Discovery via RFC 9728 protected-resource metadata at each server's `/.well-known` endpoints. Each connection is bound to the Tolstoy workspace you authorize with.

## Registry

Published in the official [MCP Registry](https://registry.modelcontextprotocol.io):
- `io.github.GoTolstoy/studio`
- `io.github.GoTolstoy/library`

The `server.json` for each is in [`registry/`](./registry).

## About

Tolstoy is the agentic platform for AI-native ecommerce brands, powering shoppable video for thousands of stores — https://www.gotolstoy.com
